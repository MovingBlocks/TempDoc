# Versioning Guideline

## Motivation

Currently we just try to keep the current source of the engine and all modules compatible. There are often API changes without an version increment.

Sometimes however you want to go back to an older source version:
* To try out a branch of another developer that has not yet been ported to the new API
* To search the first revision that introduced a bug in order to find the cause of some mysterious bugs (git bisect is a nice command for searching quickly the commit that introduced a bug).

Finding a working version of the dependency is then really a pain if there had been multiple releases with the same version identifier that aren't API compatible.

Also for third party modules it would be good if the version numbers have a clear and reliable meaning like SemVer.

## Guideline Suggestion 1 by Flo
### Suggestion
When you make an API change, that requires other modules to be updated then change the version number from 0.x.y-SNAPSHOT to 0.x+1.0-SNAPSHOT.

Increase locally the maxVersion field of the dependent modules you test, so that they get used.

In the pull request for the other modules that need to be updated set the minVersion of the dependency entry to 0.x+1.0.

When you are publishing the jar, do the following (ideally via a script/jenkins task):
* Change the version number from 0.x.y-SNAPSHOT to 0.x.y and release it as 0.x.y. 
* Instantly afterwards change the version number from 0.x.y to 0.x.(y+1)-SNAPSHOT. 
* When the version number is 0.x.0, increase the exclusive maxVersion field of all dependent modules to 0.x+1.0, if that hasn't been done already. Release the dependent modules like this one.

### Comments
Flo: The system gives good version numbers but requries you to increment the maxVersion number for testing.


## Guideline Suggestion 2 by Flo
### Suggestion
When you make an API change, that requires other modules to be updated then change the version number from 0.x.y-SNAPSHOT to 0.x+1.0-SNAPSHOT.

In the pull request for the other modules that need to be updated set the minVersion of the dependency entry to 0.x+1.0.

The maxVersion of dependent modules does not need to be increased as the engine (in this suggestion) will assume that 0.x.w is compatible with anything < 1.0.0.

In the pull request for the other modules that need to be updated set the minVersion of the dependency entry to 0.x+1.0.

When you are publishing the jar, do the following (ideally via a script/jenkins task):
* Change the version number from 0.x.y-SNAPSHOT to 0.x.y and release it as 0.x.y. 
* Instantly afterwards change the version number from 0.x.y to 0.x.(y+1)-SNAPSHOT. 
* When the version number is 0.x.0, check if there are dependent modules that are broken in version 0.z.w. Set maxVersion in this modules to 0.x.0 and release it as 0.z.w+1. (it is a bug fix release to fix the dependency information)

### Comments
Flo: The big advantage of this approach is that the developer does not need to increment of dependent modules if they aren't broken. Teh second biggest advantage is that it avoids release spam if only a few dependent modules are broken by the API change.
A disadvantage of this approach is that it is not possible to go back in history of a dependent module as its dependency information is wrong.
So at the end the version numbers bring little gain.