# Alternative Git setups
This page describes alternative ways for setting up the project with different Git setups/GitHub clients and for other Java IDEs.

Of course, this guide is not complete. If you've got an alternative setup working please share it.

## Plain HTTPS (no SSH)
If you prefer not to use SSH you have to change ever `git@github.com:<user>` to `https://github.com/<user>`. When pushing changes to your fork you will be asked to enter your username and password for GitHub. Your password can be cached by a credential helper, see https://help.github.com/articles/set-up-git for more details.

## GitHub application (Windows, Mac)
An alternative to the Git command line tool is the GitHub application for Windows (http://windows.github.com/) or Mac (http://mac.github.com/). 

The application will set up Git and the SSH key for GitHub for you. When logged in to your GitHub account in the application you will see your fork of the repository. To clone the repo to your hard drive just click "clone". You can change the destination via the settings menu. 

After cloning was successful you will find the clonde repo under "local". If desired, you can change the branch via the application as well.

# Alternative Java IDEs
Although IntelliJ IDEA is the recommended IDE for Terasology you may want to use Eclipse, Netbeans or any other Java IDE of your choice. 

## Eclipse
If you want to work with Eclipse you have to change the Gradle command for generating project files as follows:

    > ./gradlew eclipse         # on Linux/Mac
    > gradlew.bat eclipse       # on Windows

After the project files are generated you can import the project to Eclipse. Make sure that "search for nested projects" is checked!
