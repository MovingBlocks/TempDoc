This page is a stub, help us expand it!

Right now all that exists on the block architecture is this:

All blocks are defined in .block files in the assets/ folder for the mod they are contained in.  These files can be given certain attributes, which allow the blocks to be associated with block textures. These textures are usually stored as simple .png files in the assets/blockTiles/ directory. Note that only the block attributes below can be included in the .block file, any additional metadata a programmer wishes to attach to a block class must be specified in the associated .prefab file, which is located in the mod folders assets/prefabs subfolder.

Block Attributes:

 // If not specified, is the ProperCase of the file name
    "displayName" : "Block",
    "liquid" : false,
 
    // Copies and then overrides settings from another block
    "basedOn" : "engine:plant",
    // If true, this block exists only for being based on, and shouldn't become an actual block
    "template" : false,
 
    // The shape of the block, cube if there are any issues
    "shape" : "engine:cube",
    // If specified, creates a block family based on the settings for each shape - not compatible with "rotation"
    "shapes" : ["engine:cube", "engine:stair", "engine:slope"]
 
    // The rotation type of the block. If horizontal or align to surface, then makes a block family combining the different rotations needed
    "rotation" : "none/horizontal/alignToSurface",
 
    "sides/top/bottom" : {
        // both which parts to have for align to surface, and what override settings they should have. Can override any of the other setting (allows torch to have a different shape when on the ground, for instance)
    },
 
 
    // Hardness 0 for indestructable, maybe make that a separate flag too?
    "hardness" : 3,
 
    // Can other blocks be attached to this. Should add settings for this per side of the block
    "attachmentAllowed" : true,
    // Whether this block should be destroyed if the below block is destroyed, should adapt this for
    // other cases like torches on walls.
    "supportRequired" : false,
 
    // Can the block be passed through like a liquid or air
    "penetrable" : false,
    // Can the block be targeted by the player
    "targetable" : true,
 
    "invisible" : false,
    // Whether the texture is masked (need a separate flag for semi-transparent?)
    "translucent" : false,
 
    // Should both sides of the mesh be rendered (for billboards)
    "doubleSided" : false,
    // Is Faux SSAO (shadows) created around this block
    "shadowCasting" : true,
    "waving" : false,
 
  "luminance" : 0,
 
    // The image to use.  Defaults to the tile with the same uri as the block.
    "tile" : "engine:stone",
    // Or can specify per side
    "tiles" : {
        "all" : "engine:stone",
        "sides" : "engine:stone",
        "topBottom" : "engine:stone",
        "center" : "engine:stone",
        "left" : "engine:stone",
        "right" : "engine:stone",
        "top" : "engine:stone",
        "bottom" : "engine:stone",
        "front" : "engine:stone",
        "back" : "engine:stone"
    },
 
    // Special color maps
    "colorSource" : "default/color_lut/foliage_lut",
    "colorSources" : {
        "all" : "default",
        // per side options again, same as tiles
    },
 
    // Color tinting, can be a 3 or 4 dimensional color.
    "colorOffset" : [1,1,1,1],
    "colorOffsets" : {
        // again, per side options as per tiles
    },
 
    // Not yet functional because of physics system work needed, but the mass of the block debris
    "mass" : 10,
 
    // Whether the block becomes debris
  "debrisOnDestroy" : true,
 
    "entity" : {
        // The entity prefab associated with this block (maybe allow it to be inlined?)
        "prefab" : "engine:chest",
        // Whether the entity should be persistant
        "temporary" : false,
        // whether changes to the components of an entity are persisted
        "keepActive" : true
    },
 
  "inventory" : {
        // Should the block go straight into the havester's inventory
        "directPickup" : false,
        "stackable" : true
    }