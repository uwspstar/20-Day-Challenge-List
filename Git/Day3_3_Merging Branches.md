# Merging Branches: `git merge`

The `git merge` command is a fundamental feature in Git that allows you to integrate changes from one branch into another. This command is essential for combining the work done in different branches, enabling teams to collaborate on different features or fixes and then merge their contributions into a shared branch, typically the `main` or `master` branch.

`git merge`命令是Git中的一个基本功能，它允许你将一个分支的更改整合到另一个分支中。此命令对于合并不同分支中的工作至关重要，使团队能够在不同的功能或修复上协作，然后将他们的贡献合并到共享的分支中，通常是`main`或`master`分支。

Here’s how you can use the `git merge` command:

以下是如何使用`git merge`命令的方法：

### 1. Basic Branch Merge

The most common use of `git merge` is to merge a feature branch into the `main` branch. Before merging, ensure that you are on the branch where you want the changes to be integrated.

`git merge`的最常见用途是将功能分支合并到`main`分支中。合并之前，请确保你所在的分支是你希望整合更改的分支。

```bash
# Switch to the main branch
git checkout main

# Merge the feature branch into main
git merge feature-branch
```

This code will output:

这段代码的输出将是：

```
Updating xxxxxxx..yyyyyyy
Fast-forward
 file1.txt | 2 +-
 file2.txt | 1 +
 2 files changed, 2 insertions(+), 1 deletion(-)
```

### 2. Fast-Forward Merge

A fast-forward merge occurs when the branch being merged has no commits of its own, making it possible to simply move the branch pointer forward. This happens when the main branch hasn't moved forward since the feature branch was created.

当被合并的分支没有自己的提交时，会发生快进合并，使得可以简单地将分支指针向前移动。这种情况发生在自创建功能分支以来，主分支没有前进时。

```bash
git merge feature-branch
```

This code will output:

这段代码的输出将是：

```
Updating xxxxxxx..yyyyyyy
Fast-forward
```

### 3. Recursive Merge

When both branches have diverged, meaning there are commits on both branches that need to be integrated, Git performs a recursive merge. This merge strategy attempts to automatically combine changes from both branches.

当两个分支都发生了分歧，即两个分支上都有需要整合的提交时，Git会执行递归合并。此合并策略尝试自动合并两个分支的更改。

```bash
git merge feature-branch
```

This code will output something like:

这段代码的输出将是类似的内容：

```
Merge made by the 'recursive' strategy.
 file1.txt | 2 +-
 file2.txt | 1 +
 2 files changed, 2 insertions(+), 1 deletion(-)
```

### 4. Handling Merge Conflicts

Sometimes, Git cannot automatically merge changes, and you will encounter a merge conflict. When this happens, Git will stop and allow you to manually resolve the conflicts in the affected files.

有时，Git无法自动合并更改，你会遇到合并冲突。发生这种情况时，Git会停止并允许你手动解决受影响文件中的冲突。

```bash
# After running git merge and encountering a conflict
# Edit the conflicting files to resolve the conflicts
# Then stage the resolved files
git add resolved-file.txt

# Complete the merge by committing the changes
git commit -m "Resolved merge conflict"
```

This code will output:

这段代码的输出将是：

```
[main xxxxxxx] Resolved merge conflict
```

### 5. Aborting a Merge

If you want to abort a merge and return to the state before the merge attempt, you can use the `git merge --abort` command.

如果你想中止合并并返回到合并尝试前的状态，你可以使用`git merge --abort`命令。

```bash
git merge --abort
```

This code will output:

这段代码的输出将是：

```
Merge aborted
```

The comparison of `git merge` scenarios is shown in the table below:

`git merge`场景的比较如下表所示：

| Scenario                         | Description in English                                                    | Description in Chinese                                                    |
|----------------------------------|---------------------------------------------------------------------------|---------------------------------------------------------------------------|
| Basic Merge                      | Merges the changes from one branch into another                            | 将一个分支的更改合并到另一个分支                                          |
| Fast-Forward Merge               | Moves the branch pointer forward, occurring when there are no new commits on the main branch | 将分支指针向前移动，当主分支上没有新的提交时发生                          |
| Recursive Merge                  | Combines changes from both branches when they have diverged                | 当两个分支发生分歧时，合并两个分支的更改                                    |
| Merge Conflict                   | Occurs when Git cannot automatically merge changes, requiring manual resolution | 当Git无法自动合并更改时发生，需要手动解决                                   |
| Abort Merge                      | Cancels the merge process and returns to the previous state                | 取消合并过程并返回到之前的状态                                             |

The `git merge` command is very useful for combining the work of different branches, ensuring that all contributions are integrated into a cohesive project.

`git merge`命令在合并不同分支的工作时非常有用，确保所有贡献都整合到一个统一的项目中。

#### 以下是关于合并分支的5个面试问题及其答案

### 1. What does the `git merge` command do? `git merge`命令的作用是什么？

 
The `git merge` command combines changes from one branch into another, integrating the work done in different branches.

`git merge`命令将一个分支的更改合并到另一个分支中，整合不同分支中的工作。

### 2. What is a fast-forward merge? 什么是快进合并？

 
A fast-forward merge occurs when the branch being merged has no new commits on the base branch, allowing the branch pointer to be moved forward without creating a new commit.

快进合并发生在被合并的分支在基础分支上没有新提交时，允许将分支指针向前移动而不创建新的提交。

### 3. How do you resolve a merge conflict? 如何解决合并冲突？

 
To resolve a merge conflict, you must manually edit the conflicting files to resolve the issues, stage the resolved files, and then complete the merge with a commit:

```bash
git add resolved-file.txt
git commit -m "Resolved merge conflict"
```

要解决合并冲突，你必须手动编辑冲突的文件以解决问题，暂存已解决的文件，然后通过提交完成合并：

```bash
git add resolved-file.txt
git commit -m "Resolved merge conflict"
```

### 4. What is the command to abort a merge? 中止合并的命令是什么？

 
The command to abort a merge is `git merge --abort`, which cancels the merge process and returns the branch to its previous state.

中止合并的命令是`git merge --abort`，它取消合并过程并将分支返回到之前的状态。

### 5. How does Git handle merging when both branches have diverged? 当两个分支都发生分歧时，Git如何处理合并？

 
When both branches have diverged, Git performs a recursive merge, which attempts to automatically combine the changes from both branches. If there are conflicts, manual resolution is required.

当两个分支都发生分歧时，Git会执行递归合并，尝试自动合并两个分支的更改。如果有冲突，则需要手动解决。

### Recommend Resource
1. [Pro Git Book - Basic Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
2. [Git Official Documentation - git merge](https://git-scm.com/docs/git-merge)
