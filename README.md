# 📁 Linux Command Reference & Cheatsheet

This repository collects the **Linux commands** and **core concepts** learned during the training period, structured by category. Each command includes a **succinct explanation** and usage tips. It serves as a quick reference and foundational learning tool for production support. (chatGPT used for formatting :))

---

## 🧭 Navigation & Directory Management

```bash
pwd                # Print current working directory
cd <dir>           # Change directory to <dir>
cd ~               # Go to home directory
cd -               # Go to previous directory
ls                 # List files
ls -a              # Include hidden files
ls -ltr            # Long listing, sorted by time (oldest to newest)
ls -d              # Show directories only
ls .               # Show current directory contents
```

---

## 📄 File & Directory Management

```bash
touch file         # Create a new file or update timestamp
mkdir folder       # Make a new directory
rm file            # Remove a file
rm -r folder       # Remove directory and contents
rm -rf folder      # Force delete without prompt
rmdir folder       # Remove empty directory
mv old new         # Rename or move file
cp src dest        # Copy file
cp -b 5 6          # Copy with backup (creates 6~)
scp file user@host:# Secure copy between hosts
```

---

## 🔐 Permissions & Ownership

```bash
ls -l              # List with permissions
chmod a+w file     # Add write permission for all
chmod o+w file     # Add write permission for others
chmod +x script.sh # Make script executable
chmod +t folder/   # Sticky bit (only owner can delete)
sudo chown user file # Change file owner
```

---

## 📂 Searching & Filtering

### `find` Examples
```bash
find . -name "*.log"                     # Find all .log files
find . -size +1M                         # Files larger than 1MB
find . -type d -empty -delete            # Delete empty directories
find . -mmin -1                          # Files modified in last minute
```

### `grep` Examples
```bash
grep -rli "error" .                      # Recursively find files with 'error'
grep -oi "error" file | wc -l           # Count 'error' occurrences
grep -riE "error|info" .                # Find lines with 'error' or 'info'
```

---

## 📊 Text Processing

### `cat`, `head`, `tail`, `less`
```bash
cat file             # Display file contents
head -5 file         # First 5 lines
tail -3 file         # Last 3 lines
head -5 file | tail -1 # Only line 5
less file            # Scrollable output
```

### `sed` Examples
```bash
sed 's/old/new/g' file     # Replace all instances
sed '/^$/d' file           # Delete empty lines
sed 's/.$//'               # Remove last char of each line
```

### `awk` Examples
```bash
awk '{print $1, $NF}' file             # First & last column
awk -F',' '{sum+=$2} END{print sum}'   # Sum of column 2
awk 'NR==2,NR==4 {print NR, $0}'       # Lines 2-4 with line number
```

---

## 🖥️ Processes & System Info

```bash
ps aux                    # All processes
ps -efH                   # Tree structure
ps -eo pid,cmd,%mem --sort=%mem  # Sort by memory
pstree -p                 # Tree view with PIDs
echo $$                  # Current shell's PID
kill <PID>               # Send SIGTERM to process
kill -9 <PID>            # Force kill (SIGKILL)
kill -l                  # List all signal names
```

---

## 🧠 Memory & Disk Monitoring

```bash
df -h                    # Disk usage (human readable)
du -h                   # Disk usage per file
sudo du / -d1 2>/dev/null | sort -k1,1n # Largest directories
top                     # Live system stats
free -h                 # Memory usage
```

---

## 🕹️ Shell, Bash & Customization

```bash
alias g='grep'          # Create alias
echo $PATH              # Print system PATH
sudo mv script /usr/local/bin/  # Install script
```

---

## 🧮 Arithmetic & Scripting

```bash
bc <<< "4+4"            # Inline math
#!/bin/bash             # Start a shell script
jobs                    # List background jobs
bg 2                    # Resume job in background
kill %+                 # Kill most recent job
```

---

## 📅 Scheduling with Cron

```bash
crontab -e              # Edit crontab
crontab -r              # Remove crontab
*/1 * * * * /path/script.sh   # Every minute
0 6 * * 1-5 /path/job.sh      # Weekdays at 6 AM
```

---

## 🧠 VIM Essentials

```vim
vi file            # Open file in VIM
i                 # Insert mode
:wq               # Save and quit
:q!               # Quit without saving
:%s/the/THE/g     # Replace all "the" with "THE"
:set mouse=a      # Enable mouse
```

---

## 🧠 Daemons & Services

```bash
ps aux | grep sshd      # Find sshd
systemctl list-units    # List services
pidof sshd              # Get PID for sshd
pgrep sshd              # Alternate method
```

---

## 🛠️ Log File Tools

```bash
tail -f log.txt          # Follow logs in real-time
lsof -p $$               # Open files for current process
```

---

## 📜 Special Patterns & Regex

```bash
sed 's/[0-9]+=//g' file   # Remove numbers ending with =
grep -qE '^[a-z]+$'       # Match only lowercase words
```

---

## 📎 Helpful Tips

- `>` = redirect stdout (overwrite)
- `>>` = append to file
- `2>` = redirect stderr
- `2>&1` = redirect stderr to stdout

---



