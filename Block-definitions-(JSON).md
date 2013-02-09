New blocks can easily be included in the game by creating a module with a `.json` block definition file. This article
 gives an overview of what can be specified in this files.

# General structure
The block definition files are structures as any other JSON document. For information see the JSON specification.

# Options

## Overall behavioural

 Option | Value(s)  | Default | Description
--------|:---------:|:-------:|-------------
**attachmentAllowed**   | _true, false_ | true  | Determines whether other blocks can be attached to this block.
**craftPlace**          | _true, false_ | true  | Determines whether the player can open up the [[crafting system]] on this block.
**hardness**            | \<int\>       | 3     | Specifies the hardness of the block. If the value is very low, the block is easy breakable in the game. The specified value approximately corresponds to the number of hits necessary to destroy the block.
**liquid**              | _true, false_ | false | Determines if the block is a liquid. There's nothing special so far about it, just that the player can go through it. This may change with a new [[Liquid Simulation System]].
**replacementAllowed**  | _true, false_ | false | Spefifies whether the block can be replaced freely by other blocks. **In order to make a block replaceable, it requires the block not to be targetable!**
**supportRequired**     | _true, false_ | false | Specify whether the block should be destroyed when no longer attached to any other block. **Does work only for vertically adjacent blocks.**

## Rendering related
You can use different texture tiles for the different sides of the block. To do so,
you have to name the corresponding tiles in a `tiles` section of the block definition, e.g. for the chest block:

    "tiles" : {
        "sides"     : "core:ChestSides",
        "front"     : "core:ChestFront",
        "topBottom" : "core:ChestTopBottom"
    }

Possible block parts are
 * **sides** refers to all four sides (excluding only top and bottom) and can itself be overriden
 * **front, left, right, back, top, bottom** refer to the specific sides
> Are there other combinations possible (topBottom)?

Option | Value(s)  | Default | Description
--------|:---------:|:-------:|-------------
**tiles**           | _"\<blockPart\>" : "\<tile\>"_    |       | Specify the block tiles corresponding to the block parts. For non mentioned block  parts, the default block texture (texture with the same name) is used.
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
**colorSource**     | _"\<source\>"_                    | e.g. `"colorSource" : "color_lut"`.
**colorSources**    | _"\<blockPart\>" : "\source\>"_   | Enumerate the different color sources, `default` can be used to exclude LUTs for specific block parts.
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
**shape**   | _"\<shape\>"_         | "engine:cube" | Define the shape of the block. You can use either existing shapes or use self created ones. For more information, see [[Block Shapes in Blender]] or [[Shapes]] in general.
**shapes**  | _[ <shape>, ... ]_    |               | You can restrict the usage of a block type to some shapes. If not explicitly defined, a block type can be instantiated as any available shape.

## Other options
> A lot more information is neede here!

 Option | Value(s)  | Description
--------|:---------:|-------------
**rotation**                    | _{"AlignToSurface", "horizontal"_ |
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
**basedOn**     | _"\<blockName\>"_ |       | You can base new blocks on existing ones, so you can create a template for similar blocks, like different foliage blocks.
**template**    | _true, false_     | false | Mark a block definition as template for other blocks.

# Block Families
> Note: [[Block Families | Block Family]] should probably get an own article.

You can specify the block category or family by

 Option | Value(s) | Description
--------|:--------:|-------------
**categories**  | _\<listOfCategories\>_    | Give a list of categories the block belongs to, e.g. new soil types might go into `"categories" : '["soil"']`.

# Growth information for plants
> Note: Will it stay in the block definition or should that be controlled by a generator?

# Suggestions
* Add soundfile specification fo walking sounds on specific block types?
