# Alternative Git setups
This page describes alternative ways for setting up the project with different Git setups/GitHub clients and for other Java IDEs.

Of course, this guide is not complete. If you've got an alternative setup working please share it.

## Plain HTTPS (no SSH)
If you prefer not to use SSH you have to change ever `git@github.com:<user>` to `https://github.com/<user>`. When pushing changes to your fork you will be asked to enter your username and password for GitHub. Your password can be cached by a credential helper, see https://help.github.com/articles/set-up-git for more details.

## GitHub application (Windows, Mac)
An alternative to the Git command line tool is the GitHub application for Windows (http://windows.github.com/) or Mac (http://mac.github.com/). 

The application will set up Git and the SSH key for GitHub for you. When logged in to your GitHub account in the application you will see your fork of the repository. To clone the repo to your hard drive just click "clone". You can change the destination via the settings menu. 

After cloning was successful you will find the cloned repo under "local". If desired, you can change the branch via the application as well.

## Git-less setup
Rather than use Git at all you can simply download all source from entire repos via GitHub's `Download Zip` button, available at the bottom of the right-hand menu on the main repo page, such as https://github.com/MovingBlocks/Terasology

When you do this the zip will extract into a directory named something like `Terasology-develop`, or `Crops-master`. For the root project the directory shouldn't matter (although it may in some IDEs or other setups - plain `Terasology` is still best) but for modules you want to be sure to rename the directory so you have it at `/modules/Crops` and likewise for other modules.

Finally the modules won't have a build.gradle in their root directory, they normally get that during the download process through Gradle. You need to copy this in from the Core module in the root project. So `/modules/Crops/build.gradle` to `/modules/Crops/build.gradle`

Only after the build file in place can you run the game or generate IDE project files correctly. Otherwise the module will be ignored as invalid. Only keeping one copy of the file is to avoid having to push updates to every module ever as well as to safeguard our build server from rogue build files (precautions there delete any attempt to inject non-standard build scripting into the process).

If you don't mind having a local Git repo generated (just makes a `/.git` dir under `/modules/Crops/.git` that doesn't do anything) you can still safely use `gradlew fetchModuleCrops` instead which includes the copy of the Core build script. But grabbing zips instead can help if you need to download from somewhere else with no internet available on your developer machine. Gradle still needs internet access when it runs for the first time to download itself and required engine library files.

# Alternative Java IDEs
Although IntelliJ IDEA is the recommended IDE for Terasology you may want to use Eclipse, Netbeans or any other Java IDE of your choice. 

## Eclipse
If you want to work with Eclipse you have to change the Gradle command for generating project files as follows:

    > ./gradlew eclipse         # on Linux/Mac
    > gradlew.bat eclipse       # on Windows

After the project files are generated you can import the project to Eclipse using "Import -> Existing projects into the workspace" with "Terasology" as the root.

## Everything after this point is no longer needed, unless you are working with an older branch of the project


  Make sure that "search for nested projects" is checked!





__NOTE: There are currently some other issues that need to be handled  manually:__

1.

Force "natives" to be an eclipse project by creating a .project file for it.   This probably needs to be done before you import projects into Eclipse.  You will need to create "natives" by running `gradlew extractNatives` first.  The natives .project file can be as simple as this:

```
<?xml version="1.0" encoding="UTF-8"?>
<projectDescription>
	<name>natives</name>
	<comment></comment>
	<projects>
	</projects>
	<buildSpec>
	</buildSpec>
	<natures>
	</natures>
</projectDescription>
```

Once "natives" exists as a project, you can update the engine project's .classpath file to define an attributes section for the lwjgl jar file like this.  Pick the correct operating system -- the example below uses linux.

```
	<classpathentry exported="true" kind="lib" path="~/.gradle/caches/artifacts-26/filestore/org.lwjgl.lwjgl/lwjgl/2.9.0/jar/5654d06e61a1bba7ae1e7f5233e1106be64c91cd/lwjgl-2.9.0.jar" sourcepath="~/.gradle/caches/artifacts-26/filestore/org.lwjgl.lwjgl/lwjgl/2.9.0/source/c93326bd0f3a21f3b2c8c22b6f345ab6ca1dd683/lwjgl-2.9.0-sources.jar">
		<attributes>
			<attribute name="org.eclipse.jdt.launching.CLASSPATH_ATTR_LIBRARY_PATH_ENTRY" value="natives/linux"/>
		</attributes>
	</classpathentry>
```

This seems to work at least for Eclipse 3.4.1 through 4.3.1, which is the oldest and newest versions I have installed.

2.

You will need to remove from Core's .classpath the line referencing "Terasology/engine/build/testClasses"

3.

To run the project, you will need to change the current working directory to the root Terasology folder.  The easiest way to do this is to create a custom Eclipse launcher configuration, such as the following one -- copy it into your workspace's PC project as Terasology.launcher and update the WORKING_DIRECTORY path.

```
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<launchConfiguration type="org.eclipse.jdt.launching.localJavaApplication">
<stringAttribute key="bad_container_name" value="/PC/launchScripts/eclipse"/>
<listAttribute key="org.eclipse.debug.core.MAPPED_RESOURCE_PATHS">
<listEntry value="/PC/src/main/java/org/terasology/engine/Terasology.java"/>
</listAttribute>
<listAttribute key="org.eclipse.debug.core.MAPPED_RESOURCE_TYPES">
<listEntry value="1"/>
</listAttribute>
<stringAttribute key="org.eclipse.jdt.launching.MAIN_TYPE" value="org.terasology.engine.Terasology"/>
<stringAttribute key="org.eclipse.jdt.launching.PROJECT_ATTR" value="PC"/>
<stringAttribute key="org.eclipse.jdt.launching.VM_ARGUMENTS" value="-Xms128m -Xmx1024m"/>
<stringAttribute key="org.eclipse.jdt.launching.WORKING_DIRECTORY" value="<TERASOLOGY CHECKOUT DIRECTORY>/Terasology"/>
</launchConfiguration>
```
Related issues and discussion:

- http://forum.movingblocks.net/threads/eclipse-setup-fails-to-run.883/

- https://github.com/MovingBlocks/Terasology/pull/755
- https://github.com/Nanoware/Terasology/pull/58
- https://github.com/MovingBlocks/Terasology/pull/783

- https://github.com/Nanoware/Terasology/issues/54
- https://github.com/Nanoware/Terasology/issues/56
- https://github.com/Nanoware/Terasology/issues/57
