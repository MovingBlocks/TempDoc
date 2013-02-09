New blocks can easily be included in the game by creating a module with a `.json` block definition file. This article
 gives an overview of what can be specified in this files.

# General structure
The block definition files are structures as any other JSON document. For information see the JSON specification.

# Options
In the following all the options are specified in the form
```"<option>" : <possibleValues>, '[<default>'] - <description>```.

## Overall behavioural
* **"attachmentAllowed" : {true,false}, '[true'] ** - determines whether other blocks can be attached to this block.

* **"craftPlace" : {true,false}, '[true'] ** - determines whether the player can open up the [[crafting system]] on
this block.

* **"hardness" : <int>, '[ 3 ']** - specifies the hardness of the block. If the value is very low,
the block is easy breakable in the game. The specified value approximately corresponds to the number of hits
necessary to destroy the block.

* **"liquid" : {true,false}, '[false'] ** - determines if the block is a liquid. There's nothing special so far about
it, just that the player can go through it. This may change with a new [[Liquid Simulation System]].

* **"replacementAllowed" : {true,false}, '[false'] ** - spefifies whether the block can be replaced freely by other
blocks.
> In order to make a block replaceable, it requires the block not to be targetable!

* **"supportRequired" : {true,false}, '[false'] ** - specify whether the block should be destroyed when no longer
attached to any other block.
> Does work only for vertically adjacent blocks.

## Rendering related
You can use different texture tiles for the different sides of the block. To do so,
you have to name the corresponding tiles in a `tiles` section of the block definition, e.g. for the chest block:

    "tiles" : {
        "sides"     : "core:ChestSides",
        "front"     : "core:ChestFront",
        "topBottom" : "core:ChestTopBottom"
    }

* **"tiles" : { <tiles> } ** - specify the block tiles corresponding to the block parts. For non mentioned block
parts, the default block texture (texture with the same name) is used.
    * **sides** refers to all four sides (excluding only top and bottom) and can itself be overriden
    * **front, left, right, back, top, bottom** refer to the specific sides

* **"doubleSided" : {true,false}, '[false'] ** - Whether this block should be rendered double sided. This done for
billboard plants to render both sides of polygons.

* **"invisible" : {true,false}, '[false'] ** - If set to `true` the block is not rendered at all.

* **"translucent" : {true,false}, '[false'] ** - determine whether the block is translucent or not. Blocks with this
option enabled can use textures with transparency. Moreover, translucent blocks do not prevent occluded blocks behind
them from beeing rendered (blocks behind a translucent glass block are still displayed).

* **"shadowCasting" : {true,false}, '[true'] ** - Should this block cast a slight shadow around it?

* **"waving" : {true,false}, '[false'] ** - Whether the blocks waves in the wind. Mainly used for grass and foliage.

* **"luminance" : <int>, '[0'] ** - The light level of the block. The default torches have a light value of 15,
for reference.

### Color Lookup tables (LUTs)
Color gradients can be used to change the color of specific blocks, e.g. grass or fooliage.
* **"colorSource" : "<src>"** - e.g. `"colorSource" : "color_lut"`.

* **"colorSources" : { <sources> } ** - enumerate the different color sources, `default` can be used to exclude LUTs
for specific block parts.

* **"colorOffset" : '[R, G, B, A '] ** - specify a color offset, e.g. given for red leaves: `"colorOffset" : '[2.0,
0.0, 0.5, 1.0']`.

## Collision related
* **"penetrable" : {true,false}, '[false']** - a block is penetrable if it does not block solid objects.

* **"targetable" : {true,false}, '[true']** - determine whether the block can be targeted for interactions.
> Must be set to `false` to allow direct replacement.

## Physics related
* **"debrisOnDestroy" : {true,false}, '[true']** - If enabled destroyed blocks will drop a miniature instance of the
block that can be picked up by the player.

* **"mass" : <int>, '[10']** - The mass value for the physics simulation.
> Does not seem to have any markable influence at all.

## Entity integration
The options for enity integration are wrapped in the `entity` option, e.g. for a chest:

    "entity" : {
        "prefab" : "core:chest",
        "mode"   : "persistent"
    }

* **"prefab" : <String>** - The corresponding entity prefab for this block.

* **"mode" : <EntityMode>, '[on_interaction']** - specify the mode for the entity. For information on the enity
 modes see [[Entity Modes]].

## Inventory settings
The inventory settings have to be in an `inventory` section as well, e.g. again for the chest definition:

    "inventory" : {
        "stackable" : false,
        "directPickup" : true
    }

* **"directPickup" : {true,false}, '[false']** - Whether this block should go directly into a character's inventory
when harvested.

* **"isStackable" : {true,false}, '[true']** - Determines whether the block type is stackable in the inventory.

## Mesh related
* **"shape" : "<shape>", '["engine:cube"']** - Define the shape of the block. You can use either existing shapes or
use self created ones. For more information, see [[Block Shapes in Blender]] or [[Shapes]] in general.

* **"shapes" : '[ <shape>, ... ']** - you can restrict the usage of a block type to some shapes. If not explicitly
defined, a block type can be instantiated as any available shape.

## Other options
* **"rotation" : {"AlignToSurface", "horizontal"}** -
> Note: Add info here!

* **Blockpart specific options** - You can specify different shapes for different attachment positions,
like done for the torch block:

    "sides" : {
        "shape" : "engine:TorchWall"
    },
    "top" : {
        "shape" : "engine:TorchGrounded"
    }

> Note: More information is needed here.

# Base new blocks on existing ones
* **"basedOn" : "<blockName>"** - You can base new blocks on existing ones, so you can create a template for similar
blocks, like different foliage blocks.

* **"template" : {true,false}, '[false']** - mark a block definition as template for other blocks.

# Block Families
> Note: [[Block Families | Block Family]] should probably get an own article.
You can specify the block category or family by
* **"categories" : <listOfCategories>** - give a list of categories the block belongs to,
e.g. new soil types might go into `"categories" : '["soil"']`.

# Growth information for plants
> Note: Will it stay in the block definition or should that be controlled by a generator?

# Suggestions
* Add soundfile specification fo walking sounds on specific block types?
