# Linux Basics: Essential Commands

Hi everyone! 👋  
Welcome to the comprehensive guide on Linux basic commands. This chapter covers all essential commands with detailed explanations, examples, and tips. Anyone can copy these commands and use them in their Linux environment.

## Getting Started with Linux

I’ll be using **Ubuntu 22.04 LTS** on a Windows desktop via WSL. The commands work on most Linux distributions.

### Terminal Structure
After logging in, you'll see a prompt like:
```
username@hostname:~$
```
- `username`: Your login name
- `hostname`: Computer name
- `~`: Home directory
- `$`: Regular user prompt (# for root)

**Important Notes:**
- Linux is case-sensitive (A ≠ a)
- Use Tab for auto-completion
- Use ↑/↓ arrows for command history

## 1. Navigation Commands

### pwd (Print Working Directory)
Shows your current location in the file system.
```
pwd
# Output: /home/username
```

### ls (List)
Lists files and directories in current location.
```
ls                    # Basic list
ls -l                 # Long format with details
ls -a                 # Show hidden files (start with .)
ls -h                 # Human-readable sizes
ls -la                # Combine options
```

### cd (Change Directory)
Changes your current directory.
```
cd /path/to/directory    # Absolute path
cd relative/path         # Relative path
cd ..                    # Go up one level
cd ~                     # Go to home directory
cd -                     # Go to previous directory
```

### mkdir (Make Directory)
Creates new directories.
```
mkdir newfolder              # Create single directory
mkdir -p path/to/nested/dir  # Create nested directories
```

## 2. File Operations

### touch
Creates empty files or updates timestamps.
```
touch filename.txt           # Create empty file
touch file1.txt file2.txt    # Create multiple files
```

### cp (Copy)
Copies files and directories.
```
cp source.txt destination.txt                    # Copy file
cp -r source_dir destination_dir                 # Copy directory recursively
cp -i source.txt destination.txt                 # Interactive (ask before overwrite)
cp -v source.txt destination.txt                 # Verbose output
```

### mv (Move/Rename)
Moves or renames files and directories.
```
mv oldname.txt newname.txt      # Rename file
mv file.txt /path/to/directory/ # Move file
mv -i source destination        # Interactive mode
```

### rm (Remove)
Deletes files and directories.
```
rm filename.txt                # Delete file
rm -r directory/               # Delete directory recursively
rm -i filename.txt             # Interactive deletion
rm -f filename.txt             # Force deletion (no prompts)
```

### rmdir (Remove Directory)
Removes empty directories.
```
rmdir emptydir/                # Remove empty directory
rmdir -p path/to/empty/dir     # Remove nested empty directories
```

## 3. File Permissions

### chmod (Change Mode)
Changes file permissions.
```
chmod 755 filename             # rwxr-xr-x
chmod u+x filename             # Add execute for user
chmod g-w filename             # Remove write for group
chmod o=r filename             # Read only for others
chmod -R 755 directory/        # Recursive
```

### chown (Change Owner)
Changes file ownership.
```
chown username filename        # Change owner
chown username:group filename  # Change owner and group
chown -R user:group directory/ # Recursive
```

## 4. Text Processing

### cat (Concatenate)
Displays file contents.
```
cat filename.txt               # Display file
cat file1.txt file2.txt        # Concatenate multiple files
cat -n filename.txt            # Show line numbers
```

### more/less
Views large files page by page.
```
more filename.txt              # Page through file
less filename.txt              # Better pager with search
# In less: /search, n(next), q(quit)
```

### head
Shows first lines of a file.
```
head filename.txt              # First 10 lines
head -n 20 filename.txt        # First 20 lines
```

### tail
Shows last lines of a file.
```
tail filename.txt              # Last 10 lines
tail -n 20 filename.txt        # Last 20 lines
tail -f logfile.txt            # Follow file (real-time)
```

### grep (Global Regular Expression Print)
Searches for patterns in files.
```
grep "pattern" filename.txt    # Search for pattern
grep -i "pattern" file.txt     # Case-insensitive
grep -r "pattern" directory/   # Recursive search
grep -n "pattern" file.txt     # Show line numbers
```

### wc (Word Count)
Counts lines, words, characters.
```
wc filename.txt                # Lines, words, characters
wc -l filename.txt             # Only lines
wc -w filename.txt             # Only words
wc -c filename.txt             # Only characters
```

### sort
Sorts lines in a file.
```
sort filename.txt              # Sort alphabetically
sort -n numbers.txt            # Numeric sort
sort -r filename.txt           # Reverse sort
sort -u filename.txt           # Unique (remove duplicates)
```

### uniq
Removes duplicate lines.
```
uniq filename.txt              # Remove consecutive duplicates
uniq -c filename.txt           # Count occurrences
uniq -d filename.txt           # Show only duplicates
```

## 5. System Information

### whoami
Shows current username.
```
whoami
# Output: username
```

### uname
Shows system information.
```
uname                        # Kernel name
uname -a                     # All information
uname -r                     # Kernel release
```

### date
Shows or sets system date/time.
```
date                         # Current date and time
date +"%Y-%m-%d"             # Formatted date
```

### df (Disk Free)
Shows disk space usage.
```
df                           # All filesystems
df -h                        # Human-readable
df -T                        # Include filesystem type
```

### du (Disk Usage)
Shows directory/file sizes.
```
du                           # Directory sizes
du -h                        # Human-readable
du -s directory/             # Summary for directory
```

### free
Shows memory usage.
```
free                         # Memory info
free -h                      # Human-readable
free -m                      # In megabytes
```

### top/htop
Shows running processes.
```
top                          # Process monitor
# Press q to quit, k to kill process
```

### ps (Process Status)
Shows current processes.
```
ps                           # Current shell processes
ps aux                       # All processes
ps -ef                       # Full format
```

## 6. Networking

### ping
Tests network connectivity.
```
ping google.com              # Ping host
ping -c 4 google.com         # Ping 4 times
```

### ifconfig/ip
Shows network interface information.
```
ifconfig                     # Network interfaces (older)
ip addr show                 # Show IP addresses (newer)
ip route show                # Show routing table
```

### wget
Downloads files from the web.
```
wget https://example.com/file.txt
wget -O newname.txt https://example.com/file.txt  # Save as different name
```

### curl
Transfers data from servers.
```
curl https://example.com     # Download webpage
curl -O https://example.com/file.txt  # Save file
curl -I https://example.com  # Show headers only
```

### ssh (Secure Shell)
Connects to remote machines.
```
ssh username@hostname        # Connect to host
ssh -p 2222 user@host        # Specify port
```

## 7. Package Management (Ubuntu/Debian)

### apt
Package manager for Debian-based systems.
```
sudo apt update              # Update package list
sudo apt upgrade             # Upgrade packages
sudo apt install package     # Install package
sudo apt remove package      # Remove package
sudo apt search keyword      # Search packages
sudo apt show package        # Show package info
```

## 8. Other Useful Commands

### history
Shows command history.
```
history                      # Show all commands
history 10                   # Show last 10 commands
!123                         # Execute command number 123
!!                           # Execute last command
```

### alias
Creates command shortcuts.
```
alias ll='ls -la'            # Create alias
alias                        # Show all aliases
unalias ll                   # Remove alias
```

### export
Sets environment variables.
```
export PATH=$PATH:/new/path  # Add to PATH
export EDITOR=nano           # Set default editor
echo $PATH                   # Show variable
```

### man (Manual)
Shows command documentation.
```
man ls                       # Manual for ls command
man -k keyword               # Search manuals
```

### which
Shows location of commands.
```
which ls                     # Path to ls command
```

### find
Searches for files.
```
find . -name "*.txt"         # Find .txt files in current dir
find /home -type f -size +1M # Find files >1MB in /home
```

### tar
Archives files.
```
tar -cvf archive.tar files/   # Create archive
tar -xvf archive.tar         # Extract archive
tar -czvf archive.tar.gz files/  # Create compressed
tar -xzvf archive.tar.gz     # Extract compressed
```

### zip/unzip
Works with ZIP files.
```
zip archive.zip file1 file2  # Create ZIP
unzip archive.zip            # Extract ZIP
```

## Tips for Using Commands

1. **Combine Commands**: Use pipes (|)
   ```
   ls | grep txt              # List files containing "txt"
   ps aux | grep firefox      # Find Firefox process
   ```

2. **Redirect Output**:
   ```
   command > file.txt         # Redirect stdout to file
   command >> file.txt        # Append to file
   command 2> error.log       # Redirect stderr
   command > output.txt 2>&1  # Redirect both
   ```

3. **Background Jobs**:
   ```
   command &                   # Run in background
   jobs                        # Show background jobs
   fg %1                       # Bring job 1 to foreground
   bg %1                       # Resume job 1 in background
   ```

4. **Command Substitution**:
   ```
   echo "Today is $(date)"     # Insert command output
   ```

5. **Wildcards**:
   ```
   ls *.txt                    # All .txt files
   ls file[1-3].txt            # file1.txt, file2.txt, file3.txt
   ```

Remember to practice these commands in a safe environment. Use `man command` for detailed help on any command. Happy learning! 😄 👋