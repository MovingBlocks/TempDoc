This page should give you an overview of how Terasology uses textures and how you can use them on your own.

# Location
The textures can be found in the `asset` folder of the main programme or some modules. The different textures are
then ordered by their intended usage, e.g. `blockTiles` or model textures.

# BlockTiles
A very basic use of textures are the _blockTiles_, the textures for single blocks. They can be found in the
`blockTiles` subfolder of the `asset` folder.

At the moment the size of block textures is restricted to **16x16 pixels**. They are stored as **.png** files and can
 contain transparency, e.g. for colored Glass.

Block textures need to have the same name as the corresponding JSON block definition to be auto loaded.

# Related links
* [[Asset System]]
