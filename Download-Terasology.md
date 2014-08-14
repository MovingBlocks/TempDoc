Downloading Terasology
======================
Instructions here on how to download the game and start playing!

Download
---------

We offer stable milestone downloads and unstable develop downloads that may update several times daily. We also have applet versions of either that are playable in a browser.

   * Stable / master download: [Jenkins Stable](http://jenkins.movingblocks.net/job/TerasologyStable/lastSuccessfulBuild/artifact/build/distributions/Terasology.zip)
   * Applet on official site: [Applet](http://forum.movingblocks.net/pages/applet)
   * Unstable / develop download: [Jenkins](http://jenkins.movingblocks.net/job/Terasology/lastSuccessfulBuild/artifact/build/distributions/Terasology.zip)

Setup
-----

For plain setup of the game simply download the zip file, extract it, and run using one of the executable options in the root of the extracted directory based on your OS

   * Windows: Simply execute `Terasology.exe`
   * Mac: Run via `run_macosx.command`
   * Linux: Use shell script `run_linux.sh`
   * Any (if your Java is set up right): Double-click `Terasology.jar`
You need to have a 1.7+ Java JRE or JDK installed on your system. Download Java from http://www.java.com/en/download/index.jsp

If you encounter any problems running the game please drop us a note in the [Support Forum](http://forum.movingblocks.net/forums/support.20/) !

Gameplay
--------

> %TODO% - need to automate a game manual since we list this in several places.

In the meantime go to [GitHub](https://github.com/MovingBlocks/Terasology) and scroll down a ways to see what keys do what and such. You
can get more help at [[Key Bindings]] and [[Console Help]].


Known Issues
------------

There are both general known issues such as graphic or sound compatibility as well as known bugs. General issues include:

   * Some integrated video chipsets have compatibility issues with !OpenGL - this can result in anything from minor to major graphic quirks, or the game outright not working. Unless your hardware is very old it is possible we can fix it, just make a post in the [Support Forum](http://forum.movingblocks.net/forums/support.20/) with your details (check Terasology.log in the logs directory, for instance)
   * Likewise integrated / older sound cards can also cause problems, this time with !OpenAL. There is a common problem on Windows that you can test real quick by looking for =OpenAL32.dll= in your Windows System32 directory and if one is present rename it (like append =.old=). Terasology may use an existing DLL if it exists, rather than the bundled version we develop against (note: this may cause other audio issues - rename your DLL back if so)
For outstanding known bugs see [GitHub 'Bug' Issues](https://github.com/MovingBlocks/Terasology/issues?labels=Bug&sort=created&direction=desc&state=open&page=1)

Since we're still extremely early it is hard to know for sure whether something is a bug or just not implemented yet. But if you find something dramatic (like the screen going black!) feel free to report it in the [Support Forum](http://forum.movingblocks.net/forums/support.20/)

Version History
---------------

We track our release level via [GitHub Milestones](https://github.com/MovingBlocks/Terasology/issues/milestones). Completed ones are
listed below for reference with any additional notes beyond what's stored in issues on GitHub.

### 0.1 - Legacy

We ended up with a first milestone on GitHub that was never used, but it still bumped the ID by one - so this can be thought of as the
period where the project was still Blockmania. So milestone 2 actually turns out to be our first official Terasology milestone.

### 0.2 - Stratification

Completed: February 22nd 2012 - [GitHub](https://github.com/MovingBlocks/Terasology/issues?sort=created&direction=desc&state=closed&page=1&milestone=2)

The goal of this milestone was to branch out into several rough and crude implementations of basic concepts so we could see something
more inside Terasology than placing/removing blocks, as well as get a better idea of which areas of focus we'd even have to begin with
and could start getting contributors interested in working on.

[[http://www.movingblocks.net:8080/jenkins/job/TerasologyStable/1/][Build link]]

   * Groovy - Cervator embedded this within Terasology for use in extending the game, doing easy configuration, etc. Immortius later started re-adding simple predefined commands like =giveBlock(id, quantity)=
   * Tools - implemented at first with a simple Gelatinous Cube spawning addon tool (later disabled) and block selection examples, extensible via plugins. Got fancier later with a proper toolbar and more variety
   * Blueprints - implemented via selection tools and transient copy-paste abilities of terrain
   * Skysphere - small-jeeper implemented a substantial upgrade of the sky - clouds, lighting, etc, and Begla finished it up
   * Mobs - Gelatinous Cubes were introduced and spawn either by portal or tool
   * Portals - one is spawned now near where the player spawns, then starts generating slimes, but is still pretty sketchy
   * Trees - shiny new L-system trees exist now!
   * Performance - assorted tweaks and optimizations, later on fancy metrics including some spiffy ones by Immortius
   * Physics - Begla enabled block physics and did a bunch of cool stuff with it
   * Graphics - Begla implemented all sorts of spiffy graphics effects making Terasology look like a quirky 16-bit version of Crysis :-)
   * Shapes - Immortius began work on custom shaped block meshes, defined similarly to blocks themselves in Groovy definition files

#### 0.2.1 - More shiny

[[http://www.movingblocks.net:8080/jenkins/job/TerasologyStable/2/][Build link]]

   * Assorted advanced graphic tweaks including shiny shiny water!
   * Stair blocks! First custom block, although no custom colision detection yet
   * Various architecture prep for better block management

#### 0.2.2 - Fixes and things

[[http://www.movingblocks.net:8080/jenkins/job/TerasologyStable/3][Build link]]

   * More fancy graphics tweaks and fixes
   * Added more sounds & music by Exile
   * Colision detection fixes and more fun with blocks

#### 0.2.3 - Beefy update

[[http://www.movingblocks.net:8080/jenkins/job/TerasologyStable/4][Build link]]

   * Major overhaul of game state (delta timestamps now in the game loop!) and startup, no longer jumping straight to loading the game
   * Inventory tweaks!
   * Physics improvements including broken blocks chasing after the player and jumping into the inventory
   * Lots of assorted fixes for graphic issues and the applet repeatedly getting bowled over
   * More unit testing, javadoc, and other infrastructure improvements
   * Official "integrate" branch for easier pull requests
   * Persistence / config tinkering
   * Fullscreen improvements (oh yeah, Terasology does run in fullscreen, setting is just hidden in a config file currently)
   * New "take screenshot" key (F12)
   * More music/sfx
   * Placeholder debug tool that places a "fancy" portal built with new blueprints / collection classes
   * Game console got more useful, see readme for example commands: https://github.com/MovingBlocks/Terasology#readme

#### 0.2.4 - Fun with infrastructure

[[http://www.movingblocks.net:8080/jenkins/job/TerasologyStable/5][Build link]]

Done on March 18th, lots of infrastructure improvements including Gradle, along with other misc

   * Upgraded build system to use Gradle, including the Gradle Wrapper which can auto-install everything. Use =gradlew tasks= to see what it can do
   * Overhauled audio system
   * Lots more UI improvements including initial options screen
   * RAILGUN!
   * More persistence improvements
   * New camera options
   * Lots of new blocks (available via console command =cmd.getBlock "NameGoesHere"=)

### 0.3.0 - Persistence Complete

Version numbering is a little askew as well as milestones were, so counting this as final completion of Milestone 3, while the first major content for Milestone 4 will go straight to 4.0. So 0.3.0 would really have been 0.2.5, but wanting to skip forward to 4.0. Yeah...

Stable build: [[http://www.movingblocks.net:8080/jenkins/job/TerasologyStable/6][Build link]]

   * Entity System! 
      * Assorted event handling
      * "Prefabs" - ability to link blocks with fancy objects (similar in concept to the meta block thing that's been floating around)
      * Working chests! Can rearrange items! Tho not yet drag or click items to specific slots or directly use the inventory
      * Explodey TNT blocks on poking with 'E' key (same as for chests)
   * More complete GUI framework 
      * World browser / creator UI
   * Lots of assorted other improvements as always

Pending
-------

Noteworthy stuff done in develop or elsewhere not yet included in a stable build

   * Proof of concept A* pathfinding by t3hk0d3 (old branch by now)
   * Orient DB backed ES prototype by Immortius (hit performance issues)