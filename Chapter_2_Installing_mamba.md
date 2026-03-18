# 📦 Chapter 2: Installing Mamba

> **Mamba: The Fast Package Manager for Bioinformaticians**

---

## 🚀 Why Mamba?

| Feature | Mamba | Conda |
|---------|-------|-------|
| **Speed** | ⚡⚡⚡ Very Fast | ⚡ Slow |
| **Memory Usage** | 💾 Low | 💾💾 High |
| **Dependency Resolution** | ✅ Excellent | ⚠️ Often Slow |
| **Compatibility** | ✅ 100% Drop-in | - |

**TL;DR:** Mamba is **5-10x faster** than conda and uses less memory!

---

## 📥 Installation

### Step 1: Download Mambaforge
```bash
# Linux/Mac
wget https://github.com/conda-forge/miniforge/releases/download/25.3.1-0/Miniforge3-25.3.1-0-Linux-x86_64.sh 



### Step 2: Run Installer
```bash
chmod +x Miniforge3-25.3.1-0-Linux-x86_64.sh 
./Miniforge3-25.3.1-0-Linux-x86_64.sh 
```

During installation:
- Press Enter to review license
- Type `yes` to accept
- Press Enter for default location (or specify custom)
- Type `yes` to initialize mamba

### Step 3: Verify Installation
```bash
# Restart terminal or run:
source ~/.bashrc

# Check versions
mamba --version
conda --version
```

---

## 🎯 Quick Start

### Create Your First Environment
```bash
# Python 3.10 environment
mamba create -n myenv python=3.10

# Activate it
mamba activate myenv

# Deactivate when done
mamba deactivate
```

### Bioinformatics Tools Environment
```bash
# Create environment with popular bioinformatics tools
mamba create -n bioinf -c bioconda \
    fastqc trimgalore spades quast prokka kraken2

# Activate and use
mamba activate bioinf
```

---

## 📚 Common Commands

| Command | Purpose |
|---------|---------|
| `mamba create -n NAME` | Create new environment |
| `mamba activate NAME` | Activate environment |
| `mamba deactivate` | Exit current environment |
| `mamba install PACKAGE` | Install package |
| `mamba search PACKAGE` | Search for package |
| `mamba update PACKAGE` | Update package |
| `mamba remove PACKAGE` | Uninstall package |
| `mamba env list` | List all environments |
| `mamba env remove -n NAME` | Delete environment |
| `mamba list` | Show installed packages |

---

## 🔧 Advanced Usage

### Install from Specific Channel
```bash
# Bioconda channel (for bioinformatics)
mamba install -c bioconda fastqc

# Conda-forge channel
mamba install -c conda-forge numpy

# Multiple channels
mamba install -c conda-forge -c bioconda package_name
```

### Export & Share Environments
```bash
# Export your environment
mamba env export > environment.yml

# Share with others - they can recreate it:
mamba env create -f environment.yml -n restored_env
```

### Update All Packages
```bash
# Update everything in current environment
mamba update --all

# Update mamba itself
mamba update -n base mamba
```

---

## 💡 Best Practices

✅ **Do:**
- Create separate environments for each project
- Use `mamba env export` for reproducibility
- Specify package versions: `mamba install python=3.10`
- Use bioconda for bioinformatics tools

❌ **Don't:**
- Install everything in base environment
- Use generic `python` without version
- Mix environments carelessly

---

## 🛠️ Troubleshooting

### "mamba command not found"
```bash
# Initialize mamba
mamba init

# Reload shell
source ~/.bashrc
```

### "Solving environment" takes forever
```bash
# Use faster solver
mamba config --set experimental_solver libmamba

# Or upgrade mamba
mamba update -n base mamba
```

### Conflicts between packages
```bash
# Strict channel priority
mamba config --set channel_priority strict

# Try with version constraints
mamba install 'package>=1.0,<2.0'
```

---

## 📁 Environment Locations

```bash
# List where your environments are stored
mamba env list

# Typical location:
# ~/mambaforge/envs/

# View packages in an environment
mamba list -n myenv
```

---

## 🎓 Next Steps

1. ✅ Install Mamba
2. 📖 Read [Chapter 3: FastQC](Chapter_3_Fastqc.md)
3. 🔬 Create your first bioinformatics environment
4. 📊 Start analyzing data!

---

**Ready to manage packages like a pro? Let's continue! 🚀**
