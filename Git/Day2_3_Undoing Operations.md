# Undoing Operations: `git checkout`, `git revert`, `git reset`

Undoing operations in Git is crucial for managing mistakes and changes in your code. The commands `git checkout`, `git revert`, and `git reset` allow you to navigate through your project’s history, undo changes, and reset your working directory to a previous state.

在Git中取消操作对于管理代码中的错误和更改至关重要。`git checkout`、`git revert`和`git reset`命令允许你浏览项目历史、撤销更改并将工作目录重置为以前的状态。

Here’s how you can use these commands:

以下是如何使用这些命令的方法：

### 1. `git checkout`

The `git checkout` command is used to switch between branches or restore working tree files. It can be used to undo changes in a file or revert to a previous commit without altering the commit history.

`git checkout`命令用于在分支之间切换或恢复工作树文件。它可以用于撤销文件中的更改或恢复到以前的提交，而不改变提交历史。

#### a) Switching Branches

```bash
git checkout branch-name
```

This code will switch to the specified branch:

这段代码将切换到指定的分支：

```
Switched to branch 'branch-name'
```

#### b) Undoing Changes in a File

```bash
git checkout -- filename
```

This code will discard changes in the specified file:

这段代码将放弃指定文件中的更改：

```
Updated 1 path from the index
```

### 2. `git revert`

The `git revert` command is used to create a new commit that undoes the changes from a previous commit. This is useful for reversing changes while preserving the commit history.

`git revert`命令用于创建一个新的提交来撤销以前提交中的更改。这对于在保留提交历史的同时逆转更改非常有用。

```bash
git revert commit-hash
```

This code will create a new commit that reverts the specified commit:

这段代码将创建一个新的提交来撤销指定的提交：

```
[branch-name xxxxxxx] Revert "Commit message"
 1 file changed, 2 deletions(-), 2 insertions(+)
```

### 3. `git reset`

The `git reset` command is used to undo changes by moving the current branch to a specific commit. It can be used in three modes: `--soft`, `--mixed`, and `--hard`, each providing different levels of undo.

`git reset`命令通过将当前分支移动到特定提交来撤销更改。它可以以三种模式使用：`--soft`、`--mixed`和`--hard`，每种模式提供不同级别的撤销。

#### a) `git reset --soft`

Moves the branch pointer to the specified commit but keeps the changes in the staging area.

将分支指针移动到指定提交，但保留暂存区中的更改。

```bash
git reset --soft commit-hash
```

This code will output:

这段代码的输出将是：

```
# No output, but changes remain staged
```

#### b) `git reset --mixed` (default)

Moves the branch pointer to the specified commit and unstages all changes, leaving them in the working directory.

将分支指针移动到指定提交并取消暂存所有更改，将它们留在工作目录中。

```bash
git reset --mixed commit-hash
```

This code will output:

这段代码的输出将是：

```
Unstaged changes after reset:
M       filename
```

#### c) `git reset --hard`

Moves the branch pointer to the specified commit and discards all changes in the working directory and staging area.

将分支指针移动到指定提交并放弃工作目录和暂存区中的所有更改。

```bash
git reset --hard commit-hash
```

This code will output:

这段代码的输出将是：

```
HEAD is now at commit-hash Commit message
```

The comparison of these undo commands is shown in the table below:

这些取消操作命令的比较如下表所示：

| Command                    | Description in English                                                   | Description in Chinese                                                   |
|----------------------------|--------------------------------------------------------------------------|--------------------------------------------------------------------------|
| `git checkout branch-name`  | Switches to the specified branch                                         | 切换到指定分支                                                           |
| `git checkout -- filename`  | Discards changes in the specified file                                   | 放弃指定文件中的更改                                                     |
| `git revert commit-hash`    | Creates a new commit that undoes the changes from a previous commit      | 创建一个新的提交来撤销以前提交中的更改                                   |
| `git reset --soft commit-hash`  | Moves branch to the specified commit, keeps changes staged          | 将分支移动到指定提交，保留暂存的更改                                     |
| `git reset --mixed commit-hash` | Moves branch to the specified commit, unstages changes               | 将分支移动到指定提交，取消暂存的更改                                     |
| `git reset --hard commit-hash`  | Moves branch to the specified commit, discards all changes           | 将分支移动到指定提交，放弃所有更改                                       |

These commands are very useful for managing and undoing changes in your Git workflow.

这些命令在管理和撤销Git工作流程中的更改时非常有用。

#### 以下是关于取消操作的5个面试问题及其答案

### 1. What is the difference between `git checkout` and `git reset`? `git checkout`和`git reset`有什么区别？

 
`git checkout` is used to switch branches or discard changes in a working file, while `git reset` moves the current branch to a specific commit, with options to preserve or discard changes.

`git checkout`用于切换分支或放弃工作文件中的更改，而`git reset`将当前分支移动到特定提交，可以选择保留或放弃更改。

### 2. How do you undo a commit without removing the changes from the staging area? 如何在不移除暂存区更改的情况下撤销提交？

 
You can undo a commit without removing the changes from the staging area using the `git reset --soft` command:

```bash
git reset --soft commit-hash
```

你可以使用`git reset --soft`命令在不移除暂存区更改的情况下撤销提交：

```bash
git reset --soft commit-hash
```

### 3. What is the purpose of the `git revert` command? `git revert`命令的作用是什么？

 
The `git revert` command is used to create a new commit that undoes the changes from a previous commit, preserving the commit history.

`git revert`命令用于创建一个新的提交来撤销以前提交中的更改，同时保留提交历史。

### 4. How can you discard all changes in the working directory and staging area? 如何放弃工作目录和暂存区中的所有更改？

 
You can discard all changes in the working directory and staging area using the `git reset --hard` command:

```bash
git reset --hard commit-hash
```

你可以使用`git reset --hard`命令放弃工作目录和暂存区中的所有更改：

```bash
git reset --hard commit-hash
```

### 5. When should you use `git checkout` to undo changes? 什么时候应该使用`git checkout`撤销更改？

 
You should use `git checkout` to undo changes when you want to discard changes in a specific file or switch branches without affecting the commit history.

当你想放弃特定文件中的更改或切换分支而不影响提交历史时，应该使用`git checkout`撤销更改。

### Recommend Resource
1. [Pro Git Book - Undoing Things](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified)
2. [Git Official Documentation - git reset, git checkout, git revert](https://git-scm.com/docs)
