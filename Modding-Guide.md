Modding Guide
=================
This is a quick start guide specific to creating and enhancing mods for Terasology. You may also want to read the [[Contributor Guide|Contributor-Guide]] or [[Dev Setup]] for general topics and setup

Running with mods
---------------------------------------

While the modding system works as-is there are still a few quirks we need to work out. In the meantime you may have to include an additional step when running from source with mods to make sure they build properly

   * Download source via zip (easy) or Git (see [[Dev Setup]])
   * `gradlew idea` on command line in project root dir
   * Open project in IntelliJ
   * Set project SDK under Project Structure if needed
   * Build --> Make Project (CTRL-F9 - this forces the mods to build)
   * Run org.terasology.game.Terasology

Key part is using "Make Project" to force everything to compile, including the stuff under /mods. This may only be needed for IntelliJ, with Eclipse more eager to compile all the time

If you still get quirky issues on startup you may want to try selecting individual mod directories (like `Terasology/mods/miniion`), right clicking, and selecting "Compile Module". Goal is to fix this soon with better dependency management in the project


Structure of a mod
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

TODO: How to reference stuff from one mod in another safely?

Create a new mod
--------------------------------------------------

The easiest way to start with a new mod is to simply copy one of the bundled mods. Again using "portals" as an example you'd follow these steps:

   * Copy `mods/portals` to `mods/mymod` and rename `.idea/portals.iml` to `.idea/mymod.iml`
   * Go to "Project Structure" and add a new module from existing source, select your new directory's `.iml` file
   * Open `mod.txt` and update it with your mod's details. Make sure the id is unique.
   * Add the name of your mod to `settings.gradle` at the project root dir if you want to be able to include it outside your local development environment (this is likely go change)
      * With this done you should be able to run `gradlew distMods` in the project root to get your mod as a `.jar` under `builds/distributions/mods` that you can share with friends
   * Look for nice examples close to something you want to do in an existing mod and start tinkering with your own!


New content tutorial
--------------------------------------------------

Lets say you've made your new mod `mymod` and want to add some simple content to it - namely a new block that both contains an inventory (like a chest) and can spawn stuff (like a portal)

TODO :D

Related Links
--------------------------------------------------

   * [[Modding API]] - API information for what's useful to mods
   * [[Asset System]] - Information on how assets are handled within Terasology
   * [[Entity System Concepts]] - Overview of the concepts involved in the entity system