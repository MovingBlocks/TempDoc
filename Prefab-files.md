- [Note: this page has not yet been checked for accuracy -- please remove this line once this page has been reviewed and all of the TODO items have been resolved]

### What is a [[Prefab|Entity-System-Architecture#prefabs]] file?

A prefab file is the definition of a [[entity|Entity-System-Architecture#entity-and-entityref]] type in Terasology, such as a block, structure, creature, or item. Like an entity it groups a collection of [[components|Entity-System-Architecture#component]] or other prefabs.

### Definition Format
Prefab definitions are a type of [[asset|Asset-System]] and are stored in the _assets_ directory of a module in the _prefabs_ directory.

Definitions consist of an component type name (lowercase) in quotes without the trailing "Component", followed by additional properties of that component type, which may in turn be other prefabs or components in addition to Terasology [[primitive types|Entity-System-Architecture#component-data-types]].  TODO: Immortius states that you can also create an EntityBuilder starting from a prefab -- more information needed.

### Inheritance -- TODO - copy from [[Entity-System-Architecture#prefabs]]

#### Example
The following prefab, which was defined in module LightAndShadow and stored in _assets/prefabs/minions_ has no default location specified in its **LocationComponent**, has the **[[SkeletalMesh|SkeletalMesh]]** stored in _assets/skeletalmesh/readQueen.md5mesh_, has a defined animation stored in _assets/animations/redQueenStill.md5anim_ which loops, and uses the material definition found _assets/material/redQueen.mat_.   It is a custom **MinionComponent** component (on the red side with a health of 300).  It has a **CharacterMovementComponent** as well as a **Spawnable** custom component.  There are also additional animations and sounds defined.

```
{
    "persisted" : true,
    "location" : {},
    "skeletalmesh" : {
        "mesh" : "lightAndShadow:redQueen",
        "material" : "lightAndShadow:redQueen",
        "animation" : "lightAndShadow:redQueenStill",
        "loop" : true
    },
     "Minion" : {
         "side" : "red",
	     "Healthtotal" = 300
   },
	"CharacterMovement" : {
    	"faceMovementDirection" : true
  },
  "Animation" : {
		"walkAnim" = "lightAndShadow:redQueenWalk",
		"idleAnim" = "lightAndShadow:redQueenStill",
		"attackAnim" = "lightAndShadow:redQueenStill",
		"dieAnim" = "lightAndShadow:redQueenWalk",
		"fadeInAnim" = "lightAndShadow:redQueenStill",
		"fadeOutAnim" = "lightAndShadow:redQueenStill",
		"workAnim" = "lightAndShadow:redQueenStill",
		"terraformAnim" = "lightAndShadow:redQueenStill",
		"randomAnim" : ["lightAndShadow:redQueenStill"]
	},
  "CharacterSound" : {
	    "footstepSounds" : ["Slime1", "Slime2", "Slime3", "Slime4", "Slime5"],
	    "footstepVolume" : 0.7
  },
  "Spawnable" : {
    "type" : "oreon"
  }
}
```

### Creating an entity based on a Prefab from Java
```
    @In
    private EntityManager entityManager;

[...]

    String prefabName = "module:prefabIdentifier";

    // Create an entity based on your prefab
    EntityRef minion = entityManager.create(prefabName);

    // Or Create an entity based on your prefab at a specific location and
    // if one of the components in the prefab is a LocationComponent,
    // set the worldPosition to startingPosition
    Vector3f startingPosition;
    EntityRef minion = entityManager.create(prefabName, startingPosition);

    // Or Create an entity based on your prefab at a specific location and rotation
    // if one of the components in the prefab is a LocationComponent,
    // set the worldPosition to startingPosition and the rotation to startingRotation:
    Vector3f startingPosition;
    Quat4f startingRotation;
    EntityRef minion = entityManager.create(prefabName, startingPosition, startingRotation);

    // A specific example of creating the LightAndShadow redQueen prefab next to the current player:
    LocalPlayer localPlayer = CoreRegistry.get(LocalPlayer.class);
    Vector3f worldPosition = localPlayer.getPosition();
    float x = worldPosition.x + random.nextInt(3)-1;
    float z = worldPosition.z + random.nextInt(3)-1;
    Vector3f spawnPosition = new Vector3f(x, worldPosition.y+1, z);

    String prefabName = "lightAndShadow:redQueen";
    EntityRef minion = entityManager.create(prefabName, spawnPosition);

```
