# 7天学Git

![Version](https://img.shields.io/badge/version-1.0.0-blue)

以下是一个为期7天的Git学习计划，旨在帮助你快速掌握Git的基础和一些高级概念。这个计划假设你每天可以投入大约4小时的时间进行学习和实践。

---

# Git Command Cheat Sheet

| Command                                | Description in English                                           | Description in Chinese                                           | Code Example                           |
|----------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|----------------------------------------|
| `git init`                             | Initializes a new Git repository in the current directory        | 在当前目录中初始化一个新的Git仓库                                  | `git init`                             |
| `git status`                           | Shows the status of changes in the working directory             | 显示工作目录中更改的状态                                          | `git status`                           |
| `git add`                              | Stages files for the next commit                                 | 暂存文件以便进行下次提交                                          | `git add file.txt`                     |
| `git commit`                           | Records changes to the repository                                | 记录对仓库的更改                                                  | `git commit -m "Commit message"`       |
| `git clone`                            | Clones a repository into a new directory                         | 将仓库克隆到新目录中                                              | `git clone https://github.com/user/repo.git` |
| `git log`                              | Shows the commit history of the current branch                   | 显示当前分支的提交历史                                            | `git log`                              |
| `git checkout`                         | Switches branches or restores working tree files                 | 切换分支或恢复工作树文件                                          | `git checkout branch-name`             |
| `git merge`                            | Merges changes from one branch into another                      | 将一个分支的更改合并到另一个分支                                   | `git merge feature-branch`             |
| `git push`                             | Pushes local changes to a remote repository                      | 将本地更改推送到远程仓库                                          | `git push origin branch-name`          |
| `git pull`                             | Fetches and merges changes from a remote repository              | 从远程仓库获取并合并更改                                          | `git pull origin branch-name`          |
| `git add -p`                           | Interactively stages changes hunk by hunk                        | 以交互方式逐块暂存更改                                            | `git add -p`                           |
| `git stash`                            | Temporarily saves changes for later retrieval                    | 暂时保存更改以供以后检索                                          | `git stash`                            |
| `git stash pop`                        | Applies and removes the most recent stash                        | 应用并删除最近的存储                                              | `git stash pop`                        |
| `git rebase`                           | Moves or "rebases" commits onto another branch                   | 将提交移到或“变基”到另一个分支                                     | `git rebase main`                      |
| `git rebase -i`                        | Starts an interactive rebase for more control                    | 启动交互式变基以获得更多控制                                      | `git rebase -i HEAD~3`                 |
| `git branch`                           | Lists, creates, or deletes branches                              | 列出、创建或删除分支                                              | `git branch` / `git branch new-branch` |
| `git remote`                           | Manages set of tracked repositories                              | 管理已跟踪的仓库集                                                | `git remote -v`                        |
| `git fetch`                            | Downloads objects and refs from another repository               | 从另一个仓库下载对象和引用                                        | `git fetch origin`                     |
| `git reset`                            | Resets current HEAD to a specified state                         | 将当前HEAD重置为指定状态                                          | `git reset --hard HEAD~1`              |
| `git revert`                           | Reverts a commit by creating a new commit                        | 通过创建新提交来还原提交                                          | `git revert commit-hash`               |
| `git fork` (GitHub-specific)           | Creates a personal copy of another user's repository on GitHub   | 在GitHub上创建另一个用户仓库的个人副本                            | *Fork a repository via GitHub UI*      |
| `git pull-request` (GitHub-specific)   | Creates a pull request to propose changes to a repository        | 创建Pull Request以提出对仓库的更改                                 | *Create via GitHub UI*                 |
| `ssh-keygen`                           | Generates a new SSH key pair                                     | 生成新的SSH密钥对                                                 | `ssh-keygen -t ed25519 -C "your_email@example.com"` |
| `ssh-add`                              | Adds an SSH private key to the SSH-agent                         | 将SSH私钥添加到SSH代理                                            | `ssh-add ~/.ssh/id_ed25519`            |
| `git remote add`                       | Adds a new remote repository                                     | 添加新的远程仓库                                                  | `git remote add origin https://github.com/user/repo.git` |
| `git mergetool`                        | Launches a merge tool to resolve conflicts                       | 启动合并工具以解决冲突                                            | `git mergetool`                        |
| `git config`                           | Configures Git settings                                           | 配置Git设置                                                      | `git config --global user.name "Your Name"` |
---

### 第1天：Git基础
- **学习目标：**
  - 了解Git的基本概念和用途
  - 掌握Git的基本操作
- **学习内容：**
  - 版本控制简介：Git的优势
  - [Git安装与配置](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Git/Day1_1_Git%20Installation%20and%20Configuration.md)
  - [Git基础命令：`git init`, `git status`, `git add`, `git commit`](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Git/Day1_2_Git%20Basic%20Commands.md)
- **实践：**
  - 安装Git并配置用户名和邮箱
  - 初始化一个Git仓库，添加文件并提交

### 第2天：Git仓库管理
- **学习目标：**
  - 掌握Git仓库的基本管理操作
- **学习内容：**
  - [克隆远程仓库：`git clone`](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Git/Day2_1_Cloning%20a%20Remote%20Repository.md)
  - [查看历史记录：`git log`](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Git/Day2_2_Viewing%20History.md)
  - [取消操作：`git checkout`, `git revert`, `git reset`]()
- **实践：**
  - 克隆一个远程仓库并查看历史记录
  - 练习取消操作，恢复到之前的提交

### 第3天：分支管理
- **学习目标：**
  - 了解分支的概念和操作
- **学习内容：**
  - [创建和删除分支：`git branch`](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Git/Day3_1_Creating%20and%20Deleting%20Branches.md)
  - [切换分支：`git checkout`](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Git/Day3_2_Switching%20Branches.md)
  - [合并分支：`git merge`](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Git/Day3_3_Merging%20Branches.md)
- **实践：**
  - 创建新的分支并切换
  - 在不同分支上进行开发并合并

### 第4天：协作开发
- **学习目标：**
  - 掌握团队协作开发的基本操作
- **学习内容：**
  - [推送到远程仓库：`git push`](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Git/Day4_1_Pushing%20to%20a%20Remote%20Repository.md)
  - [从远程仓库拉取更新：`git pull`](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Git/Day4_2_Pulling%20Updates%20from%20a%20Remote%20Repository.md)
  - 处理冲突
- **实践：**
  - 推送本地分支到远程仓库
  - 拉取远程更新并解决冲突

### 第5天：高级操作
- **学习目标：**
  - 了解Git的高级操作
- **学习内容：**
  - [交互式暂存：`git add -p`](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Git/Day5_1_Interactive%20Staging.md)
  - [暂存和恢复更改：`git stash`](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Git/Day5_2_Stashing%20and%20Restoring%20Changes.md)
  - [Rebasing：`git rebase`](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Git/Day5_3_Rebasing.md)
- **实践：**
  - 使用交互式暂存选择性地提交更改
  - 使用`git stash`暂存未完成的工作并恢复
  - 练习Rebasing操作

### 第6天：GitHub和远程仓库
- **学习目标：**
  - 了解如何使用GitHub和其他远程仓库
- **学习内容：**
  - [GitHub基本操作：创建仓库、Fork、Pull Request](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Git/Day6_1_Creating%20a%20Repository%2C%20Forking%2C%20and%20Pull%20Requests.md)
  - [SSH配置和安全性](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Git/Day6_2_SSH%20Configuration%20and%20Security%20on%20GitHub.md)
- **实践：**
  - 创建一个GitHub仓库并推送本地仓库
  - 发起和合并Pull Request

### 第7天：项目实战与优化
- **学习目标：**
  - 将所学知识应用于实际项目
  - 了解Git的优化和最佳实践
- **学习内容：**
  - 项目开发与管理
  - Git最佳实践：提交信息规范、分支策略
- **实践：**
  - 使用Git管理一个实际项目
  - 应用Git最佳实践，优化工作流程

### 每日安排
- 每天4小时，分为学习（2小时）和实践（2小时）
- 每2天进行一次小结，调整学习计划
- 定期与同行或导师交流，获取反馈

### 总结
这个7天的学习计划旨在帮助你在短时间内掌握Git的核心技能和应用。如果有任何问题或需要进一步的指导，请随时告诉我。

希望这些信息对你有帮助！
