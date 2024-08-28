# How to change the default shell in VSCod
In Visual Studio Code (VSCode), you can configure the default shell used in the integrated terminal. This is useful if you want to use a different shell, such as Bash, Zsh, or PowerShell, instead of the default one provided by your operating system.

To set Bash as the default shell in Visual Studio Code (VS Code) instead of Zsh, follow these steps:

### 1. **Open VS Code Settings:**
   - In VS Code, press `Ctrl + ,` (or `Cmd + ,` on macOS) to open the settings.
   - Alternatively, you can click on the gear icon in the lower left corner and select "Settings."

### 2. **Search for Terminal Settings:**
   - In the settings search bar, type `terminal.integrated.defaultProfile`.

### 3. **Set Bash as the Default Shell:**
   - If you're on Windows:
     - Find the setting `terminal.integrated.defaultProfile.windows`.
     - From the dropdown menu, select "Git Bash" or the appropriate Bash option.
   - If you're on macOS or Linux:
     - Find the setting `terminal.integrated.defaultProfile.osx` (for macOS) or `terminal.integrated.defaultProfile.linux` (for Linux).
     - From the dropdown menu, select "bash."

### 4. **Restart VS Code:**
   - After making the change, close and reopen VS Code to ensure the settings take effect.

### 5. **Open a New Terminal:**
   - Now, when you open a new terminal in VS Code (`Ctrl + ` or `Cmd + `), it should start with Bash as the default shell instead of Zsh.

### 中文说明：

### 1. **打开 VS Code 设置：**
   - 在 VS Code 中，按 `Ctrl + ,`（或 macOS 上按 `Cmd + ,`）打开设置。
   - 或者，您可以点击左下角的齿轮图标并选择“Settings”（设置）。

### 2. **搜索终端设置：**
   - 在设置搜索栏中，输入 `terminal.integrated.defaultProfile`。

### 3. **设置 Bash 为默认 Shell：**
   - 如果您使用的是 Windows：
     - 找到设置 `terminal.integrated.defaultProfile.windows`。
     - 从下拉菜单中选择“Git Bash”或相应的 Bash 选项。
   - 如果您使用的是 macOS 或 Linux：
     - 找到设置 `terminal.integrated.defaultProfile.osx`（针对 macOS）或 `terminal.integrated.defaultProfile.linux`（针对 Linux）。
     - 从下拉菜单中选择“bash”。

### 4. **重启 VS Code：**
   - 更改后，关闭并重新打开 VS Code 以确保设置生效。

### 5. **打开新终端：**
   - 现在，当您在 VS Code 中打开一个新终端（`Ctrl + ` 或 `Cmd + `）时，它应该以 Bash 作为默认 Shell，而不是 Zsh。

This process should help you set Bash as your default terminal shell in VS Code.
