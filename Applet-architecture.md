We offer an applet-version of Terasology for easy review in a light-weight version of the game that'll run in a browser. It won't be quite as easy to interact with saved worlds or use plugins this way, but it is the fastest way to check out the game!

## Overview

As of this writing we're using the LWJGL applet loader and signing our jar file so Groovy can do its thing (introspection / reflection) that's a little beyond what a normal applet is allowed within the Java security model. Everything is automated in the Gradle build of the application with the right target executed. A source HTML file exists under source control that we use to load the applet.

To get log output from a running applet you have to enable the Java Console at the OS level - in Windows look for the Java item in the Control panel. You <em>also </em>have to enable extra logging under the same Java item. To clear your applet cache (in case the applet is updated and it looks like you're still loading the old version) look under a path similar to

    C:\Users\[user]\AppData\Local\Temp\lwjglcache= (on Windows, anyway)

The logging ends up (on Windows) at a place like:

    C:\Users\[user]\AppData\LocalLow\Sun\Java\Deployment\log

Game data has been changed to save to a path like

    C:\Users\[user]\AppData\Roaming\.terasology

For needed enhancements see [the bugtracker](https://github.com/MovingBlocks/Terasology/issues?labels=Applet&sort=created&direction=desc&state=open&page=1&milestone=1)

## Developer Notes

The applet breaks a lot :P

We need to change the build process to automatically generate a list of classpath jars rather than have a hard coded list in the applet's html file. Until that happens jar changes sometimes will be missed for the applet and it'll break for a while.

On top of that the version of Java can matter a fair bit. Early 2013 there were some Java security holes getting patched that for a while broke the applet in Java 1.7 while 1.6 still worked (but was less secure). To be able to test multiple versions of Java locally the following parameter can be added to the applet tag:

`<param name="java_version" value="1.6*">`

## Related Links

   * [Signed Applets by Oracle](http://java.sun.com/developer/onlineTraining/Programming/JDCBook/signed.html)
   * [LWJGL applet loader](http://lwjgl.org/wiki/index.php?title=Deploying_with_the_LWJGL_Applet_Loader_-_Introduction)
   * [Tutorial page specific to Groovy in an applet](http://www73.pair.com/bgw/applets/GroovyDemo/)
      * Includes instructions for minimizing the size of the Groovy jar
   * [how to enable the Java Console for applet output if need be](http://www.java.com/en/download/help/javaconsole.xml)
