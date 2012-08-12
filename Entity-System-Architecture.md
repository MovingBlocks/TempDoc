### Introduction

Terasology's Entity System is the core framework for game logic - most everything in the world is an entity. An entity system was chosen as it provides a lot of flexibility and support for extension, and can quite easily support in-game editors and simple mods without any code needing to be written.

Things which are not handled as entities: GUI and blocks (although some blocks may have a related entity).
### Interfaces and Implementation

Most parts of the Entity System in Terasology are defined as interfaces, and then implemented though a set of classes starting with POJO (for Plain Old Java Object). This allows for the possibility of replacing the implementation with something more exotic in the future for improved performance. Where possible code should be developed against the interfaces. The information below describes how things are done in the POJO implementation.
### Entity and !EntityRef

At the core of the Entity System we have entities - these are identifiable "things" in the world. However an Entity by itself doesn't do anything - it has no data, nor behavior. It is merely a logical container for one or more Components - these provide data, and behavior through their interaction with Systems.

In Terasology entities are worked with through the !EntityRef class. For the most part this just delegates requests to the Entity Manager - the central manager for the Entity System. The !EntityRef itself does not store components, these are stored in the Entity Manager within a hashed table, to allow ease of iterating over all entities with a given type of component.

!EntityRef uses the Null Object Pattern - instead of using Java's null, !EntityRef.NULL should be used. !EntityRef.NULL can be safely accessed with all its functions providing sensible default results - this removes the need to check whether an !EntityRef is null in many cases. Where it is needed, the exists() method can be called to check whether an !EntityRef is a valid reference.

One particular feature of the !EntityRef is that when an entity is deleted, all references to it are invalidated and act like !EntityRef.NULL from then on. This allows !EntityRef to be safely used in components, and Entity ids to be reused.
### Component

A component is a meaningful set of data, with a intention of being used to provide behavior, that can be attached to an Entity. For instance, a Location component stores data relating to an entity's position in the world - with the implication that the entity is something in the world. A Mesh component holds information about a mesh used to render the entity - but its presence along with a LocationComponent also implies the entity should be rendered.

Typically a component is a plain java object with a flat set of value objects and minimal functionality. There may be some data related methods (to ensure values are not set to null, for instance), but there should not be any game logic - that should be provided by the Systems. Components may contain !EntityRefs, but should never have a reference to other Components, or to Systems.

Each entity can have at most one Component of a given type - an entity may have a Location, but cannot have multiple locations. Generally if you come across a situation where having multiple of the same component may seem attractive, you would be better served by using multiple entities with a component to tie them to a "main" entity.

Components may only contain specific data types - this is used to support persistence. These types are:

   * Standard Java Primitives - double / float / int / boolean / long and their equivalent boxed types
   * String
   * Enums
   * Map&lt;String,X&gt;, where X is one of the supported types. The generic must be specified.
   * List&lt;X&gt;, where X is one of the supported types. The generic must be specified.
   * !EntityRef
   * !BlockFamily
   * Color4f
   * Vector2f / Vector3f / Vector2i
   * Quat4f
   * and simple POJOs composed of above (but not nested POJOs)

This list can be extended - see Component Library section below.

In general usage you use EntityRef's AddComponent method to attach a component to an entity, and RemoveComponent to remove it. GetComponent can be used to retrieve a component for inspection or modification. At the moment, after modifying a component SaveComponent should be used to save it back to the EntityRef - this causes an event to be sent, but nothing else at the moment. Future implementations may require this call for the component changes to actually occur though.


### Systems

!ComponentSystems, or Systems for short, provide behavior to entities. They do this in two ways

   * Processing entities with a desired set of components in response engine method calls like initialise(), update(float delta) and render()
   * Responding to entity events sent to entities with a desired set of components

For example, a particle system would iterate over all entities with both a Location and a Particle component (need the location to five the effect a position in the world, and the particle component is needed for the entity to be a particle effect in the first place) in each update(float delta) call, to update the particle positions. The health system would respond to an entity with a Health component receiving a Damage event, in order to reduce an entity's health - and if the health reaches 0, send a Death event to the entity.

This triple system of Entities composed of Components with Systems applying behavior provides a great deal of flexibility and extendability. Often new behavior can be introduced through new components and systems. Behavior can be completely changed by removing a system and putting a different one in its place. And new entities can be created by mix and matching existing components and changing their settings, without even writing code.
### Events and Event Handlers

