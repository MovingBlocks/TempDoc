# Alternative Git setups
This page describes alternative ways for setting up the project with different Git setups/GitHub clients and for other Java IDEs.

Of course, this guide is not complete. If you've got an alternative setup working please share it.

## Plain HTTPS (no SSH)
If you prefer not to use SSH you have to change ever `git@github.com:<user>` to `https://github.com/<user>`. When pushing changes to your fork you will be asked to enter your username and password for GitHub. Your password can be cached by a credential helper, see https://help.github.com/articles/set-up-git for more details.

## GitHub application (Windows, Mac)
An alternative to the Git command line tool is the GitHub application for Windows (http://windows.github.com/) or Mac (http://mac.github.com/). 

The application will set up Git and the SSH key for GitHub for you. When logged in to your GitHub account in the application you will see your fork of the repository. To clone the repo to your hard drive just click "clone". You can change the destination via the settings menu. 

After cloning was successful you will find the cloned repo under "local". If desired, you can change the branch via the application as well.

# Alternative Java IDEs
Although IntelliJ IDEA is the recommended IDE for Terasology you may want to use Eclipse, Netbeans or any other Java IDE of your choice. 

## Eclipse
If you want to work with Eclipse you have to change the Gradle command for generating project files as follows:

    > ./gradlew eclipse         # on Linux/Mac
    > gradlew.bat eclipse       # on Windows

After the project files are generated you can import the project to Eclipse using "Import -> Existing projects into the workspace". Make sure that "search for nested projects" is checked!


__NOTE: There are currently some other issues that need to be handled  manually:__

1)

Force "natives" to be an eclipse project by creating a .project file for it.   This probably needs to be done before you import projects into Eclipse.  It can be as simple as this:

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
			<attribute name="org.eclipse.jdt.launching.CLASSPATH_ATTR_LIBRARY_PATH_ENTRY" value="../natives/linux"/>
		</attributes>
	</classpathentry>
```

This seems to work at least for Eclipse 3.4.1 through 4.3.1, which is the oldest and newest versions I have installed.

2)

To run the project, you will need to change the current working directory to the root Terasology folder.  The easiest way to do this is to create a custom Eclipse launcher configuration, such as the following one -- copy it into your workspace's PC project as Terasology.launcher and update the WORKING_DIRECTORY path.

```
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<launchConfiguration type="org.eclipse.jdt.launching.localJavaApplication">
<stringAttribute key="bad_container_name" value="/PC/launchScripts/eclipse/Terasology.launch"/>
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
