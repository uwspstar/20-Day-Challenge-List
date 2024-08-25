# Git Basic Commands: `git init`, `git status`, `git add`, `git commit`

Git Basic Commands are fundamental operations in Git that help you initialize a repository, check the status of your files, add changes to the staging area, and commit those changes. These commands are essential for managing version control in your projects.

Git基础命令是在Git中帮助你初始化仓库、检查文件状态、将更改添加到暂存区并提交这些更改的基本操作。这些命令对于管理项目中的版本控制至关重要。

Here’s how you can use the basic Git commands:

以下是如何使用Git基础命令的方法：

### 1. `git init`

The `git init` command is used to create a new Git repository. It initializes a new repository in the current directory, allowing you to start tracking your files with Git.

`git init`命令用于创建一个新的Git仓库。它会在当前目录中初始化一个新的仓库，从而允许你开始使用Git跟踪你的文件。

```bash
git init
```

This code will output:

这段代码的输出将是：

```
Initialized empty Git repository in /path/to/your/repository/.git/
```

### 2. `git status`

The `git status` command shows the current state of the working directory and the staging area. It lets you see which changes have been staged, which haven't, and which files aren't being tracked by Git.

`git status`命令显示工作目录和暂存区的当前状态。它让你看到哪些更改已暂存，哪些未暂存，以及哪些文件未被Git跟踪。

```bash
git status
```

This code will output:

这段代码的输出将是：

```
On branch master
No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
    yourfile.txt
```

### 3. `git add`

The `git add` command adds changes from the working directory to the staging area. This command is used to prepare the content for the next commit. You can add individual files or all changes at once.

`git add`命令将工作目录中的更改添加到暂存区。该命令用于准备下一次提交的内容。你可以添加单个文件或一次性添加所有更改。

```bash
git add yourfile.txt
```

This code will output:

这段代码的输出将是：

```
# No output for successful add, but you can verify with git status
```

### 4. `git commit`

The `git commit` command captures a snapshot of the project's currently staged changes. This command is used to record changes to the repository. It requires a message that describes the commit.

`git commit`命令捕获项目当前已暂存更改的快照。该命令用于记录对仓库的更改。它需要一条描述提交的消息。

```bash
git commit -m "Initial commit"
```

This code will output:

这段代码的输出将是：

```
[master (root-commit) e69de29] Initial commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 yourfile.txt
```

The comparison of these Git basic commands is shown in the table below:

这些Git基础命令的比较如下表所示：

| Command      | Description in English                               | Description in Chinese                             |
|--------------|------------------------------------------------------|----------------------------------------------------|
| `git init`   | Initializes a new Git repository                     | 初始化一个新的Git仓库                                |
| `git status` | Shows the current state of the working directory     | 显示工作目录的当前状态                               |
| `git add`    | Adds changes to the staging area                     | 将更改添加到暂存区                                   |
| `git commit` | Records changes to the repository                    | 记录对仓库的更改                                     |

These Git Basic Commands are very useful for starting and managing version control in your projects.

这些Git基础命令在开始和管理项目中的版本控制时非常有用。

#### 以下是关于Git基础命令的5个面试问题及其答案

### 1. What does the `git init` command do? `git init`命令的作用是什么？

 
The `git init` command initializes a new Git repository in the current directory. It creates a `.git` directory that contains all the necessary metadata for the repository.

`git init`命令在当前目录中初始化一个新的Git仓库。它创建一个包含所有必要元数据的`.git`目录。

### 2. How can you check the status of your working directory in Git? 如何检查Git中工作目录的状态？

 
You can check the status of your working directory in Git using the `git status` command. This command shows you which changes are staged, which aren't, and which files are not being tracked.

你可以使用`git status`命令检查Git中工作目录的状态。该命令显示哪些更改已暂存，哪些未暂存，以及哪些文件未被跟踪。

### 3. How do you add all files to the staging area at once? 如何一次性将所有文件添加到暂存区？

 
You can add all files to the staging area at once using the following command:

```bash
git add .
```

This command stages all changes in the current directory.

你可以使用以下命令一次性将所有文件添加到暂存区：

```bash
git add .
```

此命令会暂存当前目录中的所有更改。

### 4. What is the purpose of the `git commit -m` command? `git commit -m`命令的作用是什么？

 
The `git commit -m` command is used to commit staged changes to the repository with a message that describes the changes. The `-m` option allows you to provide the commit message directly in the command line.

`git commit -m`命令用于将暂存的更改提交到仓库，并附带一条描述更改的消息。`-m`选项允许你直接在命令行中提供提交消息。

### 5. How can you view the differences between the working directory and the staging area? 如何查看工作目录和暂存区之间的差异？

 
You can view the differences between the working directory and the staging area using the `git diff` command. This command shows the changes that have been made in the working directory but not yet staged.

你可以使用`git diff`命令查看工作目录和暂存区之间的差异。此命令显示了工作目录中已做出但尚未暂存的更改。

### Recommend Resource
1. [Pro Git Book - Basic Git Commands](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control)
2. [Git Official Documentation - Command Reference](https://git-scm.com/docs)
