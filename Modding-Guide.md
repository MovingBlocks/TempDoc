This is a quick start guide specific to creating and enhancing mods for Terasology, paired with our [[Modding API]] page. You may also want to read the [[Contributor Guide]] or [[Dev Setup]] for general topics and setup.


## Overview
------------------------------------------------

Our goal is for everything, including the very player object itself, to be a content module - that is, fully modifiable or entirely replaceable without touching the game engine itself. The core game will ship with multiple selections of these "mods" making up different gameplay styles and players can then customize them further or create additional new content.

   * **What can currently be modded nicely**: Blocks and other in-game assets, world content through Components and Systems, [[console commands]].
   * **What can't be modded quite so nicely**: GUI components (a couple mods rely on matching UI changes in the engine), terrain generation and selection, game modes.
   * **Other comments:** Mods can use content from other mods but there is no formal dependency or version managing yet.

Note that in addition to the engine there is also a "core" module inside the modding system that holds what you might typically consider to be engine stuff, such as the player prefab itself, starting tools, doors and chests, etc. The `core.jar` all that lives in can then be modified and distributed to friends to showcase fundamental changes made to the game.

Lots of changes are expected in this area, far more in the game than the documentation, so apologies in advance as this will end up going out of date regularly ... :P

## Running with mods
---------------------------------------

While the modding system works as-is there are still a few quirks we need to work out. In the meantime you may have to include an additional step when running from source with mods to make sure they build properly.


   * Download source via zip (easy) or Git (see [[Dev Setup]])
   * `gradlew idea` on command line in project root dir
   * Open project in IntelliJ
   * Set project SDK under Project Structure if needed
   * _Build --> Make Project (CTRL-F9)_
   * Run org.terasology.game.Terasology

Key part is using "Make Project" to force everything to compile, including the stuff under /mods. This may only be needed for IntelliJ, with Eclipse more eager to compile all the time

If you still get quirky issues on startup you may want to try selecting individual mod directories (like `Terasology/mods/miniion`), right clicking, and selecting "Compile Module". Goal is to fix this soon with better dependency management in the project

**NOTE:** If you are using IntelliJ 12 you can enable "Make Project Automatically" under File / Settings / Compiler. This should both cause everything to build initially as well as keep up with updates in mod directories automatically.

Note that after launching the game you still have to actually **enable** mods on the world creation screen

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

Mods are picked up by the game automatically on startup and any assets like blocks or sounds are loaded and made available. The mod's id becomes a namespace through which you can reference the assets, although if unique the game will guess the namespace for some things like blocks

You can reference stuff in another mod's namespace from your mod, but keep in mind there's no explicit dependency management yet, nor versioning of mods.

Creating a new mod
--------------------------------------------------

You can create a new mod in one of two ways - the first is going to be the proper way long-term but isn't quite complete yet (for instance it may clear out project config changes you've made after an initial `gradlew idea`).

   * Add the name of your mod to `settings.gradle` at the project root dir
   * Run `gradlew cleanIdea idea` - this creates an Intellij `.iml` file for you in a new mod dir and sets it up as a module in your project
   * Manually copy in / create a mod.text along with other needed directories (see detailed steps below)

The completely manual version is simply making a copy of one of the existing bundled mods. Again using "portals" as an example you'd follow these steps:

   * Copy `mods/portals` to `mods/mymod` and rename `.idea/portals.iml` to `.idea/mymod.iml`
   * Go to "Project Structure" and add a new module from existing source, select your new directory's `.iml` file
   * Open `mod.txt` and update it with your mod's details. Make sure the id is unique.
   * Add the name of your mod to `settings.gradle` at the project root dir if you want to be able to include it outside your local development environment
      * With this done you should be able to run `gradlew distMods` in the project root to get your mod as a `.jar` under `builds/distributions/mods` that you can share with friends
   * Look for nice examples close to something you want to do in an existing mod and start tinkering with your own!

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