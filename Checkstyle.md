We use the Checkstyle project to help keep the codebase consistent with some code conventions. Said conventions are embedded within the configuration file at `config/checkstyle/checkstyle.xml`

While this was implemented fairly late and left open a lot of warnings we need to be smart about when we fix existing warnings. When working an area please keep an eye out for warnings to fix in files you're impacting anyway. Make sure to run Checkstyle on any new files you add since that's the best time to fix warnings.

The simplest way to run Checkstyle is from the command line in the project root:

`gradlew check`

For more details see the forum thread at http://forum.movingblocks.net/threads/terasology-code-style-conventions.501/

## IDE Integration

You should be able to use the Checkstyle plugin for at least IntelliJ and Eclipse. With this enabled you can run checks on individual files when on the Checkstyle tab. Here are sample instructions for setup in IntelliJ:

1. Open Plugin-Manager
1. Browse repositories ...
1. Search for "ChechStyle"
1. Install "CheckStyle-IDEA
1. Open Project
1. File / Settings...
1. Checkstyle
1. Add (select `config/checkstyle/checkstyle.xml`)
1. Edit properties: `samedir = config/checkstyle`

## Jenkins Integration

Checkstyle stats are calculated per build and turned into nifty metrics