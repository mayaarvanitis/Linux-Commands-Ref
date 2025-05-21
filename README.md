# 📁 Linux Command Reference & Cheatsheet

---

## 🧭 Navigation & Directory Management

```bash
pwd                    # Print current working directory
cd <dir>               # Change directory to <dir>
cd ~ / cd $HOME        # Go to home directory
cd -                   # Go to previous directory
ls                     # List files
ls -a                  # Include hidden (dot) files
ls -ltr                # Long format, sort by modification time (oldest first)
ls -d */               # List directories only
ls .                   # Show contents of current directory
```

---

## 📄 File & Directory Management

```bash
touch file             # Create file or update timestamp
mkdir folder           # Make a new directory
rmdir folder           # Delete empty directory
rm file                # Remove file
rm -r folder           # Recursively delete folder and contents
rm -rf folder          # Force remove without prompt
rm *txt                # Delete all .txt files (glob pattern)
rm *                   # Delete all in current folder
mv old new             # Rename or move file
cp old new             # Copy file
cp -b file copy        # Copy with backup: copy~ is backup
scp file user@host:/dir# Secure copy to/from remote
```

---

## 🔐 Permissions & Ownership

```bash
ls -l                    # List files with permissions
chmod a+w file           # Add write permission to all
chmod o+w file           # Add write permission to others
chmod +x file.sh         # Make executable
chmod -R +t folder/      # Sticky bit (only owner can delete)
sudo chown user file     # Change owner of file
chmod 777 file           # Read/write/execute for all
chmod 644 file           # Standard file perm (rw-r--r--)
```

---

## 📂 File Search & Pattern Matching

### `find`
```bash
find . -name "*.log"                         # Find .log files
find . -size +1M                             # Files over 1MB
find . -type d -empty -delete                # Delete empty directories
find . -type f -mmin -1                      # Files modified in last minute
find . -type f -name "*.sh" -exec chmod +x {} \;   # Make all .sh files executable
find . -type f -executable ! -name "*.sh" -exec chmod -x {} \;  # Remove exec except .sh
find . -perm 0777 -exec chmod 644 {} \;     # Fix over-permissive files
```

### `locate`
```bash
locate myfile.txt                           # Fast search for files
locate *pattern*                            # Wildcard pattern match
```

### `which`
```bash
which command                               # Path to the command binary
```

---

## 🔎 Text Search & Regex (grep)

```bash
grep -rli "error" .                         # Files with 'error', recursive, case-insensitive
grep -rLi "error" . | wc -l                # Files without 'error'
grep -ri "error" .                         # All error lines in all files
grep -oir "error" . | wc -l                # Count of all 'error' appearances
grep -riE "error|info"                     # Lines with either pattern
grep -ri "error" . | grep "05/15/2025"     # Filter by date
```

```bash
grep -ri "error" . | sort | uniq              # Unique error messages
grep -ri "error" . | sort | uniq -c           # Count repeated messages
grep -ri "error" . | sort | uniq -c | awk '$1 > 1'  # Repeats > 1
```

---

## 📊 Text Processing Tools

### `cat`, `head`, `tail`, `less`
```bash
cat file                      # Output file content
head -n 10 file               # First 10 lines
tail -n 10 file               # Last 10 lines
head -5 file | tail -1        # Just line 5
less file                     # Scroll through file
```

### `sed`
```bash
sed 's/ /,/g' file.csv > new.csv             # Replace spaces with commas
sed 's/.$//' file.txt                        # Delete last character per line
sed 's/Linux/Advanced Linux/' file           # First occurrence only
sed 's/\bC\b/C++/g' file                    # Replace standalone 'C'
sed '/^$/d' file.txt                         # Remove empty lines
```

### `awk`
```bash
awk '{print $1, $NF}' file                  # First and last column
awk -F, '{sum+=$2} END {print sum}'         # Sum of second column
awk 'NR==2,NR==4 {print NR, $0}'            # Lines 2 to 4 with number
awk '/pattern/ {print}'                     # Lines with pattern
awk '$0 ~ /Linux/'                          # Match pattern in full line
```

---

## 🧠 Processes & Signals

```bash
ps aux                        # All running processes
ps -efH                       # Full tree view
ps -eo pid,cmd,%mem --sort=%mem  # Sort by memory
pstree -p                     # Tree view with PIDs
kill <PID>                    # Send default signal (SIGTERM)
kill -9 <PID>                 # Force kill (SIGKILL)
kill -l                       # List all signals
```

```bash
echo $$                       # PID of current shell
sudo lsof -p $$               # Open files for current process
```

---

## 📈 Monitoring & System Info

```bash
top                          # Live system stats (CPU, MEM, etc)
free -h                      # Human-readable memory
uptime                       # System uptime
df -h                        # Disk usage
sudo du / -d1 2>/dev/null | sort -k1,1n # Large directories
du -h                        # Folder size usage
```

---

## 🖥️ Background Jobs & Screens

```bash
./script.sh &                # Run script in background
jobs                         # List background jobs
bg %1                        # Resume job 1 in background
kill %+                      # Kill most recent job
nohup sleep 6000 &           # Run detached from terminal
screen -list                 # List active screens
screen -r <ID>               # Reattach to screen
```

---

## 🛠️ Bash & Shell Scripting

```bash
#!/bin/bash                  # Shebang for shell script
echo $PATH                   # Show system path
alias g='grep -r'            # Example alias
```

---

## 📅 Cron & Automation

```bash
crontab -e                          # Edit crontab
crontab -r                          # Remove all cron jobs
0 6 * * 1-5 /path/script.sh         # Weekdays at 6AM
*/5 * * * * /path/script.sh         # Every 5 mins
```

Example:
```bash
#!/bin/bash
echo $(date) >> /home/user/log.txt
```
Add to crontab:
```cron
*/1 * * * * /bin/bash /home/user/script.sh
```

---

## 📝 VIM Editor

```vim
vi file              # Open file in vim
i                    # Insert mode
:wq                  # Save & quit
:q!                  # Quit without saving
:%s/the/THE/g        # Replace 'the' with 'THE'
:set mouse=a         # Enable mouse support
```

Other keys:
```
yy        # Yank (copy) line
p         # Paste
x         # Delete char
r<key>    # Replace character
u         # Undo
Ctrl+r    # Redo
```

---

## 🧩 Daemons & Services

```bash
systemctl list-units          # All systemd units (daemons)
pidof sshd                    # Get PID for sshd
pgrep sshd                    # Alternative to find PID
```

```bash
echo $$                       # PID of current bash shell
ps -ef | grep sshd            # Find sshd process
```

---

## 🧪 Regex & Shell Globbing

```bash
grep -qE '^[a-z]+$' file       # Match only lowercase
sed -r 's/[0-9]+=//g' file     # Remove digits ending in '='
```
