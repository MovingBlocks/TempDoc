While Javadoc may be more useful for just being present in code there might also be other niceties by having it around. Since generating it is effortless anyway, might as well!

## Generating it

To generate Javadoc for the project simply execute `gradle javadoc` at the root of the project. The actual `build.gradle` doesn't need to have any related scripting in it, the Javadoc Gradle plugin does it all!

Javadoc will generate to `Terasology/out/docs/javadoc`

**TODO**: We need to actually enable this in Jenkins and put it somewhere :-)
