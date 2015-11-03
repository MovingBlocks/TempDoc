You're probably wondering that your self. Our answer: Minecraft is not suited  for what it has become. 

We aid to create a technically superior voxel engine, in order to address the short commings of minecraft.

For example:

*A mod API is our main and formost feature, modules are easily created, easily added, and do not break beween versions. 

*Infinite height and depth, commonly know as Cubic Chunks

*Blocks and block shapes are seperate. Once you define a shape, all blocks will have that variation. 

*65,000 IDs for biomes, A biome is defined per gride space, allowing for vertical biomes.

*Community controlled and community ran

*Open source and gratis, as well most modules. 


This is in sharp contrast to Minecraft, which you need to pay a sum of money just to own, and are restricted on what you can do with the code. 

Now, unless you install mods or develope mods, this means nothing for you. You've already bought minecraft, and you're happy, even happier if you're a windows10 user and got the windows10 version for free. 


This one will hit home for the building type: Dynamic block shapes. Shapes are seperate from blocks. We define a shape, and now all blocks have that variation. So yes, that means every blocks comes in a slab, stair, pillar, slope(s), colom, axel, stack, small cube, smaller cube, vertical slab, etc.... even the things you don't think about, like a dirt block in the shape of a torch. Still not enough, you can define your own shapes in Blender. 



Now here is the real intresting part: we natively include a mod API and it is our main feature. Perhaps you are just a player, who doesn't know how to install mods, or just wants to play a packaged version.  Perhaps you love installing mods, or perhaps you make mods yourself. Good news for all. 


Installing mods (we call them modules) is as simple as clicking which ones you want in a menu when you create a world. All dependancies handled, downloaded, updated, you name it. You join a server and all the mods will be automatically downloaded and configured. All stable modules organized in one place, new modules automatically showing up in menu.  Maybe you don't want to choose your own, thats fine as well, module packs can and are created for a packaged and tested game experiance, just like vanilla minecraft, or mod packs for minecraft. Unlike Minecraft mods, these don't break between versions! No need to waste your time waiting for a mod loader to update, or update your mod to a new version. 



Now, you ask, "As a mod developer why should I care, i'd have to do all that work to convert my mod over" 

Well, for one, you don't have to learn a new language, we're still in java (8 to be exact), and secondly, since we have a API, you don't have to worry about having to update it or change your code. Because of the API you can do quite a lot with out knowing any java, all in json. 

To prevent the duplication of work, we have a nice selection of frameworks and libraries. No longer will you have to worry about ores or compatability, we have an ore/mineral library of 121. As well as a collection of other libraries and frame works. Like a Soils and sand one, a one to add genetics, one for plants/trees and growing, one for weather/climate. 

Its recommend you look at the modules yourself to see how they're made, and tweak an add to them. Perhaps even contributing to them if you think it fits. So in the act of good will, it'd be nice if you made your modules gratis, and open source (under apache 2.0) so others can learn, improve, and in general just reduce the amount of work needed. After all, you could put your plant in the plant library, and everyone could help improve it and maintain it, and easy compatability between modules is achieved. . 

So if you're a wannabe mod creator, Terasology is right for you. Come look at these sands, https://github.com/Terasology/Soils/tree/master/assets/blockTiles/auto/sands , they're new simple blocks being created by litterally putting a texture in a folder, no coding needed. 

Look at this, https://github.com/Terasology/Soils/blob/master/assets/blockTiles/fancy/BlackSand.png A fancy block has been created simply by giving it a texture, and defing some properties in a textfile in json https://github.com/Terasology/Soils/blob/master/assets/blocks/fancy/BlackSand.block 


If you're not creating new behaviors, you won't need to do any java coding at all. Which, is again, a reason for everyone to help contribute to libraries, less duplication of work, and more time for things  you actually want to do. 