Console Help
===============================

The in-game console (default key: `tab`) can be used both for chat and system commands, although there won't necessarily be anybody to chat with for a while

Copy paste is supported and you can use the up and down arrows to scroll through history. Additionally you can press `tab` again within the console with a partial command written to get full suggested command options.

Chat
---------

To send chat messages simply open the console and write anything that doesn't start with a /

Commands
---------

First a few quick notes:
* All commands must be prefixed with a single slash character: `/` - this is new with stable build 15
* Parameters should be spaced apart with no commas needed (also new). Strings should still be in double quotes
* Block and shape names are no longer case sensitive

Block related:
* giveBlock "Water" - Gives 16 water blocks
* giveBlock "IronPyrites", 42 - Gives 42 Iron Pyrite (Fool's Gold) blocks
* giveBlock "Clay" "Slope" - Gives you 16 clay blocks that are sloped
* giveBlock "Chest" - Gives you a Chest block you can place, activate ('E'), put stuff in, destroy, pick up, place elsewhere, find same stuff in it!
* giveBlock "Tnt" - Gives you 16 TNT blocks you can place and activate ('E') to blow up
* listBlocks - Lists all actively used blocks (have been loaded for the world)
* listFreeShapeBlocks - Lists all blocks that can be requested in any known shape
* listShapes - Lists the available shapes

Misc:
* teleport 42 42 42 - Warps the player to x = 42, y = 42, z = 42
* fullHealth - Fully restores the player's health
* gotoWorld "GhostTown" - Loads the world "GhostTown" if present, otherwise initializes a new world "GhostTown" with a randomized seed value
* gotoWorld "GhostTown", "Pie!" - Loads the world "GhostTown" if present, otherwise initializes a new world "GhostTown" with the seed value "Pie!"
