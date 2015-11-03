You're probably wondering that yourself. Our answer: Minecraft is not suited  for what it has become. 
Minecraft was a smash hit and received a massive amount of support from a community, far exceeding what it was envisioned for, which lead to lackluster support for what the community wanted as fans could not directly improve the engine. Modding became minecraft largest community, but recieved no offical support, thus mods needed to be updated at every release. Which sadly can cause whole game types and communities to dissappear if the mod cannot remain up to date. 

We aim to create a technically superior voxel engine, to address the short commings of minecraft.



For example:

0. A mod API is our main and formost feature. For end users all module adding, updating, and downloading is handled through a simple GUI at world creations. Modules are automatically added at server join. Module packs exist for a tested and packaged experiance.

0. The creation of modules is simple, and if  behavior already exists, in libraries or frameworks, no java code is needed. Modules do not break beween versions, and dependacies are automatically handled. Json is used heavily.

0. A tiny core, all content should be added using modules. Freedom of gameplay

0. Infinite height and depth, commonly know as Cubic Chunks

0. Blocks and block shapes are seperate. Once you define a shape, all blocks will have that variation. 

0. 65,000 IDs for biomes, A biome is defined per grid space, allowing for vertical biomes.

0. Community controlled and community ran. 

0. Open source and gratis. All currently existing modules as well, but the licenses is to be decided by the Author. 

0. Its in java8(?)

For mod developers, a selection of libraries and frameworks has been created, to aid compataibility, and reduce duplication of work. Such as defining ores, common plants and how they grow, climate and weather, networking between blocks, how ores spawn etc. Modules are a good source of code refrence, for seasoned and budding mod developers alike.

  
#  Converting a minecraft mod to a terasology module

first get a working dev enviroment. 

    `git clone https://github.com/MovingBlocks/Terasology.git `

in the directory.
 
`./gradlew` then `./gradlew createModuleModuleName` then `./gradlew` again to autopopulate the folder.

you can go `./gradlew fetchModuleModuleName` if you want the source of an existing module instead. 

you can then do `./gradlew idea` if you prefer using an IDE, specifically the idea one, or `./gradlew eclipse` for the eclipse IDE. 


Unless you want to just manually create all the folders and files for a module, and place it in your module folder. 

___ 

textures can be placed in ModuleName/assets/blockTiles/auto 

(if you want to create multiple textures for a block that get randomized, simply create a folder by the block name, then put the textures with in it. blockTiles/auto/dirt/dirt1.png, dirt2.png, dirt3.png etc)

where a basic block with properties inherited is created. 

placing  texture(s) in ModuleName/assets/blockTiles/fancy 

and creating a simple json file of ModuleName/assets/blocks/BlockName.block

allows properties to be set, such as the shape it comes in, its display name, catagories its in, hardness, the textures for each sides, its mass,translucent, if you can go through it, if you can target it, its tint, its prefab, debrisOnDestroy, if it waves in the wind, color source, its rotation, if you can climb it, if it drops when you break it or if you directly pick it up, if it casts a shadow etc. 


creating a file in ModuleName/assets/prefabs/BlockOrItemName.prefab allows for the block or item to store data, becoming an entity. (as well as advanced data) Such as a chests ability to store items, and retain them inside when broken. Or torches needing a block to be on. Water being unbreathable, how items damage other items (like tools), the icons they use. Chests inventory being public to everyone, the sound it plays, the GUI screen it uses.  


assets/blockSounds for sounds of when you want on blocks, in the ogg format. 

assets/sounds for general sounds. 

assets/music for music, assets/music/ambiance for ambiance. 

define prefabs on how to trigger them. 





All with out a single line of java. You can even get custom ores spawning using the OreGeneration library. 



