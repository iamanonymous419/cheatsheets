# Linux Command Line Cheatsheet

A comprehensive reference guide for Linux command-line operations.

## Table of Contents
- [Linux Command Line Cheatsheet](#linux-command-line-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [System Information](#system-information)
  - [Hardware Information](#hardware-information)
  - [File and Directory Operations](#file-and-directory-operations)
  - [File Permissions](#file-permissions)
  - [File Searching](#file-searching)
  - [File Content](#file-content)
  - [Archive and Compression](#archive-and-compression)
  - [User Management](#user-management)
  - [Process Management](#process-management)
  - [Disk Usage](#disk-usage)
  - [Network](#network)
  - [SSH](#ssh)
  - [Package Management](#package-management)
    - [Debian/Ubuntu (APT)](#debianubuntu-apt)
    - [Red Hat/CentOS/Fedora (YUM/DNF)](#red-hatcentosfedora-yumdnf)
    - [Arch Linux (Pacman)](#arch-linux-pacman)
  - [Text Processing](#text-processing)
  - [System Control](#system-control)
  - [Scheduling Tasks](#scheduling-tasks)
  - [Shell Scripting Basics](#shell-scripting-basics)
  - [Environment Variables](#environment-variables)
  - [Useful Shortcuts](#useful-shortcuts)

## System Information
```bash
# Display kernel release information
uname -a

# Show system hostname
hostname

# Display the IP addresses of the host
hostname -I

# Show system reboot history
last reboot

# Show which users are logged in
who

# Display current date and time
date

# Show system uptime
uptime

# Show system and kernel logs
dmesg

# Display kernel messages
dmesg | less

# Show OS information
cat /etc/os-release

# Display current shell
echo $SHELL
```

## Hardware Information
```bash
# Display CPU information
lscpu

# Display memory information
free -h

# Display PCI devices
lspci -tv

# Display USB devices
lsusb -tv

# Show hardware information from the BIOS
dmidecode

# Show disk partitions
fdisk -l

# Display disk usage
df -h

# Show memory usage
free -m

# Show disk space usage by directory
du -sh /path/to/directory

# Show information about block devices
lsblk
```

## File and Directory Operations
```bash
# List files in the current directory
ls

# List files with details
ls -l

# List all files (including hidden)
ls -la

# List files with human-readable sizes
ls -lh

# List files sorted by size
ls -S

# List files sorted by modification time
ls -t

# List files within a folders
ls -R

# Create a directory
mkdir directory_name

# Create nested directories
mkdir -p parent/child/grandchild

# Change directory
cd directory_name

# Change to home directory
cd or cd ~

# Change to previous directory
cd -

# Show current directory
pwd

# Copy files
cp source destination

# Copy directories recursively
cp -r source_dir destination_dir

# Move/rename files or directories
mv source destination

# Remove a file
rm filename

# Remove a directory and its contents
rm -rf directory_name

# Remove an empty directory
rmdir directory_name

# Create an empty file or update timestamp
touch filename

# Create a symbolic link
ln -s target_path link_name

# Compare two files
diff file1 file2

# Show differences side by side
diff -y file1 file2
```

## File Permissions
```bash
# Change file permissions
chmod permissions filename

# Numeric permissions examples:
# 644 (rw-r--r--): Owner can read/write, group/others can read
# 755 (rwxr-xr-x): Owner can read/write/execute, group/others can read/execute
# 777 (rwxrwxrwx): Everyone can read/write/execute

# Symbolic permissions:
# u: user/owner, g: group, o: others, a: all
chmod u+x file    # Add execute permission for owner
chmod go-w file   # Remove write permission from group and others
chmod a+r file    # Add read permission for all

# Change file owner
chown user:group filename

# Change file owner recursively
chown -R user:group directory

# Change group ownership
chgrp group filename
```

## File Searching
```bash
# Find files by name
find /path/to/search -name "filename"

# Find files by type
find /path/to/search -type f  # Files
find /path/to/search -type d  # Directories

# Find files by size
find /path/to/search -size +100M  # Files larger than 100MB
find /path/to/search -size -10k   # Files smaller than 10KB

# Find files by permission
find /path/to/search -perm 644

# Find files by modification time
find /path/to/search -mtime -7  # Modified in the last 7 days

# Find and execute a command on each file
find /path/to/search -name "*.txt" -exec rm {} \;

# Locate files using database (update with updatedb)
locate filename

# Find files by content
grep -r "text" /path/to/search
```

## File Content
```bash
# Display the entire file
cat filename

# Display with line numbers
cat -n filename

# Display the first 10 lines
head filename

# Display the first n lines
head -n 20 filename

# Display the last 10 lines
tail filename

# Display the last n lines
tail -n 20 filename

# Follow the growth of a file (useful for logs)
tail -f filename

# Display file with pagination
less filename
more filename

# Display sorted content
sort filename

# Display unique lines only
uniq filename

# Count lines, words, and characters
wc filename
wc -l filename  # Lines only
wc -w filename  # Words only
wc -c filename  # Characters only

# Replace string in file and save results
sed 's/original/replacement/g' filename > newfile

# In-place replacement
sed -i 's/original/replacement/g' filename
```

## Archive and Compression
```bash
# Create a tar archive
tar -cvf archive.tar files_or_directories

# Extract a tar archive
tar -xvf archive.tar

# Create a gzipped tar archive
tar -czvf archive.tar.gz files_or_directories

# Extract a gzipped tar archive
tar -xzvf archive.tar.gz

# Create a bzipped tar archive
tar -cjvf archive.tar.bz2 files_or_directories

# Extract a bzipped tar archive
tar -xjvf archive.tar.bz2

# Create a ZIP archive
zip -r archive.zip files_or_directories

# Extract a ZIP archive
unzip archive.zip

# Compress a file with gzip
gzip filename

# Decompress a gzip file
gzip -d filename.gz

# Compress a file with bzip2
bzip2 filename

# Decompress a bzip2 file
bzip2 -d filename.bz2
```

## User Management
```bash
# Add a user
sudo adduser username

# Add a user without home directory
sudo useradd username

# Delete a user
sudo deluser username

# Delete a user with home directory
sudo deluser --remove-home username

# Change user password
sudo passwd username

# Change your own password
passwd

# Switch user
su - username

# Run command as another user
sudo -u username command

# List all users
cat /etc/passwd

# Add a user to a group
sudo usermod -aG groupname username

# Create a new group
sudo groupadd groupname

# Delete a group
sudo groupdel groupname

# List all groups
cat /etc/group

# Show groups for current user
groups

# Show groups for specific user
groups username
```

## Process Management
```bash
# List running processes
ps

# List all processes
ps aux

# List processes with real-time updates
top

# Interactive process viewer (better alternative to top)
htop

# Kill a process by PID
kill PID

# Kill a process by name
killall process_name

# Force kill a process
kill -9 PID

# Run a process in the background
command &

# List background jobs
jobs

# Bring a background job to foreground
fg %job_number

# Send a foreground job to background
Ctrl+Z, then bg

# Run a command immune to hangups
nohup command &

# Show process tree
pstree

# Run a command with modified priority (-20 to 19, lower is higher priority)
nice -n 10 command

# Change priority of a running process
renice 10 -p PID
```

## Disk Usage
```bash
# Show free and used space on mounted filesystems
df -h

# Show disk usage for a directory
du -h /path/to/directory

# Show total disk usage for a directory
du -sh /path/to/directory

# Show the top disk space users in current directory
du -h | sort -hr | head

# Show inode usage
df -i

# Check disk for errors (run on unmounted filesystem)
fsck /dev/sdXY

# Mount a filesystem
mount /dev/sdXY /mnt/mount_point

# Unmount a filesystem
umount /mnt/mount_point

# Show mounted filesystems
mount

# Create a filesystem
mkfs.ext4 /dev/sdXY

# List block devices
lsblk
```

## Network
```bash
# Display all network interfaces and IP addresses
ifconfig
ip addr show

# Display and manipulate network interfaces
ip link

# Test connectivity to a host
ping host

# Show routing table
route -n
ip route

# Trace route to host
traceroute host

# Show listening ports
netstat -tuln
ss -tuln

# Show active connections
netstat -tuan
ss -tuan

# Download a file
wget URL
curl -O URL

# Display DNS information
dig domain
nslookup domain

# Show listening services and ports
sudo lsof -i

# Scan open ports on a host
nmap host

# Configure network interface
ifconfig eth0 192.168.1.100 netmask 255.255.255.0
ip addr add 192.168.1.100/24 dev eth0

# Show hostname and IP of the current host
hostname -I

# Show local DNS entries
cat /etc/hosts
```

## SSH
```bash
# Connect to a remote server
ssh username@remote_host

# Connect to a remote server with a specific port
ssh username@remote_host -p port_number

# Connect with a specific private key
ssh -i private_key.pem username@remote_host

# Generate SSH key pair
ssh-keygen -t rsa -b 4096

# Copy public key to remote server
ssh-copy-id username@remote_host

# Run a command on a remote server
ssh username@remote_host command

# Secure copy files to a remote system
scp /local/file username@remote_host:/remote/directory

# Secure copy files from a remote system
scp username@remote_host:/remote/file /local/directory

# Secure copy directory recursively
scp -r /local/directory username@remote_host:/remote/directory

# Mount remote directory using SSHFS
sshfs username@remote_host:/remote/directory /local/mount_point
```

## Package Management
### Debian/Ubuntu (APT)
```bash
# Update package lists
sudo apt update

# Upgrade all packages
sudo apt upgrade

# Install a package
sudo apt install package_name

# Remove a package
sudo apt remove package_name

# Remove a package and its configuration files
sudo apt purge package_name

# Search for a package
apt search package_name

# Show package information
apt show package_name

# List installed packages
dpkg -l

# Check if a package is installed
dpkg -l | grep package_name

# Clean up unused packages
sudo apt autoremove
```

### Red Hat/CentOS/Fedora (YUM/DNF)
```bash
# Update package lists
sudo yum check-update
sudo dnf check-update

# Upgrade all packages
sudo yum update
sudo dnf upgrade

# Install a package
sudo yum install package_name
sudo dnf install package_name

# Remove a package
sudo yum remove package_name
sudo dnf remove package_name

# Search for a package
yum search package_name
dnf search package_name

# Show package information
yum info package_name
dnf info package_name

# List installed packages
rpm -qa

# Check if a package is installed
rpm -qa | grep package_name
```

### Arch Linux (Pacman)
```bash
# Update package lists and upgrade all packages
sudo pacman -Syu

# Install a package
sudo pacman -S package_name

# Remove a package
sudo pacman -R package_name

# Remove a package and its dependencies
sudo pacman -Rs package_name

# Search for a package
pacman -Ss package_name

# Show package information
pacman -Si package_name

# List installed packages
pacman -Q

# Check if a package is installed
pacman -Q | grep package_name
```

## Text Processing
```bash
# Search for a pattern in a file
grep "pattern" filename

# Search recursively in directories
grep -r "pattern" /path/to/directory

# Search case-insensitive
grep -i "pattern" filename

# Search for whole words only
grep -w "pattern" filename

# Show line numbers
grep -n "pattern" filename

# Count matching lines
grep -c "pattern" filename

# Show lines that don't match
grep -v "pattern" filename

# Search for multiple patterns
grep -e "pattern1" -e "pattern2" filename

# Replace text using sed
sed 's/old_text/new_text/g' filename

# Process column-based text
awk '{print $1}' filename  # Print first column
awk -F: '{print $1}' filename  # Use : as separator

# Join lines of two sorted files
join file1 file2

# Sort file content
sort filename

# Sort numerically
sort -n filename

# Sort by specific column
sort -k2 filename

# Remove duplicate lines
uniq filename

# Count occurrences of each line
uniq -c filename

# Cut specific columns
cut -d: -f1 filename  # Cut first field with : delimiter

# Convert tabs to spaces
expand filename

# Merge lines from multiple files
paste file1 file2
```

## System Control
```bash
# Shutdown the system
sudo shutdown -h now

# Reboot the system
sudo reboot

# Suspend the system
sudo systemctl suspend

# Hibernate the system
sudo systemctl hibernate

# Show system boot messages
dmesg

# Clear memory cache
sudo sync && echo 3 | sudo tee /proc/sys/vm/drop_caches

# Show current runlevel
runlevel

# Change to different runlevel
sudo init runlevel_number

# Show systemd services status
systemctl status

# Start a service
sudo systemctl start service_name

# Stop a service
sudo systemctl stop service_name

# Enable a service to start at boot
sudo systemctl enable service_name

# Disable a service at boot
sudo systemctl disable service_name

# View system logs
sudo journalctl

# View logs for a specific service
sudo journalctl -u service_name
```

## Scheduling Tasks
```bash
# Edit current user's crontab
crontab -e

# List current user's crontab
crontab -l

# Edit another user's crontab
sudo crontab -e -u username

# Crontab format:
# minute hour day_of_month month day_of_week command
# * * * * * command  # Run every minute
# 0 * * * * command  # Run every hour
# 0 0 * * * command  # Run every day at midnight
# 0 0 * * 0 command  # Run every Sunday at midnight
# */5 * * * * command  # Run every 5 minutes

# Run a command at a specific time (one-time)
at 10:00 AM
> command
> Ctrl+D

# View scheduled 'at' jobs
atq

# Remove a scheduled 'at' job
atrm job_number

# Schedule a job to run once system load average drops below 1.5
batch
> command
> Ctrl+D
```

## Shell Scripting Basics
```bash
#!/bin/bash
# This is a comment

# Variables
NAME="Linux"
echo $NAME

# Command substitution
DATE=$(date)
echo "Today is $DATE"

# Conditional statements
if [ "$1" = "hello" ]; then
    echo "Hello back!"
elif [ "$1" = "bye" ]; then
    echo "Goodbye!"
else
    echo "What?"
fi

# Loops
for i in 1 2 3 4 5; do
    echo "Number: $i"
done

# While loop
count=1
while [ $count -le 5 ]; do
    echo "Count: $count"
    count=$((count + 1))
done

# Functions
say_hello() {
    echo "Hello, $1!"
}

# Call a function
say_hello "World"

# Exit status
ls /nonexistent 2>/dev/null
echo "Exit status: $?"

# Read user input
echo "Enter your name:"
read user_name
echo "Hello, $user_name!"
```

## Environment Variables
```bash
# Display all environment variables
env

# Display specific environment variable
echo $HOME

# Set an environment variable for current session
export VAR_NAME=value

# Unset an environment variable
unset VAR_NAME

# Add to PATH temporarily
export PATH=$PATH:/new/directory

# Set environment variables permanently for a user
# Add to ~/.bashrc or ~/.bash_profile:
export VAR_NAME=value

# View the search path for executables
echo $PATH

# View the current shell
echo $SHELL

# View the home directory
echo $HOME

# View username
echo $USER

# View terminal type
echo $TERM
```

## Useful Shortcuts
```
Ctrl+C     - Interrupt (kill) current process
Ctrl+Z     - Suspend current process
Ctrl+D     - Exit current shell or logout
Ctrl+L     - Clear screen
Ctrl+A     - Move to beginning of line
Ctrl+E     - Move to end of line
Ctrl+U     - Cut everything before cursor
Ctrl+K     - Cut everything after cursor
Ctrl+W     - Cut the word before cursor
Ctrl+Y     - Paste previously cut text
Ctrl+R     - Search command history
Ctrl+G     - Cancel history search
Tab        - Auto-complete commands and filenames
Up/Down    - Navigate command history
!!         - Repeat last command
!$         - Last argument of previous command
!*         - All arguments of previous command
!n         - Repeat command number n from history
!string    - Repeat last command starting with "string"
Alt+.      - Insert last argument of previous command
```

---

This cheatsheet covers the most common Linux commands and operations. For more detailed information on any command, use the `man` command:

```bash
man command_name
```

Or for a brief help text:

```bash
command_name --help
```