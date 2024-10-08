# Git Rebasing

## Overview

Git **rebase** is a powerful tool that allows you to move or reapply commits from one branch onto another. Unlike merging, which combines two branches while preserving their history, rebasing rewrites the commit history to create a linear sequence of commits. This can make your project history cleaner and easier to understand.

In this guide, we'll cover the basics of rebasing, how to use it in your workflow, a practical example, and the pros and cons of rebasing.

---

## Why Use Rebasing?

The primary reasons for using `git rebase` include:

1. **Clean and Linear History**: Rebasing allows you to maintain a more linear project history, without the noise of unnecessary merge commits.
2. **Better Context**: It ensures your feature branch's commits are based on the latest changes from the target branch, providing a clearer context for changes.
3. **Avoiding Merge Conflicts**: Rebasing frequently helps reduce merge conflicts by keeping your branch up to date with the latest changes.

---

## Pros and Cons of Rebasing

### Pros:
- **Cleaner History**: Rebasing ensures a linear history by eliminating unnecessary merge commits, which makes the history easier to read and follow.
- **Simplifies Code Review**: With fewer merge commits, your changes are grouped in a straightforward manner, making the code review process simpler.
- **Works Well with Feature Branches**: Rebasing keeps all feature branches up to date without the need for multiple merges.

### Cons:
- **Risk of Data Loss**: Rebasing rewrites commit history, so there is a risk of losing commits if done incorrectly. This is especially dangerous if used on public branches.
- **Potential Conflicts**: Rebasing can introduce more frequent conflicts since you are replaying all your commits on top of the latest changes.
- **Force Pushing Required**: .After rebasing, you usually need to force-push (`git push --force-with-lease`), which can be risky if other developers are working on the same branch.

---

### GIT Rebase Commands
- `git rebase master`, this command uses the commits from the current branch and reapplies them on top of the latest commits in the master branch.
- `git rebase –continue`, this commit resumes the rebasing process after conflicts have been resolved.
- `git rebase –abort`, this command terminates the ongoing rebase and resets the branch to its original state before the rebase began.
- `git rebase –skip`, this command is used during a rebase to bypass the current commit with unresolved conflicts and continue with the rest of the rebase process.

## Git Rebase Workflow
Let us consider a scenario where you start working on a new feature in a separate branch, while another team member pushes new commits to the main branch leading to a split in the commit history as displayed in [Figure 1](#Rebase).

<figure id="Rebase" style="text-align: center;">
  <img src="Figures/Rebase_setup.svg" alt="Basic setup" width="450"/>
  <figcaption>Figure 1: Setup</figcaption>
</figure>
<p style="text-align: center;">
  Figure source: www.atlassian.com 
</p>
<https://www.atlassian.com/git/tutorials/merging-vs-rebasing>

Adding the new commits into the feature branch using `git rebase` is displayed in [Figure 2](#Rebase_final).
<figure id="Rebase_final" style="text-align: center;">
  <img src="Figures/Rebase_final.svg" alt="Basic setup" width="450"/>
  <figcaption>Figure 2: Rebase final</figcaption>
</figure>
<p style="text-align: center;">
  Figure source: www.atlassian.com 
</p>
<https://www.atlassian.com/git/tutorials/merging-vs-rebasing>

This shifts the feature branch to start at the tip of the main branch, integrating all new main commits. Instead of a merge commit, rebasing rewrites history by creating new commits for each original one. As [Figure 2](#Rebase_final) shows, rebasing provides cleaner and perfectly linear project history.

### Comparison to Git Merge

The same situation can be solved using `git merge` as shown in [Figure 3](#Merge).

<figure id="Merge" style="text-align: center;">
  <img src="Figures/Merge_final.svg" alt="Basic setup" width="450"/>
  <figcaption>Figure 3: Merge option</figcaption>
</figure>
<p style="text-align: center;">
  Figure source: www.atlassian.com 
</p>
<https://www.atlassian.com/git/tutorials/merging-vs-rebasing>

The [Figure 3](#Merge) shows that the existing branches are not changed in any way, which prevents all of the problems connected to `git rebase`.

However, frequent use of the main can make it hard for other developers to understand the history of the project. This can be solved by using `git rebase`.

## Interactive rebasing

Interactive rebasing in Git is a method for refining commit history by reordering, editing, or combining commits interactively. It allows you to systematically clean up and organize the commit history for a clearer, more structured project history.

To begin interactive rebasing, pass the `-i` option to the git rebase command as:
```
git rebase -i main
```
For example, to see the last 3 commits, we will type:

```
git rebase -i HEAD~3
```
To combine the second and first commit, we will use the `pick` and `fixup` commands as:

```
pick 33d5b7a Info for commit #1
fixup 9480b3d Info for commit #2
pick 5c67e61 Info for commit #3
```
[Figure 4](#INT) displays the final project history after combining the first and second commit.

<figure id="INT" style="text-align: center;">
  <img src="Figures/INT.svg" alt="Basic setup" width="450"/>
  <figcaption>Figure 4: Interactive rebasing</figcaption>
</figure>
<p style="text-align: center;">
  Figure source: www.atlassian.com 
</p>
<https://www.atlassian.com/git/tutorials/merging-vs-rebasing>

## Sources

- https://www.30secondsofcode.org/git/s/interactive-rebase/
- https://www.atlassian.com/git/tutorials/merging-vs-rebasing
- https://git-scm.com/docs/git-rebase
- https://www.geeksforgeeks.org/what-is-git-interactive-rebasing/