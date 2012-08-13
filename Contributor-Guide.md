Contributor Guide
=================
If you're interested in contributing in some way or just learn about some more developer stuff, you're in the right place!

First steps - for those who want to learn
-----------------------------------------

If you aren't yet too comfortable with some of the technology we use then there are lots of external resources you can look at. Just hit up Google and go nuts! Here are a few links to get you started

   * Git for source control: http://www.vogella.de/articles/Git/article.html
   * !IntelliJ for IDE: http://wiki.jetbrains.net/intellij/
   * Java for core engine: http://docs.oracle.com/javase/tutorial/
   * JSON for config and properties: http://en.wikipedia.org/wiki/Json
   * Javascript possibly for mods: http://en.wikipedia.org/wiki/JavaScript (tricky to dig up relevant tutorials since we're _not_ using it for website stuff)
   * Blender for models: http://www.blender.org/education-help/tutorials/
   * Groovy: http://groovy.codehaus.org/Beginners+Tutorial

Early project steps - learning the code
---------------------------------------

After you've made it through the DevSetup instructions so you can run Terasology from source - then what?

   * Find something you're interested in. 
      * Are you more into code, art, design, infrastructure, or something else?
      * Like tinkering with inventory, creatures, world generation, snazzy 3d effects, general content?
      * Would you rather work on the core engine or more peripheral stuff like mods?
   * For code, find something that exists under source control that seems relevant to your interests
   * Start walking the code to understand what happens where - our entity system and especially the involved events can be a little tricky to get into, execution flow can be sort of unorthodox

The following pages might come in handy:

    * [[Asset System]] - Information on how assets are handled within Terasology

Next steps - got the skills, need something to do!
--------------------------------------------------

We submit issues on GitHub for stuff we could use in the project, and tag some of them as friendly for contributors (although friendly may differ widely based on whether you know a little Java, some art, etc). Look in the following categories in particular, but just about any item is up for grabs unless indicated otherwise. The categories may overlap.

   * [[https://github.com/MovingBlocks/Terasology/issues?labels=Contributor-friendly&sort=created&direction=desc&state=open&page=1&milestone=1][Contributor friendly]] - these should be fairly approachable if you have some technical skill for the sort of stuff we use
   * [[https://github.com/MovingBlocks/Terasology/issues?labels=Research&sort=created&direction=desc&state=open&page=1&milestone=1][Research Items]] - you may be able to help do research without even touching our codebase - tho these items may be more advanced

Texturing
---------

We're purposedly using low-res textures akin to Minecraft to allow the massive number of blocks in the world to render efficienctly. We're not opposed to an optional higher res mode if it can perform well enough, but are not putting effort toward that goal unless one or more contributors step up to that particular plate. In the meantime here are some helpful bits for low-res texturing!

   * One contributor's guide to how he makes blocks (and he's made dozens, so it works!): http://board.movingblocks.net/viewtopic.php?f=5&t=313
   * Current starting texture pack (made for Minecraft) is Good Morning Craft by Louis Durrant hosted at http://www.carrotcakestudios.co.uk/gmcraft/ 
      * As a helper to know for sure what blocks are what you can review: <a href="http://www.minecraftwiki.net/images/7/78/TerrainGuide.png">http://www.minecraftwiki.net/images/7/78/TerrainGuide.png</a> (watch out for updates that may happen without this link being updated as well)
   * DwarfFortress uses an extensive collection of stones, minerals, gems, etc, which makes up a great inspiration for something similar we want to accomplish - see http://df.magmawiki.com/index.php/Stone for details. While DF is essentially text-based the amount of different "blocks" there is impressive and something we'd like to see happen with actual _graphics_ !
   * http://webmineral.com/help/Color.shtml - a very nice real-life mineral site with individual pictures of an unimaginably large number of minerals. Any interesting minerals we'd like to have in the game could have textures inspired by these images or others like them

To see Art related issues that need work see [[https://github.com/MovingBlocks/Terasology/issues?labels=Art&sort=created&direction=desc&state=open&page=1&milestone=1][this page on GitHub]]

Block Design
------------

[[Block Shapes In Blender]]
Related Sections
----------------

   * DevSetup - how to use Git, IntelliJ and so forth to get set up for developing!
   * IssueTracking - details on how we're working with issue tracking on GitHub
   * UnitTesting - you know you gotta, it helps!
   * JavaDoc - and so does this

Related Resources
-----------------

   * GitHub syntax for issues and such - http://github.github.com/github-flavored-markdown and http://daringfireball.net/projects/markdown/syntax
