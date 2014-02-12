# Google Summer of Code proposals

The items listed here are drawn from our issue tracker's GSOC category, suggesting tasks suitable to be worked by a student over a summer. As such they're generally time non-critical items fairly separated from more active areas. They may also end up being completed outside of GSOC and the issue may contain later updates than listed here (feel free to edit this page if you notice an outdated item or find a new one in the tracker not yet listed here). More links are likely also available in the issue linked in each section below.

More conceptual work is likely needed for most items and there may be existing contributors familiar with and able to help guide a student, beyond any mentors made available for GSOC normally. Other proposals are of course also welcome :-)

Newest issues are listed first and may be shorter on detail than older ones. Difficulties and contacts are best estimates

## Leap Motion implementation

* https://github.com/MovingBlocks/Terasology/issues/934
* Difficulty: Intermediate (and need to have a Leap Motion Controller - Cervator has a spare he's willing to part with)
* Contacts: Cervator, nh_99, begla

We did a proof-of-concept implementation for using the Leap Motion Controller in-game quite a while ago and actually made a video on it: http://www.youtube.com/watch?v=H8-afb0yUoc

While Terasology isn't really super apt for motion control there are some interesting niche areas like spell casting or flying that could lend some novelty if a user happens to have a Leap unit laying around. This is a fairly open-ended item on how it should work, although an external library named [Jitter](https://github.com/openleap/jitter) was started to help out the effort and fleshing it out further would be ideal.

A few existing contributors have Leap units (we've had some good contact with the company - they actually reached out to us first!) and begla additionally has the Oculus Rift, which we also support, so there could be some interesting combination potential there ... :-)

## Mobile server management utility

* https://github.com/MovingBlocks/Terasology/issues/929
* Difficulty: Intermediate
* Contacts: Immortius (multiplayer), mkienenb (AWT facade)

While our headless server is still under heavy development it does launch! We need to start expanding administrative options available and it would be very convenient (and a novel experiment to break into mobile land with) to also offer a small utility for smart phones and tablets to interact with a server, from managing users to viewing logs and maybe even observing from a map view (the AWT facade could hold some premise here)

Work on this item would go hand-in-hand with actual server options being developed, and working on both at once would be a bonus. Although the headless server is likely to be more mature by the time GSOC coding actually begins.

There are likely existing similar utilities for administering MC servers that could be used for inspiration.

## Standalone NUI editor

* https://github.com/MovingBlocks/Terasology/issues/849
* Difficulty: Easy (to intermediate if supporting bonus features)
* Contacts: Immortius, mkienenb, synopia

Our "New UI" authored by Immortius is in-game and getting more complete every day. However, it can still be a bit tricky editing in text files and running the game to see how it turns out :-)

A standalone editor with a preview option would be an excellent utility for developers/modders and might also help NUI stand out as a library should it get extracted from the engine one day

Bonus features could involve expanding into non-traditional GUI elements like those that would help support touch screen and other alternatives

Immortius in particular can supply additional details and architecture hints, along with a few others getting used to the framework.

## Village / city generation

* https://github.com/MovingBlocks/Terasology/issues/466
* Difficulty: Easy (established codebase, active contributors, multiple related papers published on the web)
* Contacts: msteiger, skaldarnar, glasz, Nym Traveel, Perdemot, Ten'son'

This topic has actually become quite active since the original issue was created, with a Cities module and quite a few forum threads live. It is a huge field however and I'm sure our active contributors would appreciate the help in breaking ground on new features.

For instance currently the Cities module creates fully-grown cities from scratch, while an agent-based step-by-step city growth model has been suggested, declaring lots and slowly building them up over time. This would be a good way to maintain and keep cities dynamic.

Existing contributors can offer more guidance on this topic

## Anatomy system

* https://github.com/MovingBlocks/Terasology/issues/465
* Difficulty: Easy to intermediate depending on selection of features
* Contacts: Assorted, none actively working in the area. Aherber (original combat author) if he can be reached. Glasz for procedural models / pieces dropping off. Immortius for related architecture and animation. UltimateBudgie for hunger

This is a very open ended idea that could be approached in all sorts of ways:

* Procedural generation of creatures with differing organs, limbs, etc
* Combat system targeting parts of the body (external and internal) instead of working on straight HP (Dwarf Fortress style)
* Models with parts that can fall off when damaged
* Indirect affects such as diseases and poisons that damage a creature over (possibly very long) time

We actually had directional damage (physics-based) in the old combat system but its maintainer Aherber disappeared before it was committed :-(

A start on this could simply be defining a range of body parts in prefabs and components, differing them by creatures, and letting damage and/or effects target them randomly. Perhaps a ragdoll type display in-game showing affected parts of the body. Maybe a relation to the existing hunger system

## Android / OUYA compatibility

* https://github.com/MovingBlocks/Terasology/issues/464
* Difficulty: Hard (or easier for smaller pieces like touchscreen or controller support on Windows)
* Contacts: mkienenb, Immortius, begla, Cervator, MrBarsack

Cervator has a founder account and dev special OUYA so it would be nice if we were to put that to use one day! :D

Android compatibility is not a topic for the faint of heart, even if we're already in Java. While we're phasing LWJGL out of the engine to support different facades, with one still using LWJGL and another based on LibGDX to support Android, there are other parts of the code like our heavy usage of annotations or bytecode manipulation that could run into trouble on Android's flavor of Java.

mkienenb has started a 2D version of Terasology displayed in AWT that is our first added facade - this may be a very good exercise in developing the facade concept further and may even make some initial inroads on Android easier.

There are different pieces / stages to this implementation:

* Developing a touchscreen UI for Windows (tablets, or even standalone touch screens)
* Basic Android implementation able to do something with the engine or worlds (not necessarily full 3D display - like starting with a 2D AWT style facade)
* Game functional normally on Android
* Expanded options on OUYA with its local multiplayer options and controllers (could also theoretically develop support for controllers on PC)

## New rendering approach for very far distances

* https://github.com/MovingBlocks/Terasology/issues/319
* Difficulty: Unknown (intermediate or even straight forward for a fellow 3D wizard?)
* Contacts: begla, KaiKratz

This is a new rendering technique to support showing the world beyond normally visible chunks (where every block is rendered). The more distant detail would have to be reduced in some fashion to display the world in a more simplistic fashion at range. While there is a little more detail in the issue begla or KaiKratz would need to be consulted for more details, or any other 3D wizard we have with the know-how :-)

## Port advanced organic growth simulator from Python

* https://github.com/MovingBlocks/Terasology/issues/218
* Difficulty: Intermediate (most concept work already done, sample code available)
* Contacts: Woodspeople, MarcinSc, glasz, ddr2, ahoehma

Long ago cfkurtz / Woodspeople reviewed some old work she had done and prepared a growth simulator in Python that bases its growth on available water and mineral values in the soil, among other things (sunlight!). While we've since gotten an initial "growing trees" implementation working that is sufficient for showcasing growth in-game (doesn't consider its location much) it could be amazing to take it one (to many) steps further!

