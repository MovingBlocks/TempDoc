We use the [Checkstyle](http://checkstyle.sourceforge.net/) project to help keep the codebase consistent with some code conventions. Said conventions are embedded within the configuration file at `config/checkstyle/checkstyle.xml`

When working an area please keep an eye out for existing warnings to fix in files you're impacting anyway. Make sure to run Checkstyle on any new files you add since that's the best time to fix warnings.

You can run Checkstyle either from an IDE or from the command line in the project root:

`gradlew check` All checks and tests

`gradlew engine:checkstyleMain` Checkstyle for just the engine's main source directory (would be `modules:MyModule:checkstyleMain` for a module of that name)

For more details see the forum thread at http://forum.movingblocks.net/threads/terasology-code-style-conventions.501/

## IntelliJ Integration

You should be able to use the Checkstyle plugin for at least IntelliJ and Eclipse. With this enabled you can run checks on individual files when on the Checkstyle tab. Here are sample instructions for one-time setup in IntelliJ:

1. Open Plugin-Manager under File->Settings->Plugins
1. Browse repositories ...
1. Search for "CheckStyle"
1. Install "CheckStyle-IDEA"

After that our automated customization should already have left the correct configuration in place for the plugin to find and use our rules. If not (or in other IDEs) you may have to find a Checkstyle configuration item and browse to our rule file at `config/checkstyle/checkstyle.xml`

## Eclipse Integration
1. Open Help -> Eclipse Marketplace
1. Search for "Checkstyle"
1. Install "Checkstyle Plug-In"
1. Open Properties for Project
1. Select "Checkstyle"
1. Switch to tab "Local Check Configurations"
1. Create a new configuration (Type="Project Relative Configuration", Name="Terasology", Location="/Terasology/config/checkstyle/checkstyle.xml")
1. Switch to tab "Main"
1. Choose Checkstyle "Terasology (local)"
1. Select "Checkstyle active for this project"

## Jenkins Integration

Checkstyle stats are calculated per build and turned into nifty metrics