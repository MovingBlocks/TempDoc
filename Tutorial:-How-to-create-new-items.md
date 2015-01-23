# Introduction
This short tutorial shows some ways to create your own items. This covers the required *prefab* for the item as well as how to specify a texture or icon for the new item.

# Defining the item
A quite general base for a new item is the following prefab. The content goes into a file with name `awesomeAxe.prefab` (or whatever the item should be called) under the `assets/prefabs` folder of your module. 

```json
{
	"parent" : "engine:iconItem",
  "DisplayName" : {
    "name": "My Awesome Axe"
  },
  "Item" : {
  	"icon" : "engine:items.Axe",
  	"renderWithIcon" : true,
  	"damageType" : "axeDamage"
  }
}
```

This will give the item two components (see the [[Entity System Architecture]] page for more information), the `DisplayName` component and the `Item` component. The statements within the component specifications define attributes of the components (see [[Prefab Files]] page). 

In this case, our item gets the name *"My Awesome Axe"* via the first component. In the second component the used visuals are specified. We reuse the default axe icon and tell the game to render the item via the icon. To learn more about icons and textures go to the section about [Using Icons and Textures](#Using Icons and Textures). Furthermore, the new item retrieves the *axe damage* as damage type. 

In order to see what else can be tweaked and set via these components have a look at the repsective Java classes (`DisplayNameComponent.java` and `ItemComponent.java`). Moreover, check out other item prefabs to see which other components are already in use, to which module they belong (possible dependency), and how to use them. 

__TODO:__ Explain some basic components, e.g., Durabilty, Crafting via recipes, ... 


# Using Icons and Textures
There are several ways of retrieving textures for your item. Basically, you can either reference a single icon file or an icon from a texture atlas.

## Single File Textures
If you want to start simple with a single item you can do so with just one prefab file and one icon image. The graphic goes under `assets/textures`, e.g., `assets/textures/awesomeAxe.png`. Then the `"icon": ...` line in the prefab is replace with the following:

```json
{
	...
  "Item" : {
  	"icon" : "myModule:awesomeAxe",
  	...
  }
}
```

## Texture Atlas
A [[Texture Atlas]] is used to divide a big texture or image into smaller chunks and allows to easily reference these parts. For instance, an item spreadsheet may contain several item icons side-by-side, each of them having a size of 32x32 pixels. The texture atlas now tells us where the axe item is. 

The following snippet shows how to access the *myAxe* texture from the *myItems* atlas in your module. The atlas file would go to `assets/atlas/myItems.atlas` and the used texture file would go into the `textures` subfolder again.

```json
{
	...
  "Item" : {
  	"icon" : "myModule:myItems.myAxe",
  	...
  }
}
```


## Reuse Textures
Instead of using your own textures, you can reuse existing icons and images from other modules. Therefore, just reference them appropriately (either from an atlas or as single file) as desribed above, but make sure to use the correct module prefix. If you are using another module's asset, make sure to put it in the list of dependencies. 

The following snippet shows how to use the *magic axe* icon form the *items* atlas from *some other* module.

```json
{
	...
  "Item" : {
  	"icon" : "otherModule:items.magicAxe",
  	...
  }
}
```
