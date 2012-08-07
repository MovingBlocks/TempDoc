Welcome to the Terasology Wiki!
===============================
This is the Terasology wiki, used for game documentation and other resources like how to get started as a contributor.

Game Info
---------

_What is Terasology ?_ Founded by Benjamin 'begla' Glatzel as an open source tech demo to research procedural terrain generation a team is now taking it to the next level - a full fledged game. We're aiming for a survival and discovery game with a strong influence from Minecraft, Dwarf Fortress, and Dungeon Keeper. A key part of the game will be building up an estate of some sort and managing specialized minions to climb up the ladder of discovery, while surviving in a world that might just be full of things that want to kill you.
 * [[What is Terasology?|What-is-Terasology]] - more details on exactly what our goals are
 * [[Download Terasology|DownloadTerasology]] - basic instructions for how to download and set up the game. Also contains version history and other useful links
 * [[Dev Team|Dev-Team]] - the who's who of Terasology and what holes we might especially need more people to help with

Contributing
------------

Interested in getting involved with working on the game? This section is for you!

  * [[ContributorGuide]] - anything related to contributing to Terasology including links to help you learn the related technologies 
  * [[DevSetup]] - specifically how to set up to develop on Terasology on your local machine
  * [[FancyGit]] - more advanced Git topics that you don't _need_ to be able to run from source, but may need to submit source or maintain your source setup over time
  * [[IssueTracking]] - how and what we're tracking using the !GitHub issue system
  * [[UnitTesting]] - or the lack thereof, the most common developer sin!
  * [[JavaDoc]] - well-written code explains itself, but it doesn't help to have that in an exportable format!
  * [[TextureOrigin]] - an index for textures we use and who contributed them. That way we can give credit where due and keep track of how many of our core textures are unique vs sourced from texture packs
  * [[CommunitySuggestions]] - a place for us to store suggestions made by the public in a place that's not good for potential long-term storage (tickets, forum, etc)

Communication
-------------

We have several ways to get the word out on updates, and likewise there are several ways to contact us

 * [[http://board.movingblocks.net][Forum]] - new development / game topics will be posted here, and any questions posted answered
 * [[https://github.com/MovingBlocks/Terasology][GitHub]] - "Watch" the official project here to be able to easily spot commits
 * [[http://twitter.com/#!/Terasology][Twitter]] - we'll tweet regularly about significant commits or new discussion topics posted, so "Follow" us for updates
 * [[http://www.facebook.com/pages/Terasology/248329655219905][Facebook]] (Google+ coming) - if you prefer to keep updated via Facebook (or G+ soon) you can "Like" us on there to keep up
 * [Blog](http://blog.movingblocks.net/blog/) - Major news like milestones reached, new videos posted, etc will get posted to our blog
 * [IRC](http://webchat.freenode.net/) #terasology - We're setting this up for live chat but it may take a while to stabilize with people only rarely on (or AFK), See UsingIRC for setup details
 * [[http://www.movingblocks.net:8080/jenkins/rssAll][Jenkins RSS]] - If you really want to know when something has just been built ;-)

Architecture
------------

These pages offer more advanced insight into specific features of the game are architected and why

   * [[AppletArchitecture]] - structure of the applet version of the game and related info
   * [[BlockArchitecture]] - development overview of our Block system (pending changes needed to make the game work in an applet again)
   * [[ShapeArchitecture]] - defining 3D meshes via definitions in Groovy!
   * [[EntitySystemArchitecture]] - describes the structure and usage of the entity system