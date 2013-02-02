This article is intended for (mod) developers that want to specify own (refinement) recipes in their mods. 
For the general usage of the crafting system in-game go to [[Crafting System]].

# Recipes
The whole craft system is based on recipes. All crafting (and refinement) results are based on these recipes. New recipes are defined via a "CraftRecipe" section in the _*.prefab_ files. 

You can change the behaviour of the recipes by specifying different options. These options will be explained in detail right after the section on basic recipe definitions.

## Recipe definitions
This section will explain the general structure of recipes. Therefore, the example of a pickaxe will be used. As already said, the _pickaxe.prefab_ must contain the following section:

    "CraftRecipe" : {}

The next step is to add the **"recipe"** subsection to the prefab file. Within this sections we will define the main recipse, i.e. specify the 3x3x3 matrix for the recipe. For convenience, you do not have to write down layers that are completely empty. Thus, our example for the pickaxe may end up like this:

    "CraftRecipe" : {
      "recipe" : {
		"bottom" :
		  [
		    "stone", "stone", "stone",
			" "	   , "stick", " ",
			" "	   , "stick", " "
		  ]
      }
    }
	
In general you will specify recipes with more than just one layer like in the following:

    "CraftRecipe" : {
      "recipe" : {
		"bottom" : [ ],
		"middle" : [ ],
		"top"    : [ ]
      }
    }
	
where **bottom**, **middle** and **top** denote the respective layers. For the content matrices, you can think of the bottom row to be closest to the player.

## Recipe Options
In addition to the simple recipe definition, you can specify several options to change the behaviour of the recipes. 
In the following list the options are explained in detail.

* **fullMatch** : If the value is `true` (by default) then the positions of elements in the craft block will be checked for exact positions in the recipe matrix. 
	This means given a recipe matrix <u>A</u>
	
		0 0 0
		1 0 0
		1 0 0
	and a craft block matrix <u>B</u>
	
		0 1 0
		0 1 0
		0 0 0
		
	that these two matrices are different, and thus the placed blocks in the crafting block do not match with the recipe <u>A</u>. 
	If the value of **fullMatch** is `false` both matrices, <u>A</u> and <u>B</u> are reduced to the more simple matrix
	
		1
		1
		
	and thus the given block configuration will match the recipe. The reduced matrices will be checked for equality by taking rotations into consideration. E.g. the following to matrices will match if **fullMatch* is set to `false`.
	
		1 1 1		1 0 0
		0 1 0		1 1 1
		0 1 0		1 0 0

	The option **fullMatch** still has some nuances. If you assing `false` to it, empty rows and columns may get deleted when matrices are compared. But this removal does only happen if the "space" in all cells of the row respectively column are not important to recipe. Think of some kind of recipe similar to the shoes recipe in good old Minecraft. 
	
		0 0 0 
		1 0 1
		1 0 1
		
	You do not want to end up comparing the recipe matrix like this:
	
		1 1
		1 1
		
	Thus, the space inbetween is preserved during the tranformation process, ending up in the simplified version
	
		1 0 1
		1 0 1
		
	If the recipe contains more than one layer the empty columns and rows will be removed when they are empty for all the matrices and contain no "important space". For example, in the following recipe where we use all three layers with option **fullMatch** set to false the two rightmost colums are removed.
	
		bottom	center	top				bottom	center	top
		1 0 0	1 0 0	1 0 0			1		1		1
		1 0 0	1 0 0	0 0 0	==>		1		1		0
		1 0 0	0 0 0   0 0 0			1		0		0
		
* **recipe** : The **recipe** option is used as described above. You may use up to three layers, each specified by its name. If a cell in the grid is empty, it is denoted by a space `" "`, if it should contain a specific item 
	or block you denote by the block/item name: `"stone"`, or `"engine:sand"` for a more specific notation.
	
* **resultCount** : Via the **resultCount** option you can specify the output for the crafted result. The default value is 1, but you can decide on any other integer value. 

To sum up the recipe definition and its options so far I want to give you the recipe for torches. Torches can be crafted out of a stick and one piece of coal, you will get four torches at once by crafting and the exact positions of blocks in the grid do not matter.

	"CraftRecipe" : {
	  "fullMatch"   : false,
	  "resultCount" : 4,
      "recipe" : {
		"bottom" :
		  [
		    " ", " ",     " ",
			" ", "coal",  " ",
			" ", "stick", " "
		  ]
      }
    }

## Refinements
You can specify a **refinement** by replacing the **recipe** subsection through a refinement subsection. 
Currently, the structure for this section is like the following:
  
    "refinement" : {
		"<instigator>:<target>:<resultCount>" : {
			"instigator"  : "<instigator>",
			"target"      : "<target>",
			"resultCount" : "<resultCount>"
		}
	}
	
Where the types mentioned are defined as follows:

* _<instigator>_ : The block or item that is used to refine another element. The instigator is the block/item that the player must select in the toolbar.
* _<target>_ : A block or item in the craft block the player is pointing at. The target is the block that will be refined in the refinement process.
* _<resultCount>_ : everything should be clear with that ;)

> **Note:** The way how refinements are specified will change within the next versions!
