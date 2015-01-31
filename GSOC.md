# Google Summer of Code proposals

We, the Terasology community, are eager to participate in GSOC and hope to be accepted as an organization. This page lists some ideas with corresponding references/guidelines/requirements to give you, the students, some entry points to our project.

The items listed here are drawn from our [issue tracker's GSOC category](https://github.com/MovingBlocks/Terasology/labels/GSOC), suggesting tasks suitable to be worked by a student over a summer. As such they're generally time non-critical items fairly separated from more active areas. Over time the issues may change and if you notice inaccuracies between issues and this page please feel free to edit! More links are likely also available in the issue linked in each section below.

More conceptual work is likely needed for most items and there may be existing contributors familiar with and able to help guide a student, beyond any mentors made available for GSOC normally. Other proposals are of course also welcome :-)

Newest issues are listed first and may be shorter on detail than older ones. Difficulties and contacts are best estimates - please see the "How to get involved" section below.

# What is Terasology

In short [Terasology's](http://terasology.org) goal is to make a heavily extensible voxel world game where actual gameplay can be defined in batches of modules. The engine is minimal, primarily serving to support modules of different kinds. Even systems that seem central to games in general, like a first person player, inventory, combat, and so on is here provided in modules instead and everything can be replaced with a customized version or disabled if not needed.

We plan to make a few typical game types available, like a content creation sand box mode, a twisted Alice in Wonderland style "defend your base and destroy theirs" mode, a more difficult "start from scratch" world with a realistic tech tree to claw your way up while surviving, and so on.

Inspiration is obviously sourced from Minecraft, as well as other classics like Dwarf Fortress and Dungeon Keeper. One heavy focus is making sure the world contains more realistic creatures that'll interact with the player in a number of different ways as well as develop their own societies.

# Overall Requirements
As an incoming student you should meet these general requirements:

* Intermediate level Java skills
* Knowledge of version control, preferably Git (the project is hosted on GitHub)
* Experience with an IDE such as IntelliJ or Eclipse would be helpful

More specific requirements (if any) can be found listed with corresponding proposals.

To earn some bonus points familiarize yourself with the [[Codebase Structure]] and the [concepts of our entity system](Entity-System-Concepts). Get an [overview of the project](Project-Overview) and [get set up](https://github.com/MovingBlocks/Terasology/wiki/Dev-Setup)!

# How to get involved

The sooner you contact us the better! As mentioned above, [set up your environment](Dev-Setup), browse through our [Issue Tracker](https://github.com/MovingBlocks/Terasology/issues) and get your hands on some minor fixes or a simple module.

If you have any questions don't hesitate to enter #terasology on [Freenode IRC](https://webchat.freenode.net) or post a thread in our [dev portal forum](http://forum.terasology.org/forum/developer-portal.5).

Here is a more step-by-step guide:

* Check our [main site](http://forum.terasology.org), look at the source code and read the available guidelines
* Pick an idea that you think is interesting from the ideas list or come up with your own idea.
* Get familiar with what exactly GSOC is! We can provide you with some information to get started, and most of the time give you some feedback, but its still *you* working out an idea.
* Post an introduction of yourself in our [intro forum](http://forum.terasology.org/forum/contributor-introductions.7) and of what your interests are, including what you might like to do for GSOC
* After we know each other a bit and you've picked an item then write a draft proposal, posting updates in your intro thread.
* The contact people listed below aren't necessarily going to be your mentor - although some will mentor - but during discussion we'll find out who can be yours. By keeping the discussion open we might even find that the best mentor isn't even listed yet :-)

# Project Ideas

## Game / saved world / module preview image content

* https://github.com/MovingBlocks/Terasology/issues/1487
* Difficulty: Easy
* Contacts: ?
* Helpful skills: resource loading/locating, web design, presentation

This is a fairly straight forward addition to the create world / load game screens, and similar locations in the main menu. Currently we only use text to describe modules and worlds. But a picture is worth a thousand words!

When a player looks at an existing world we could present any screenshots the player has taken in that game, or if none have been taken use a logo or other placeholder graphic from the primary module.

For viewing modules you could again have logos or preview screenshots associated with each module. These could also be used on a module browsing site on GitHub or elsewhere.

For bonus points this could be extended into easy screenshot uploading (to imgur maybe?) or even in-game video recording made available along with the world as saved assets.

## Improve visibility of missing resource scenarios and general user reporting

* https://github.com/MovingBlocks/Terasology/issues/1402
* Difficulty: Easy to intermediate (depending on how deep you go down the rabbit hole)
* Contacts: [msteiger](http://forum.terasology.org/members/msteiger.1197), [skaldarnar](http://forum.terasology.org/members/skaldarnar.270)
* Helpful skills: familiarity with debugging, application lifecycle (initialization, disposal, etc), awareness of user report support frameworks

Currently we've put a fair amount of work into hardening the game against missing resources, crashes, and leaks, and want to improve that further and make even non-fatal warnings more visible.

We have our own [Crash Reporter](https://github.com/MovingBlocks/CrashReporter) project that'll catch most ways the game crashes then encourage the user to report the error back to us.

However, some issues are subtle and non-fatal, like some missing resources just not being drawn instead of crashing the game. And it could be easier yet to report back details.

Frameworks exist for better reporting of errors, warnings, metrics, and so on, sending them automatically to a database (if the user opts in). This would be a good next step.

## Agent-based simulation of land usage

* https://github.com/MovingBlocks/Terasology/issues/944
* Difficulty: Intermediate (most concept work already done, sample code available)
* Contacts: [msteiger](http://forum.terasology.org/members/msteiger.1197), [skaldarnar](http://forum.terasology.org/members/skaldarnar.270)
* Helpful skills: knowledge of procedural generation, advanced mathematics, AI

In order to define and place high-level structures in generated worlds, different usage areas must be identified. Different areas are preferable for one type of land usage or another.

Using the ContourTracer, different terrain features can be explicitly referenced (e.g. polygon shapes of lakes, forests, deserts, etc). 

Based on a set of environment-aware agents, the usage of these areas can be simulated.
As a result, farms would be settled in grassland areas while fishing lodges are placed at the shore.

On a different level, the location of entire settlements could be derived based on some simulation of optimality constraints.

## Noise-based generation of distinguishable terrain features

* https://github.com/MovingBlocks/Terasology/issues/943
* Difficulty: Intermediate (most concept work already done, sample code available)
* Contacts: [msteiger](http://forum.terasology.org/members/msteiger.1197), [MarcinSc](http://forum.terasology.org/members/marcin-sciesinski.1103)
* Helpful skills: knowledge of procedural generation, advanced mathematics, terrain generation

Infinite terrain worlds are typically generated by noise generators such as Perlin or simplex. While the generated patterns are aperiodic, no distinguishable terrain features are created.
Regions such as desert areas have only very little high-frequency noise while mountainous regions will have a lot. 

A first step could be to create abstract, large, high-level regions which are then refined depending on the type. Smooth transitions between such regions must be created.

Some regions such as lakes have additional requirements (flatness). Some effort on that particular issues has already been invested:

http://procworld.blogspot.com/2014/01/leveling-lakes.html

Sorted by difficulty, desired regions are: grassland, ocean, dessert, forest, mountain, lake.

## Leap Motion implementation

* https://github.com/MovingBlocks/Terasology/issues/934
* Difficulty: Intermediate (and need to have a Leap Motion Controller)
* Contacts: [Cervator](http://forum.terasology.org/members/cervator.2), [nh_99](http://forum.terasology.org/members/nh_99.1095), [begla](http://forum.terasology.org/members/begla.1)
* Helpful skills: user interface design, user experience (UX), library design

We did a proof-of-concept implementation for using the Leap Motion Controller in-game quite a while ago and actually made a video on it: http://www.youtube.com/watch?v=H8-afb0yUoc

While Terasology isn't really super apt for motion control there are some interesting niche areas like spell casting or flying that could lend some novelty if a user happens to have a Leap unit laying around. This is a fairly open-ended item on how it should work, although an external library named [Jitter](https://github.com/openleap/jitter) was started to help out the effort and fleshing it out further would be ideal.

A few existing contributors have Leap units (we've had some good contact with the company - they actually reached out to us first!) and some additionally have Oculus Rifts, which we can also support, so there could be some interesting combination potential there like Leap VR... :-)

## Mobile server management utility

* https://github.com/MovingBlocks/Terasology/issues/929
* Difficulty: Intermediate
* Contacts: [Immortius](http://forum.terasology.org/members/immortius.35), [mkienenb](http://forum.terasology.org/members/mike-kienenberger.1215)
* Helpful skills: mobile development (Android, _maybe_ iOS), web services, server software administration, user interface design

You can launch a Terasology server easily enough, but configuration is still pretty manual. We need to start expanding administrative options available and it would be very convenient (and a novel experiment to break into mobile land with) to also offer a small utility for smart phones and tablets to interact with a server, from managing users to viewing logs and maybe even observing from a map view (the AWT facade could hold some premise here)

Work on this item would go hand-in-hand with actual server configuration options being developed, and working on both at once would be a bonus.

There are likely existing similar utilities for administering MC servers that could be used for inspiration.

## Standalone NUI editor

* https://github.com/MovingBlocks/Terasology/issues/849
* Difficulty: Easy (to intermediate if supporting bonus features)
* Contacts: [Immortius](http://forum.terasology.org/members/immortius.35), [mkienenb](http://forum.terasology.org/members/mike-kienenberger.1215), [synopia](http://forum.terasology.org/members/synopia.1101)
* Helpful skills: user interface design, library design, JSON

We use our own "New UI" framework authored by Immortius. It works great but still relies on plain editing in text files and running the game to see how it turns out :-)

A standalone editor with a preview option would be an excellent utility for developers/modders and might also help NUI stand out as a library should it get extracted from the engine one day.

Bonus features could involve expanding into non-traditional GUI elements like those that would help support touch screen and other alternatives.

Immortius in particular knows the architecture well, along with a few others getting used to the framework.

*Update:* We have improved support for changing UI at runtime, reloading certain elements dynamically.

## Anatomy system

* https://github.com/MovingBlocks/Terasology/issues/465
* Difficulty: Easy to intermediate depending on selection of features
* Contacts: Assorted, [Aherber](http://forum.terasology.org/members/aherber.57/) (original combat author) if he can be reached, [glasz](http://forum.terasology.org/members/glasz.66) (models), [Immortius](http://forum.terasology.org/members/immortius.35), [UltimateBudgie](http://forum.terasology.org/members/ultimatebudgie.1205) (hunger)
* Helpful skills: biology, 3D modelling, Blender, JSON

This is a very open ended idea that could be approached in all sorts of ways:

* Procedural generation of creatures with differing organs, limbs, etc
* Combat system targeting parts of the body (external and internal) instead of working on straight HP (Dwarf Fortress style)
* Models with parts that can fall off when damaged
* Indirect affects such as diseases and poisons that damage a creature over (possibly very long) time

We actually had directional damage (physics-based) in the old combat system but its maintainer Aherber disappeared before it was committed :-(

A start on this could simply be defining a range of body parts in prefabs and components, differing them by creatures, and letting damage and/or effects target them randomly. Perhaps a ragdoll type display in-game showing affected parts of the body. Maybe a relation to the existing hunger system.

*Update:* Since this was suggested the engine has improved by leaps and bounds. We even have a system for procedurally generating flower textures, and another for handling plant genome/breeding.

## Android / OUYA compatibility

* https://github.com/MovingBlocks/Terasology/issues/464
* Difficulty: Hard (or easier for smaller pieces like touchscreen or controller support on Windows)
* Contacts: [mkienenb](http://forum.terasology.org/members/mike-kienenberger.1215), [Immortius](http://forum.terasology.org/members/immortius.35), [begla](http://forum.terasology.org/members/begla.1), [Cervator](http://forum.terasology.org/members/cervator.2), [MrBarsack](http://forum.terasology.org/members/mrbarsack.282)
* Helpful skills: Android development, advanced Java (annotations, bytecode manipulation, memory management), LibGDX, user experience (UX)

Cervator has a founder account and dev special OUYA so it would be nice if we were to put that to use one day! :D

Android compatibility is not a topic for the faint of heart, even if we're already in Java. We're abstracting LWJGL/OpenGL out of the engine to support different facades/renderers, possibly moving to LibGDX to support Android one day. There are also other parts of the code like our heavy usage of annotations or bytecode manipulation that could run into trouble on Android's flavor of Java.

mkienenb has started a 2D version of Terasology displayed in AWT that is our first added facade - this may be a very good exercise in developing the facade concept further and may even make some initial inroads on Android easier.

There are different pieces / stages to this implementation:

* Developing a touchscreen UI (tablets, or even standalone touch screens).
* Basic Android implementation able to do something with the engine or worlds (not necessarily full 3D display - like starting with a 2D AWT style facade)
* Game functional normally on Android
* Expanded options on OUYA with its local multiplayer options and controllers (could also theoretically develop support for controllers on PC)

## New rendering approach for very far distances

* https://github.com/MovingBlocks/Terasology/issues/319
* Difficulty: Unknown (intermediate or even straight forward for a fellow 3D wizard?)
* Contacts: [begla](http://forum.terasology.org/members/begla.1), [KaiKratz](http://forum.terasology.org/members/kai-kratz.53), [Immortius](http://forum.terasology.org/members/immortius.35), [manu3d](http://forum.terasology.org/members/manu3d.1256)
* Helpful skills: 3D graphics, LWJGL, OpenGL, rendering

This calls for a new rendering technique to support showing the world beyond normally visible chunks (where every block is rendered). The more distant detail would have to be reduced in some fashion to display the world in a more simplistic fashion at range. While there is a little more detail in the issue begla or KaiKratz would probably need to be consulted for more details, or any other 3D wizard we have with the know-how :-)

## Port advanced organic growth simulator from Python

* https://github.com/MovingBlocks/Terasology/issues/218
* Difficulty: Intermediate (most concept work already done, sample Python code available)
* Contacts: [Woodspeople](http://forum.terasology.org/members/woodspeople.34), [MarcinSc](http://forum.terasology.org/members/marcin-sciesinski.1103), [glasz](http://forum.terasology.org/members/glasz.66), [ddr2](http://forum.terasology.org/members/ddr2.178), [ahoehma](http://forum.terasology.org/members/ahoehma.801)
* Helpful skills: Python, procedural generation, biology

Long ago cfkurtz / Woodspeople reviewed some old work she had done and prepared a growth simulator in Python that bases its growth on available water and mineral values in the soil, among other things (sunlight!). While we've since gotten an initial "growing trees" implementation working that is sufficient for showcasing growth in-game (doesn't consider its location much) it could be amazing to take it one (to many) steps further!

At a minimum this would port the Python version to Java based on simulated values where no exact data currently exists

* Sunlight is available
* Soil nutrients could be approximated by soil type, possibly the block could even change as it is depleted (and fertilizer bring it back)
* Moisture could be based on distance to water or again on block type (while aquifers could later yield a more exact per-block moisture level)
* Custom block shapes could be added to get higher detail level for branches and other smaller tree components

Any additional detail in the original plant simulator could be considered for extras.

*Update:* Since this topic was originally posted we improved engine support to where a large amount of extra information can be included via per-block biome data. There are also several more advanced flora-related content modules.

## Advanced and dynamic geology based on plate tectonics

* https://github.com/MovingBlocks/Terasology/issues/141
* Difficulty: Hard (more supporting systems needed, possible interaction with native C code)
* Contacts: [Laurimann](http://forum.terasology.org/members/laurimann.586), [Nym Traveel](http://forum.terasology.org/members/nym-traveel.213), [Immortius](http://forum.terasology.org/members/immortius.35), [MarcinSc](http://forum.terasology.org/members/marcin-sciesinski.1103), [msteiger](http://forum.terasology.org/members/msteiger.1197), [skaldarnar](http://forum.terasology.org/members/skaldarnar.270)
* Helpful skills: geology, procedural generation, advanced mathematics, advanced Java (dealing with native code)

This item is for generating a world based on plate tectonics such as provided by PlaTec or some sort of simulated version. At a minimum it should be able to read maps generated separately from PlaTec (or some comparable source) and in turn prepare one or several layered maps usable in-game to guide placement of actual blocks such as minerals in appropriate layers. A series of bonus features are possible:

* Connecting to PlaTec natively from Java to C to request a map (and maybe to take advantage of extra per-step data)
* Visually showing the plates moving during world generation in a simple map view mode in-game
* Placement in the world of volcanic and other interesting biomes related to tectonics

An actual study of the involved sciences is best left to surfing Wikipedia although a certain level of artistic creativity to enhance gameplay value would be welcome :-)

