## Contributing
The development of Scratch is an ongoing process, and we love to have people in the Scratch, ScratchJr, and open source communities help us along the way.

### Ways to Help

* **Documenting bugs**
  * If you've identified a bug in Scratch or ScratchJr, you should first check to see if it's been filed as an issue. If it has not been filed, please file an issue!  Make sure you follow the issue template.
  * It's important that we can consistently reproduce issues. When writing an issue, be sure to follow our [reproduction step guidelines](https://github.com/LLK/scratch-gui/wiki/Writing-good-repro-steps).
    * Some issues are marked "Needs Repro". Adding a comment with good reproduction steps to those issues is a great way to help.
  * If you don't have an issue in mind already, you can look through the [Bugs & Glitches forum.](https://scratch.mit.edu/discuss/3/) Look for users reporting problems, reproduce the problem yourself, and file new issues following our guidelines. 

* **Fixing bugs**
  * You can request to fix a bug in a comment on the issue if you mention the repo coordinator for this repository, using the @ symbol with their Github username. Check the list of [Repository Coordinators](./CONTRIBUTING.md#repository-coordinators) to find out who to @-mention.
    * If the issue is marked "Help Wanted" you can go ahead and start working on it!
  * **We will only accept Pull Requests for bugs that have an issue filed that has a priority label** 
    * If you're interested in fixing a bug that does not have an issue already, please file the issue first and wait for it to have a priority added to it.
  
  * We are not looking for Pull Requests ("PR") for every issue and may deny a PR if it doesn't fit our criteria.
    * We are far more likely to accept a PR if it is for an issue marked with the "Help Wanted" label.
    * We will not accept PRs for issues marked with "Needs Discussion" or "Needs Design."
    * Wait until an issue has been assigned a priority before working on it. Also leave a comment if you start working on a prioritized issue, so other people don't start working on it also.

#### Repository Coordinators
Public repositories where we encourage contributions have a repository coordinator. Here are the current assignments:
* scratch-audio @ericrosenbaum
* scratch-blocks @ericrosenbaum
* scratch-desktop @cwillisf
* scratch-gui @chrisgarrity
* scratch-link @cwillisf
* scratch-render @cwillisf
* scratch-storage @cwillisf
* scratch-svg-renderer @cwillisf
* scratch-vm @ericrosenbaum
* scratch-www @benjiwheeler
* scratchjr @chrisgarrity
* scratchjr-website @chrisgarrity

Repositories that do not accept external PRs:
* scratch-l10n
* scratch-paint
* scratch-parser
* scratch-render-fonts
* scratch-resources
* scratch-sb1converter

### Learning Git and Github

If you want to work on fixing issues, you should be familiar with Git and Github.

* [Learn Git branching](https://learngitbranching.js.org/) includes an introduction to basic git commands and useful branching features.
* Here's a general introduction to [contributing to an open source project](https://egghead.io/courses/how-to-contribute-to-an-open-source-project-on-github).

**Important:** we follow the [Github Flow process](https://guides.github.com/introduction/flow/) as our development process.

### How to Fix Bugs
1. Identify which Github issue you are working on. Leave a comment on the issue to let us (and other contributors) know you're working on it.
2. Make sure you have a fork of this repo (see [Github's forking a repo](https://help.github.com/en/github/getting-started-with-github/fork-a-repo) for details)
3. Switch to the `develop` branch, and pull down the latest changes from upstream
4. Run the code, and reproduce the problem
5. Create your branch from the `develop` branch
6. Make code changes to fix the problem
7. Test your changes and make sure existing tests pass. In most scratch repositories running `npm test` will run the tests. We strongly encourage you to write tests for any changes.
8. Commit your changes
9. Push your branch to your fork
10. Create your pull request
    1. Make sure to follow the template in the PR description
    1. Remember to check the “[Allow edits from maintainers](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/allowing-changes-to-a-pull-request-branch-created-from-a-fork)” box

When submitting pull requests keep in mind:
* please be patient -- it can take a while to find time to review them
* try to change the least amount of code necessary to fix the bug
* the code can't be radically changed without significant coordination with the Scratch Team, so these types of changes should be avoided
* if you find yourself changing a substantial amount of code or considering radical changes, please ask for clarification -- we may have envisioned a different approach, or underestimated the amount of effort

### Suggestions
![Block sketch](https://user-images.githubusercontent.com/3431616/77192550-1dcebe00-6ab3-11ea-9606-8ecd8500c958.png)

Please note: **_we are unlikely to accept PRs with new features that haven't been thought through and discussed as a group_**.

Why? Because we have a strong belief in the value of keeping things simple for new users. It's been said that the Scratch Team spends about one hour of design discussion for every pixel in Scratch. To learn more about our design philosophy, see [the Scratch Developers page](https://scratch.mit.edu/developers), or [this paper](http://web.media.mit.edu/~mres/papers/Scratch-CACM-final.pdf).

We welcome suggestions! If you want to suggest a feature, please post in our [suggestions forum](https://scratch.mit.edu/discuss/1/). Your suggestion will be helped if you include a mockup design; this can be simple, even hand-drawn.

### Other resources
Beyond this repo, there are also some other resources that you might want to take a look at:
* [Community Guidelines](https://github.com/LLK/scratch-www/wiki/Community-Guidelines) (we find it important to maintain a constructive and welcoming community, just like on Scratch)
* [Open Source forum](https://scratch.mit.edu/discuss/49/) on Scratch
* [Suggestions forum](https://scratch.mit.edu/discuss/1/) on Scratch
* [Bugs & Glitches forum](https://scratch.mit.edu/discuss/3/) on Scratch
