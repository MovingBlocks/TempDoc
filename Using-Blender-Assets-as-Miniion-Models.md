### NOTE: This page assumes you have decent experience with Blender and are familiar with the features included.  It is not a tutorial on creating the models.

### NOTE: This page may contain errors, as it is heavily out of date.

---------------------------------------------

To start with, you will need a wavefront (.OBJ) model, complete with UV mapping, as well as a .PNG image containing the desired textures.

To use these assets, you will need to copy them to the correct location within a mod in the project.
Throughout the tutorial, when "asset folder" is said, it refers to, within the project, the directory \mods\<MOD NAME>\assets\.

PNG files go into the asset folder under the \textures\ sub-folder, while OBJ files go into the \mesh\ sub-folder.
NOTE: Since this project is in constant development, these locations may change.

Let's say, for example, that your model is called tutorial_model.obj, and the texture is called tutorial_model_texture.png - this is the example used for the tutorial.

### Create a Material
The first thing to do is to create a material for your model.  Material files are essentially JSON files that tell Terasology which image to load as a texture for the model.  These go into the asset folder underneath \materials\.  To do this, create a new file called "tut_model.mat", inside of the materials folder.  Open it up using a text editor of some sort.

In order to set up the material, put the following code within the file.

    {
        "shader" : "engine:genericMesh",
        
        "params" : {
            "diffuse" : "engine:IMAGE_NAME",
            "colorOffset" : [1.0, 1.0, 1.0],
            "textured" : true
        }
    }

The important things to get from this is the "params" block:

    "diffuse" : "engine:IMAGE_NAME",

where you change IMAGE_NAME to the name of your image, minus the extension - in this case, the line would look like this:

    "diffuse" : "engine:tutorial_model_texture"

Congratulations, you just created your first material file!

### Creating a Prefab
This is the next important step to the process.  We need a "prefab", which is another JSON file in which all of the various pieces are brought together.  This file will go in the assets folder under the \prefabs\ sub-folder.
Create a file called "tutorial_test.prefab" in this folder, and open it, again with a text editor.  Paste in the following code:

    {
        "name": "miniion:gelatinousMinion",
        "Minion" : {
            "icon" = "gelcube"
        },
        "Location" : {},
        "Mesh" : {
        "mesh" : "engine:tutorial_model",
        "material" : "engine:tut_model"
        },
        "CharacterMovement" : {
            "faceMovementDirection" : true
        },
        "SimpleMinionAI" : {},
        "AABBCollision" : {
            "extents" : [0.5, 0.5, 0.5]
        },
        "CharacterSound" : {
            "footstepSounds" : ["Slime1", "Slime2", "Slime3", "Slime4", "Slime5"],
            "footstepVolume" : 0.7
        },
        "Inventory": {
            "itemSlots": [
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0
            ]
        },
        "AccessInventoryAction": {}
}

A couple lines are of interest to us at this point :
first we want to give our model a name, you do this by modifying the line:

    "name": "miniion:gelatinousMinion",

into:

    "name": "miniion:tutorial_test_Minion",

this is merely an example, tuttestMinion is a index / key we will use later in the factory to reference our model.
notice the prefix miniion: which specifies what mod the prefab belongs to. Change this if you created your own mod.

Now that we changed the name, we need to specify the mesh and material to use.
Modify the line:

    "mesh" : "engine:testmonkey",

into:

    "mesh" : "engine:tutorial_test",

to let Terasology know you want it to render the tutorial_test.obj file.
then modify the line under it:

    "material" : "engine:monkeyHead"

into:

    "material" : "engine:tutorial_test_image"

notice again that I didn't specify the extension .mat again,
this line will tell Terasology to use the tutorial_test_image.mat file to color our model.
ignore the prefix engine: for now, just let it be.

