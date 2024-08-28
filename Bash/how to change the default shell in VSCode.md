# How to change the default shell in VSCod
In Visual Studio Code (VSCode), you can configure the default shell used in the integrated terminal. This is useful if you want to use a different shell, such as Bash, Zsh, or PowerShell, instead of the default one provided by your operating system.

Here’s how to change the default shell in VSCode:

### Changing the Default Shell in VSCode

#### 1. **Open VSCode Settings**

1. **Open Command Palette**: Press `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (Mac) to open the Command Palette.
2. **Open Settings**: Type and select `Preferences: Open Settings (JSON)` to directly edit the settings file.

#### 2. **Edit Settings**

In the settings file, you need to specify the path to the shell you want to use. Add or modify the following configuration:

```json
{
    "terminal.integrated.shell.linux": "/bin/bash",      // For Linux
    "terminal.integrated.shell.osx": "/bin/bash",        // For macOS
    "terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe" // For Windows
}
```

Replace the path with the correct path to your desired shell executable. Here’s a breakdown based on your operating system:

- **Linux**: Set `"terminal.integrated.shell.linux"` to the path of your desired shell. For Bash, it is usually `/bin/bash`.

- **macOS**: Set `"terminal.integrated.shell.osx"` to the path of your desired shell. For Bash, it is usually `/bin/bash`.

- **Windows**: Set `"terminal.integrated.shell.windows"` to the path of your desired shell executable. For Git Bash, it might be `"C:\\Program Files\\Git\\bin\\bash.exe"`.

#### 3. **Save and Close**

Save the changes to the `settings.json` file and close it. 

#### 4. **Restart VSCode**

Restart VSCode to ensure that the new terminal settings take effect.

### Additional Configuration

- **Setting Up Shell Arguments**: You can also provide arguments to the shell if needed. For example:

  ```json
  {
      "terminal.integrated.shellArgs.osx": ["--login"]  // macOS example
  }
  ```

- **Switching Terminal Profiles**: VSCode also supports terminal profiles which can be configured if you need more customization. This allows you to create different terminal profiles and select them as needed. For detailed configuration, refer to the [VSCode Terminal Profiles documentation](https://code.visualstudio.com/docs/terminal/profiles).

### Example Configurations

**For macOS and Linux:**

```json
{
    "terminal.integrated.shell.osx": "/bin/bash",
    "terminal.integrated.shell.linux": "/bin/bash"
}
```

**For Windows (with Git Bash):**

```json
{
    "terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe"
}
```

**For Windows (with Windows Subsystem for Linux):**

```json
{
    "terminal.integrated.shell.windows": "C:\\Windows\\System32\\wsl.exe"
}
```

### Summary

- **Open Settings**: Use the Command Palette to access `settings.json`.
- **Edit Settings**: Add or modify the relevant configuration for your operating system.
- **Restart VSCode**: To apply the changes.

By following these steps, you can configure VSCode to use your preferred default shell in the integrated terminal.
