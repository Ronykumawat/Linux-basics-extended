# Chapter 0: Installing Linux on Windows
![Ubuntu Logo](https://assets.ubuntu.com/v1/29985a98-ubuntu-logo32.png)

This chapter covers different ways to install and run Linux on a Windows system.

## Method 1: Via Windows Store (WSL - Windows Subsystem for Linux)

Windows Subsystem for Linux allows you to run Linux distributions directly on Windows.

### Steps:

1. **Enable WSL:**
   - Open PowerShell or Command Prompt as Administrator.
   - Run: `wsl --install`
   - This installs WSL and the default Ubuntu distribution.

2. **Install Specific Distribution:**
   - Open Microsoft Store.
   - Search for your preferred Linux distribution (e.g., Ubuntu, Debian, Fedora).
   - Click "Get" or "Install".

3. **Launch Linux:**
   - Search for the installed app in Start menu.
   - Launch it.
   - Set up username and password when prompted.

4. **Update and Use:**
   - Run `sudo apt update && sudo apt upgrade` to update packages.
   - You're now running Linux on Windows!

## Method 2: Online Web Server

Use online platforms that provide Linux environments in your browser.

### Options:

1. **GitHub Codespaces:**
   - Create a repository on GitHub.
   - Click "Code" > "Codespaces" > "Create codespace".
   - Choose Ubuntu or other Linux environments.

2. **Replit:**
   - Go to replit.com
   - Create a new repl with "Bash" or "Ubuntu" template.
   - Run Linux commands in the web terminal.

3. **Gitpod:**
   - Go to gitpod.io
   - Connect your GitHub repo or start with a template.
   - Get a Linux workspace in the browser.

4. **Online IDEs like VS Code Web:**
   - Some provide Linux terminals.const (
	PackageVar = types.PackageVar
	LocalVar   = types.LocalVar
	RecvVar    = types.RecvVar
	ParamVar   = types.ParamVar
	ResultVar  = types.ResultVar
	FieldVar   = types.FieldVar
)

These are great for learning without installing anything locally.

## Method 3: Through Terminal (WSL Command Line)

Install WSL entirely through command line.

### Steps:

1. **Open PowerShell as Admin:**
   - Right-click Start > Windows PowerShell (Admin)

2. **Install WSL:**
   ```
   wsl --install
   ```

3. **Install Specific Distro:**
   ```
   wsl --install -d Ubuntu-22.04
   ```
   Available distros: Ubuntu, Debian, SUSE, etc.

4. **Set Default Version (if needed):**
   ```
   wsl --set-default-version 2
   ```

5. **Launch:**
   ```
   wsl
   ```

6. **List Installed Distros:**
   ```
   wsl -l -v
   ```

7. **Shutdown WSL:**
   ```
   wsl --shutdown
   ```

## Additional Tips

- **WSL Versions:** WSL 2 is recommended for better performance.
- **File Access:** Access Windows files from Linux at `/mnt/c/`
- **Access Linux files from Windows:** Use `\\wsl$\` in File Explorer.
- **Uninstall:** `wsl --unregister <DistroName>`

Now you're ready to learn Linux basics!