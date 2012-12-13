# Getting fancy with Git

This page is for more advanced issues related to Git and our source code - that way we keep the [[Dev Setup]] page from becoming _too_ overwhelming

## Fancy Gradle

We have the Gradle Wrapper in use so you can simply start a local setup with `gradle idea` but there are some fancier things you can do!

* Set your `GRADLE_HOME` environment variable to the directory Gradle lives in (either the automatically installed version or download yourself from http://gradle.org/downloads)
* Find and install the Gradle GUI plugin for IntelliJ
* Set the Gradle Home in IntelliJ under File / Settings / Project Settings / Gradle (and be sure to restart IntelliJ after this step)
* You should now be able to use a nice Gradle GUI element to execute Gradle targets within IntelliJ! There's also a spot to pick a custom Gradle executable, which can be the `gradlew` wrapper in the project root

There are more interesting pieces that can be auto configured via Gradle - we just need time to work some of them out! You can also have Gradle set up Eclipse, but that is less commonly used by the project team and may not work as well as for IntelliJ. Here are some more Gradle tasks:

* Execute the game from command line: `gradlew run`
* Generate javadoc: `gradlew javadoc`
* Build the applet: `gradlew applet`

## Fancy Git Setup

Rather than use the IntelliJ GUI options to get started with source code you can do more of it via command line

* Pick a parent directory you want to check the project out into, like `C:\Dev`
* Bring up a command prompt and have your GitHub URL handy - `cd` to the parent directory you chose
* Execute `git clone [git url]` - example: `git clone git@github.com:Cervator/Terasology.git`
* Wait for the download to finish, then `cd` to your shiny new Terasology directory
* Run `gradlew idea` and you'll get the IntelliJ project config files all set - continue

## Powershell Git

An alternative to using the Git Bash shell on Windows - original instructions at http://forum.movingblocks.net/threads/replace-git-bash-with-powershell.209/

* Make sure you have the Git executable on the system `PATH` - this should be the case if you selected that option during Git install
* Run `powershell` as administrator (enter into Run box and right click the option that should appear above, then run as admin)
* Enter the following command (and confirm with 'Y' twice) to allow the execution of Powershell scripts: `Set-ExecutionPolicy RemoteSigned -Confirm`
 * Go to a working directory of some sort, like `cd C:\Dev`
 * Retrieve Posh Git for syntax highlighting: `git clone git://github.com/dahlbyk/posh-git.git`
 * Execute its installer: `posh-git\install.ps1`
 * Restart Powershell and fancy highlighting will appear in Git directories!

You can enhance this one step further by also making sure the Git bin dir is on the system `PATH` - which you can set specific to PS only (there are a **lot** of very systemy commands in that bin dir, that may get in the way of other system things) by modifying your PS profile usually stored at something like `C:\Users\[user]\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1` adding the following:

> $env:path += ";" + (Get-Item "Env:ProgramFiles(x86)").Value + "\Git\bin"

This should allow PS with Posh Git to also store your password for subsequent requests. You can also use `ssh-keygen` easily this way to generate keys, one contributor had to use that trick to get around a greek keyboard issue (setting the `HOME` variable to force Git to look there for the `.ssh` dir can also help)

## Branch Management

If you're going to be working with Git beyond the absolute minimum you'll likely need to know more about how to deal with branches

### Update branch

Aside from the easier IntelliJ GUI option on the [Dev Setup] page there's also a way to do branch updates via command line.

* `git fetch --all` to have all the right Git data refreshed locally
* Make sure you have your desired local branch selected - check with `git branch -a` (the asterisk is your active branch)
* `git merge remotes/movingblocks/develop` will grab changes from there and place them in your local directory, including conflict markers if appropriate (more info on how to avoid this better would be good...) 
 * What would the difference be between pull and merge here? Hmm - still a gray area!
* At this point you can run `git status` to see what's prepared for you locally **OR** just look at IntelliJ, which will suddenly show the new files and conflict markers if present 
 * You can even use the right click file / Git / Merge Tool in IntelliJ to get a nice three-way merge tool and options to outright accept your own or the remote changes alone
* When you're done resolving conflicts do a final `git status` to make sure all is well and nothing remains
* Do a `git commit -m [your commit message here]` to submit your changes to the local repo
* `git push` will then also push the code to your remote repo
* Alternatively IntelliJ still works - right click the project top level object / Git / Commit Directory 
 * Review the comment and click the Commit and Push button
 * Warnings may pop up about open TODO items, code conventions, etc - you can expect these. In the perfect world we'd fix them all first, but then we'd never manage to commit! One fix at a time
 * Enter your password and click the Rebase and Push button for finally submitting everything in one squashed commit. IntelliJ does at least figure out all the prior commits you're dealing with

This whole area still needs more certain details - Git is confusing :-(

### Create a branch

Should you want an extra branch for a while to tinker with, you can make one with the following:

* Make sure you have the desired source branch checked out first 
 * `git checkout master` will select your local "master" branch
* `git branch myfeature` will create a local "myfeature" branch based off the "master"
* `git branch -a` will help you verify that the branch created successfully
* `git push origin -u myfeature` will then push the new branch to your remote origin on GitHub, while the `-u` also makes a local alias for it

*Note:* If you have changes in the currently checked out branch then they will exist in a new branch created from it. That's handy for always working in `develop` yet being able to switch to a topic branch for initial commit really easily.

### Deleting a branch

After a while a branch may have served its purpose, or possibly gotten messed up to the point where you don't want to work from it anymore.

* Make sure the branch you want to delete isn't your "default" branch on GitHub - look under Admin when you're looking at your repo there and set something else to default 
 * Git will actually refuse to delete a remote branch if it is your default on GitHub
* To delete the local version: `git branch -d develop`
 * You may get an error if Git doesn't believe all your changes have gone somewhere else - you can override by making the d uppercase (so `git branch -D develop`)
* Execute `git push origin :develop` (which in essence means to push "empty" to your origin/develop, thus deleting it - of course, make sure _origin_ is the right remote repo first!)

### Handy commands

Should a remote branch be closed it'll still show in your local list with `git branch -a` until you prune with the following command (remove the `--dry-run` to truly do it)

* `git remote prune movingblocks --dry-run`
 * Looks like `-n` also works rather than the longer `--dry-run`

Likewise if a new remote branch has appeared it won't show locally until you "fetch" the knowledge of the remote updates (note that this does **not** modify your local workspace - just updates what git knows locally)

* `git fetch --all`
 * You can also be more specific and use something like `get fetch movingblocks`

While not as fancy as Perforce's P4V Revision Graph, Git can do graphs! .... in text:

* `git log --graph --oneline --all`

And you can sometimes end up without a `origin/HEAD` setting if you've been deleting default branches and what not, to set one do something like:

* `git remote set-head origin master`

### Keeping the branch map clean

This looks to be a little tricky as we've hit scenarios where pulling/pushing code around didn't result in a nice connection on the branch map. Need more info on exactly what makes this tick - usually it has been fairly easy to fix, although it can result in duplicate listings of earlier commits. A big warning: It is very easy in trying to revert or undo stuff on a local branch to submit a pile of silly commits you don't want to pollute the main branch network with. This is especially the case if you're new to Git. Be cautious! :D

Rebasing can be useful to do locally if you've been making frequent or messy commits with lots of debug statements, reverted changes, etc

   * TODO

If mistakes are pushed somewhere you can revert back one or more commits and force-push the older commit to your remote. To revert back one commit look for the parent commit ID you want and locally with the right branch checked out do:

   * `git checkout [branch]` - pick a local branch you want to roll back commits on (oh, and you might want to branch a backup ..)
   * `git reset [id]` - reset to the commit with the id supplied (easy to confirm on GitHub - the IDs are linked to their respective commits)
   * `git status` - to confirm that you're now behind 'x' commits
   * `git branch -avv` - to again confirm that the active commit descriptions line up like you expect - can't be too careful!
   * `git push origin [branch]` - to confirm that you get an error saying you'd lose commits - just in case!
   * `git push origin [branch] -f` - do the revert to the older commit - no going back at this point so be certain you are doing the right thing!

## MovingBlocks

Our GitHub Organization is called MovingBlocks ("MB" for short) and lives at https://github.com/MovingBlocks/Terasology

If you're on the core team or otherwise able to push code directly into Organization branches you don't need a fork, and can instead simply clone the Organization project instead. IntelliJ doesn't like that approach due to claiming you don't have read/write rights even if you're the owner of an Organization (or at least that happened when last checked, anyway!) but it is pretty easy to do from the command line.

* `cd` to the base directory you want the `Terasology` directory from source control to be created in (you don't want to start inside a project directory as the clone will create one)
* `git clone git@github.com:MovingBlocks/Terasology.git`

### Organization tricks

Encountered some quirks trying to set up the test Nanoware organization on GitHub. Our main `MovingBlocks` organization was actually a move from begla's old personal remote repo, so that didn't create a new fork.

* Change your "context" to the Organization you're part of (done from your dashboard)
* Find a project to fork - this is the tricky part as if your _user_ already has an active fork you may just see the "Your Fork" button/link!
* If you look at your _own_ fork you suddenly have a normal "Fork" button - but clicking it may at first do nothing, then on the second try give you the valid option to fork to your user (already exists!) or to your Organization
* Don't forget to watch and follow yourself. Yeah. Nothing strange about that! ;-)

Other misc:

* Some of the menus don't seem to like Firefox at certain times of day or with some special planetary alignments in the sky. Have seen some items both work and not work. Between it and IE something usually works eventually.
 * GitHub suggested that if Organization owners also want notifications from the Organization they can be added to a Team (other than "owners") that also contains the repo. Might alternatively be enough to just track down every spot you can "Watch" or "Follow", tho that still likely won't show you your own changes on the main dashboard (you'd have to select your own account)

## Contributing Code

If you've gotten to the point where you've written unique code (or art resources, etc) and committed them to GitHub then congratulations! And thank you. There are two main ways for code (or any kind of asset) to make it to the official project root. If you're still not on top of how push, pull, and merge differ this might also provide some good examples. If something still seems weird, ask us! Git is confusing and we probably get terminology and other stuff wrong ourselves.

### Merge

We're eager for contributed code and might spot you writing nifty code and even grab it immediately if it is tempting enough - but usually we'll ask first, or you'll ask, in the [Dev Portal](http://forum.movingblocks.net/forums/developer-portal.5/) somewhere. The process there is simply that a member of the team with Push (write) rights to MB will set up a reference to whatever [featurebranch] in your [remote] repo has the code, then run through something like the following:

* Be sure you have MB's `develop` branch checked out (or whatever is the appropriate base for the merge)
* `git remote add [remote] git@github.com:[user]/Terasology.git` - sets up the remote reference to the [user] providing the code
* `git fetch --all` - fetches all the remote data
* `git branch myfeature` - make a local myfeature branch that'll eventually be what gets pushed to MB remote
* `git push origin -u myfeature` - pushes new myfeature to remote, identical to the checked out branch (for later easy diffs)
* `git checkout myfeature` - use the `myfeature` branch for the actual merge
* `git merge [remote]/[featurebranch]` - merges stuff from the remote branch into the shiny new local `myfeature` branch, there may be additional conflict resolution and such here 
 * This can also be done in IntelliJ via the "Merge" option under Version Control
* `git push` - pushes the `myfeature` branch to MB, where we can then test it together with the latest changes from `develop` and verify that all is well before merging it onwards

Alternatively you can merge straight into `develop` or use the project `integrate` branch (usual target for pull requests)

### Create a Pull request

If alternatively you're happy with the state of some changes you'd like to package up officially for somebody else to accept into MB you can prepare a Pull request on GitHub. 

* While showing the project on your GitHub dashboard click the "Pull Request" button
* Make sure the source (likely your `origin`) and target branch (our preferred target is the `integrate` branch) are correct - this can easily be wrong, so use the "Change Commits" button to adjust
* Add comments as needed
* Should you push more commits to the remote source branch for the Pull it'll automatically update to the request as long as it hasn't been processed yet

## Related Links

* [[Dev Setup]]
* [[IssueTracking]]
* [[UnitTesting]]
* [[JavaDoc]]
