# Linux Commands Cheat Sheet

Essential Linux/Unix commands for system administration, file management, and everyday terminal tasks. Examples work on most Linux distributions and macOS.

## Table of Contents

- [Basics](#basics)
- [File and Directory Operations](#file-and-directory-operations)
- [File Viewing and Editing](#file-viewing-and-editing)
- [File Permissions](#file-permissions)
- [Searching and Finding](#searching-and-finding)
- [Text Processing](#text-processing)
- [Process Management](#process-management)
- [System Information](#system-information)
- [Disk Usage](#disk-usage)
- [Networking](#networking)
- [Package Management](#package-management)
- [Archiving and Compression](#archiving-and-compression)
- [User Management](#user-management)
- [SSH and Remote Access](#ssh-and-remote-access)
- [System Services](#system-services)
- [Environment Variables](#environment-variables)
- [Redirection and Pipes](#redirection-and-pipes)
- [Job Control](#job-control)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Tools & References](#tools--references)

## Basics

```bash
# Get help
man <command>              # manual page
<command> --help           # help flag
info <command>             # info page

# Navigate
pwd                        # print working directory
cd /path/to/directory      # change directory
cd ~                       # home directory
cd -                       # previous directory
cd ..                      # parent directory

# List files
ls                         # list files
ls -l                      # long format
ls -la                     # include hidden files
ls -lh                     # human-readable sizes
ls -lt                     # sort by modification time
ls -lR                     # recursive listing

# Clear screen
clear                      # or Ctrl+L
```

## File and Directory Operations

```bash
# Create
touch file.txt             # create empty file or update timestamp
mkdir directory            # create directory
mkdir -p path/to/dir       # create nested directories

# Copy
cp source.txt dest.txt     # copy file
cp -r source/ dest/        # copy directory recursively
cp -i source dest          # interactive (prompt before overwrite)
cp -v source dest          # verbose

# Move/Rename
mv old.txt new.txt         # rename file
mv file.txt /path/to/      # move file
mv -i source dest          # interactive

# Delete
rm file.txt                # remove file
rm -r directory/           # remove directory recursively
rm -rf directory/          # force remove (be careful!)
rm -i file.txt             # interactive (prompt before delete)
rmdir empty_dir/           # remove empty directory

# Links
ln -s target link_name     # create symbolic link
ln target link_name        # create hard link

# Find file type
file filename              # determine file type
```

## File Viewing and Editing

```bash
# View files
cat file.txt               # display entire file
cat file1 file2            # concatenate files
less file.txt              # paginated view (q to quit)
more file.txt              # simple pager
head file.txt              # first 10 lines
head -n 20 file.txt        # first 20 lines
tail file.txt              # last 10 lines
tail -n 20 file.txt        # last 20 lines
tail -f file.txt           # follow file (watch for changes)

# Text editors
nano file.txt              # simple editor
vim file.txt               # vi improved
vi file.txt                # classic vi editor

# Count
wc file.txt                # word count (lines, words, bytes)
wc -l file.txt             # count lines
wc -w file.txt             # count words
```

## File Permissions

```bash
# Permission format: rwxrwxrwx (owner, group, others)
# r=read(4), w=write(2), x=execute(1)

# View permissions
ls -l file.txt             # see permissions

# Change permissions
chmod 755 file.txt         # rwxr-xr-x
chmod 644 file.txt         # rw-r--r--
chmod +x script.sh         # add execute permission
chmod -w file.txt          # remove write permission
chmod u+x file.txt         # add execute for user
chmod g-w file.txt         # remove write for group
chmod o+r file.txt         # add read for others
chmod -R 755 directory/    # recursive

# Change ownership
chown user file.txt        # change owner
chown user:group file.txt  # change owner and group
chown -R user:group dir/   # recursive

# Change group
chgrp group file.txt       # change group
```

## Searching and Finding

```bash
# Find files
find . -name "*.txt"       # find by name
find . -iname "*.TXT"      # case-insensitive
find . -type f             # find files
find . -type d             # find directories
find . -size +10M          # files larger than 10MB
find . -mtime -7           # modified in last 7 days
find . -name "*.log" -delete  # find and delete
find . -name "*.sh" -exec chmod +x {} \;  # find and execute

# Locate (faster, uses database)
locate filename            # find file by name
sudo updatedb              # update locate database

# Which
which python               # show path to command
whereis python             # locate binary, source, manual

# Search in files
grep "pattern" file.txt    # search for pattern
grep -r "pattern" .        # recursive search
grep -i "pattern" file     # case-insensitive
grep -v "pattern" file     # invert match (exclude)
grep -n "pattern" file     # show line numbers
grep -l "pattern" *.txt    # show only filenames
grep -c "pattern" file     # count matches
grep -A 3 "pattern" file   # show 3 lines after match
grep -B 3 "pattern" file   # show 3 lines before match
grep -C 3 "pattern" file   # show 3 lines around match
```

## Text Processing

```bash
# Sort
sort file.txt              # sort lines alphabetically
sort -r file.txt           # reverse sort
sort -n file.txt           # numeric sort
sort -u file.txt           # sort and remove duplicates

# Unique
uniq file.txt              # remove adjacent duplicates (use with sort)
sort file.txt | uniq       # remove all duplicates
uniq -c file.txt           # count occurrences

# Cut
cut -d',' -f1 file.csv     # extract first column (comma delimiter)
cut -c1-10 file.txt        # extract characters 1-10

# Awk
awk '{print $1}' file.txt  # print first column
awk -F',' '{print $2}' file.csv  # CSV with comma delimiter
awk '/pattern/ {print $0}' file.txt  # print matching lines

# Sed
sed 's/old/new/' file.txt  # replace first occurrence per line
sed 's/old/new/g' file.txt # replace all occurrences
sed -i 's/old/new/g' file.txt  # in-place edit
sed '1,10d' file.txt       # delete lines 1-10
sed -n '5,10p' file.txt    # print lines 5-10

# Diff
diff file1.txt file2.txt   # compare files
diff -u file1 file2        # unified format
diff -r dir1/ dir2/        # compare directories

# Tr (translate)
tr 'a-z' 'A-Z' < file.txt  # convert to uppercase
tr -d '[:digit:]' < file   # delete digits
```

## Process Management

```bash
# View processes
ps                         # current processes
ps aux                     # all processes (detailed)
ps aux | grep python       # find specific process
top                        # interactive process viewer
htop                       # better process viewer (if installed)

# Process info
pgrep process_name         # find process ID by name
pidof process_name         # get PID

# Kill processes
kill PID                   # terminate process (SIGTERM)
kill -9 PID                # force kill (SIGKILL)
killall process_name       # kill all by name
pkill process_name         # kill by pattern

# Background/Foreground
command &                  # run in background
jobs                       # list background jobs
fg %1                      # bring job 1 to foreground
bg %1                      # resume job 1 in background
Ctrl+Z                     # suspend current process
Ctrl+C                     # interrupt current process

# Nice (priority)
nice -n 10 command         # run with lower priority
renice -n 5 -p PID         # change priority of running process
```

## System Information

```bash
# System
uname -a                   # system information
uname -r                   # kernel version
hostname                   # system hostname
uptime                     # uptime and load average
date                       # current date and time
cal                        # calendar
whoami                     # current username
id                         # user and group IDs

# Hardware
lscpu                      # CPU information
lsblk                      # block devices (disks)
lsusb                      # USB devices
lspci                      # PCI devices
free -h                    # memory usage (human-readable)
cat /proc/cpuinfo          # detailed CPU info
cat /proc/meminfo          # detailed memory info

# Distribution info
cat /etc/os-release        # OS information
lsb_release -a             # distribution info (if available)
```

## Disk Usage

```bash
# Disk space
df -h                      # disk space (human-readable)
df -i                      # inode usage
du -h directory/           # directory size
du -sh directory/          # summary size
du -h --max-depth=1        # size of subdirectories

# Sort by size
du -h | sort -h            # sort human-readable sizes
du -sh * | sort -h         # size of items in current dir

# Find large files
find . -type f -size +100M -exec ls -lh {} \;
du -a | sort -n -r | head -n 10  # top 10 largest
```

## Networking

```bash
# Network interfaces
ip addr                    # show IP addresses
ip link                    # show network interfaces
ifconfig                   # older command (still common)

# Connectivity
ping google.com            # test connectivity
ping -c 4 google.com       # send 4 packets
traceroute google.com      # trace route to host
mtr google.com             # combined ping/traceroute

# DNS
nslookup google.com        # DNS lookup
dig google.com             # detailed DNS query
host google.com            # simple DNS lookup

# Network connections
netstat -tuln              # listening ports
netstat -tuln | grep :80   # check specific port
ss -tuln                   # modern alternative to netstat
lsof -i :8080              # what's using port 8080

# Download
wget https://example.com/file.zip   # download file
wget -c url                # continue interrupted download
curl https://api.example.com        # make HTTP request
curl -O https://example.com/file    # save to file

# Firewall (ufw)
sudo ufw status            # firewall status
sudo ufw enable            # enable firewall
sudo ufw allow 22          # allow port 22
sudo ufw deny 80           # deny port 80

# Test ports
telnet host port           # test TCP connection
nc -zv host port           # test port (netcat)
```

## Package Management

```bash
# Debian/Ubuntu (apt)
sudo apt update            # update package list
sudo apt upgrade           # upgrade packages
sudo apt install package   # install package
sudo apt remove package    # remove package
sudo apt autoremove        # remove unused packages
sudo apt search keyword    # search for package
apt list --installed       # list installed packages

# Red Hat/CentOS/Fedora (yum/dnf)
sudo yum update            # update packages
sudo yum install package   # install package
sudo yum remove package    # remove package
sudo yum search keyword    # search for package

# Or newer dnf
sudo dnf update
sudo dnf install package

# Arch Linux (pacman)
sudo pacman -Syu           # update system
sudo pacman -S package     # install package
sudo pacman -R package     # remove package
sudo pacman -Ss keyword    # search for package

# Snap (universal)
snap find package          # search
sudo snap install package  # install
sudo snap list             # list installed
```

## Archiving and Compression

```bash
# Tar (archive)
tar -czf archive.tar.gz directory/   # create gzip archive
tar -cjf archive.tar.bz2 directory/  # create bzip2 archive
tar -xzf archive.tar.gz              # extract gzip archive
tar -xjf archive.tar.bz2             # extract bzip2 archive
tar -xzf archive.tar.gz -C /path/    # extract to specific directory
tar -tzf archive.tar.gz              # list contents
tar -xzf archive.tar.gz file.txt     # extract single file

# Zip
zip -r archive.zip directory/   # create zip
unzip archive.zip               # extract zip
unzip -l archive.zip            # list contents
unzip archive.zip -d /path/     # extract to specific directory

# Gzip (compress single files)
gzip file.txt              # compress (creates file.txt.gz)
gunzip file.txt.gz         # decompress
gzip -k file.txt           # keep original file

# Bzip2
bzip2 file.txt             # compress
bunzip2 file.txt.bz2       # decompress
```

## User Management

```bash
# User info
whoami                     # current user
id                         # user and group info
w                          # who is logged in
last                       # login history

# Add/modify users (requires sudo)
sudo useradd username      # add user
sudo useradd -m username   # add user with home directory
sudo passwd username       # set/change password
sudo usermod -aG group username  # add user to group
sudo userdel username      # delete user
sudo userdel -r username   # delete user and home directory

# Groups
groups                     # show current user's groups
groups username            # show user's groups
sudo groupadd groupname    # create group
sudo groupdel groupname    # delete group

# Switch user
su username                # switch user
su -                       # switch to root with environment
sudo -i                    # interactive root shell
sudo command               # run command as root
```

## SSH and Remote Access

```bash
# SSH
ssh user@host              # connect to remote host
ssh -p 2222 user@host      # custom port
ssh -i keyfile user@host   # use specific key

# SSH key generation
ssh-keygen                 # generate SSH key pair
ssh-keygen -t ed25519      # use ed25519 algorithm
ssh-copy-id user@host      # copy public key to remote

# SCP (secure copy)
scp file.txt user@host:/path/        # copy to remote
scp user@host:/path/file.txt .       # copy from remote
scp -r directory/ user@host:/path/   # copy directory

# Rsync (better for large transfers)
rsync -avz source/ user@host:/dest/  # sync directories
rsync -avz --progress source/ dest/  # show progress
rsync -avz --delete source/ dest/    # delete files not in source

# SSH config (~/.ssh/config)
# Host myserver
#     HostName example.com
#     User username
#     Port 22
#     IdentityFile ~/.ssh/id_ed25519

# Then connect with: ssh myserver
```

## System Services

```bash
# Systemd (modern Linux)
sudo systemctl start service       # start service
sudo systemctl stop service        # stop service
sudo systemctl restart service     # restart service
sudo systemctl status service      # check status
sudo systemctl enable service      # enable at boot
sudo systemctl disable service     # disable at boot
systemctl list-units --type=service  # list services

# View logs
sudo journalctl -u service         # service logs
sudo journalctl -f                 # follow logs
sudo journalctl -b                 # logs since last boot
sudo journalctl --since "1 hour ago"

# Init.d (older systems)
sudo /etc/init.d/service start
sudo service service_name start
```

## Environment Variables

```bash
# View variables
env                        # all environment variables
echo $PATH                 # specific variable
echo $HOME
echo $USER

# Set variables
export VAR=value           # set for current session
VAR=value command          # set for single command

# Permanent variables
# Add to ~/.bashrc or ~/.bash_profile
export PATH="$PATH:/new/path"

# Reload config
source ~/.bashrc           # or
. ~/.bashrc
```

## Redirection and Pipes

```bash
# Output redirection
command > file.txt         # redirect stdout to file (overwrite)
command >> file.txt        # redirect stdout to file (append)
command 2> error.log       # redirect stderr
command &> all.log         # redirect both stdout and stderr
command > /dev/null 2>&1   # discard all output

# Input redirection
command < input.txt        # read from file

# Pipes
command1 | command2        # pipe output to next command
ls -l | grep ".txt"        # chain commands
cat file | sort | uniq     # multiple pipes

# Tee (write to file and stdout)
command | tee file.txt     # write to file and display
command | tee -a file.txt  # append to file and display

# Here documents
cat << EOF > file.txt
Line 1
Line 2
EOF
```

## Job Control

```bash
# Background jobs
command &                  # run in background
nohup command &            # run immune to hangup signal
nohup command > output.log 2>&1 &  # background with logging

# Screen (terminal multiplexer)
screen                     # start new session
screen -S name             # start named session
Ctrl+A, D                  # detach from session
screen -ls                 # list sessions
screen -r                  # reattach to session
screen -r name             # reattach to named session

# Tmux (modern alternative)
tmux                       # start new session
tmux new -s name           # start named session
Ctrl+B, D                  # detach
tmux ls                    # list sessions
tmux attach -t name        # attach to session
```

## Best Practices

- Use `man` pages to understand commands before using them
- Be extremely careful with `rm -rf`, especially with wildcards
- Always double-check paths before running destructive commands
- Use `sudo` judiciously; avoid running as root unnecessarily
- Keep your system updated regularly
- Use tab completion to avoid typos and speed up typing
- Learn keyboard shortcuts (Ctrl+A, Ctrl+E, Ctrl+R, Ctrl+L)
- Use aliases for frequently used commands
- Keep backups before making system changes
- Test commands on non-critical data first

```bash
# Useful aliases (add to ~/.bashrc)
alias ll='ls -lah'
alias ..='cd ..'
alias grep='grep --color=auto'
alias update='sudo apt update && sudo apt upgrade'

# History shortcuts
!!                         # repeat last command
!$                         # last argument of previous command
!^                         # first argument of previous command
!*                         # all arguments of previous command
Ctrl+R                     # reverse search history
```

## Troubleshooting

- **Permission denied**: Check file permissions with `ls -l`, use `sudo` if needed
- **Command not found**: Check if installed, verify PATH with `echo $PATH`
- **Disk full**: Use `df -h` to check space, `du -sh *` to find large files
- **Process not responding**: Use `kill -9` as last resort, try `kill` first
- **Can't delete file**: Check permissions, ensure file isn't in use (`lsof filename`)
- **Slow system**: Check with `top` or `htop`, look for high CPU/memory usage
- **Network issues**: Test with `ping`, check interface with `ip addr`, verify DNS with `nslookup`
- **Package conflicts**: Try `sudo apt --fix-broken install` (Debian/Ubuntu)

```bash
# Common fixes

# Free up disk space
sudo apt autoremove        # remove unused packages
sudo apt clean             # clear package cache
find . -name "*.log" -mtime +30 -delete  # delete old logs

# Kill unresponsive process
ps aux | grep process_name
kill -9 PID

# Check system logs
sudo journalctl -xe        # recent errors
tail -f /var/log/syslog    # follow system log

# Network reset
sudo systemctl restart NetworkManager
```

## Tools & References

- **tldr**: Simplified man pages with examples (`tldr command`)
- **explainshell.com**: Explains shell commands in detail
- **man pages**: Built-in documentation
- **The Linux Command Line** (book by William Shotts)
- **Linux Journey**: Interactive learning platform
- **Bash Guide**: Advanced bash scripting guide

---

Quick tip: Use `history | grep keyword` to find commands you've used before, then `!number` to re-run a specific command from history.
