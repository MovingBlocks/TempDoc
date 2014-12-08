This is a quick start guide specific to creating and enhancing mods for Terasology, paired with our [[Modding API]] page. You may also want to read the [[Contributor Guide]] or [[Dev Setup]] for general topics and setup.


## Overview
------------------------------------------------

Our goal is for everything, including the very player object itself, to be a content module - that is, fully modifiable or entirely replaceable without touching the game engine itself. The core game will ship with multiple selections of these "modules" making up different gameplay styles and players can then customize them further or create additional new content.

   * **What can currently be modded nicely**: Blocks and other in-game assets, world content through Components and Systems, [[console commands]], UI.
   * **Other comments:** Modules can use content from other modules. (TODO explain how it is done)

Note that in addition to the engine there is also a "core" module inside the modding system that holds what you might typically consider to be engine stuff, such as the player prefab itself, starting tools, doors and chests, etc. The `core.jar` all that lives in can then be modified and distributed to friends to showcase fundamental changes made to the game.

Lots of changes are expected in this area, far more in the game than the documentation, so apologies in advance as this will end up going out of date regularly ... :P

## Running terasology from source
---------------------------------------
The stable versions of terasology contain already some modules which just need to be activated to be used.

As a developer you typically first setup your IDE:

   * Download source via zip (easy) or Git (see [[Dev Setup]].)
   * `gradlew idea` on command line in project root dir
   * Open project in IntelliJ
   * Set project SDK under Project Structure if needed
   * _Build --> Make Project (CTRL-F9)_ (edit: still needed?)
   * Use the TerasologyPC launch config to start Terasology

## Downloading the source of a module
---------------------------------------

If you download the terasology source you don't get any modules as they are in their own repositories at https://github.com/Terasology. You don't need to download the modules manually. Instead you can run the following command to do so:

` gradlew fetchModule<moduleName>`

Note that there is no space between fetchModule and the module name. It is also possible to specify multiple modules like this:

`gradlew fetchModule<moduleName1> fetchModule<moduleName2>`

The downloaded module source can be found in the modules subdirectory.

The above command does not create idea project files. To generate those run:

` gradlew idea`


## Creating a new module
---------------------------------------

To create a new module, you can run the command: 

` gradlew createModuleTest`

The created module can be found in the modules subdirectory.

It is propably also necessary to generate the idea project files with:

` gradlew idea`

## Structure of a mod
---------------------------------------

Each mod currently needs to live as its own IntelliJ sub-module / something similar in Eclipse under the `mods` directory. Using the bundled "portals" mod as an example we find:

   * `/.idea` - no real need to worry about this after the mod is created (see the next section)
   * `/assets` - place resources related to the mod under here and our [[Asset System]] will find them. You can optionally introduce additional directory levels under each asset type to organize better
      * `/blocks` - block definitions go here, which are simple JSON files holding any special instructions related to each block (or nothing at all). Each block may reference one or more textures for its faces. See [[Block System]] for more details
      * `/blockTiles` - block textures go here and are usually matched by block definition files. However, if you place an `auto` directory under here any images there will automagically become basic blocks (same texture on all sides, no special traits)
      * `/prefabs` - these JSON files describe entity recipes that can be used by the game engine to create objects in-game. This could for instance be a Portal describing what it is able to spawn, or a chest block able to hold items. See [[Entity system concepts]]
      * `/sounds` - another asset type example. You can place an audio file here in the OGG format and then reference it using the mod's namespace, such as `portals:spawn`
   * `/src` - actual source code for custom functionality goes under here. Usually this will be custom Components and Systems that make up the core content in our [[Entity System Architecture]]

Modules are picked up by the game automatically on startup and any assets like blocks or sounds are loaded and made available. The modules's id becomes a namespace through which you can reference the assets, although if unique the game will guess the namespace for some things like blocks

You can reference stuff in another module's namespace from your mod, but keep in mind there's no explicit dependency management yet, nor versioning of mods.

## Creating new content
--------------------------------------------------

So you've got your basic mod set up, and want to add some new goodies to the game.  This is just the section to get you started.

* [[Tutorial: How to make blocks with custom UI]]
* [[Using Blender Assets]] - A guide on how to take a model from Blender and import it to the game in a friendly format.

### Related Links
--------------------------------------------------

   * [[Modding API]] - API information for what's useful to mods
   * [[Asset System]] - Information on how assets are handled within Terasology
   * [[Entity System Concepts]] - Overview of the concepts involved in the entity system