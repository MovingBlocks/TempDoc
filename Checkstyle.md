We use the [Checkstyle](http://checkstyle.sourceforge.net/) project to help keep the codebase consistent with some code conventions. Said conventions are embedded within the configuration file at `config/checkstyle/checkstyle.xml`

While this was implemented fairly late and left open a lot of warnings we need to be smart about when we fix existing warnings. When working an area please keep an eye out for warnings to fix in files you're impacting anyway. Make sure to run Checkstyle on any new files you add since that's the best time to fix warnings.

The simplest way to run Checkstyle is from the command line in the project root:

`gradlew check` All checks and tests

`gradlew checkstyleMain` Checkstyle for "src/main/java"

For more details see the forum thread at http://forum.movingblocks.net/threads/terasology-code-style-conventions.501/

## IntelliJ Integration

You should be able to use the Checkstyle plugin for at least IntelliJ and Eclipse. With this enabled you can run checks on individual files when on the Checkstyle tab. Here are sample instructions for setup in IntelliJ:

1. Open Plugin-Manager under File->Settings->Plugin Manager
2. Browse repositories ...
3. Search for "CheckStyle"
4. Install "CheckStyle-IDEA
5. Open Project
6. File / Settings...
7. Checkstyle
8. Add (select `config/checkstyle/checkstyle.xml`)
9. Edit properties: `samedir = config/checkstyle`

Note: The color setting for Checkstyle warnings can be found and tweaked under Settings / Inspections / CheckStyle / Real-time scan (you can make a new Severity specific to checkstyle from there). It can be a little tricky to get the setting to take effect, try restarting IntelliJ if it doesn't seem to change.

## Eclipse Integration
1. Open Help -> Eclipse Marketplace
2. Search for "Checkstyle"
3. Install "Checkstyle Plug-In"
4. Open Properties for Project
5. Select "Checkstyle"
6. Switch to tab "Local Check Configurations"
7. Create a new configuration (Type="Project Relative Configuration", Name="Terasology", Location="/Terasology/config/checkstyle/checkstyle.xml")
8. Switch to tab "Main"
9. Choose Checkstyle "Terasology (local)"
10. Select "Checkstyle active for this project"

## Jenkins Integration

Checkstyle stats are calculated per build and turned into nifty metrics