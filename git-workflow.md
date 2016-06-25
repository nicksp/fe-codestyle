# Git Workflow

## Table of Contents

  1. [Expectations](#expectations)
  1. [Commit Message Guidelines](#commit-message-guidelines)
      - [Commit Message Format](#commit-message-format)
        - [Revert](#revert)
        - [Type](#type)
        - [Scope](#scope)
        - [Subject](#subject)
        - [Body](#body)
        - [Footer](#footer)
      - [Examples](#examples)
  1. [Centralized Workflow](#centralized-workflow)
  1. ['Feature Branches' Workflow](#feature-branches-workflow)
  1. ['Rebase Feature Branch Commits' Workflow](#rebase-feature-branch-commits-workflow)
  1. [Tips](#tips)
  1. [References](#references)

## Expectations

All of these workflows assume that you have a remote repository and by default the main branch is called `master`.

Also, I don't cover every possible detail about git and how it works; thus a certain level of past experience from the you is assumed. By this I mean, for example, if you don't know what a `merge conflict` is you'll need to read up on git a bit more first in order to benefit from this document.

## Commit Message Guidelines

I'm using the Angular commit style (even when I don't write any Angular code) which prefixes with `fix:` or `feature:` and subjects are limited to 50 characters with more details in the body. This tend to lead to **more readable messages** that make the commit history looks clear and so much easier to scan through.

### Commit Message Format

- Each commit message consists of a **header**, a **body** and a **footer**, separated by a blank line.

  ```
  <type>(<scope>): <subject>
  <BLANK LINE>
  <body>
  <BLANK LINE>
  <footer>
  ```

- The header has a special format that includes a **type**, a **scope** and a **subject**.
- The only mandatory part is a **header** (with optional **scope** field).

#### Revert

If the commit reverts a previous commit, it should begin with `revert:`, followed by the header of the reverted commit. In the body it should say: `This reverts commit <hash>.`, where the hash is the SHA of the commit being reverted.

#### Type

This describes the kind of change that this commit is providing.

- **feat**: New feature
- **fix**: Bug fix
- **chore**: Changes to the build process or auxiliary tools and libraries such as documentation generation, maintain
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **docs**: Documentation only changes
- **test**: Adding missing tests
- **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing
  semi-colons, etc)
- **perf**: A code change that improves performance

#### Scope

The scope could be anything specifying place of the commit change. For example `moduleName`, `namespace`, `subModule`, `specificObject`, `constructor`, etc...

#### Subject

This is a very short description of the change:

* use imperative, present tense: "change" not "changed" nor "changes"
* use nice and descriptive commit message
* Capitalize first letter
* no period (.) at the end. Trailing punctuation is unnecessary in subject lines.
* shoot for 50 characters, but consider 69 the hard limit

The imperative can sound a little rude; that's why we don't often use it. But it's perfect for git commit subject lines. This tells someone what applying the commit **will do**, rather than **what you did**. Also, if you look at your repository history you will see that the Git generated messages are written in this tense as well - "Merge" not "Merged", "Rebase" not "Rebased", so writing in the same tense keeps things consistent.

To remove any confusion, here's a simple rule to get it right every time.

**A properly formed git commit subject line should always be able to complete the following sentence:**

* If applied, this commit will _&lt;your subject line here&gt;_

```
If applied, this commit will refactor subsystem X for readability
If applied, this commit will update getting started documentation
If applied, this commit will remove deprecated methods
If applied, this commit will release version 1.0.0
If applied, this commit will merge PR #123 from user/branch
```

> Remember: Use of the imperative is important only in the subject line. You can relax this restriction when you're writing the body.

#### Body

Git never wraps text automatically. When you write the body of a commit message, you must mind its right margin, and wrap text manually.

The recommendation is to do this at 72 characters, so that git has plenty of room to indent text while still keeping everything under 80 characters overall.

- Just as in the [subject](#subject) use imperative, present tense: "change" not "changed" nor "changes".
- Include motivation for the change and contrast with previous behavior. Explain what the change is and why the change is being made.

[Great example](https://github.com/bitcoin/bitcoin/commit/eb0b56b19017ab5c16c745e6da39c53126924ed6) of explaining what changed and why.

```
Simplify serialize.h's exception handling

Remove the 'state' and 'exceptmask' from serialize.h's stream implementations,
as well as related methods.

As exceptmask always included 'failbit', and setstate was always called with
bits = failbit, all it did was immediately raise an exception. Get rid of
those variables, and replace the setstate with direct exception throwing
(which also removes some dead code).

As a result, good() is never reached after a failure (there are only 2
calls, one of which is in tests), and can just be replaced by !eof().

fail(), clear(n) and exceptions() are just never called. Delete them.
```


#### Footer

The footer should contain any information about **Breaking Changes** and is also the place to reference GitHub (or other code hosting facilities) issues that this commit **closes**.

Closed bugs should be listed on a separate line in the footer prefixed with `Closes` keyword like this:

```
Closes #123
```

or in case of multiple issues:

```
Closes #123, #456, #789
```

### Examples

```
test: Raise coverage to 100%
chore: Fix tests back to es5
docs: Fix sample code in examples
```

```
feat(slider): onNextChange event handling

Add new event to slider:
- forward popstate event if available
- forward hashchange event if popstate not available
- do polling when neither popstate nor hashchange available
```

```
fix(module): Couple of unit tests for IE9

Older IEs serialize html uppercased, but IE9 does not...
Would be better to expect case insensitive, unfortunately jasmine does
not allow to user regexps for throw expectations.

Closes #392
```

```
docs(guide): Update fixed docs from Google Docs

Couple of typos fixed:
- indentation
- batchLogbatchLog -> batchLog
- start periodic checking
- missing brace
```

## Centralized Workflow

> Everyone works from the `master` branch

- Everyone clones the remote repo and commits changes to `master` locally
- Local changes are then pushed to the remote repository
- If someone pushes changes before you, then your push will fail
- You'll need to pull their changes (`git pull origin master`) first
- Any merge conflicts will then need to be resolved locally
- Once merge conflicts are resolved, you can push to the remote

### Pros

- Can be less complex and time consuming than dealing with feature branches (assuming small teams of < 5)

### Cons

- Everyone committing to `master` can be uncomfortable for some teams
- No categorised history, just multiple isolated commits
- Merge commits are ugly and make the git history harder to reason about

## 'Feature Branches' Workflow

> Everyone works from their own `feature` branch

- Everyone clones the remote repo and creates a feature branch
- For example `git checkout -b feature/add-client-cache`
- Commits are made to the feature branch locally
- The feature branch should be pushed to the remote regularly
- Feature branch is reviewed by other developers
- Once approved the feature branch is merged into `master` locally
- The updated `master` branch is then pushed to the remote
- If someone pushes changes before you to `master`, then your push will fail
- You'll need to pull their changes (`git pull origin master`) first
- Any merge conflicts will then need to be resolved locally
- Once merge conflicts are resolved, you can push to the remote

### Notes

To reduce the likeliness of a merge conflict, developers should consider updating their `master` branch regularly and merging those changes into their feature branch (e.g. `git merge master`).

Developers can also consider pulling `master` directly into their feature branch either by using `git pull origin master` or by using `git pull --rebase origin master` (which will unshift their feature branch commits so that they sit on top of whatever is inside `master`; meaning the feature branch commits are **top of the stack**).

Also, when using `--rebase` you do typically experience less conflicts.

### Pros

- Most recognised/popular workflow model
- Use of **short lived** feature branches allow decoupled development

### Cons

- No clean history, just multiple isolated commits
- Merge commits are ugly and make the git history harder to reason about

## 'Rebase Feature Branch Commits' Workflow

> Work from a `feature` branch, but `rebase` commits before merge

- Checkout a new branch from `master` and prepend the `project code` + `JIRA/Github ticket/issue number` to the name of the feature branch
- For example `git checkout -b feature/PC-01-add-client-cache`
- Run tests and report breaking tests to the team
- Commits are made to the feature branch locally
- The feature branch should be pushed to the remote regularly
- Cover the new feature with test cases and fix any breakage caused by the new code. (Must do this before submitting the PR as it saves the reviewers a lot of time)
- When ready, submit a PR on GitHub against `master`
- Feature branch is reviewed by other developers
- Make any changes asked for by the reviewers and push the changes as new commits
- Once approved (you need at least one reviewer's "Looks Good To Me" `LGTM` or "thumbs up"), the feature branch commits are rebased on top of latest from `master` (`git rebase -i master`) into a single commit
- Some very large changes may need to be in multiple commits to better reflect the history of changes, however vast majority of changes should be in one commit
- Commit message has specific format (`Closes #1 - Add client cache (Fixes #2)`)
- Runs tests again and make sure everything is in order
- Commit is then cherry-picked into `master` (`git checkout master` -> `git cherry-pick squashed-commit-hash`)
- The updated `master` branch is then pushed to the remote
If someone pushes changes before you to `master`, then your push will fail
- You'll need to pull their changes (`git pull --rebase origin master`) first
- Any merge conflicts will then need to be resolved locally
- Once merge conflicts are resolved, you can push to the remote (`git push origin master`)
- Delete the branch from GitHub (option can be found on the PR page) and locally (`git branch -D feature/PC-01-add-client-cache`)

### Notes

GitHub specifically offers a feature where by GitHub issues are automatically closed whenever a push to `master` includes the phrase `Fixes #n` (where `n` is the issue number); similarly it'll automatically close a pull request when the commit message in `master` includes the phrase `Closes #n` (where `n` is the pull request number).

Also, the GitHub user interface now (as of 2016) suppports the ability to squash commits when merging. This might be a preferable option to the above steps.

### Pros

- Allows maintaining linear git history (vs using merge capabilities of Github)
- Use of **short lived** feature branches allow decoupled development
- Auto closing of Pull Requests and Issues within GitHub (assuming relevant commit syntax is used)
- Access to original commit history within GitHub Pull Request interface

### Cons

- If a feature branch takes too long to merge, it can become a conflict nightmare
- Requires steps that are more complicated for beginner git users (e.g. interactive rebasing and cherry picking)
- Can't access original commit history via a terminal shell.

> Note: if branches are deleted from GitHub then eventually the commits will be garbage collected and history lost there as well. So pick this option according to whether it fits your team's long term needs

## Tips

- Read Pro Git.
  The [Pro Git](https://git-scm.com/book/en/v2) book is available online for free, and it's fantastic. Take advantage!

## References

- [Atlassian: Comparing Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [GitHub: Understanding the GitHub Flow](https://guides.github.com/introduction/flow/)
