Welcome to the Terasology Wiki!
===============================
This is the Terasology wiki, used for game documentation and other resources like how to get started as a contributor.

Game Info
---------

_What is Terasology ?_ Founded by Benjamin 'begla' Glatzel as an open source tech demo to research procedural terrain
 generation a team is now taking it to the next level - a full fledged game. We're aiming for a survival and
 discovery game with a strong influence from Minecraft, Dwarf Fortress, and Dungeon Keeper. A key part of the game
 will be building up an estate of some sort and managing specialized minions to climb up the ladder of discovery,
 while surviving in a world that might just be full of things that want to kill you.
* [[About Terasology|What-is-Terasology]] - more details on exactly what our goals are
* [[Download Terasology]] - basic instructions for how to download and set up the game. Also contains version history
 and other useful links
* [[Dev Team|Dev-Team]] - the who's who of Terasology and what holes we might especially need more people to help with

Player Guide
---------

These pages explain how the game's _unstable / develop_ version works, in detail. The stable / master version may
differ as it isn't updated as frequently. See the [[GitHub README|https://github.com/MovingBlocks/Terasology#terasology]] for a current summary of that release.

* [[Key Bindings]] - how to control yourself inside the game
* [[Tool Functions]] - what the tools do
* [[Console Help]] - commands available in the console opened with `tab`
* [[Debug Features]] - special features only active with debug mode enabled using `F3`

Contributing
------------

Interested in getting involved with working on the game? This section is for you!

* [[Contributor Guide]] - notes for general contributions to Terasology including links to help you learn the related
 technologies
* [[Modding Guide]] - details on how to create mods for the game (quick guide making some assumptions of development
familiarity)
* [[Project Overview]] - a summary of the different GitHub projects involved and what libraries we use
* [[GSOC]] - we keep a set of proposals ready for Google Summer of Code participation if we get accepted

### Programming

* [[Codebase Structure]] - reviews how the codebase is put together
* [[Dev Setup]] - a more detailed set up guide for developing Terasology on your local machine
* [[Fancy Git]] - more advanced Git topics that you don't _need_ to be able to run from source,
but may need to submit source or maintain your source setup over time
* [[Checkstyle]] - notes about our code conventions and how to automatically check them
* [[Unit Testing]] - or the lack thereof, the most common developer sin!
* [[JavaDoc]] - well-written code explains itself, but it doesn't help to have that in an exportable format!
* [[Modding API]] - Information on the engine and how what features are available for modding
* [[Console commands]] - instructions to create new console commands

### Art

* [[Contributor Guide]] covers most art related contribution tasks.
* [[Texture Origin]] - an index for textures we use and who contributed them. That way we can give credit where due
and keep track of how many of our core textures are unique vs sourced from texture packs

### Documentation, Issue Reporting, and Community

* [[Markdown and Wiki]] - how to tweak away with Markdown and the GitHub wiki
* [[Issue Tracking]] - how and what we're tracking using the GitHub issue system
* [[Community Suggestions]] - a place for us to store suggestions made by the public in a place that's not good for
potential long-term storage (tickets, forum, etc)

Architecture
------------

These pages offer more advanced insight into how specific features of the game are architected and why.

* [[Applet Architecture]] - structure of the applet version of the game and related info.
* [[Block Architecture]] - development overview of our Block system. (pending changes needed to make the game work in an applet again)
* [[Shape Architecture]] - defining 3D meshes via definitions in JSON!
* [[Block Shapes In Blender]] - more on shapes.
* [[Entity System Architecture]] - describes the structure and usage of the entity system.
* [Pathfinder Algorithm](https://github.com/Terasology/Pathfinding) - some notes about pathfinding.
* [[Behavior Tree System]] - how to use and extend the behavior tree (editor).  

Modules
------------
A list of modules maintained at Terasology can be found here:
[[http://jenkins.movingblocks.net/view/Modules/]]
[[http://jenkins.movingblocks.net/view/ModulesPending/]]

* [[Crafting System]] - Introduction to the crafting system, its usage and extenstion.
* [[Procedural Architecture Grammar]] - Introduction to the PAG for procedural building generation.
* [[Miniions]] - Introduction to the miniion system.

Communication
-------------

We have several ways to get the word out on updates, and likewise there are several ways to contact us.

* [Forum](http://forum.movingblocks.net) - new development / game topics will be posted here, and any questions answered.
* [GitHub](https://github.com/MovingBlocks/Terasology) - "Watch" the official project here to be able to easily spot commits and changes.
* [Twitter](http://twitter.com/#!/Terasology) - we'll tweet regularly about significant commits or new discussion topics posted, so "Follow" us for updates.
* [Facebook](http://www.facebook.com/pages/Terasology/248329655219905) - if you prefer to keep updated via Facebook you can "Like" us on there to keep up.
* [Google+](https://plus.google.com/b/103835217961917018533/103835217961917018533) - help prove people actually use G+ ! ;-)
* [Blog](http://blog.movingblocks.net/blog/) - Major news like milestones reached, new videos posted,
etc will get posted to our blog.
* [IRC](http://webchat.freenode.net/) #terasology - We're setting this up for live chat but it may take a while to stabilize with people only rarely on (or AFK), See [Using IRC](Using IRC) for setup details.
* [Jenkins RSS](http://jenkins.movingblocks.net/rssAll) - If you really want to know when something has just been built ;-)
