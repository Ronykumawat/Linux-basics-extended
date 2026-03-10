# 🪟 Chapter 0: Installing Linux on Windows

> **Get Linux running on your Windows machine in 3 simple ways!**

---

## 📋 Quick Overview

| Method | Speed | Ease | Recommended |
|--------|-------|------|-------------|
| **WSL 2 (Windows Store)** | ⚡⚡⚡ Fast | ⭐⭐⭐ Easy | ✅ **Best** |
| **Online Platforms** | ⚡ Medium | ⭐⭐⭐ Easy | ✅ No installation |
| **PowerShell Command Line** | ⚡⚡ Fast | ⭐⭐ Medium | For experts |

---

## 🚀 Method 1: WSL 2 via Windows Store (RECOMMENDED)

### Why WSL 2?
- ✅ Fastest performance
- ✅ Native Windows integration
- ✅ Full Linux compatibility
- ✅ Easiest setup for beginners

### Installation Steps

#### Step 1: Enable WSL
```powershell
# Open PowerShell as Administrator (right-click → Run as administrator)
wsl --install
```

This automatically installs WSL 2 and Ubuntu. The system may restart.

#### Step 2: Set Up Ubuntu
After restart, Ubuntu will launch automatically:
```
Ubuntu initialization...
Enter new UNIX username: [your_username]
New password: [enter password]
Retype password: [confirm]
```

#### Step 3: Update System
```bash
sudo apt update
sudo apt upgrade
```

#### Step 4: Install Required Tools
```bash
sudo apt install git curl wget build-essential
```

✅ **Done!** You now have Linux running on Windows!

---

## 🌐 Method 2: Online Web Platforms (No Installation!)

### Option A: GitHub Codespaces
```
1. Go to github.com
2. Create or open any repository
3. Click Code → Codespaces → Create codespace
4. Choose Ubuntu environment
5. Start coding in your browser!
```

**Pros:** Free tier, no local installation, collaborative  
**Cons:** Internet dependent

### Option B: Replit
```
1. Go to replit.com
2. Click "+ Create" → New Repl
3. Select "Bash" or "Ubuntu" template
4. Start using Linux immediately!
```

**Pros:** Simple, no setup, fast  
**Cons:** Limited storage

### Option C: Gitpod
```
1. Visit gitpod.io
2. Connect GitHub account
3. Open any repo with Gitpod
4. Get full Linux environment in VS Code!
```

**Pros:** IDE integration, powerful, free tier  
**Cons:** Requires GitHub account

### Option D: OnWorks (Full Desktop)
```
https://www.onworks.net/
- Full Linux desktop in browser
- No installation needed
- Free tier available
```

---

## ⌨️ Method 3: PowerShell Command Line

### Step 1: Open PowerShell as Administrator
```powershell
Right-click Start Menu → Windows PowerShell (Admin)
```

### Step 2: Install WSL
```powershell
wsl --install
```

### Step 3: Install Specific Distribution
```powershell
wsl --install -d Ubuntu-22.04
```

**Available distributions:**
- Ubuntu (latest)
- Ubuntu-22.04 LTS
- Ubuntu-20.04 LTS
- Debian
- Fedora
- Kali Linux

### Step 4: Set WSL 2 as Default
```powershell
wsl --set-default-version 2
```

### Step 5: Launch and Setup
```powershell
wsl
# Follow Ubuntu setup (username, password)
```

---

## 🎯 Verify Installation

Once in Linux, run:
```bash
uname -a
# Should show Linux kernel information

whoami
# Should show your username

pwd
# Should show /home/username
```

---

## 💾 Important Paths

### Access Windows from Linux
```bash
cd /mnt/c/
# Browse Windows C: drive
cd /mnt/c/Users/YourUsername/Documents
```

### Access Linux from Windows
```
File Explorer → \\wsl$\
# Browse Linux files directly
```

---

## 🛠️ Common Issues & Solutions

### Issue: WSL command not found
**Solution:**
```powershell
# Check Windows version (must be 10 version 2004+)
winver
# If old, update Windows
```

### Issue: Ubuntu won't launch
**Solution:**
```powershell
wsl --set-default-version 2
wsl --install -d Ubuntu-22.04
```

### Issue: Slow performance
**Solution:**
```
Settings → WSL2 → Virtual Machine
Increase allocated memory/storage
```

### Issue: No internet connection in WSL
**Solution:**
```bash
sudo nano /etc/resolv.conf
# Add: nameserver 8.8.8.8
```

---

## 🎓 Next Steps

1. ✅ Install WSL 2 (or use online platform)
2. 📖 Read [Chapter 1: Linux Commands](Chapter_1_Linux_commands.md)
3. 🛠️ Practice basic commands
4. 📦 Install [Mamba](Chapter_2_Installing_mamba.md)
5. 🧬 Start with bioinformatics!

---

## 📚 Resources

- [WSL Official Documentation](https://docs.microsoft.com/en-us/windows/wsl/)
- [Ubuntu Official Site](https://ubuntu.com/)
- [Linux Beginners Guide](https://ubuntu.com/tutorials/command-line-for-beginners)

---

**Ready? Let's get started! 🚀**