Congratulations, you just finished creating a model for the miniions mod (or your own mod).
Now what's left is actually telling Terasology where to render your model in the world.
That's where the miniion mod comes in handy, I created a factory located in
\Terasology\src\main\java\org\terasology\mods\miniions\componentsystem\entityfactory
called MiniionFactory.java
Open that file and you will see something like this:

    package org.terasology.mods.miniions.componentsystem.entityfactory;

    import org.terasology.components.LocationComponent;
    import org.terasology.components.MeshComponent;
    import org.terasology.entitySystem.EntityManager;
    import org.terasology.entitySystem.EntityRef;
    import org.terasology.utilities.FastRandom;

    import javax.vecmath.Vector3f;

    /**
    * copied from @author Immortius
    * modified by @author Overdhose
    */
    public class MiniionFactory {

        private static final Vector3f[] COLORS = {new Vector3f(1.0f, 1.0f, 0.2f), new Vector3f(1.0f, 0.2f, 0.2f), new Vector3f(0.2f, 1.0f, 0.2f), new Vector3f(1.0f, 1.0f, 0.2f)};

        private FastRandom random;

        private EntityManager entityManager;

        // generates minion cubes for minion toolbar
        public EntityRef generateMiniion(Vector3f position, int index) {
            EntityRef entity = null;
            switch (index) {
            case 0: {
                entity = entityManager.create("miniion:monkeyMinion1");
                break;
            }
            case 1: {
                entity = entityManager.create("miniion:monkeyMinion2");
                break;
            }
            case 2: {
                entity = entityManager.create("miniion:monkeyMinion3");
                break;
            }
            case 3: {
                entity = entityManager.create("miniion:monkeyMinion4");
                break;
            }
            case 4: {
                entity = entityManager.create("miniion:monkeyMinion5");
                break;
            }
            case 5: {
                entity = entityManager.create("miniion:monkeyMinion6");
                break;
            }
            case 6: {
                entity = entityManager.create("miniion:monkeyMinion7");
                break;
            }
            case 7: {
                entity = entityManager.create("miniion:monkeyMinion8");
                break;
            }
            case 8: {
                entity = entityManager.create("miniion:monkeyMinion9");
                break;
            }
            default:
                entityManager.create("miniion:monkeyMinion1");
            }
            if (entity == null) {
                return null;
            }
    
            LocationComponent loc = entity.getComponent(LocationComponent.class);
            if (loc != null) {
                loc.setWorldPosition(position);
                loc.setLocalScale(((random.randomFloat() + 1.0f) / 2.0f) * 0.8f + 0.2f);
                entity.saveComponent(loc);
            }

            MeshComponent mesh = entity.getComponent(MeshComponent.class);
            if (mesh != null) {

                int colorId = Math.abs(random.randomInt()) % COLORS.length;
                mesh.color.set(COLORS[colorId].x, COLORS[colorId].y, COLORS[colorId].z, 1.0f);
                entity.saveComponent(mesh);
            }
            return entity;
        }

        public FastRandom getRandom() {
            return random;
        }

        public void setRandom(FastRandom random) {
            this.random = random;
        }

        public EntityManager getEntityManager() {
            return entityManager;
        }
            public void setEntityManager(EntityManager entityManager) {
            this.entityManager = entityManager;
        }
    }

Now all you have to do is modify a line in the switch statement to add your own model,
and you will be able to summon your creation using the miniion toolbar.
let's say you want to summon your model in position 1 on the toolbar,
just modify the line:

    case 0: {
         entity = entityManager.create("miniion:monkeyMinion1");
         break;
    }

into:

    case 0: {
        entity = entityManager.create("miniion:tutorial_test_Minion");
        break;
    }

and that's all you need to do.

If you now launch the game, and activate the minion bar by pressing the "x" key and left click on a block while the first slot is selected,
it should show you the model you just created in the game. If you see the toolbar shows an icon but you don't see a model, most likely the engine had a problem reading your obj file and generated an error in the log.
Please try to locate the error and let us know on the forums / irc what the error is.
If all went well you should be seeing your model in game, so take a screeny and let us see your creation.
The explanation might seem a bit long, but it's actually quite simple once you done it 1 time,
it takes max 5 minutes to create another model.