# Rebasing: `git rebase`

The `git rebase` command is a powerful Git feature that allows you to integrate changes from one branch into another. Unlike `git merge`, which combines the contents of two branches and preserves the commit history of both, `git rebase` moves or "rebases" your commits onto another branch, resulting in a linear and cleaner commit history.

`git rebase`命令是Git的一个强大功能，它允许你将一个分支的更改整合到另一个分支中。与保留两个分支提交历史并合并其内容的`git merge`不同，`git rebase`将你的提交移动或“变基”到另一个分支，从而产生一个线性且更干净的提交历史。

Here’s how you can use the `git rebase` command:

以下是如何使用`git rebase`命令的方法：

### 1. Basic Rebase

The most common use of `git rebase` is to move the changes from one branch onto the tip of another branch. This is useful when you want to incorporate changes from one branch into another while keeping the history clean.

`git rebase`的最常见用法是将一个分支的更改移到另一个分支的末端。当你想将一个分支的更改合并到另一个分支中并保持历史记录干净时，这非常有用。

```bash
# Switch to the branch you want to rebase
git checkout feature-branch

# Rebase the current branch onto the main branch
git rebase main
```

This code will output:

这段代码的输出将是：

```
First, rewinding head to replay your work on top of it...
Applying: Your commit message
```

### 2. Interactive Rebase

Interactive rebase (`git rebase -i`) gives you more control over how commits are applied during the rebase. You can reorder, squash, edit, or drop commits as you replay them onto another branch.

交互式变基（`git rebase -i`）使你可以更好地控制在变基过程中如何应用提交。你可以在将提交重放到另一个分支上时重新排序、合并、编辑或删除提交。

```bash
# Start an interactive rebase
git rebase -i HEAD~3
```

This code will open an editor with the last three commits, allowing you to choose how to handle each commit:

这段代码将打开一个包含最近三次提交的编辑器，允许你选择如何处理每个提交：

```
pick e5b9fbc Commit message 1
pick 6b1ac3e Commit message 2
pick c3f789d Commit message 3

# Rebase c3f789d..e5b9fbc onto c3f789d (3 commands)
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
```

### 3. Squashing Commits

Squashing commits combines multiple commits into a single commit. This is useful when you want to clean up a series of small, incremental commits into one meaningful commit.

合并提交将多个提交合并为一个提交。当你想要将一系列小的增量提交清理为一个有意义的提交时，这非常有用。

```bash
# Start an interactive rebase to squash commits
git rebase -i HEAD~3
```

In the editor, change `pick` to `squash` (or `s`) for the commits you want to combine:

在编辑器中，将要合并的提交的`pick`更改为`squash`（或`s`）：

```
pick e5b9fbc Commit message 1
squash 6b1ac3e Commit message 2
squash c3f789d Commit message 3
```

After saving and closing the editor, Git will prompt you to combine the commit messages.

保存并关闭编辑器后，Git会提示你合并提交消息。

### 4. Aborting a Rebase

If you encounter conflicts during a rebase or decide that you do not want to proceed with the rebase, you can abort it and return to the original branch state.

如果你在变基过程中遇到冲突或决定不继续进行变基，可以中止变基并返回到原始分支状态。

```bash
git rebase --abort
```

This code will output:

这段代码的输出将是：

```
Rebase aborted; here is your previous state:
HEAD is now at xxxxxxx Commit message
```

### 5. Continuing a Rebase After Resolving Conflicts

If you encounter conflicts during a rebase, Git will pause the rebase process and allow you to manually resolve the conflicts. After resolving the conflicts, you can continue the rebase.

如果你在变基过程中遇到冲突，Git将暂停变基过程并允许你手动解决冲突。解决冲突后，你可以继续进行变基。

```bash
# After resolving conflicts
git add resolved-file.txt
git rebase --continue
```

This code will output:

这段代码的输出将是：

```
Applying: Your commit message
```

### 6. Rebase vs. Merge

