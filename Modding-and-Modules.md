All the game content in Terasology is organized in _modules_ or _mods_, which are pretty the same.

> **Note:** In the upcoming builds the content has to be divided from the engine and is to be put into several
modules. When developing own modules, you should try to build against the modules and the [[Entity System
Architecture]] from the very beginning.

You can find more general information on modding here:
 * [[Modding API]]
 * [[Modding Guide]]

For specific information on different fields like new blocks, [[Crafting|Crafting-System]]-recipes and such please
have a look at the module's documentation.
 * [[Crafting System (Developer)]]
 * [[Procedural Architecture Grammar]]

> This list is to be continued.

# What are modules?
As everything should be a module, it becomes clear that there is no real _core functionality_ provided by the pure
game engine. Everything comes in seperate modules, and must be **enabled** when creating a new world.

The only module activated by default is the [[core module]], which contains some basic blocks and items like [[axe]]
and [[pickaxe]], [[chest]] and some more [[prefabs|prefab files]] for dropped items/blocks and the player itself.

All other modules have to be activated by the player on world creation time, using the mod selection menu in the
create new world dialog. There is already support for [[crafing|Crafting system]] and [[miniions]],
as well as modules which add more blocks to the game like fences or more light sources.
