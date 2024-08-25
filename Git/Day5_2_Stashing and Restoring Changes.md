# Stashing and Restoring Changes: `git stash`

The `git stash` command is a powerful Git feature that allows you to temporarily save changes in your working directory without committing them. This is useful when you need to switch branches or work on something else without losing your current work. You can later restore these changes when you're ready to continue working on them.

`git stash`命令是Git的一个强大功能，它允许你在不提交更改的情况下临时保存工作目录中的更改。当你需要切换分支或处理其他事情而不想丢失当前工作时，这非常有用。稍后，当你准备继续工作时，可以恢复这些更改。

Here’s how you can use the `git stash` command:

以下是如何使用`git stash`命令的方法：

### 1. Stashing Changes

The basic usage of `git stash` allows you to save your uncommitted changes, which include both staged and unstaged changes.

`git stash`的基本用法允许你保存未提交的更改，这包括已暂存和未暂存的更改。

```bash
git stash
```

This code will output:

这段代码的输出将是：

```
Saved working directory and index state WIP on branch-name: xxxxxxx Commit message
HEAD is now at xxxxxxx Commit message
```

Your working directory will be clean, meaning all your changes have been stashed.

你的工作目录将是干净的，这意味着所有更改都已被存储。

### 2. Listing Stashes

You can view the list of all stashes you have saved using the `git stash list` command. Each stash is identified by a name like `stash@{0}`, where `0` represents the most recent stash.

你可以使用`git stash list`命令查看所有已保存的存储列表。每个存储都有一个名称，如`stash@{0}`，其中`0`代表最近的存储。

```bash
git stash list
```

This code will output:

这段代码的输出将是：

```
stash@{0}: WIP on branch-name: xxxxxxx Commit message
stash@{1}: WIP on branch-name: yyyyyyy Another commit message
```

### 3. Applying a Stash

To restore the most recent stash, you can use the `git stash apply` command. This will reapply the changes from the stash to your working directory, leaving the stash itself intact (it won’t be deleted).

要恢复最近的存储，你可以使用`git stash apply`命令。这将把存储中的更改重新应用到工作目录中，并且存储本身保持不变（不会被删除）。

```bash
git stash apply
```

This code will output:

这段代码的输出将是：

```
On branch branch-name
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   file.txt
```

### 4. Popping a Stash

If you want to apply the stash and also remove it from the stash list, you can use the `git stash pop` command. This is a combination of applying and deleting a stash in one step.

如果你想应用存储并将其从存储列表中删除，可以使用`git stash pop`命令。这是在一个步骤中应用和删除存储的组合。

```bash
git stash pop
```

This code will output:

这段代码的输出将是：

```
On branch branch-name
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   file.txt
Dropped refs/stash@{0} (xxxxx)
```

### 5. Stashing with a Message

You can also stash changes with a custom message to help you identify the stash later. This is useful if you have multiple stashes and need to distinguish between them.

你还可以使用自定义消息存储更改，以帮助你稍后识别存储。如果你有多个存储并且需要区分它们，这非常有用。

```bash
git stash save "message describing the changes"
```

This code will output:

这段代码的输出将是：

```
Saved working directory and index state On branch-name: message describing the changes
HEAD is now at xxxxxxx Commit message
```

### 6. Dropping a Stash

If you no longer need a particular stash, you can delete it from the stash list using the `git stash drop` command.

如果你不再需要特定的存储，可以使用`git stash drop`命令将其从存储列表中删除。

```bash
git stash drop stash@{0}
```

This code will output:

这段代码的输出将是：

```
Dropped stash@{0} (xxxxx)
```

### 7. Clearing All Stashes

If you want to delete all stashes at once, you can use the `git stash clear` command. This will remove all stashes from the stash list.

如果你想一次删除所有存储，可以使用`git stash clear`命令。这将从存储列表中删除所有存储。

```bash
git stash clear
```

This code will output:

这段代码的输出将是：

```
# No output, but all stashes will be cleared
```

The comparison of `git stash` use cases is shown in the table below:

`git stash`用例的比较如下表所示：

| Command                              | Description in English                                            | Description in Chinese                                             |
|--------------------------------------|-------------------------------------------------------------------|-------------------------------------------------------------------|
| `git stash`                          | Stashes changes in the working directory and index                | 将工作目录和索引中的更改存储起来                                   |
| `git stash list`                     | Lists all stashes saved                                           | 列出所有已保存的存储                                               |
| `git stash apply`                    | Applies the most recent stash to the working directory            | 将最近的存储应用到工作目录中                                       |
| `git stash pop`                      | Applies the most recent stash and removes it from the stash list  | 将最近的存储应用并将其从存储列表中删除                             |
| `git stash save "message"`           | Stashes changes with a custom message                             | 使用自定义消息存储更改                                             |
| `git stash drop stash@{n}`           | Removes a specific stash from the stash list                      | 从存储列表中删除特定的存储                                         |
| `git stash clear`                    | Removes all stashes from the stash list                           | 从存储列表中删除所有存储                                           |

The `git stash` command is very useful for temporarily saving work in progress and for situations where you need to quickly switch tasks without losing your current changes.

`git stash`命令在临时保存正在进行的工作以及需要快速切换任务而不丢失当前更改的情况下非常有用。

#### 以下是关于暂存和恢复更改的5个面试问题及其答案

### 1. What does the `git stash` command do? `git stash`命令的作用是什么？

 
The `git stash` command temporarily saves your changes in the working directory and index, allowing you to switch branches or work on something else without losing your current changes.

`git stash`命令暂时保存工作目录和索引中的更改，使你能够切换分支或处理其他事情而不丢失当前更改。

### 2. How do you apply the most recent stash? 如何应用最近的存储？

 
You can apply the most recent stash using the `git stash apply` command.

你可以使用`git stash apply`命令应用最近的存储。

### 3. What is the difference between `git stash apply` and `git stash pop`? `git stash apply`和`git stash pop`有什么区别？

 
`git stash apply` reapplies the most recent stash without removing it from the stash list, while `git stash pop` applies the stash and also removes it from the stash list.

`git stash apply`重新应用最近的存储，但不将其从存储列表中删除，而`git stash pop`应用存储并将其从存储列表中删除。

### 4. How can you list all the stashes you have saved? 如何列出所有已保存的存储？

 
You can list all the stashes you have saved using the `git stash list` command.

你可以使用`git stash list`命令列出所有已保存的存储。

### 5. What command can you use to clear all stashes? 你可以使用什么命令清除所有存储？

 
You can clear all stashes using the `git stash clear` command.

你可以使用`git stash clear`命令清除所有存储。

### Recommend Resource
1. [Pro Git Book - Stashing and Cleaning](https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning)
2. [Git Official Documentation - git stash](https://git-scm.com/docs/git-stash)
