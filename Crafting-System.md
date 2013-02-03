This article will give an overview of the TS Crafting System, provided by the "Crafting"-module.
The focus of this articel is on the in-games usage. For details on how to specify own recipes please go to [[Crafting System (Developer)]]. 

> **Note:** This article is based on the stable/master branch (stable build #22). Since the crafting system is under heavy development, the given information must not be valid for the development branch versions.

# General Information
We made the decision not to stick with a conventional solution via GUI for the crafting system but introduced an intuitive and innovative in-game approach. 
The crafting "place" is made up of 27 smaller blocks, placed in a 3x3x3 cube. By doing this, we achieve the possibility of three dimensional crafting. The crafting process itself is similar to known systems -- one places blocks/items in the crafting grid and - based on some recipe - can receive some craft result.

# Activation
The Crafting-Module is integrated in the stable builds starting from build #22. You can find the module listed in the _Mods windows_ when you create a new world. In order to active the craft system in the game, select the module's name in the list and click the **Activate** button. You can now use the craft system in your fresh created worlds.

![Active the "Craft System" in the mod list.](http://terasologyblog.de/wp-content/uploads/2013/02/TS-Crafting-tutorial-menu_3.jpg)


# Usage
This sections explains the main usage of the crafting system, including information on how to start the crafting process, how to effectively use the available features and how to actually craft new items.

## Start crafting process
To start a crafting process, you have to hold the **Q** key while holding a block or item in hand so that you see the charge indicator.
![Press and hold "Q".](http://terasologyblog.de/wp-content/uploads/2013/02/TS-Crafting-tutorial-start_crafting_1.jpg) 
When **right clicking** during charging on an existing block in the world, the craft blocks appears in front of you, with one instance of the item hold in hand already placed in the grid.
![The crafting grid with the initial placed block.](http://terasologyblog.de/wp-content/uploads/2013/02/TS-Crafting-tutorial-start_crafting_2.jpg)

## The craft block (Add and remove items)
The craft block is divided into 3 layers -- bottom, middle and top -- to make the placement of blocks/item practicable to the user. The navigation through the different layers works as follows: To go a layer up, press and hold **shift** and **click right**, that will move the interactable grid one layer up. To go one layer down respectively, press and hold **shift** and **left click** on your mouse.

To place the selected block/item in the grid, point with the crosshair on a specified cell and **right click**. If the cell is empty, the selected item will be inserted into the grid. If the cell does already contain an element of the selected type, the counter in the matrix is incremented by one. In the last case, if there is already an element in the cell which is different from the selected one, you will get the full amount of the placed block back to your inventory and a single instance of the selected block/item in hand is placed in the grid. 
If the block/item could successfully be placed, the amount of the selected block/item in the player's toolbar is decreased by one unit.

You can get placed blocks/items back by selecting them via the crosshair and **left clicking** on your mouse. 

## Add and remove multiple items
Furthermore, you can **hold the right or left mouse button** pressed to add or delete items continuously. Another way of adding a higher number of items to the grid at the same time is to hold **Q** to charge the number of items that will be added. The graduation is divided into 6 parts, each stands for 1/6 of the amount of items. Thus, charging to the half circle around the crosshair will place the half of the items in the grid. 

## Mini-Inventory
You may have noticed that you only have the items in your toolbar available for crafting. This difficulty was solved by the so called _mini-inventory_, which allows to scroll easily through your inventory. To access the mini-inventroy, press and hold **shift** and use the **mouse wheel** to scroll through the rows of your inventory. 
![The mini-inventory.](http://terasologyblog.de/wp-content/uploads/2013/02/TS-Crafting-tutorial-mini-inventar.jpg)

## Crafting
Now you know how to handle the crafting system, so we can start with the actual crafting. If you have arranged the blocks and items in the craft grid in a way such that the current configuration matches with some recipe, a _thought cloud_ appears over the craft block, containing an icon hint to the craft result. 
In order to receive the item, press **E** and you will get one (or another number, specified by the recipe) of the result item to your inventory. The amount of the used items in the craft block is decreased simultaneously.
![The thought-cloud at the top indicates that the placed blocks match with the pickaxe recipe.](http://terasologyblog.de/wp-content/uploads/2013/02/TS-Crafting-tutorial-crafting_1.jpg)

## Refinement
Finally, we have refinement left. Refinement is a simple form of changing an item's properties. In order to start the refinement process, selecet an item from you toolbar, press and hold **Q** and **right click** to bring up the craft block interface. The craft grid already contains an instance of the selected item. The item in the grid is called the _target_ of the refinement process. To perform the refinement, you need to have an _instigator_, which will "trigger" the refinement. Selecet the instigator item or block in your toolbar, point with the crosshair to the item in the crafting grid and you will see the thought cloud with the refined item in it. Now press **E** to receive to add the refined item to your inventory.
![Refinement of stone.](http://terasologyblog.de/wp-content/uploads/2013/02/TS-Crafting-tutorial-refinement.jpg)

# Related Links
* [[Crafting System (Developer)]]
* [Crafting (forum thread)](http://forum.movingblocks.net/threads/crafting.247/)
* [Video Tutorial (engl.)](http://www.youtube.com/watch?v=-cdhxguyMpA)
* [Video Tutorial (german)] (http://www.youtube.com/watch?feature=player_embedded&v=XwuAC8cy7mE&list=PLfqYgIZWs3YeLZDgDQ9ztKWvhKoPqNkX3)
* [Einführung in das Craftingsystem (terasologyblog.de)](http://terasologyblog.de/2013/02/einfuhrung-in-das-crafting-system/)
