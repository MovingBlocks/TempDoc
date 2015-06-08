# Versioning Guideline
## Version format and reasoning

For multiplayer it is important that we don't release two modules with the same version number but different content.

During development however it is helpful when modules that aren't yet fully compatible can still be tested with each other.

The idea is that during development all modules have a SNAPSHOT suffix. Not only in their jar form but also in source form to make clear that they are not final releases.

Versions are always set to the next number that will be released + SNAPSHOT suffix. That makes it clear for everyone what the next release number will be.

The version number format is:
```<major>.<minor>.<patch level>```
For time being major will however always be set to 0.

While major is 0, a change in minor version indicates an API breaking change, while a <patch level> increment indicates that nothing got broken yet.

After a release only the patch level version number will be incremented in the hope that no API breaking change is made.

After an API breaking change the minor version number is only incremented once till the next release, even if there are other API breaking changes. That way dependent modules don't need to be marked unnecessarily often as compatible.

When an API breaking change is made we can mark all (snapshot versions of) dependent modules as compatible so that we can test them. Their dependencies need to be updated anyway and if we do it now or later does not matter much. Of course before a module gets released it must be fixed.

The automatic update of the dependency to the "api changing module/engine" is only done on the branch "develop". It is still possible to have other branches at which stable versions of modules are developed that are compatible with the old engine or library.

## Specifying a dependency

The dependencies of a module are specified in the module.txt file that can be found in the root directory of a module.

The module.txt is a text file in the json format. The json objectin that file can have a field called "dependencies". If it doesn't have one yet look at other files to see how it is done. To define a single dependency to the Core module in 0.54.* you would set the dependencies field to:
```
    "dependencies" : [
            {
                "id" : "Core",
                "minVersion" : "0.54.0"
            }
    ],
```
If the first major part of the version number is 0 like in the example, then the exlusive maximum version is one minor version higher. Thus the following would also specify a 0.54.* dependency:
```
    "dependencies" : [
            {
                "id" : "Core",
                "minVersion" : "0.54.0",
                "maxVersion" : "0.55.0"
            }
    ],
```

The above version range includes the version 0.54.0 and 0.54.0-SNAPSHOT and excludes the version  0.55.0 and 0.55.0-SNAPSHOT. Any other 0.54.* version like 0.54.2 is also included.


## Todo list when you make an API breaking pull request

If the patch level is not 0 already (0.x.0-SNAPSHOT), trigger a build or script that does the following:
* It increases the version number from 0.x.y-SNAPSHOT to 0.x+1.0
* It sets the maxVersion dependency field of all dependent modules to 0.x+2.0 (= compatible with 0.x+1.*) 
* Optionally: Set the minVersion dependency field of all obviously broken dependent modules to 0.x+1.0

Wait if the build server to tell you which modules are broken or test it for yourself. 

When a module you care about needs to be fixed do the following:
* Add/change the dependency to minVersion = 0.x+1.0 (It may be set already in which case you don't have to do anything)
* Create a pull request for that module

## Todo list when you make a release

When you are publishing the jar, do the following (ideally via a script/jenkins task):
* Check for each dependency if there had been at least one non snapshot release in the specified range.
* Change the version number from 0.x.y-SNAPSHOT to 0.x.y and release it as 0.x.y. 
* Instantly afterwards change the version number from 0.x.y to 0.x.(y+1)-SNAPSHOT. 
* When the version number is 0.x.0, increase the exclusive maxVersion field of all dependent modules to 0.x+1.0, if that hasn't been done already. Release the dependent modules like this one.