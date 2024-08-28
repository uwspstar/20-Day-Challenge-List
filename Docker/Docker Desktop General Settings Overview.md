### Docker Desktop General Settings Overview

| **Setting**                                                 | **Description**                                                                                                                                                                     | **Explanation**                                                                                                                                                   | **中文翻译**                                             |
|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|
| **Start Docker Desktop when you sign in to your computer**  | Automatically starts Docker Desktop when you log into your computer.                                                                                                                | Ensures Docker Desktop is ready for use immediately after you log in.                                                                                             | 登录计算机时自动启动 Docker Desktop。                           |
| **Open Docker Dashboard when Docker Desktop starts**        | Automatically opens the Docker Dashboard when Docker Desktop starts.                                                                                                                | Useful for users who want to immediately interact with the Docker GUI upon startup.                                                                               | Docker Desktop 启动时自动打开 Docker Dashboard。              |
| **Choose theme for Docker Desktop**                         | Select between Light, Dark, or System settings for the Docker Desktop theme.                                                                                                        | Allows customization of the Docker Desktop appearance to match user preferences or system settings.                                                               | 为 Docker Desktop 选择主题（浅色、深色或系统设置）。               |
| **Choose container terminal**                               | Select either the Integrated or System default terminal for opening container terminals.                                                                                            | Determines which terminal interface is used when accessing a container’s terminal.                                                                                 | 选择容器终端的集成终端或系统默认终端。                             |
| **Enable Docker terminal**                                  | Enables the Docker CLI for use in the terminal.                                                                                                                                      | Essential for interacting with Docker via command-line commands.                                                                                                  | 启用终端中的 Docker CLI。                                       |
| **Enable Docker Debug by default**                          | Turns on Docker Debug mode by default.                                                                                                                                               | Helps in troubleshooting by providing more detailed logs and diagnostic information.                                                                              | 默认启用 Docker Debug 模式。                                     |
| **Include VM in Time Machine backups**                      | Includes the Docker Desktop Linux VM in Time Machine backups (macOS).                                                                                                               | Ensures that the Docker VM is backed up along with other system files, which is useful for restoring Docker environments.                                          | 在 Time Machine 备份中包含 Docker Desktop Linux 虚拟机（macOS）。|
| **Use containerd for pulling and storing images**           | Uses containerd for image management, supporting multi-platform images, image lazy-loading, or Wasm.                                                                                 | Provides advanced image management capabilities, including support for WebAssembly (Wasm).                                                                        | 使用 containerd 拉取和存储镜像，支持多平台镜像、镜像延迟加载或 Wasm。  |
| **Use Virtualization framework**                            | Uses the Virtualization framework for Docker VM management on macOS 12.5 and above.                                                                                                 | Leverages macOS's native virtualization capabilities to manage Docker VMs more efficiently.                                                                       | 在 macOS 12.5 及以上版本中使用虚拟化框架管理 Docker VM。             |
| **[Choose file sharing implementation for your containers](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Docker/Docker%20Desktop_Choosing%20File%20Sharing%20Implementation.md)**  | Select from VirtioFS, gRPC FUSE, or osxfs (Legacy) for file sharing.                                                                                                                 | Choose the best file sharing method based on your needs (performance, compatibility, etc.).                                                                        | 为您的容器选择文件共享实现：VirtioFS、gRPC FUSE 或 osxfs（旧版）。       |
| **Use Rosetta for x86_64/amd64 emulation on Apple Silicon** | Enables Rosetta to accelerate binary emulation for x86_64/amd64 on Apple Silicon devices.                                                                                            | Required for running Intel-based Docker images on Apple Silicon with performance optimization.                                                                     | 在 Apple Silicon 上启用 Rosetta 以加速 x86_64/amd64 二进制仿真。     |
| **Send usage statistics**                                   | Sends error reports, system version, language, and Docker Desktop lifecycle information.                                                                                            | Helps Docker improve the product by sending anonymous usage data, though this can be turned off for privacy concerns.                                              | 发送错误报告、系统版本和语言以及 Docker Desktop 生命周期信息。            |
| **Use Enhanced Container Isolation**                        | Enhances security by preventing containers from breaching the Linux VM.                                                                                                             | Adds an extra layer of security, especially useful in sensitive or high-security environments.                                                                     | 通过防止容器突破 Linux VM 来增强安全性。                               |
| **Show CLI hints**                                          | Displays hints and tips when running Docker commands in the CLI.                                                                                                                    | Provides useful tips and tricks while using the Docker CLI, helping users learn new commands and best practices.                                                   | 运行 Docker 命令时显示提示和技巧。                                    |
| **SBOM indexing**                                           | Enables image SBOM indexing for Software Bill of Materials.                                                                                                                          | Helps in tracking and managing the components and dependencies of Docker images, improving transparency and security.                                               | 启用镜像的 SBOM（软件物料清单）索引。                               |
| **Enable background SBOM indexing**                         | Automatically starts SBOM indexing for newly built or pulled images.                                                                                                                | Ensures that all images are indexed for SBOM in the background, which can be useful for compliance and security audits.                                            | 自动启动新构建或拉取镜像的 SBOM 索引。                                |
| **Automatically check configuration**                       | Regularly checks your Docker Desktop configuration to ensure no unexpected changes have been made by other applications.                                                             | Prevents issues by ensuring that your Docker configuration remains consistent, helping avoid conflicts or misconfigurations caused by other software.              | 定期检查您的 Docker Desktop 配置，以确保其他应用程序未做出意外更改。        |

#### Summary

This table provides a detailed breakdown of the general settings available in Docker Desktop, helping users understand and configure their Docker environment effectively. Whether you prioritize performance, security, or ease of use, understanding these settings ensures you get the most out of Docker Desktop.

### 中文总结
这张表格详细列出了 Docker Desktop 中可用的常规设置，帮助用户有效地理解和配置他们的 Docker 环境。无论您优先考虑性能、安全性还是易用性，了解这些设置可以确保您充分利用 Docker Desktop。