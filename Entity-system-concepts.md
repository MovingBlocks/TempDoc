This guide is intended to be a quick, non-technical overview of the entity system used by Terasology.

# Entities and Components

The heart of the Entity System is a simple data structure composed of Entities and Components. Each Entity is unique object in the world - the Player is an entity, a single enemy is an Entity, a chest is also an Entity. Entities don't have to be objects that are visible in the world either - they can be scoreboards, loot tables and other gameplay related things.

An entity on its own isn't really anything, though. For an Entity to be of use it needs to be given Components. Each component is a feature that an entity can have: a Location component gives an entity a position in the world, a Mesh component gives it appearance, a RigidBody component along with a shape component gives it collision, and so forth.  Each component also can have properties that can be set, that relate the the feature it provides - Location component has a position property, Mesh component has the mesh to display.

This structure provides flexibility and reuse when creating entities - you can add any of the existing components to make use of their features, and concentrate on creating new components for any features that don't presently exist - if any.

# Components and Systems

