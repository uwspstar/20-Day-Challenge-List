# Viewing History: `git log`

The `git log` command is a powerful tool in Git that allows you to view the history of commits in a repository. This command provides detailed information about each commit, including the author, date, and commit message, enabling you to track the evolution of the codebase.

查看历史记录使用`git log`是Git中一个强大的工具，它允许你查看仓库中的提交历史。该命令提供了每个提交的详细信息，包括作者、日期和提交信息，使你能够跟踪代码库的演变。

Here’s how you can use the `git log` command:

以下是如何使用`git log`命令的方法：

### 1. Basic `git log` Command

The basic `git log` command displays the commit history of the current branch, showing each commit in reverse chronological order (most recent commit first).

基本的`git log`命令显示当前分支的提交历史，按时间倒序显示每个提交（最近的提交在最前面）。

```bash
git log
```

This code will output:

这段代码的输出将是：

```
commit f5c3b65b1a1234567890abcdef1234567890abcd
Author: Your Name <your.email@example.com>
Date:   Mon Aug 23 12:34:56 2024 +0200

    Add feature X

commit 5b3c4a9b2c0987654321fedcba9876543210fedc
Author: Another Name <another.email@example.com>
Date:   Sun Aug 22 09:21:33 2024 +0200

    Fix bug Y
```

### 2. Viewing a Single Line per Commit

The `git log --oneline` command condenses the commit history, showing each commit on a single line. This is useful for getting a quick overview of the commit history.

`git log --oneline`命令将提交历史压缩到一行中显示每个提交。这样可以快速概览提交历史。

```bash
git log --oneline
```

This code will output:

这段代码的输出将是：

```
f5c3b65b Add feature X
5b3c4a9b Fix bug Y
```

### 3. Limiting the Number of Commits Shown

You can limit the number of commits displayed by using the `-n` option followed by the number of commits you want to see.

你可以使用`-n`选项并指定你希望查看的提交数量来限制显示的提交数量。

```bash
git log -n 3
```

This code will output the last three commits:

这段代码将输出最近的三次提交：

```
commit f5c3b65b1a1234567890abcdef1234567890abcd
Author: Your Name <your.email@example.com>
Date:   Mon Aug 23 12:34:56 2024 +0200

    Add feature X

commit 5b3c4a9b2c0987654321fedcba9876543210fedc
Author: Another Name <another.email@example.com>
Date:   Sun Aug 22 09:21:33 2024 +0200

    Fix bug Y

commit 8c9f1b2a3d4c56789012345678901234567890ab
Author: Your Name <your.email@example.com>
Date:   Sat Aug 21 16:42:18 2024 +0200

    Update documentation
```

### 4. Filtering Commits by Author

The `git log --author` command allows you to filter commits by a specific author. This is useful when you want to see only the commits made by a particular contributor.

`git log --author`命令允许你按特定作者筛选提交。当你只想查看特定贡献者的提交时，这非常有用。

```bash
git log --author="Your Name"
```

This code will output:

这段代码的输出将是：

```
commit f5c3b65b1a1234567890abcdef1234567890abcd
Author: Your Name <your.email@example.com>
Date:   Mon Aug 23 12:34:56 2024 +0200

    Add feature X

commit 8c9f1b2a3d4c56789012345678901234567890ab
Author: Your Name <your.email@example.com>
Date:   Sat Aug 21 16:42:18 2024 +0200

    Update documentation
```

### 5. Viewing Commit History with File Changes

You can view the commit history along with the changes made to each file using the `git log -p` command. This is helpful for understanding the specific changes introduced in each commit.

你可以使用`git log -p`命令查看提交历史及每个文件的更改。这对于了解每次提交中引入的具体更改非常有帮助。

```bash
git log -p
```

This code will output:

这段代码的输出将是：

```
commit f5c3b65b1a1234567890abcdef1234567890abcd
Author: Your Name <your.email@example.com>
Date:   Mon Aug 23 12:34:56 2024 +0200

    Add feature X

diff --git a/file.txt b/file.txt
index 83db48f..f1e2d9a 100644
--- a/file.txt
+++ b/file.txt
@@ -1,2 +1,2 @@
-Old line
+New line
```

The comparison of `git log` options is shown in the table below:

`git log`选项的比较如下表所示：

| Option                    | Description in English                                      | Description in Chinese                                      |
|---------------------------|-------------------------------------------------------------|-------------------------------------------------------------|
| `git log`                 | Displays the commit history                                 | 显示提交历史                                                |
| `git log --oneline`       | Shows a summary of the commit history, one line per commit  | 以摘要形式显示提交历史，每个提交占一行                     |
| `git log -n <number>`     | Limits the number of commits shown                          | 限制显示的提交数量                                           |
| `git log --author=<name>` | Filters commits by author                                   | 按作者筛选提交                                               |
| `git log -p`              | Shows commit history with changes made to files            | 显示提交历史及文件的更改                                     |

The `git log` command is very useful for understanding the history of a project and tracking the changes made over time.

`git log`命令在理解项目历史和跟踪随时间推移所做的更改时非常有用。

#### 以下是关于查看历史记录的5个面试问题及其答案

### 1. What is the `git log` command used for? `git log`命令的用途是什么？

 
The `git log` command is used to view the commit history of a repository. It shows details about each commit, including the author, date, and commit message.

`git log`命令用于查看仓库的提交历史。它显示每个提交的详细信息，包括作者、日期和提交信息。

### 2. How can you display the commit history in a condensed format? 如何以简洁的格式显示提交历史？

 
You can display the commit history in a condensed format using the `git log --oneline` command, which shows each commit on a single line.

你可以使用`git log --oneline`命令以简洁的格式显示提交历史，该命令将每个提交显示在一行中。

### 3. How do you filter commits by a specific author? 如何按特定作者筛选提交？

 
You can filter commits by a specific author using the `git log --author` option followed by the author's name:

```bash
git log --author="Your Name"
```

你可以使用`git log --author`选项并在后面添加作者姓名来按特定作者筛选提交：

```bash
git log --author="Your Name"
```

### 4. What command can you use to see the changes made in each commit? 你可以使用什么命令查看每个提交中所做的更改？

 
You can see the changes made in each commit using the `git log -p` command, which shows the differences introduced in each commit.

你可以使用`git log -p`命令查看每个提交中所做的更改，该命令显示每个提交中引入的差异。

### 5. How can you limit the number of commits shown in the log? 如何限制日志中显示的提交数量？

 
You can limit the number of commits shown in the log using the `-n` option followed by the number of commits you want to see:

```bash
git log -n 3
```

你可以使用`-n`选项并在后面添加你希望查看的提交数量来限制日志中显示的提交数量：

```bash
git log -n 3
```

### Recommend Resource
1. [Pro Git Book - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)
2. [Git Official Documentation - git log](https://git-scm.com/docs/git-log)
