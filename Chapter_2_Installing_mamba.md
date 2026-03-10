# Chapter 2: Installing Mamba
![Anaconda Logo](https://upload.wikimedia.org/wikipedia/en/c/cd/Anaconda_Logo.png)

Mamba is a faster, drop-in replacement for conda that dramatically speeds up package management.

## Why Mamba?

- **Speed**: 5-10x faster than conda
- **Compatibility**: 100% compatible with conda packages
- **Memory Efficient**: Uses less RAM
- **Better Dependency Resolution**: Solves complex issues

## Installation Steps

### Step 1: Download Mambaforge
```bash
wget https://github.com/conda-forge/mambaforge/releases/latest/download/Mambaforge-Linux-x86_64.sh
```

### Step 2: Install
```bash
chmod +x Mambaforge-Linux-x86_64.sh
./Mambaforge-Linux-x86_64.sh
```

### Step 3: Verify
```bash
mamba --version
conda --version
```

## Creating Environments

```bash
# Basic environment
mamba create -n myenv python=3.10
mamba activate myenv
mamba deactivate

# With bioinformatics tools
mamba create -n bioinf -c bioconda fastqc trimgalore spades quast
```

## Common Commands

| Command | Description |
|---------|-------------|
| `mamba create -n env` | Create environment |
| `mamba activate env` | Activate environment |
| `mamba install package` | Install package |
| `mamba env list` | List environments |
| `mamba env remove -n env` | Delete environment |

## Tips

```bash
# Export environment for sharing
mamba env export > environment.yml

# Create from file
mamba env create -f environment.yml

# Update mamba
mamba update -n base mamba
```

Now you're ready to manage Python environments efficiently!