While both `git rebase` and `git merge` integrate changes from one branch into another, they do so in different ways. `git merge` preserves the commit history of both branches, while `git rebase` rewrites the history to create a linear progression of commits.

虽然`git rebase`和`git merge`都可以将一个分支的更改整合到另一个分支中，但它们的方式不同。`git merge`保留了两个分支的提交历史，而`git rebase`重写历史，以创建线性提交进程。

| Feature        | `git merge`                                         | `git rebase`                                      |
|----------------|-----------------------------------------------------|--------------------------------------------------|
| History        | Preserves history of both branches                  | Rewrites history to create a linear progression  |
| Commit History | Results in a merge commit                           | Results in a series of commits on top of another |
| Use Case       | When you want to preserve all branch histories      | When you want a clean, linear history            |

The comparison of `git rebase` use cases is shown in the table below:

`git rebase`用例的比较如下表所示：

| Command                             | Description in English                                           | Description in Chinese                                           |
|-------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|
| `git rebase main`                   | Moves the current branch’s commits on top of the main branch     | 将当前分支的提交移到main分支的顶部                               |
| `git rebase -i HEAD~3`              | Starts an interactive rebase for the last three commits          | 对最近的三次提交启动交互式变基                                   |
| `git rebase --abort`                | Aborts the rebase and returns to the original branch state       | 中止变基并返回到原始分支状态                                     |
| `git rebase --continue`             | Continues the rebase after resolving conflicts                   | 解决冲突后继续变基                                               |
| `git rebase --skip`                 | Skips the current commit during rebase                           | 在变基过程中跳过当前提交                                         |

The `git rebase` command is very useful for maintaining a clean and linear commit history, especially when collaborating with others and integrating changes from different branches.

`git rebase`命令在维护干净且线性的提交历史时非常有用，尤其是在与他人协作并整合不同分支的更改时。

#### 以下是关于变基的5个面试问题及其答案

### 1. What does the `git rebase` command do? `git rebase`命令的作用是什么？

 
The `git rebase` command moves or "rebases" your commits onto another branch, creating a linear commit history by placing your changes on top of the specified branch.

`git rebase`命令将你的提交移到或“变基”到另一个分支，通过将你的更改放在指定分支的顶部创建线性提交历史。

### 2. How does `git rebase` differ from `git merge`? `git rebase`与`git merge`有何不同？

 
`git rebase` rewrites the commit history to create a linear progression, while `git merge` preserves the commit history of both branches and results in a merge commit.

`git rebase`重写提交历史以创建线性进程，而`git merge`保留两个分支的提交历史，并导致合并提交。

### 3. What is an interactive rebase, and when would you use it? 什么是交互式变基，什么时候使用它？

 
An interactive rebase (`git rebase -i`) allows you to edit, reorder, squash, or drop commits during the rebase process. It is used when you want to refine the commit history before applying it to another branch.

交互式变基（`git rebase -i`）允许你在变

基过程中编辑、重新排序、合并或删除提交。当你想在将提交应用到另一个分支之前优化提交历史时使用它。

### 4. How can you abort a rebase if something goes wrong? 如果出现问题，你如何中止变基？

 
You can abort a rebase using the `git rebase --abort` command, which will return the branch to its original state before the rebase started.

你可以使用`git rebase --abort`命令中止变基，这将使分支返回到变基开始前的原始状态。

### 5. What is the purpose of squashing commits during a rebase? 在变基过程中合并提交的目的是什么？

 
Squashing commits during a rebase combines multiple commits into a single commit, helping to clean up the commit history and make it more meaningful and concise.

在变基过程中合并提交将多个提交合并为一个提交，帮助清理提交历史，使其更有意义且简洁。

### Recommend Resource
1. [Pro Git Book - Rebasing](https://git-scm.com/book/en/v2/Git-Branching-Rebasing)
2. [Git Official Documentation - git rebase](https://git-scm.com/docs/git-rebase)
