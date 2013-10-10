Codebase Structure
===============================

This is an overview of the different parts of our primary codebase and will be primarily of interest to developers/modders. See also Project Overview for a higher level view across more different projects.

Gradle
---------

Most our projects are organized using [Gradle](http://www.gradle.org), a build automation tool similar to [Maven](http://maven.apache.org), but using [Groovy](http://groovy.codehaus.org) as its language. This allows for some pretty powerful scripting and customization of a local developer setup.

You interact with Gradle using a "gradlew" wrapper script that takes care of setting up Gradle itself. No need to install anything. You simply run the command "gradlew" on any OS in the directory you've cloned the primary Terasology engine repo to and the correct version will be downloaded and executed.

Gradle works great with multiple sub-projects and builds a "project tree" before any functional work begins. This is great for dealing with dependencies but does also mean that if the project structure changes on one execution (such as when fetching a new module from GitHub) the new sub-project will only be included on the next execution.

As you work on Terasology you might find out that you need source or binaries for other sub-projects, which can then be added easily to your existing workspace through an assortment of Gradle tasks. Keep reading to learn more.

Note: On Linux and Mac OS you may have to first mark the "gradlew" file as executable.

For more details on our use of Gradle see [[Fancy Gradle]]

Engine
---------

The heart and soul of Terasology. All facades and modules depend on the engine.

The primary repo containing the engine is the first and only thing you need to run the game and allows you to use Gradle commands to fetch everything else. Always assume you need to execute "gradlew" from the root directory of this project unless stated otherwise. This is the one repo you need to clone manually:

`git clone git@github.com:MovingBlocks/Terasology.git`

Along with the engine you get the PC Facade and Core Module. Everything else lives in independent GitHub repos that can be added to your local workspace as sub-projects. You can edit several at once, commit files across multiple Git roots, and push it all to each affected repo on GitHub in one action.

It also comes with several utility tasks, such as project file generation for [IDEA IntelliJ](http://www.jetbrains.com/idea). This is our recommended IDE (with a [freebie Ultimate Edition available](http://forum.movingblocks.net/threads/how-to-use-this-forum.33/#post-8778) for contributors) and the customized setup for it is fairly detailed.

You can also use [Eclipse](http://www.eclipse.org/), [NetBeans](https://netbeans.org/), or anything else you like, but you might have to figure out some of the setup details yourself - and if you do please post them in the [forum](http://forum.movingblocks.net/forums/developer-portal.5/) so we can improve the instructions to set up with alternative IDEs :-)

`gradlew idea`

This creates the IntelliJ files you can then use to open the project. Always open using the .ipr file - do not open using the directory or the Gradle file. You never need to create a new project from scratch or import anything. With this task you get:

* A run configuration called "TerasologyPC" will be created and immediately be available for execution. This run configuration includes memory settings and the "-homedir" parameter that makes game data files save in the install directory rather than the data directory (easier for development)
* Git will be mapped as the VCS of choice - as you add additional source modules they'll have their own "Git Root" and be set up likewise
* [[Checkstyle]] integration with IntelliJ will be enabled. This allows you to catch style violations that clash with the project conventions. Please check these before committing :D
* You'll be able to automatically insert the [[Project Header]] (copyright etc) in new files (TODO: More details)
* Some compiler settings will be tweaked, such as "Make Automatically"
* [[Annotations]], which are used extensively in the project, will get some special consideration when IntelliJ looks at whether code is used or not

The biggest architectural piece of the engine is our [[Entity System|Entity System Architecture]] which powers just about everything, much more than just creatures (typical considered "movable entities" or "mobs")

Facades
---------

The engine alone is not executable. It needs to run in some sort of context - facades supply that by wrapping the engine.

The most basic one is the "PC Facade" which simply runs the game normally as an application on Windows, Linux, or Macs. This facade is bundled with the engine repo and available right out of the box.

Another simple one runs the game in an applet out of a user's browser. To be able to work with a separate facade you can fetch it automatically:

`gradlew fetchFacadeApplet`

Facades are hosted in the MovingBlocks organization on GitHub and have their own custom build scripts.

Rarely should a new facade be needed, one could be made with:

`gradlew createFacadeWorldEditor`

This would create a "facades/WorldEditor" sub-project initialized with a few template files and its own Git repo

TODO: Swap example to the "Developer Facade" (when we have it) which provides additional developer tools at runtime

Modules
---------

If the heart of Terasology is the engine and the facades make up its different faces then the content modules are the different organs - delicious!

While usually "mods" are user-created modifications to a game our modules are a little more fundamental. Even the systems and various bits of content in the base game are stored in modules that can be enabled, disabled, or even replaced.

Modules have access to a limited part of the engine through the Modding API. Each is sandboxed for security. Modules do not get their own custom build file, instead one is supplied by the central project's "modules.gradle" template that builds all modules equally. If you change that template you can refresh all generated module build files with:

`gradlew refreshModuleGradle`

This is also a good time to point out that you can abbreviate task names. "gradlew refresh" works as well.

A module can define a "Game Mode" which is similar to a "modpack". Several such modes are also supplied in the base game like our "Free Style" which is similar to the Minecraft "Creative" mode.

TODO: "Game Mode" or "Game Type" ? Rename to type everywhere? Also, we need to make this work in multiplayer again, it actually only works in develop ...

With the primary repo you'll only have the bundled Core module (which contains the player object and similar important stuff). Here's an example that fetches the Signalling module:

`gradlew fetchModuleSignalling`

On the next execution of Gradle the new module will be detected and scanned. If it has dependencies on other modules Gradle will attempt to resolve them:

* Does the dependency exist as another local source module? If so then use that. Example: "modules/BlockNetwork" source directory fetched before the Signalling module (Signalling depends on BlockNetwork).
* If not then look for a local binary version present in the modules directory. If you later fetch a source module the binary version will be ignored. Example: "modules/BlockNetwork.jar"
* If a dependency is still not found go to our [[Artifactory]] instance and look there. If found the binary is copied to the local modules directory to be available at runtime. This will resolve as a local binary next time.

You can also create a brand new module and have it filled in with some template content:

`gradlew createModuleMyLittleModule`

This would create "modules/MyLittleModule" and initialize a new Git repo for it locally. TODO: also map a remote reference and finish teaching [[Gooey]] (our IRC bot) to create actual repos on GitHub under the Terasology organization

After the next Gradle execution (like "gradlew idea" to regenerate IntelliJ files to know about the new module) you can immediately run the game and see the new module available. It won't do much yet though!

For more on modules see:

* [[Module.txt]] - the manifest for a module. Includes description stuff, author info, dependencies, etc.
* [[Version Handling]] - we follow [Semantic Versioning](http://semver.org) (SemVer).
* [[Modding Guide]]
* TODO: Moar links!

Other File Types
---------

Beyond Java we have a few major groups of stuff

* Game assets - this is content wrapped in various ways. Might be textures, block shapes, models, etc. See [[Asset Types]] for more information
* [Protobuf](http://code.google.com/p/protobuf/) - this is a tool to encode structured data provided by Google. It is used to store data in a binary format for efficient transfer over network connections and such
* Module manifests - as mentioned above. These are also used in some other cases like for the engine and are used heavily for versioning and dependencies
* Shaders - scary OpenGL 3D wizardry making Terasology look spectacular

We heavily use [JSON](http://www.json.org/) throughout our projects to store text data / assets, configuration, meta-data, and so on. To make the different types more distinct we use some custom file extensions:

* .block = Block definition files. See [[Block Architecture]] for more details. Might be outdated at the moment though :-(
* .shape = Defines a 3d shape that can be applied to blocks. These can be exported from Blender using a [[bundled addon|Block Shapes In Blender]] (that we need to make sure works ..)
* .prefab = "Prefabricated" object, more or less a recipe for our entity system
* .texinfo = Added configuration for fancy textures like foliage gradients
* TODO: add more and ask Immortius to fill in any future ideas :-)

Changes from legacy
---------

If you've worked on (or even played) Terasology before [The Great Convergence](http://forum.movingblocks.net/threads/the-great-convergence.826/) there are quite a few changes to be mindful of:

* The game data directory moved around several times at the late stages in legacy and early multiplayer. TODO: Include examples here or put it in a general section
* Saved world format has likewise changed. Legacy worlds are not compatible with the latest code and you'll have to delete any outdated data to play or develop on the latest.
 * This is the most common cause of problems upgrading from legacy - if something doesn't work first try deleting the old game data dir
* The main "src" directory moved from project root into the engine sub-project. However, there are no functional changes as part of the restructure so if you have pending code based on the multiplayer branch it should work when simply moved to the new location. Old code that predates multiplayer will need to be rewritten.

Common Issues and Other Notes
---------

* If your command window loses focus while working on something that'll pop up an SSH passphrase prompt it may load in the background and be easy to miss. This can leave you with an incomplete sub-project dir
 * Incomplete or otherwise corrupt nested git directories (modules, facades ..) may cause trouble, such as complaining about "cannot find task 'classes' on [name]". When in doubt: Delete and fetch again
 * Same issue may cause tasks to think you already have a particular module locally - again just delete the partial directory and try again
* You cannot add the "idea" task to the same execution of Gradle as a task that messes with the project structure. "gradlew createModuleTestExecutionOrder idea" will not correctly apply the IntelliJ generation step to the brand new TestExecutionOrder module. Same goes for other tasks that base off the project structure - mess with the structure in one step then apply it in another
* If you get compile errors on trying to run with the provided configuration immediately after setting up IntelliJ try doing a full Project Rebuild (may be a poor dependency order compilation issue)
* IntelliJ will likely show/warn about a circular dependency between the PC facade and the engine. This is actually a known issue in IntelliJ where it doesn't distinguish between a compile dependency and a unit testing dependency. The PC facade needs to compile against the engine and the engine needs to unit test against the PC facade. Both work fine :-)


Related Pages
---------

TODO: Insert some architecture pages here
