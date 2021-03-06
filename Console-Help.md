Console Help
===============================

The in-game console (default key: `tab`) can be used both for chat and system commands, although there won't necessarily be anybody to
chat with for a while.

Copy paste is supported and you can use the up and down arrows to scroll through history. Additionally you can press `tab` again within
the console with a partial command written to get full suggested command options.

Chat
---------

To send chat messages simply open the console and write anything that doesn't start with a `/`.

Commands
---------

First a few quick notes:
* All commands must be prefixed with a single slash character: `/`.
* Parameters should be spaced apart with no commas needed. Strings should still be in double quotes.
* Block and shape names are not case sensitive, in most cases you do not have to specify the module either.
* To list all available commands type `/help`.

In following some commands are explained in more detail. You may find module specific commands explained on the module's page.

Block related:
* The command to get some blocks is `/giveBlock "<blockName>" "<blockShape>" <amount>`. The last two arguments are optional. Some examples
are given below
    * `/giveBlock "Water"` - Gives 16 water blocks
    * `/giveBlock "Rutile" 42` - Gives 42 Rutile blocks (colorful mineral)
    * `/giveBlock "Clay" "Slope"` - Gives you 16 clay blocks in the "slope" shape
    * `/giveBlock "Marble" "Stair" 99` - Gives you 99 marble stair blocks
    * `/giveBlock "Chest"` - Gives you a [[Chest]].
    * `/giveBlock "TNT"` - Gives you 16 TNT blocks you can place and activate ('E') to blow up
* `/listBlocks` - Lists all actively used blocks (blocks that have been loaded for the world).
* `/listFreeShapeBlocks` - Lists all blocks that can be requested in any known shape.
* `/listShapes` - Lists the available shapes.
* `/placeBlock "Dirt"` - place a dirt block in front of the player.

Misc:
* `/help` - Show in-game help (more thorough)
* `/help "giveBlock"` - Shows detailed help on the "giveBlock" command
* `/teleport 42 42 42` - Warps the player to x = 42, y = 42, z = 42
* `/fullHealth` - Fully restores the player's health

Keyboard Layouts:
* `/AZERTY` - set keyboard layout to _AZERTY_
* `/NEO` - set key bindings to _NEO 2_ layout  

See [[Key Bindings]] for more information.