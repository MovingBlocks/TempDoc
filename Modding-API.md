Modding API
=================
This is the official Modding API for Terasology, detailing each extension point and status of relevant development.
You may also want to read the [[Modding Guide]].

The API consists of an overview of all extension points and their status, as well as brief descriptions of each and
links to relevant JavaDoc pages. Or, at least, that's the plan, it isn't all done yet :D

Overview
---------------------------------------

   * [[Events and Systems]]


### Implemented

   * Components - for storing data and assigning behavior to entities (blocks, creatures, tools, etc)
   * Systems - for the logic to process entities with Components relevant to the System
   * Events - for communication between systems
   * Actions - similar to events, need more detail
   * Blocks - definitions & textures simply go in the right spot, no need to extend anything
   * Commands - can be included by implementing CommandProvider and using annotations for descriptions. See [[Console Commands]] for details

### Pending

   * Per-block data - see [[this thread|http://forum.movingblocks.net/threads/per-block-data-storage.146/]]
   * GUI modding - see [[this thread|http://forum.movingblocks.net/threads/gui-where-to-put-what.623]]
   * Generators - for terrain creation
   * Game modes - predefined selections of mods / settings for a play style

# Engine Behavior

* [[Entity Lifecycle]]
* [[Component Lifecycle]]
* [[Chunk Lifecycle]]
* [[Block Types and Block Families]]
* [[Block Type Entities]]
* [[Block Entities]]
* [[Prefabs|Prefab-files]]

Related Links
--------------------------------------------------

* [[Modding Guide]] - API information for what's useful to mods
* [[Asset System]] - Information on how assets are handled within Terasology
* [[Entity System Concepts]] - Overview of the concepts involved in the entity system
* [[Randomness and Noise]] - Overview on different generators for random numbers and noise
