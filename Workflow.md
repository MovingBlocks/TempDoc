This workflow is based on the free e-book "[[http://progit.org/book/ch5-2.html]]" (Chapter 5.3: Public Small Project).

## General

**Always use the _develop branch_ as base for your development.**

## Step by step guide

 1. Create a local fork of the main repository (simply use the **_Fork_** button on the main project page)
 2. Clone the newly created fork to your workstation: `git clone <URL>`
 3. Add the main repository as a remote called **upstream**: `git remote add upstream git://github.com/begla/Blockmania.git`
 4. Switch to the **develop **branch: `git checkout develop`
 4. Create a topic branch (named after the issue on GitHub) for the feature/fix you're working on: `git checkout -b <issueNumber>-<description>`
 5. Work, work... Commit... Work, work... Commit... Push... Work, work... And so on
 6. When you're finished, use `git rebase -i` to squash your commits to a single commit
 7. Switch to the develop branch: `git checkout develop`
 8. Fetch the current changes from the main develop branch: `git fetch upstream`
 9. Rebase your local develop branch on top of the main develop branch: `git rebase upstream/develop`
 10. Switch to your local topic branch: `git checkout <issueNumber>-<description>`
 11. Rebase your local topic branch on top of your local develop branch: `git rebase develop`
 12. Push your work: `git push origin <issueNumber>-<description>`

 