At a minimum this would port the Python version to Java based on simulated values where no exact data currently exists

* Sunlight is available
* Soil nutrients could be approximated by soil type, possibly the block could even change as it is depleted (and fertilizer bring it back)
* Moisture could be based on distance to water or again on block type (while aquifers could later yield a more exact per-block moisture level)
* Custom block shapes could be added to get higher detail level for branches and other smaller tree components

Any additional detail in the original plant simulator could be considered for extras.

## Advanced and dynamic geology based on plate tectonics

* https://github.com/MovingBlocks/Terasology/issues/141
* Difficulty: Hard (more supporting systems needed, possible interaction with native code)
* Contacts: Laurimann, Nym Traveel, Immortius, MarcinSc, msteiger, Skaldarnar

This item is for building an ore distribution technique based on plate tectonics such as provided by PlaTec or some sort of simulated version. At a minimum it should be able to read maps generated separately from PlaTec (or some comparable source) and in turn prepare one or several mineral maps usable in-game to guide placement of actual blocks. A series of bonus features are possible:

* Connecting to PlaTec natively from Java to C to request a map (and maybe to take advantage of extra per-step data)
* Visually showing the plates moving during world generation in a simple map view mode in-game
* Placement in the world of volcanic and other interesting biomes related to tectonics

An actual study of the involved sciences is best left to surfing Wikipedia although a certain level of artistic creativity to enhance gameplay value would be welcome :-)

## Noise-based generation of distinguishable terrain features

Infinite terrain worlds are typically generated by noise generators such as Perlin or simplex. While the generated patterns are aperiodic, no distinguishable terrain features are created.
Regions such as desert areas have only very little high-frequency noise while mountainous regions will have a lot. 

A first step could be to create abstract, large, high-level regions which are then refined depending on the type. Smooth transitions between such regions must be created.

Some regions such as lakes have additional requirements (flatness). Some effort on that particular issues has already been invested:

http://procworld.blogspot.com/2014/01/leveling-lakes.html

Sorted by difficulty, desired regions are: grassland, ocean, dessert, forest, mountain, lake.
