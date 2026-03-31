# Contributing

The development of Scratch is an ongoing process, and we love to have people in the Scratch, ScratchJr, and open
source communities help us along the way.

## Ways to Help

* **Documenting bugs**
  * If you've identified a bug in Scratch or ScratchJr, you should first check to see if it's been filed as an issue.
    If it has not been filed, please file an issue!  Make sure you follow the issue template.
  * It's important that we can consistently reproduce issues. When writing an issue, be sure to follow our
    [reproduction step guidelines](https://github.com/LLK/scratch-gui/wiki/Writing-good-repro-steps).
    * Some issues are marked "Needs Repro". Adding a comment with good reproduction steps to those issues is a great
      way to help.
  * If you don't have an issue in mind already, you can look through the [Bugs & Glitches forum](
    https://scratch.mit.edu/discuss/3/). Look for users reporting problems, reproduce the problem yourself, and file
    new issues following our guidelines.

* **Fixing bugs**
  * **We will prioritize Pull Requests for bugs that have an issue filed, especially those with a priority label**
    * If you're interested in fixing a bug that does not have an issue already, please file an issue first. This helps
      us avoid making the same mistake again later, and speeds up fixing it if we do.
  * If you plan to work on an issue, please leave a comment on the issue to let us and other contributors know you're
    working on it.
    * The "help wanted" label indicates issues that the Scratch Team thinks would be appropriate for an external
      contributor to work on.
  * We are not looking for Pull Requests ("PR") for every issue and may deny a PR if it doesn't fit our criteria.
    * We are far more likely to accept a PR if it is for an issue marked with the "Help Wanted" label.
    * We will not accept PRs for issues marked with "Needs Discussion" or "Needs Design."
  * Keep in mind that we are also making our own changes, and may not be able to respond in detail to every
    contribution. We appreciate your patience and understanding. A few reasons we might need to delay a PR include:
    * We are working on other changes in the same area of the codebase
    * We want to limit the number of changes we make to the codebase in a given time period to limit the risk or QA
      load for a release
    * We are just short on time (it's usually this one - sorry!)

## AI-Assisted Development

See [CONTRIBUTING.AI.md](CONTRIBUTING.AI.md) for our policy and guidelines regarding AI-assisted development.

## Development Standards

The following standards apply across Scratch repositories. Per-repo `CONTRIBUTING.md` files may add or override
them for that specific repo.

### Technology choices

* **Language**: TypeScript is preferred. JavaScript is acceptable when a package is not yet configured for
  TypeScript.
* **Linting**: All JS/TS code uses [`eslint-config-scratch`](https://github.com/scratchfoundation/eslint-config-scratch).
* **Bundler**: Vite for new repos; existing webpack configs are being migrated to Vite over time.
* **Test framework**: Vitest for new packages; existing packages may use Jest or Tap.
* **Commit messages**: [Conventional Commits](https://www.conventionalcommits.org/) style as understood by
  `semantic-release` (e.g., `feat:`, `fix:`, `chore:`). Not all repos enforce this automatically, but please
  follow the convention regardless.
* **Browser targets**: Code targeting browsers should work within the
  [Baseline Widely Available](https://web.dev/baseline) feature set. Avoid features outside that set without
  calling it out explicitly; don't add polyfills for features already within it.

### Dependencies and bundling

Getting dependency classification right keeps downstream consumers clean and makes it possible for third parties
to use our packages independently.

* **`peerDependencies`**: packages that are part of this package's public interface, or where two copies in the
  same application would cause runtime errors — React and ReactDOM being the primary example. Always externalize
  peer dependencies in the bundle.
* **`dependencies`**: packages owned as private implementation details. For example, `scratch-vm` is a dependency
  of `scratch-gui`; a consuming application like `scratch-www` does not need to know it exists.
* **`devDependencies`**: anything only needed during development, build, or testing.
* **Bundling**: application packages (`scratch-www`, `scratch-desktop`) bundle everything into the final output;
  library packages externalize peer dependencies and bundle regular dependencies.

Many existing repos don't yet fully follow these rules; the direction is to drift toward them incrementally.

## Learning Git and Github

If you want to work on fixing issues, you should be familiar with Git and Github.

* [Learn Git branching](https://learngitbranching.js.org/) includes an introduction to basic git commands and useful
  branching features.
* Here's a general introduction to [contributing to an open source project](
  https://egghead.io/courses/how-to-contribute-to-an-open-source-project-on-github).

**Important:** we follow the [Github Flow process](https://guides.github.com/introduction/flow/) as our development
process.

## How to Fix Bugs

1. Identify which Github issue you are working on. Leave a comment on the issue to let us (and other contributors)
   know you're working on it.
2. Make sure you have a fork of the repo (see [Github's forking a repo](
   https://help.github.com/en/github/getting-started-with-github/fork-a-repo) for details)
3. Switch to the primary branch (usually `develop` or `main`), and pull down the latest changes from upstream
4. Run the code, and reproduce the problem
5. Create your branch from the primary branch
6. Make code changes to fix the problem
7. Test your changes and make sure existing tests pass. In most scratch repositories running `npm test` will run the
   tests. We strongly encourage you to write tests for any changes.
8. Commit your changes
9. Push your branch to your fork
10. Create your pull request
    1. Make sure to follow the template in the PR description
    2. Remember to check the "[Allow edits from maintainers](
       https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/allowing-changes-to-a-pull-request-branch-created-from-a-fork
       )" box

When submitting pull requests, keep in mind:

* please be patient -- it can take a while to find time to review them
* try to change the least amount of code necessary to fix the bug
* the code can't be radically changed without significant coordination with the Scratch Team, so these types of
  changes should be avoided
* if you find yourself changing a substantial amount of code or considering radical changes, please ask for
  clarification -- we may have envisioned a different approach, or underestimated the amount of effort

## Suggestions

![Block sketch](https://user-images.githubusercontent.com/3431616/77192550-1dcebe00-6ab3-11ea-9606-8ecd8500c958.png)

Please note: **_we are unlikely to accept PRs with new features that haven't been thought through and discussed as a
group_**.

Why? Because we have a strong belief in the value of keeping things simple for new users. It's been said that the
Scratch Team spends about one hour of design discussion for every pixel in Scratch. To learn more about our design
philosophy, see [the Scratch Developers page](https://scratch.mit.edu/developers), or [this paper](
http://web.media.mit.edu/~mres/papers/Scratch-CACM-final.pdf).

We welcome suggestions! If you want to suggest a feature, please post in our [suggestions forum](
https://scratch.mit.edu/discuss/1/). Your suggestion will be helped if you include a mockup design; this can be
simple, even hand-drawn.

## Other resources

Beyond this repo, there are also some other resources that you might want to take a look at:

* [Community Guidelines](https://github.com/LLK/scratch-www/wiki/Community-Guidelines) (we find it important to
  maintain a constructive and welcoming developer community, just like on Scratch)
* [Open Source forum](https://scratch.mit.edu/discuss/49/) on Scratch
* [Suggestions forum](https://scratch.mit.edu/discuss/1/) on Scratch
* [Bugs & Glitches forum](https://scratch.mit.edu/discuss/3/) on Scratch
