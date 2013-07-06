# Developer Setup

How to get set up with IntelliJ, Git, and other related tools for contributing to Terasology. Technical details ahead! Refer to the relevant websites for the various tools to learn more, this setup should get you able to run from source and develop locally but won't teach you how it all works :)

## Terminology

Git can be sort of confusing - see [[Fancy Git]] for more involved details. Here's a quick term list that'll be accurate assuming the steps below are followed:

* https://github.com - an online service storing remote Git repos for people and allowing easy forking of projects with lots of neat stats and graphs - in particular linking together commits from different contributors on the same project "tree" like at https://github.com/MovingBlocks/Terasology/network
* `repo` - a Git repository, which may be yours, and may contain more than one branch. `git remote -v` will state which remote repos a Git-tracked directory on your computer knows about (is "tracking")
* `branch` - one "collection" of code in a repo, which usually differs a little from other branches in the same repo. `git branch -avv` will tell you what you've got including mappings between local and remote branches
* `upstream` - general term referring to a repo away from yours that is closer to the "ultimate source" of a project (it may also be used as an alias, we're avoiding that for clarity - upstream does _not_ refer to anything specific for us)
* `origin` - Usually your remote repo you created on GitHub when you forked from MovingBlocks.  You clone from your personal fork to your local machine, hence the name **origin** of your local repo.  May also be listed as `remotes/origin/master` with "master" as the example branch
* `movingblocks` - reference to our remote Organization repo - likewise may be listed as `remotes/movingblocks/develop` and such.  In many GitHub guides, this would be the concept of a "upstream" repo.
* `master` - your local master branch. Should be paired with your `remotes/origin/master`
* `develop` - generally the place where the primary changes happen. More specific development may take place in "topic branches" (that are exactly what they sound like)
* `Commit` - submit changes to your local development environment (you have a local repo where stuff gets stored until you're ready to push somewhere remote) - allows you to keep better control of your local work via revisions
* `Push` - take changes from your local development environment and submit them somewhere else (usually to your remote `origin` repo). This can be a follow-up action to a Commit (IntelliJ has a "Commit and Push" option)
* `Pull` - retrieves updates from a remote repo (usually your `origin` or `movingblocks`) and puts them in your local repo.
* `Pull Request` - submit a request for _somebody else_ to pull code from your repo to theirs (usually means you're offering up your code for integration into an `upstream` repo)
* `Merge` - merges together unique changes made in different branches. `Pull` may turn into one of these if there are changes on both sides

## Steps

To be able to run Terasology from source (and potentially get started for contributing stuff!) follow these steps!

### Initial setup

Stuff you need! Download / install / register for the following (if you don't already have them handy)

* Download and install a recent Java SDK - http://www.oracle.com/technetwork/java/javase/downloads/index.html
 * Latest 1.6 is recommended (http://www.oracle.com/technetwork/java/javase/downloads/jdk6u35-downloads-1836443.html)
 * Set JAVAHOME.  This is listed under trouble-shooting below, but if you're going to do this better to know now than after a couple of things have failed.
* Git for source control - http://git-scm.com/download
 * Pick the option to run Git from the Windows Command Prompt (middle option) and check out windows, commit unix (that is, if you're on Windows)
 * Optional (Windows): Git provides an option to add the Git Bash folder to the Windows path - I didn't do this had a couple of problems. 
 * You can otherwise follow the install steps at this tutorial: http://help.github.com/win-set-up-git/
* IntelliJ for IDE - http://www.jetbrains.com/idea/download
 * You can start with the free community edition - if you become a regular contributor we have a [[freebie open source project license for the Ultimate edition|http://forum.movingblocks.net/threads/intellij-12-has-been-released.652/]]
* Sign up for GitHub - https://github.com/signup/free
 * Keep following the steps at http://help.github.com/win-set-up-git/ to *set up your SSH key* in particular
   * Parts of that guide have been moved to https://help.github.com/articles/generating-ssh-keys

### Configuration

Follow these instructions to get ready to run from code - unless you're a core contributor with Push access to the main repo, you can then use the MovingBlocks section on [[Fancy Git]] instead - no fork needed

* "Fork" the project by opening https://github.com/MovingBlocks/Terasology and clicking the little fork button in the upper right
* Note the url to your fork, should be something like `git@github.com:[user]/Terasology.git` or `https://github.com/[user]/Terasology.git` if you're using the Windows native version.
* You can **either** set up once from the command line (suggested) or start with IntelliJ (get a new project via "Check out from version control" and follow the prompts)
   * Pick a working directory (like `C:\Dev` on Windows), bring up a command prompt there, then execute `git clone git@github.com:MovingBlocks/Terasology.git` (replace "MovingBlocks" with your username to use your own fork)
   * If you use IntelliJ then make sure only the _parent_ directory exists (Git won't check out into a project directory that already exists)
* This will clone the remote repo to your local drive - *NOTE:* this can take quite a while! Be patient for at least a few minutes :-)
* Open a command prompt in the directory you checked out into (so run `cmd` and do `cd C:\Dev\Terasology` or so) and execute `gradlew idea` there - this fetches the right version of Gradle automatically and builds the project config
* There's also a version for Eclipse - `gradlew eclipse` - more work on the project generation might be coming. See the Gradle section on [[Fancy Git]]
* Open the Terasology project in your shiny new source controlled directory
 * `File` -> `Open Project` -> select the root Terasology folder from your Git working directory. _**THIS IS VERY IMPORTANT!**_ If you try to import a gradle project than you have to go through and do things manually, which takes a very long time. You will also have many other issues.
* Go to the Version Control (may be CVS) menu / Enable Version Control Integration, and pick Git (prepares Git IDE integration)
* In the project explorer under `src/main/java`, navigate to `org/terasology/game/` and right-click `Terasology`, then pick run(see note if not available) to start the game!   
   * **Note:** If no run option available, right-click 'Terasology' and click `Compile`.  The Project Structure window may open under the Modules tab, asking you to set the SDK for the project.  Next to 'Module SDK: No Project SDK' click `New...`->`JSDK`(for some reason it seems you have to click this twice before it opens the next window)->Browse to and select SDK folder( _e.g._ jdk1.6.0_35, Googling `jdk path MyOSNameHere` will find lots of posts showing you how to find this path).  It may ask you if you want to setup the project, choose yes.


Extras:

* You can "Watch" the various repositories and "Follow" contributors on GitHub to more easily keep track of what's going on
* Look at the readme section on https://github.com/MovingBlocks/Terasology (scroll down) for instructions on what you can do - don't forget looking at the Options menu in-game to adjust the graphic settings as they default to minimum
* If you end up with heap size errors, you should add the VM option `-Xmx1024m` in the run configuration. (it will allow Java to use up to 1024m for the heap)

#### Common issues:

* Usually the project will find a 1.6 Java SDK and know about Java - if you get a massive amount of Java errors (or don't see the "Run" option on Terasology.java) you may have to check under File / Project Structure / Platform Settings / SDKs to see if you have a valid Java setup. Sometimes you may only have a 1.7 SDK installed, that will trigger this issue too. Just add the 1.7 and use that instead or install a 1.6.  
   * Click [HERE](https://raw.github.com/CallMeAsher/TeraMisc/master/wiki/AddSdkGuide.jpg) to see how to add the 1.6 SDK if IntelliJ doesn't show it by default.
* You may have to set your JAVA_HOME also - such as on Linux with a command like this: `export JAVA_HOME="/usr/lib/jvm/java-6-sun"`
* Outdated graphics card drivers can cause startup problems and some cards just seem quirky. Please post in the [Support Forum](http://forum.movingblocks.net/forums/support.20/) if you still have issues after installing your latest drivers and attach the log file from the /logs directory
* We've seen a Windows 7 machine once fail to use Git to communicate with GitHub properly from command line and IntelliJ, yet be okay with Git Bash. Turned out the user home dir wasn't set right, so Git couldn't find the SSH files. Solution was to set the `HOME` environment variable to the user's home directory (like `C:\Users\[Username]`). Git Bash was smart enough to do without.
* You may have to re-run =gradlew idea= occasionally if new project library files (jars) or settings are added/changed
* LWJGL and Java 1.7 on Macs may not work due to a JAWT dependency error. This is a known (and fairly critical) issue to LWJGL due to some changes in the Apple-Oracle (Apracle?) approach to Java on Macs. For now please use Java 1.6. See http://lwjgl.org/forum/index.php/topic,4326.0.html for more details
* On older versions of Java 1.6 you may get the following error on compilation - the solution is to upgrade to the latest 1.6 or even 1.7 (though that may bring other issues). More info at http://stackoverflow.com/questions/314572/bug-in-eclipse-compiler-or-in-javac
 * `type parameters of <T>T cannot be determined; no unique maximal instance exists for type variable T with upper bounds T,java.lang.Object`
* On Linux you may end up with a line-ending issue on the Gradle wrapper script. If you get an error like the following try to either just run `dos2unix` on `gradlew` or alternatively copy paste its content into a new file and overwrite the old file with it
 * `bash: ./gradlew: /bin/bash^M: bad interpreter: No such file or directory`

### Development

To be completely set up for full development you need a few more steps, including some quick command line magic (there might be a way to do this through IntelliJ, add it in if you find one!)

* Bring up a command prompt and `cd` to the directory your Git project lives in
* Add an upstream connection to the primary repository, named "movingblocks"
 * `git remote add movingblocks git@github.com:MovingBlocks/Terasology.git`
* Fetch all the remote data. This does not change your workspace, it just loads up your local Git database - newly added repos / branches won't show up until after this step
 * `git fetch --all`
* Now all the remote stuff should look fine! You'll probably have only the "develop" branch locally if you check with `git branch -avv` you can easily add more in IntelliJ via Version Control / Git / Checkout branch

Now you're finally ready to actually make changes and commit + push them somewhere!

* IntelliJ will happily let you change your local files no problem, no need to do anything until you actually want to submit your changes somewhere.
* You can use `git status` to get a list of local files you've created/modified/etc. They'll also show in different colors in IntelliJ
* To add a new file to Git use the right-click menu in IntelliJ on the target file then select the Git sub-menu and the "add" command
* This will "stage" files for a local commit (read up on Git more if you're confused, it really can be kind of confusing). IntelliJ will remember modified files on its own for commits, command line Git won't unless you tell it
* If you want to push your changes to your remote repository you can use the Git / Commit right-click option on top level project entry in IntelliJ and follow the prompts (includes all sorts of technical terms!)
* An important distinction here is if you do a plain "Commit" or a "Commit and Push..." - the first one will only store your changes safely in your local Git repository, while including a Push will also send the changes to your personal remote repo
* If you do use "Commit and Push..." another screen will pop up asking you to confirm by also pressing "Rebase and Push" (exact label may differ by version)
 * *Note:* If you've got nothing but local changes from a clean pull (no merges) the "Commit" option may do nothing other than change your revision ID (as you've added nothing unique) and "Push" will just, well, push!

If you encounter any issues configuring remote repos (or forget what local branch goes to what remote branch) try this useful command: =git remote show origin= (or some other remote repo instead of origin)

### Get Latest

Say some updates have been checked in to one of the `movingblocks` branches and you want to get the latest to keep up. There's an easy way to do this via IntelliJ - just make sure you've made the remote reference to `movingblocks`

* Right click the project top element (or use the Version Control / VCS menu) and go to Git / Pull Changes
* Update the Remote branches with the "Get Branches" button and make sure you select the right current branch (local) and remote repository. Alternatively you may need to use the "Fetch" menu item.
* Select the remote branch(es) you want to merge to your local and click "Pull" !
* You'll get a nice summary in your Version Control window with what was changed. Yay GUIs!
* To push the update to _your_ remote branch (your Pull only updated your local) right click the project top again and select Git / Push Changes
* Make sure the remote and selected branches look right and hit the "Push" button!

You can also do it via command line:

* Make sure your local repo knows about all recent changes: `git fetch --all`
* Make sure the local branch you want to update is checked out: `git checkout develop` (or any other appropriate branch)
* Pull from root remote repository: `git pull movingblocks/develop` (be mindful of the potential for conflicts, if you have any local changes you might want to review first and/or use `git merge` instead)
* Update your personal remote: `git push develop`

Ample usage of `git branch -avv` is recommended to double check on the state and origin of your branches - the `avv` flag will both list all the branches and which local branches connect to which remote branches. You can also verify that the latest commit messages match what you expect this way.

## Related Links

Similar pages here in the wiki

* [[Fancy Git]] - more technically detailed Git instructions and observations
* [[IssueTracking]] - details on how we use the issue tracking system on `GitHub
* [[UnitTesting]] - highly appreciated :-)
* [[JavaDoc]] - likewise!

Tutorials, Git info, etc

* http://www.vogella.de/articles/Git/article.html
* http://gitref.org/
* http://progit.org/
    * In particular Chapter 5.3: Public Small Project
* https://github.com/blog/674-introducing-organizations - some details on how Organizations work on GitHub