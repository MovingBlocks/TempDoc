## Introduction
This is a tutorial on how to make a block with which the user can interact with.
## Defining the block
Firstly we need to define the actual block. A block is a text file ending with ".block". It needs to be placed in the assets/blocks directory. Example: To add a HiddenChest block to the module WoodAndStone you would put the file under:
`modules/WoodAndStone/assets/blocks/HiddenChest.block`

The block file is json. For the start we will put the following content into the text file:
```
{
    "attachmentAllowed": false,
    "rotation": "horizontal",
    "tiles": {
        "sides": "Core:GreenLeaf",
        "front": "Core:ChestFront",
        "topBottom": "Core:ChestTopBottom"
    },
    "entity": {
        "prefab": "WoodAndStone:HiddenChest"
    },
    "inventory": {
        "stackable": false
    }
}
```
### Specifiying the texture of the block
With the tiles object it is possible to specify cube like blocks with up to 6 different textures on the side of the block. The "tiles" object can have the following properties:
* all
* sides (-> 4 horizontal sides)
* topBottom
* top
* front
* back
* left
* right
* center
The generic ones like sides can be overriden by specic ones like front.

The properties of the "tiles" object need to be set to texture identifiers. A texture
identifer has the following structure:
* <module name>:<tile image name without extension>
Any image under assets/blockTiles in module can be referenced that way.

### Other block properties
Feel free to explain them

## Specifing the entity of the block
With the `entity` property of the block it is possible to specify which entity is representing the block. The sub property "prefab" takes a prefab identifer. Like with texture identifiers, the value before the conon specifies the module in which the prefab is in. The value after the conon specifies the extension less filename of the prefab. Prefabs files should be placed in the assets/prefabs directory and must have the extension .prefab. Example:
* assets/prefabs/HiddenChest.prefab

In a prefab you specify which components your entity has by default.
Every class that extends from Component can be used as a property in the prefab file.
All component classes end with "Component". The property has the same name like the component class except that it lacks the suffix. For example an instance of the InteractionTargetComponent class can be added to the prefab, by adding a property called InteractionTarget.

The following prefabs makes the block behave like a chest with 4 item slots:
```
{
    "Inventory": {
        "privateToOwner": false,
        "itemSlots": [
            0,
            0,
            0,
            0
        ]
    },
    "PlaySoundAction": {
        "sounds": "engine:click"
    },
    "InteractionTarget": {},
    "InteractionScreen": {
        "screen": "engine:containerScreen"
    }
}
```
The Inventory component makes the entity have an inventory. The 4 zeros mean that there should be 4 empty slots.

The PlaySoundAction component makes the entity play a sound when it gets activated with E

The InteractionTarget component makes it possible to start an interaction with the component by pressing E while the cursor is on the block. An interaction for itself is invisible to the user, until you add a visualization for it.

The InteractionScreen component makes it possible to specify an UI screen, which will automatically be opened when the user starts an interaction with the block. Closing that UI will automatically end the interaction with the block. The InteractionScreen component has a property called "screen". It specifies which UI should be opened.

