### Asset types

This list might be out of date. Therefore it is always a good idea to take a look at `org.terasology.asset.AssetType` when in doubt. The list should be read as follows:

    ENUM_ID(typeId, subDirectory, fileExtension, assetLoader)

And now for the actual asset list:

    PREFAB("prefab", "prefabs", null, null),
    SOUND("sound", "sounds", "ogg", new OggSoundLoader()),
    MUSIC("music", "music", "ogg", new OggStreamingSoundLoader()),
    SHAPE("shape", "shapes", "json", new JsonBlockShapeLoader()),
    MESH("mesh", "mesh", "obj", new ObjMeshLoader()),
    TEXTURE("texture", "textures", "png", new PNGTextureLoader()),
    SHADER("shader", "shaders", "glsl", new GLSLShaderLoader()) {
    MATERIAL("material", "materials", "mat", new MaterialLoader()),
    BLOCK_DEFINITION("blockdef", "blocks", null, null),
    BLOCK_TILE("blocktile", "blockTiles", "png", new TileLoader()),
    GUI_DEFINITION("menudef", "menus", "json", new MenuDefinitionLoader()),
    GUI_STYLE("guistyle", "guiStyles", null, null);

### Referencing an Asset from Java

To reference an Asset that has a loader assigned to it, you can do the following:

    AssetManager.load(new AssetUri(AssetType.TEXTURE, "engine:terasology"), Texture.class)

or

    AssetManager.load(new AssetUri("texture:engine:terasology"), Texture.class)

The previous statement will load the file `terasology.png` from the `textures/` subdirectory (see the "Asset types" section) and return it as an instance of the `Texture class. There is a shorthand available for loading textures, which does the exact same thing as above:

    AssetManager.loadTexture("engine:terasology")