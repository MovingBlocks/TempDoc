We currently use the built-in issue tracking system on !GitHub - https://github.com/MovingBlocks/Terasology/issues

**TODO**: Still need to finish fleshing this out

## Issues

Whenever we're pretty much sure we want to implement something in the near future we'll make an item in the issue tracking system for it. If the idea is too vague or far into the future it stays in the planning phases which may be in a discussion thread on the forum, the CommunitySuggestions page here in the wiki, or in other sneaky places.

   * Commits that simply reference an issue number (like #42) along with a keyword like "fixed" will actually close the specific item in the issue tracking system when it is pushed to the repo the issue lives in
   * You can also reference users in the issue tracking system by prefixing their name with @ - that will auto-notify them on !GitHub

### Pull Requests

Interestingly enough these gadgets are both pull requests and issues at the same time. Completing a pull request also completes it as an item, and it will also auto-detect whether a commit is completing it (**TODO**: Confirm)

## Labels

We have a few labels that act as categories. They classify issues by concept more than technical area - there are only a few colors available and we'd have to re-use some to be able to classify by area (which likely would over-complicate the system anyway). So we have "Art" and "Architecture" rather than "Skysphere" and "Block system"

## Milestones

Individual issues can be grouped into milestones - we aim to use this to put focus on a particular area over a period of time like a month, as well as embedding the milestone into the version info.

## Test Organization

Cervator at first tested out the issue tracking system using a separate Organization called Nanoware

   * Pull requests submitted to Nanoware/Terasology also count as Issues, so a new pull request gets the next numeric entry for the issue tracking system
   * Issues submitted (including Pull request) can be referenced via the !MarkDown, uh, markup, on assorted !GitHub screens. 
      * `#2` will auto-link to https://github.com/Nanoware/Terasology/issues/2 (if written on one of the Nanoware screens)
      * `#3` will auto-link to https://github.com/Nanoware/Terasology/pull/3 (because it is a pull request `/issues/3` automatically redirects to the =/pull/= address)
      * `Nanoware#3` will link to the same, but from any user/organization screen - plain #3 elsewhere will link to the project root's issue system (so issue 3 for `movingblocks`)
   * Certain keywords in a check-in may auto-associate (and possibly close) issues in !GitHub, like "Fixes #123" - example at https://github.com/MovingBlocks/Terasology/issues/48

## Related Links

   * [[Dev Setup]] - the basics
   * [[Fancy Git]] - more advanced source control