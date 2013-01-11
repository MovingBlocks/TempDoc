# Introduction

While you _could_ write block shape definitions by hand, it is also possible to define them in blender.

## Installing Terasology Block Shape Addon

* First you will want to install blender - Blender 2.60 was used when developing the addon, but it should hopefully be compatible with similar versions.
* Obtain the Terasology project, as described on the [[Dev Setup]] page. Alternatively you can download the addon manually from  https://github.com/MovingBlocks/Terasology/tree/develop/blender_addons
* In the project, you will find a directory called blender_addons, with a sub directory called io_mesh_terasology. 

Copy this entire directory into `[your blender install directory]/[your blender version]/scripts/addons` (typically something like `C:\Program Files\Blender Foundation\Blender\2.60\scripts\addons`). 

* Start Blender, and open the user preferences page (under the File menu). On the Addons tab find the "Import-Export: Terasology Block Shape Export" addon and activate it by checking the box on the right.
* While you are in the user preferences page, you may wish to go to the System tab and uncheck Mipmaps. This will prevent blender from blurring the pixels of textures, allowing you to see them as they will appear in-game.

## Fundamentals

A block shape in blender is a set of meshes corresponding to the various parts of the block shape. For each side and the center part of the block shape, a mesh of the same name can be present (Top, Bottom, Left, Right, Front, Back and Center). Additionally extra meshes can be used to define the collision for the block shape.

All the information in [[Shape Architecture]] may be useful, but some additional pointers:
* Blocks should be created centered on the origin
* A standard block is half the scale of a new Blender cube
* Blender axes are different from Terasology's axes, and are instead as follows:

**Sub-block** / **Direction**
* Center 
* Top / +Z axis
* Bottom / -Z axis
* Front / -Y axis
* Back / +Y axis
* Left / +X axis
* Right / -X axis

Notes:

* Do not scale in Object mode, only in Edit mode
* When UV mapping, you should map against a single 16x16 texture, not the image manifest.

## Terasology Properties

<img src="https://raw.github.com/MovingBlocks/Terasology/develop/src/main/resources/org/terasology/data/blockTiles/Brick.png"/> (TODO: Put the right image somewhere)

The Terasology Block Shape plugin adds a properties pane to Blender. The first two items are universal (not based on what mesh you have selected):
* Author - who created this shape
* Auto-generate Collider - if checked, then a Collider will be created that encapsulates all the meshes composing the block shape

The next two properties are set for each mesh
* Full Side - does this mesh fill the side it is for. That is, if this side is against another blocks side, would that other block side be completely obscured
* Is AABB Collider - should this mesh be used to generate a collider. This can be used by non-side mesh.

## Related Links

* [[Shape Architecture]]
* [[German Tutorial|http://terasologyblog.de/2012/08/tutorial-erstellen-eines-json-blockes]]