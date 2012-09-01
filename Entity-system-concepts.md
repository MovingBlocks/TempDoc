This guide is intended to be a quick, non-technical overview of the entity system used by Terasology.

# Entities and Components

The heart of the Entity System is a simple data structure composed of Entities and Components. Each Entity is unique object in the world - the Player is an entity, a single enemy is an Entity, a chest is also an Entity. Entities don't have to be objects that are visible in the world either - they can be scoreboards, loot tables and other gameplay related things.

An entity on its own isn't really anything, though. For an Entity to be of use it needs to be given Components. Each component is a feature that an entity can have: a Location component gives an entity a position in the world, a Mesh component gives it appearance, a RigidBody component along with a shape component gives it collision, and so forth.  Each component also can have properties that can be set, that relate the the feature it provides - Location component has a position property, Mesh component has the mesh to display.

This structure provides flexibility and reuse when creating entities - you can add any of the existing components to make use of their features, and concentrate on creating new components for any features that don't presently exist - if any.

# Components and Systems

In Terasology, a component is essentially just a request for an entity to be given a feature, and some data that feeds into how that feature works.  A component itself does not contain any logic for a feature - instead that is left to Systems.

A System provides the actual logic behind a component or combination of components - it can process them each frame, or respond to events dealing with them.  Multiple components being involved is common - rendering a mesh from a Mesh component cannot be done without a location from a Location component, for instance.

There are a number of advantages to the separation between data (in the Components) and logic (in the Systems)
* Allows mods to modify the behaviour of components. If a modder doesn't like the default behaviour of the Health component, they can replace the Health system with their own version - that will still work with all the existing entities with a Health component.
* Allows optimisation of the processing of multiple entities.

# Events

# Prefabs

# Persistence
