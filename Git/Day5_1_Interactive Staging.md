# Interactive Staging: `git add -p`

The `git add -p` command is an advanced Git feature that allows you to stage changes interactively, making it easier to selectively include parts of files in your next commit. This is particularly useful when you have multiple changes in a single file but only want to commit some of them.

`git add -p`命令是Git的一个高级功能，它允许你以交互方式暂存更改，从而更轻松地选择性地将文件的部分更改包含在下一次提交中。当你在一个文件中有多个更改但只想提交其中一些时，这非常有用。

Here’s how you can use the `git add -p` command:

以下是如何使用`git add -p`命令的方法：

### 1. Basic Usage of `git add -p`

The `git add -p` command splits the changes in your working directory into individual hunks and presents them to you one by one. You can then choose which hunks to stage and which to leave out.

`git add -p`命令将工作目录中的更改分成单个块，并逐个呈现给你。然后你可以选择哪些块要暂存，哪些块要排除。

```bash
git add -p
```

This command will output a series of prompts for each hunk:

这段代码将为每个块输出一系列提示：

```
diff --git a/file.txt b/file.txt
index abc1234..def5678 100644
--- a/file.txt
+++ b/file.txt
@@ -1,3 +1,4 @@
 Line 1
 Line 2
+New Line 3
 Line 4

Stage this hunk [y,n,q,a,d,/,s,e,?]?
```

### 2. Understanding the Prompts

When you run `git add -p`, Git presents you with several options for each hunk:

当你运行`git add -p`时，Git会为每个块提供多个选项：

- **y**: Stage this hunk
- **n**: Do not stage this hunk
- **q**: Quit; do not stage this hunk or any of the remaining hunks
- **a**: Stage this hunk and all the remaining hunks in the file
- **d**: Do not stage this hunk or any of the remaining hunks in the file
- **s**: Split the current hunk into smaller hunks
- **e**: Manually edit the current hunk
- **?**: Print help for these options

选择这些选项可以帮助你逐步控制哪些更改被暂存。

### 3. Splitting a Hunk (`s` Option)

If a hunk is too large or includes changes that you want to stage separately, you can use the `s` option to split the hunk into smaller pieces.

如果一个块太大或包含你希望单独暂存的更改，你可以使用`s`选项将块拆分为更小的部分。

```bash
Stage this hunk [y,n,q,a,d,/,s,e,?]? s
```

This command will attempt to split the hunk and present smaller hunks for staging.

此命令将尝试拆分块并显示较小的块以供暂存。

### 4. Manually Editing a Hunk (`e` Option)

The `e` option allows you to manually edit the hunk, enabling you to precisely control which changes are included in the commit.

`e`选项允许你手动编辑块，使你能够精确控制哪些更改包含在提交中。

```bash
Stage this hunk [y,n,q,a,d,/,s,e,?]? e
```

This command opens the hunk in your default text editor, where you can modify it to include or exclude specific lines.

此命令将在默认文本编辑器中打开块，在这里你可以修改它以包含或排除特定的行。

### 5. Staging All Changes in a File (`a` Option)

If you decide that you want to stage all changes in the current file after reviewing a hunk, you can use the `a` option.

如果你在检查完一个块后决定要暂存当前文件中的所有更改，可以使用`a`选项。

```bash
Stage this hunk [y,n,q,a,d,/,s,e,?]? a
```

This command will stage the current hunk and all remaining hunks in the file.

此命令将暂存当前块及文件中的所有剩余块。

The comparison of `git add -p` options is shown in the table below:

`git add -p`选项的比较如下表所示：

| Option | Description in English                                     | Description in Chinese                                     |
|--------|------------------------------------------------------------|------------------------------------------------------------|
| `y`    | Stage the current hunk                                      | 暂存当前块                                                 |
| `n`    | Do not stage the current hunk                               | 不暂存当前块                                               |
| `q`    | Quit; do not stage the current or remaining hunks           | 退出；不暂存当前块或剩余块                                 |
| `a`    | Stage the current hunk and all remaining hunks in the file  | 暂存当前块及文件中的所有剩余块                             |
| `d`    | Do not stage the current hunk or any remaining hunks        | 不暂存当前块或任何剩余块                                   |
| `s`    | Split the current hunk into smaller hunks                   | 将当前块拆分为较小的块                                     |
| `e`    | Manually edit the current hunk                              | 手动编辑当前块                                             |
| `?`    | Show help for the options                                   | 显示选项的帮助                                             |

The `git add -p` command is very useful for controlling which changes to include in a commit, especially in situations where you want to make a series of related but separate commits.

`git add -p`命令在控制哪些更改包含在提交中时非常有用，尤其是在你想要进行一系列相关但独立的提交时。

#### 以下是关于交互式暂存的5个面试问题及其答案

### 1. What does the `git add -p` command do? `git add -p`命令的作用是什么？

 
The `git add -p` command allows you to stage changes interactively, hunk by hunk, giving you fine-grained control over what is included in the next commit.

`git add -p`命令允许你以交互方式逐块暂存更改，从而精细控制下一个提交中包含的内容。

### 2. How do you split a hunk into smaller pieces during interactive staging? 如何在交互式暂存过程中将块拆分为较小的部分？

 
You can split a hunk into smaller pieces during interactive staging by using the `s` option when prompted.

你可以在交互式暂存过程中使用`s`选项将块拆分为较小的部分。

### 3. What does the `e` option allow you to do in `git add -p`? `git add -p`中的`e`选项允许你做什么？

 
The `e` option in `git add -p` allows you to manually edit the current hunk, giving you precise control over which lines are included in the commit.

`git add -p`中的`e`选项允许你手动编辑当前块，从而精确控制提交中包含的行。

### 4. How do you stage all changes in a file during interactive staging? 如何在交互式暂存过程中暂存文件中的所有更改？

 
You can stage all changes in a file during interactive staging by using the `a` option after being prompted for a hunk.

你可以在交互式暂存过程中在提示块后使用`a`选项暂存文件中的所有更改。

### 5. What is the purpose of the `q` option in `git add -p`? `git add -p`中`q`选项的作用是什么？

 
The `q` option in `git add -p` allows you to quit the interactive staging process without staging the current or any remaining hunks.

`git add -p`中的`q`选项允许你退出交互式暂存过程，而不暂存当前或任何剩余的块。

### Recommend Resource
1. [Pro Git Book - Interactive Staging](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)
2. [Git Official Documentation - git add](https://git-scm.com/docs/git-add)
