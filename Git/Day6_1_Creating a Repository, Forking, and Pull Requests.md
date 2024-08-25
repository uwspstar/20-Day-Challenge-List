# Basic GitHub Operations: Creating a Repository, Forking, and Pull Requests

GitHub is a popular platform for hosting Git repositories and collaborating on projects. Understanding the basic operations on GitHub, such as creating a repository, forking a repository, and submitting pull requests, is essential for effective collaboration and project management.

GitHub是一个流行的托管Git仓库和协作项目的平台。了解在GitHub上的基本操作，如创建仓库、Fork仓库和提交Pull Request，对于有效的协作和项目管理至关重要。

Here’s how you can perform these basic GitHub operations:

以下是如何执行这些GitHub基本操作的方法：

### 1. Creating a Repository

Creating a new repository on GitHub is the first step in starting a new project. A repository, or "repo," is where your project's files and revision history are stored.

在GitHub上创建新仓库是启动新项目的第一步。仓库（或“repo”）是存储项目文件和修订历史记录的地方。

#### Steps to Create a Repository:

1. **Log in to GitHub**: Go to [GitHub](https://github.com) and log in to your account.
2. **Create a New Repository**:
   - Click on the **+** icon in the upper-right corner of the page and select **New repository**.
   - Enter a **Repository name**.
   - Optionally, add a **Description**.
   - Choose between making the repository **Public** (visible to everyone) or **Private** (visible only to you and selected collaborators).
   - Optionally, initialize the repository with a **README** file, which provides an overview of your project.
   - Click **Create repository**.

#### 在GitHub上创建仓库的步骤：

1. **登录GitHub**：访问[GitHub](https://github.com)并登录你的帐户。
2. **创建新仓库**：
   - 点击页面右上角的**+**图标，选择**New repository**。
   - 输入**Repository name**（仓库名称）。
   - 可选地，添加**Description**（描述）。
   - 选择将仓库设置为**Public**（公开，所有人可见）还是**Private**（私有，仅你和选定的协作者可见）。
   - 可选地，用一个**README**文件初始化仓库，该文件提供了项目的概述。
   - 点击**Create repository**。

### 2. Forking a Repository

Forking is the process of creating a copy of someone else’s repository under your own GitHub account. This allows you to make changes to the project without affecting the original repository. It's commonly used to propose changes (via pull requests) to someone else's project or to use someone else’s project as a starting point for your own.

Fork是指在自己的GitHub帐户下创建其他人仓库的副本。这使你能够对项目进行更改而不影响原始仓库。通常用于向他人的项目提出更改建议（通过Pull Request），或将他人的项目用作自己项目的起点。

#### Steps to Fork a Repository:

1. **Navigate to the Repository**: Go to the repository you want to fork on GitHub.
2. **Fork the Repository**:
   - Click the **Fork** button at the top-right corner of the repository page.
   - GitHub will create a copy of the repository under your account.
   - After forking, you can make changes in your forked repository.

#### Fork仓库的步骤：

1. **导航到仓库**：在GitHub上转到你想要Fork的仓库。
2. **Fork仓库**：
   - 点击仓库页面右上角的**Fork**按钮。
   - GitHub将在你的帐户下创建该仓库的副本。
   - Fork之后，你可以在Fork的仓库中进行更改。

### 3. Creating a Pull Request

A pull request (PR) is a method of submitting your changes to a repository for review and inclusion in the original project. When you create a pull request, you propose that the changes you made to your forked repository be merged into the original repository. This is a key feature of collaborative development on GitHub.

Pull Request（PR）是一种提交更改到仓库以供审查并包含在原始项目中的方法。当你创建一个Pull Request时，你提议将对Fork仓库所做的更改合并到原始仓库中。这是GitHub上协作开发的关键功能。

#### Steps to Create a Pull Request:

1. **Push Your Changes**: Make sure your changes are committed and pushed to your forked repository on GitHub.
2. **Open a Pull Request**:
   - Navigate to the original repository where you want to submit the changes.
   - Click on the **Pull requests** tab.
   - Click the **New pull request** button.
3. **Select Branches**:
   - Compare the changes between the base branch (the branch of the original repository) and the head branch (your branch with the changes).
   - GitHub will show the differences and indicate if the branches can be merged without conflicts.
4. **Create the Pull Request**:
   - Add a title and description for your pull request to explain what changes you made and why they should be merged.
   - Click **Create pull request**.

#### 创建Pull Request的步骤：

1. **推送更改**：确保已提交并推送更改到GitHub上的Fork仓库。
2. **打开Pull Request**：
   - 导航到你想提交更改的原始仓库。
   - 点击**Pull requests**标签。
   - 点击**New pull request**按钮。
3. **选择分支**：
   - 比较基础分支（原始仓库的分支）和头部分支（包含更改的分支）之间的差异。
   - GitHub会显示差异，并指示这些分支是否可以无冲突地合并。
4. **创建Pull Request**：
   - 添加Pull Request的标题和描述，解释你做了哪些更改以及为什么应该合并。
   - 点击**Create pull request**。

### Summary of GitHub Basic Operations

| Operation        | Description in English                                  | Description in Chinese                                   |
|------------------|---------------------------------------------------------|----------------------------------------------------------|
| Creating a Repository | Start a new project by creating a GitHub repository | 通过创建GitHub仓库启动一个新项目                          |
| Forking a Repository  | Create a personal copy of another user's repository | 创建另一个用户仓库的个人副本                              |
| Creating a Pull Request | Propose changes to the original project by submitting a PR | 通过提交PR向原始项目提出更改建议                          |

These basic operations—creating repositories, forking, and pull requests—are fundamental to collaborating on GitHub, enabling multiple people to work together on projects, propose changes, and review each other’s work.

这些基本操作——创建仓库、Fork和Pull Request——是GitHub上协作的基础，能够让多人协作处理项目、提出更改建议并相互审查工作。

#### 以下是关于GitHub基本操作的5个面试问题及其答案

### 1. What is the purpose of creating a repository on GitHub? 在GitHub上创建仓库的目的是什么？

 
Creating a repository on GitHub allows you to start a new project, store its files, and manage its version history. It also enables collaboration with others.

在GitHub上创建仓库允许你启动一个新项目，存储其文件并管理其版本历史记录。它还可以使你与他人协作。

### 2. What does forking a repository mean? Fork仓库是什么意思？

 
Forking a repository means creating a copy of someone else's repository under your own GitHub account, allowing you to make changes without affecting the original repository.

Fork仓库意味着在自己的GitHub帐户下创建其他人仓库的副本，从而允许你进行更改而不影响原始仓库。

### 3. How do you propose changes to a project on GitHub? 如何向GitHub上的项目提出更改建议？

 
You propose changes to a project on GitHub by creating a pull request, which submits your changes for review and possible inclusion in the original repository.

你通过创建Pull Request向GitHub上的项目提出更改建议，这会提交你的更改供审查并可能包含在原始仓库中。

### 4. What is the difference between a public and a private repository on GitHub? GitHub上的公开仓库和私有仓库有什么区别？

 
A public repository is visible to everyone, while a private repository is only visible to you and selected collaborators.

公开仓库对所有人可见，而私有仓库仅对你和选定的协作者可见。

### 5. How do you create a pull request after forking a repository? Fork仓库后如何创建Pull Request？

 
After forking a repository, you create a pull request by pushing your changes to your forked repository, navigating to the original repository, and using the Pull Request tab to propose your changes.

Fork仓库后，你可以通过将更改推送到Fork仓库，导航到原始仓库，并使用Pull Request标签来提出更改，从而创建Pull Request。

### Recommend Resource
1. [GitHub Docs - Create a Repository](https://docs.github.com/en/get-started/quickstart/create-a-repo)
2. [GitHub Docs - Fork a Repo](https://docs.github.com/en/get-started/

quickstart/fork-a-repo)
3. [GitHub Docs - About Pull Requests](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes/about-pull-requests)