Events are a mechanism used to allow systems to interact with each other. Events are typed, and carry data - for instance, there is a DamageEvent that holds an amount of damage being cause, and the instigator responsible for the damage. Events are sent to entities. Systems can then provide event handlers to pick up specific events that have been sent entities with a desired set of components. Expanding on the Damage event, you may have System that handles damage events that occur on entities with health components, in order to reduce health. Or an System that handles damage events for for entities with a location and physics component, to knock the entity away from the damage causer.

The advantage of using events rather than straight method calls between systems is that it decouples systems and provides the ability to add new systems in the future to react to the same event. By sending a damage event rather than modifying the health component directly, it allows for systems that modify the damage being dealt based on arbitrary conditions, or cancel it, or display some sort of effect, or for the damage to be handled in a different way entirely without having to change the damage causer at all.

New events should extend !AbstractEvent, which provides the event with the default cancellation functionality.

Systems that handle events should implement the !EventHandler interface. They can then add new event handling methods by adding methods of the form:
<pre>@ReceiveEvent(components = {HealthComponent.class, AnotherComponent.class}, priority = ReceiveEvent.PRIORITY_NORMAL)
public void onDamage(DamageEvent event, EntityRef entity) {
   // Do something
}</pre>

The method must have the signature `public void (T, !EntityRef)`, where T is an type of Event - this determines which event will be sent to the method. The second parameter is the !EntityRef for the entity that received the event. The name of the method and parameters can be anything, though I suggest starting the method name with "on", as in "onDamage". The method must also be annotated with @ReceiveEvent. The annotation must list what components an entity must have for the event handler method to be invoked - this allows you to filter out entities which are inappropriate for the event handler. You optionally may specify a priority, either using one of the preset priority levels or with an integer - this determines the order in which event handlers functions will be called when multiple are valid for a given event.

Events also support cancellation - this allows a system to stop an event before it reaches systems with a lower priority - for instance if you add an invincibility component to make an entity temporarily immune to damage, you can add a system that will intercept the Damage event and cancel it before it can reach the health system.

Inheritance structures of events are also supported - if you have a MouseButtonEvent, and a LeftMouseButtonEvent that inherits it, subscribing to MouseButtonEvent will also pick up LeftMouseButtonEvents.
### Prefabs

Prefabs are recipes for creating entities. They describe what components an entity should have, and what settings those components should start with. This can be described in JSON, with a typical prefab looking like:
<pre>{
 "name": "core:gelatinousCube",
 "Location" : {},
 "Mesh" : {
   "renderType" : "GelatinousCube"
 },
 "CharacterMovement" : {
   "faceMovementDirection" : true
 },
 "SimpleAI" : {},
 "AABBCollision" : {
   "extents" : [0.5, 0.5, 0.5]
 },
 "CharacterSound" : {
   "footstepSounds" : ["engine:Slime1", "engine:Slime2", "engine:Slime3", "engine:Slime4", "engine:Slime5"],
   "footstepVolume" : 0.7
 }
}</pre>

The prefab has a name that identifies it (TODO: this will be derived from its file name in a mod), and a number of components (referred to by the name of the component class with "Component" dropped from the end if present). Within each component the default values for each property can be overridden.

Prefabs also support inheritance from one or more parent prefabs, like so:
<pre>{
 "name": "core:angryGelatinousCube",
 "parent" : "core:gelatinousCube",
 "CharacterMovement" : {
   "maxGroundSpeed" : 50
 }
}
</pre>

This will inherit all of the parent components and settings and then add any additional components or change any different settings.

Prefabs can then be instantiated at runtime through the !EntityManager.

Usage of prefabs provides a number of benefits. Prefabs reduce the size of save data and network data - rather than using the full set of data for an entity, just the prefab the entity uses and delta of differences can be used. Prefabs also allow existing objects to be updated - when you change a prefab and load a level, any changes to the prefab will be reflected in any instances in that level. There is also potential to use prefabs as static data - for instance they could be used to describe crafting recipes or materials without ever creating an entity.

Prefabs are still an area for future development - at the moment they have a number of limitations:

   * You cannot specify nested entities that should be created and related to a !EntityRef property when a prefab is instantiated (like the items in a player's starting inventory).
   * A child prefab cannot remove an entity defined by a parent prefab.

### Component Library

The ComponentLibrary stores information about the components, which is used to handle persistence. When a component is registered with the ComponentLibrary, all of the properties of the component are enumerated, and a ComponentMetadata object is created with a list of those properties, their types, and methods to get and set that field in an object.
### Persistence

### Entities and Blocks

### Actions

### Future Work

### Further Reading

http://www.richardlord.net/blog/what-is-an-entity-framework

http://www.richardlord.net/blog/why-use-an-entity-framework

http://t-machine.org/index.php/2007/09/03/entity-systems-are-the-future-of-mmog-development-part-1/
