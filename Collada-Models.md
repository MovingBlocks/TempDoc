Terasology directly supports models in Collada format.  Our support for static mesh models is mostly complete, while our support for animation -- controllers/visual scene nodes/animations -- is a work in progress (More sample models needed!)

## Importing Static Meshes
To import a static mesh model, copy your collada .dae file into the "**assets/mesh**" folder.

You will then need to create a prefab file in order to represent your model.  Your prefab will need a Mesh Component, with the "mesh" attribute containing the name of the dae file (without the .dae ending) and a "materal" file describing how to texturize your model.   The prefab file will need to be placed in the "**assets/prefabs**" folder.  As an example, if you had MyAnimalModule containing a "dogA.dae" file, you could use something like this:

```
{
    "persisted" : true,
    "Location" : {
    },
    "Character" : {},
    "Mesh" : {
        "mesh" : "MyAnimalModule:dogA",
        "material" : "engine:vertexColored"
    }
}
```

Mesh is the only requirement, but most meshes will want a Location and will likely be a Character as well.

If your model only uses colored vertexes, such as a model exported from VoxelShop, then you can use "engine:vertexColored" as your material.  If your model uses a texture image, you will need to manually create a Terasology material file and place it into the "**assets/materials**" folder, as we do not currently use the material information contained in the collada file.   Copy the texture image into the "**assets/textures**" folder.   If your image texture file were named "dogB.png", you would create a dogB.mat file that looks like the following:

```
{
    "shader" : "engine:genericMeshMaterial",
    "params" : {
        "diffuse" : "MyAnimalModule:dogB",
        "colorOffset" : [1.0, 1.0, 1.0],
        "textured" : true
    }
}
```

Currently, only one texture image is supported, and the texture image must be in png format.

Collada allows a wide range of exported data formats, so it is possible that your particular internal geometry format is not yet supported.  Check your console log to insure that your model loaded properly, and open an issue if your static mesh was not able to be loaded.

Terasology uses a unit of 1 meter, and as long as you have specified the correct scale for your model, the importer will make the necessary adjustments.  Note that VoxelShop also uses a unit of 1 meter, so this likely will need to be changed to something else after you export to a collada file.

To use your model, use the console "spawnPrefab <prefab-name>" command.   For example, if your prefab is named "dogC.prefab", then type "spawnPrefab MyAnimalModule:dogC"

## Importing Skeletal Meshes
A collada file can also be dropped into the "assets/skeletalMesh" folder to be parsed as SkeletalMesh.  However this support is pre-alpha and unlikely to produce a functional result at this time.  For now you will need to convert these models into md5 format (although providing your original model and your converted md5 model would go a long way towards getting full support for Collada in place!)

