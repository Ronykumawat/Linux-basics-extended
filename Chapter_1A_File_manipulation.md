# 📁 Linux Basics - Chapter 1A: File Manipulation

## 🎯 Welcome to File Manipulation!

In this module, we'll master **file manipulation in the terminal**. 

> ⚠️ **Did you know?** 90%+ of a Bioinformatician's work is performed in the terminal! Master these skills and you'll become unstoppable! 🚀

---

## 📥 Step 1: Download Data Files

First, let's get data to work with using `wget`:

```bash
wget https://github.com/Mollinak10/Linux-basics/raw/main/exercise_files.tar.gz
```

**Alternative:** If wget doesn't work, download manually from the GitHub repo GUI.

💡 **Tip:** You can paste commands directly into your terminal. Copy the command above and paste it!

---

## 📋 Step 2: Copy Files

Once downloaded, copy the file from your Downloads folder:

```bash
cp /mnt/c/Users/YOUR_USERNAME/Downloads/exercise_files.tar.gz .
```

**Explanation:**
- `cp` = copy command
- `/mnt/c/Users/YOUR_USERNAME/Downloads/` = full path to Downloads (replace YOUR_USERNAME with your actual username)
- `exercise_files.tar.gz` = the file to copy
- `.` = current directory (destination)

💡 **Quick Tip:** Double-press TAB in terminal to auto-complete your username!

---

## 🗜️ Step 3: Extract/Decompress Files

`tar` is used to compress and decompress files. Let's extract our file:

```bash
tar -xzvf exercise_files.tar.gz
```

**Parameters explained:**
- `-x` = extract/unpack
- `-z` = gzip (compressed)
- `-v` = verbose (show what's being extracted)
- `-f` = file (read from file)
- `-f` = file name follows

---

## 📂 Step 4: Explore the Directory Structure

```bash
cd data
ls -la
```

**You should see:**
- `BacteriaData/` directory
- `VirusData/` directory

List contents without entering the directory:

```bash
ls BacteriaData/
ls VirusData/
```

---

## 🔍 Exercise 1: Discover Subdirectories

### 📌 Challenge
What subdirectories are present inside BacteriaData and VirusData?

**Command to try:**
```bash
ls BacteriaData/*/
```

**Expected Output:**
Each folder contains organism-specific subdirectories with genome assemblies and annotations!

---

## ⚙️ Step 5: Understanding File Organization

Inside each organism folder, you'll find:
- Genome assemblies (`.fa` files)
- Protein annotations (`.faa` files)
- Other genomic data

**The Problem:** Files are mixed up and disorganized! 😱

**The Solution:** Use the `mv` command to organize them! 🎯

---

## 🔄 Step 6: Moving & Organizing Files

Navigate to an organism folder:

```bash
cd BacteriaData/a_baumannii
ls
```

**You'll see:**
- `a_baumannii_nt.fa` ✅ (correct - bacteria assembly)
- `flu_nt.fa` ❌ (wrong - this is a virus!)

### Fix the misplaced file:

```bash
mv flu_nt.fa ../../VirusData/influ-A/
```

**Breaking it down:**
- `mv` = move/cut command
- `flu_nt.fa` = source file to move
- `../../` = go up 2 directories
- `VirusData/influ-A/` = destination folder

---

## 📦 Exercise 2: Organize All Files

### 📌 Challenge
Your task is to organize ALL misplaced files!

Find files that don't belong in each directory and move them to the correct folder.

**Workflow:**
1. Explore each organism folder
2. Identify misplaced files
3. Use `mv` to move them to correct locations

---

## 🎁 Final Exercise: Sort by File Type

Create two new directories to organize by type:

```bash
mkdir assemblies annotations
```

### Copy all assemblies (`_nt.fa` files):

```bash
cp */*_nt.fa assemblies/
```

### Copy all annotations (`_aa.fa` files):

```bash
cp */*_aa.fa annotations/
```

**Result:**
- `assemblies/` = all genome sequences
- `annotations/` = all protein sequences

---

## 📚 Key File Commands Summary

| Command | What it does | Example |
|---------|------------|---------|
| `cp` | **Copy** files/dirs | `cp file.txt backup/` |
| `mv` | **Move/Rename** | `mv old.txt new.txt` |
| `rm` | **Delete** permanently | `rm file.txt` |
| `mkdir` | **Create** directory | `mkdir new_folder` |
| `ls` | **List** contents | `ls -la` |
| `cd` | **Change** directory | `cd folder_name` |
| `pwd` | **Print** working dir | `pwd` |
| `tar` | **Compress/Extract** | `tar -xzvf file.tar.gz` |

---

## ⚡ Advanced Tips

🔹 **Wildcards:** `*` matches anything
- `cp data/*_nt.fa backup/` - Copy all files ending in _nt.fa

🔹 **Safe deletion:** Add `-i` flag to be asked before deleting
- `rm -i file.txt` - Asks for confirmation

🔹 **Move vs Copy:** `mv` cuts the file, `cp` keeps original
- Use `cp` when you want to keep backup
- Use `mv` to reorganize

---

## ✅ Checklist - Did You Master This?

- ✓ Downloaded files using `wget`
- ✓ Extracted `.tar.gz` files
- ✓ Navigated directories with `cd` and `ls`
- ✓ Copied files with `cp`
- ✓ Moved files with `mv`
- ✓ Created directories with `mkdir`
- ✓ Organized genomic data by type

---

## 🎓 Congratulations! 🎉

You now have essential file manipulation skills for bioinformatics! These skills will be used in EVERY data analysis pipeline.

**Next Step:** Move to Chapter 2 to install Mamba and create environments!

---

**Happy learning! You're doing great! 💪🧬**