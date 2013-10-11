This is a quick overview of all the involved GitHub repositories and related projects that are involved with Terasology

Primary Repositories
---------

The central components of Terasology live under two GitHub Organizations. The ones needed to run the base game are listed below.

See [[Codebase Structure]] for more details on each piece

* [MovingBlocks](https://github.com/MovingBlocks) - this organization primarily contains the engine itself plus facades. It also holds some library projects - more below
 * [Engine](https://github.com/MovingBlocks/Terasology): The beating heart of the game. Also contains the PC Facade (the standard application) and the Core Module, as they're required for the base game to run normally
* [Terasology](https://github.com/Terasology) - this organization is entirely meant for hosting content modules. These come in two flavors
 * Root repos: Modules that follow the full [[Contributor Guidelines]] and may be maintained to some degree by the official community
 * Fork repos: Modules hosted by modders elsewhere on GitHub that follow the [[Modder Guidelines]] and are eligible for inclusion in official distributions and the launcher

Libraries
---------

We've created some library projects while working on Terasology that are used in-game

* [TeraBullet](https://github.com/MovingBlocks/TeraBullet) - Offers some voxel-world integrations with [JBullet](http://jbullet.advel.cz)
* [TeraOVR](https://github.com/MovingBlocks/TeraOVR) - Wrapper for the [Oculus Rift](http://www.oculusvr.com) SDK
* [Jitter](https://github.com/openleap/jitter) - Utility framework for the [Leap Motion](https://www.leapmotion.com/) (hosted under the [OpenLeap](https://github.com/openleap) organization)

Other projects
---------

These are indirect parts of the project, such as our supporting site work and launcher

* [Launcher](https://github.com/MovingBlocks/TerasologyLauncher) - the best way to run the game. Allows easy auto-updating and managing different versions of the game
* Applet - the Facade running the applet version of the game you can [play in your browser](http://forum.movingblocks.net/pages/applet)
 * TODO: Need to actually split this one out into a working separate repo and build it in the new structure :-)
* [Splash Site](https://github.com/MovingBlocks/movingblocks.github.com) - our GitHub-hosted front-end site at http://terasology.org offering a few quick links and what not - just in case our primary site gets slammed or something :-)
* [Gooey](https://github.com/MovingBlocks/Gooey) - our handy little [Hubot](http://hubot.github.com/)-based IRC bot offering witty banter and useful functionality like auto-creating GitHub repos. When he feels like it, anyway!
* [TeraMisc](https://github.com/MovingBlocks/TeraMisc) - a repository for miscellaneous stuff that doesn't really fit  anywhere else. Like raw model files, assorted utility scripts, stuff for our [XenForo](http://xenforo.com) site ([forum/portal](http://forum.movingblocks.net))

External projects
---------

These are noteworthy external projects we use

* [LWJGL](http://lwjgl.org) - foundation for graphics, sound, and input
* [Gradle-Git](https://github.com/ajoberstar/gradle-git) - makes Gradle even more magical by adding Git tasks
* [Jenkins CI](http://jenkins-ci.org) - continuous integration tool, builds our stuff at http://jenkins.movingblocks.net
* [Artifactory](http://www.jfrog.com/home/v_artifactory_opensource_overview) - repository manager, holds our builds and assorted library files, at http://artifactory.movingblocks.net
* [XenForo](http://xenforo.com) - our portal/forum site at http://forum.movingblocks.net


