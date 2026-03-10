# 📁 Linux Basics - Chapter 1A: File Manipulation

<style>
  @keyframes slideInLeft {
    from { opacity: 0; transform: translateX(-30px); }
    to { opacity: 1; transform: translateX(0); }
  }
  @keyframes slideInRight {
    from { opacity: 0; transform: translateX(30px); }
    to { opacity: 1; transform: translateX(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }
  
  h1 { animation: slideInLeft 0.8s ease-out; color: #0066cc; border-bottom: 3px solid #0066cc; padding-bottom: 10px; }
  h2 { animation: slideInLeft 0.8s ease-out; color: #0088ff; margin-top: 30px; }
  .section { animation: fadeIn 0.6s ease-in; margin: 20px 0; padding: 15px; background: #f0f8ff; border-left: 4px solid #0066cc; border-radius: 5px; }
  .command { background: #2d2d2d; color: #00ff00; padding: 12px; border-radius: 5px; font-family: 'Courier New', monospace; margin: 10px 0; animation: slideInRight 0.6s ease-out; overflow-x: auto; }
  .tip { background: #fffacd; border-left: 4px solid #ffd700; padding: 12px; margin: 10px 0; border-radius: 3px; }
  .exercise { background: #ffe4e1; border-left: 4px solid #ff6347; padding: 12px; margin: 10px 0; border-radius: 3px; }
</style>

## 🎯 Welcome to File Manipulation!

In this module, we'll master **file manipulation in the terminal**. 

> ⚠️ **Did you know?** 90%+ of a Bioinformatician's work is performed in the terminal! Master these skills and you'll become unstoppable! 🚀

---

## 📥 Step 1: Download Data Files

First, let's get data to work with using `wget`:

<div class="command">
wget https://github.com/Mollinak10/Linux-basics/raw/main/exercise_files.tar.gz
</div>

**Alternative:** If wget doesn't work, download manually from the GitHub repo GUI.

<div class="tip">
💡 **Tip:** You can paste commands directly into your terminal. Copy the command above and paste it!
</div>

---

## 📋 Step 2: Copy Files

Once downloaded, copy the file from your Downloads folder:

<div class="command">
cp /mnt/c/Users/YOUR_USERNAME/Downloads/exercise_files.tar.gz .
</div>

**Explanation:**
- `cp` = copy command
- `/mnt/c/Users/YOUR_USERNAME/Downloads/` = full path to Downloads (replace YOUR_USERNAME with your actual username)
- `exercise_files.tar.gz` = the file to copy
- `.` = current directory (destination)

<div class="tip">
💡 **Quick Tip:** Double-press TAB in terminal to auto-complete your username!
</div>

---

## 🗜️ Step 3: Extract/Decompress Files

`tar` is used to compress and decompress files. Let's extract our file:

<div class="command">
tar -xzvf exercise_files.tar.gz
</div>

**Parameters explained:**
- `-x` = extract/unpack
- `-z` = gzip (compressed)
- `-v` = verbose (show what's being extracted)
- `-f` = file name follows

---

## 📂 Step 4: Explore the Directory Structure

<div class="command">
cd data
ls -la
</div>

**You should see:**
- `BacteriaData/` directory
- `VirusData/` directory

List contents without entering the directory:

<div class="command">
ls BacteriaData/
ls VirusData/
</div>

---

## 🔍 Exercise 1: Discover Subdirectories

<div class="exercise">
<strong>📌 Challenge:</strong> What subdirectories are present inside BacteriaData and VirusData?<br><br>
<strong>Command to try:</strong>
<div class="command">
ls BacteriaData/*/
</div>
</div>

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

<div class="command">
cd BacteriaData/a_baumannii
ls
</div>

**You'll see:**
- `a_baumannii_nt.fa` ✅ (correct - bacteria assembly)
- `flu_nt.fa` ❌ (wrong - this is a virus!)

### Fix the misplaced file:

<div class="command">
mv flu_nt.fa ../../VirusData/influ-A/
</div>

**Breaking it down:**
- `mv` = move/cut command
- `flu_nt.fa` = source file to move
- `../../` = go up 2 directories
- `VirusData/influ-A/` = destination folder

---

## 📦 Exercise 2: Organize All Files

<div class="exercise">
<strong>📌 Challenge:</strong> Your task is to organize ALL misplaced files!<br><br>
Find files that don't belong in each directory and move them to the correct folder.
</div>

**Workflow:**
1. Explore each organism folder
2. Identify misplaced files
3. Use `mv` to move them to correct locations

---

## 🎁 Final Exercise: Sort by File Type

Create two new directories to organize by type:

<div class="command">
mkdir assemblies annotations
</div>

### Copy all assemblies (`_nt.fa` files):

<div class="command">
cp */*_nt.fa assemblies/
</div>

### Copy all annotations (`_aa.fa` files):

<div class="command">
cp */*_aa.fa annotations/
</div>

**Result:**
- `assemblies/` = all genome sequences
- `annotations/` = all protein sequences

---

## 📚 Key File Commands Summary

<div class="section">

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

</div>

---

## ⚡ Advanced Tips

<div class="tip">
🔹 **Wildcards:** `*` matches anything
- `cp data/*_nt.fa backup/` - Copy all files ending in _nt.fa

🔹 **Safe deletion:** Add `-i` flag to be asked before deleting
- `rm -i file.txt` - Asks for confirmation

🔹 **Move vs Copy:** `mv` cuts the file, `cp` keeps original
- Use `cp` when you want to keep backup
- Use `mv` to reorganize
</div>

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