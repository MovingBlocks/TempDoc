New blocks can easily be included in the game by creating a module with a `.json` block definition file. This article
 gives an overview of what can be specified in this files.

# General structure
The block definition files are structures as any other JSON document. For information see the JSON specification.

# Options

## Inheritance

Block definitions can extend from other block definitions, specifying just the features by which they differ. This simplifies creating classes of block (like plants).

 Option | Value(s)  | Default | Description
--------|:---------:|:-------:|-------------
**basedOn**   | _A block definition uri (e.g. "engine:plant")_ |  | Specifies the block to base this block on.
**template** | _true, false_ | false | If true, this block cannot be created and exists only to be based on.

## Informational

 Option | Value(s)  | Default | Description
--------|:---------:|:-------:|-------------
**displayName** | <string> | The file name of the block, with the first letter capitalised | The name of the block that is shown to players - particularly when the block is picked up and in their inventory.

## Core behavioural

 Option | Value(s)  | Default | Description
--------|:---------:|:-------:|-------------
**attachmentAllowed**   | _true, false_ | true  | Determines whether other blocks can be attached to this block.
**hardness**            | \<int\>       | 3     | Specifies the hardness of the block - effectively its health.
**liquid**              | _true, false_ | false | Determines if the block is a liquid.
**replacementAllowed**  | _true, false_ | false | Specifies whether the block can be replaced freely by other blocks - that you can place another block over it. **In order to make a block replaceable, it requires the block not to be targetable!**
**supportRequired**     | _true, false_ | false | Specify whether the block should be destroyed when no longer attached to any other block. **Only works for vertically adjacent blocks - e.g. grass is removed if the ground under it is destroyed**

## Tiles
By default, a block will try to use a tile texture with a matching filename. e.g. A block defined in Grass.json will use the block tile Grass.png from the same module.

You can specify a different tile to be used with the "tile" property:

    "tile" : "engine:grass"

You can also use different texture tiles for the different sides of the block. To do so,
you have to name the corresponding tiles in a `tiles` section of the block definition, e.g. for the chest block:

    "tiles" : {
        "sides"     : "core:ChestSides",
        "front"     : "core:ChestFront",
        "topBottom" : "core:ChestTopBottom"
    }

