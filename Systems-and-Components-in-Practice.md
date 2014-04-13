Terasology's codebase can be daunting for somebody new to the project. This list, stemming from [a question](http://forum.movingblocks.net/threads/systems-and-components-to-learn-from.1016/) posed in the forum, attempts to provide some guidance for those who'd like to see how systems and components work in practice, starting from simpler modules and progressing to more complex ones.

1. **[Hunger](https://github.com/Terasology/Hunger)** mod (basic complexity) - simple component, single widget UI, simple event handling.
1. **[Journal](https://github.com/Terasology/Journal)** mod (intermediate) - simple component, composite widgets in UI, key binding, introduces events sent over network.
1. **[GrowingFlora](https://github.com/Terasology/GrowingFlora)** mod (advanced) - advanced components, interaction with world generation and use of scheduled events, introduces concept of chunk states, I'd suggest not looking too much into the tree shape and growth generation itself (implementation) just look at the interfaces.
1. **[Workstation](https://github.com/Terasology/Workstation)** mod (moderately scary) - use of components for defining flow, use of prefabs for defining new types of objects, complex interaction with inventory, both player and entity.
1. **[BlockNetwork](https://github.com/Terasology/BlockNetwork)** and **[Signalling](https://github.com/Terasology/Signalling)** mods (insane complexity) - maintains a separate data structure for loaded entities to improve performance, listens on Component, Entity and Chunk life-cycle events to keep the data structure up-to-date, complex logic, delay handling of events.

Credits to [Marcin](https://github.com/MarcinSc) for the initial list. 