Possible block parts are
 * **all** to change every tile (same as using the "tile" property)
 * **topBottom** to change the top and bottom tile
 * **sides** to change the four horizontal sides (excluding only top and bottom) and can itself be overridden
 * **front, left, right, back, top, bottom** refer to the specific sides
 * **center** to change the tile on the center part of the block (see the section on shapes_

Option | Value(s)  | Default | Description
--------|:---------:|:-------:|-------------
**tile** | __a blockTile uri__ | A block tile with the same module and name as block definition | Specifies what blockTile to use to texture this block
**tiles**           |    |       | Allows the blockTile used by different parts/sides of the block to be overridden.
**doubleSided**     | _true, false_                     | false | Whether this block should be rendered double sided. This done for billboard plants to render both sides of polygons.
**invisible**       | _true, false_                     | false | If set to `true` the block is not rendered at all.
**translucent**     | _true, false_                     | false | Determine whether the block is translucent or not. Blocks with this option enabled can use textures with transparency. Moreover, translucent blocks do not prevent occluded blocks behind them from beeing rendered (blocks behind a translucent glass block are still displayed).
**shadowCasting**   | _true, false_                     | true  | Should this block cast a slight shadow around it?
**waving**          | _true, false_                     | false | Whether the blocks waves in the wind. Mainly used for grass and foliage.
**luminance**       | _\<int\>_                         | 0     | The light level of the block. The default torches have a light value of 15, for reference.

### Color Lookup tables (LUTs)
Color gradients can be used to change the color of specific blocks, e.g. grass or fooliage.

 Option | Value(s)  |  Description
--------|:---------:|-------------
**colorSource**     | _\<source\>_                    | e.g. `"colorSource" : "color_lut"`.
**colorSources**    |    | Enumerate the different color sources, `default` can be used to exclude LUTs for specific block parts.
**colorOffset**     | [R, G, B, A ]                     | Specify a color offset, e.g. given for red leaves: `"colorOffset" : '[2.0, 0.0, 0.5, 1.0']`.

## Collision related

Option | Value(s)  | Default | Description
--------|:---------:|:-------:|-------------
**penetrable**  | _true, false_ | false | A block is penetrable if it does not block solid objects.
**targetable**  | _true, false_ | true  | Define whether the block can be targeted for interactions. $$Must be set to `false` to allow direct replacement.$$

## Physics related
Option | Value(s)  | Default | Description
--------|:---------:|:-------:|-------------
**debrisOnDestroy** | _true, false_ | true  | If enabled destroyed blocks will drop a miniature instance of the block that can be picked up by the player.
**mass**            | _\<int\>_     | 10    | The mass value for the physics simulation.

> The mass does not seem to have any influence on the objects in the game.

## Entity integration
The options for enity integration are wrapped in the `entity` option, e.g. for a chest:

    "entity" : {
        "prefab" : "core:chest",
        "mode"   : "persistent"
    }

Option | Value(s)  | Default | Description
--------|:---------:|:-------:|-------------
**prefab**  | _\<prefab\>_      |               | The corresponding entity prefab for this block.
**mode**    | _\<EntityMode\>_  | onInteraction | Specify the mode for the entity. For information on the enity  modes see [[Entity Modes]].

## Inventory settings
The inventory settings have to be in an `inventory` section as well, e.g. again for the chest definition:

    "inventory" : {
        "stackable" : false,
        "directPickup" : true
    }

Option | Value(s)  | Default | Description
--------|:---------:|:-------:|-------------
**directPickup**    | _true, false_ | false | Whether this block should go directly into a character's inventory when harvested.
**isStackable**     | _true, false_ | true  | Determines whether the block type is stackable in the inventory.

## Mesh related

Option | Value(s)  | Default | Description
--------|:---------:|:-------:|-------------
**shape**   | _\<shape\>_         | "engine:cube" | Define the shape of the block. You can use either existing shapes or use self created ones. For more information, see [[Block Shapes in Blender]] or [[Shapes]] in general.
**shapes**  | _[\<shape\>,...]_    |               | You can restrict the usage of a block type to some shapes. If not explicitly defined, a block type can be instantiated as any available shape.

## Other options
> A lot more information is neede here!

 Option | Value(s)  | Description
--------|:---------:|-------------
**rotation**                    | "AlignToSurface", "horizontal"  |
**Blockpart specific options**  |                                   | You can specify different shapes for different attachment positions, like done for the torch block. See the example below.

    "sides" : {
        "shape" : "engine:TorchWall"
    },
    "top" : {
        "shape" : "engine:TorchGrounded"
    }

# Base new blocks on existing ones
Option | Value(s)  | Default | Description
--------|:---------:|:-------:|-------------
**basedOn**     | _\<blockName\>_ |       | You can base new blocks on existing ones, so you can create a template for similar blocks, like different foliage blocks.
**template**    | _true, false_     | false | Mark a block definition as template for other blocks.

# Block Families
> Note: [[Block Families | Block Family]] should probably get an own article.

You can specify the block category or family by

 Option | Value(s) | Description
--------|:--------:|-------------
**categories**  | _\<listOfCategories\>_    | Give a list of categories the block belongs to, e.g. new soil types might go into `"categories" : '["soil"']`.

# Temporary/deprecated

 Option | Value(s)  | Default | Description
--------|:---------:|:-------:|-------------
**craftPlace**          | _true, false_ | true  | Determines whether the player can open up the [[crafting system]] on this block.

# Suggestions
* Add soundfile specification for walking sounds on specific block types?
