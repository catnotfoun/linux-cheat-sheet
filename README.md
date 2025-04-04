# linux-cheat-sheet
> **This repository contains a comprehensive Linux command cheat sheet organized by functional categories. Whether you're a beginner learning the basics or an experienced user who needs a quick reference, this guide provides essential commands for daily Linux operations.**
## Table of Contents
- [Basic File and Directory Operations](#basic-file-and-directory-operations)
  - [Navigation Commands](#navigation-commands)
  - [File and Directory Management](#file-and-directory-management)
- [Text Processing and Editing](#text-processing-and-editing)
  - [Basic Text Commands](#basic-text-commands)
  - [Text Processing Tools](#text-processing-tools)
- [System Monitoring and Management](#system-monitoring-and-management)
  - [System Information Commands](#system-information-commands)
  - [Process Monitoring](#process-monitoring)
  - [System Logs](#system-logs)
- [User and Permission Management](#user-and-permission-management)
  - [User Management](#user-management)
  - [Group Management](#group-management)
  - [Permission Management](#permission-management)
- [Networking and Communication](#networking-and-communication)
  - [Network Configuration](#network-configuration)
  - [Network Diagnostics](#network-diagnostics)
  - [File Transfer](#file-transfer)
- [Disk and File System Utilities](#disk-and-file-system-utilities)
  - [File System Management](#file-system-management)
  - [Partition Management](#partition-management)
- [Compression and Archiving](#compression-and-archiving)
- [Process Management](#process-management)
  - [Process Control](#process-control)
  - [Job Control](#job-control)
- [System Configuration and Settings](#system-configuration-and-settings)
  - [Configuration Management](#configuration-management)
- [Package Management](#package-management)
  - [Debian-based Systems (Ubuntu, Debian)](#debian-based-systems-ubuntu-debian)
  - [Red Hat-based Systems (CentOS, Fedora)](#red-hat-based-systems-centos-fedora)
  - [Arch Linux](#arch-linux)
- [Scripting and Programming](#scripting-and-programming)
  - [Shell Scripting](#shell-scripting)
  - [Programming Languages](#programming-languages)


## Basic File and Directory Operations

### Navigation Commands

#### `pwd` - Print Working Directory
> The `pwd` command displays the full pathname of your current directory, starting from the root directory. It helps you determine your current location in the file system hierarchy.

**Syntax:**
```bash
pwd [options]
```

**Options:**
- `-L`, `--logical`: Displays the logical current directory, including any symbolic links.
- `-P`, `--physical`: Displays the physical current directory by resolving all symbolic links.

**Example:**
```bash
pwd
# Output: /home/user/Documents
```

#### `cd` - Change Directory
> The `cd` command allows you to change your current working directory. Without any arguments, `cd` takes you to your home directory.

**Syntax:**
```bash
cd [directory]
```

**Examples:**
```bash
cd /var/www/html    # Change to absolute path
cd Documents        # Change to relative path (subdirectory)
cd ../              # Move up one directory level
cd ~                # Go to home directory
cd -                # Go to the previous directory
```

#### `ls` - List Directory Contents
> The `ls` command lists files and directories. By default, it lists the contents of the current directory.

**Syntax:**
```bash
ls [options] [file|dir]
```

**Common Options:**
- `-a`: Shows all files, including hidden files (starting with `.`).
- `-l`: Uses a long listing format, showing permissions, owner, size, modification date, etc.
- `-h`: With `-l`, displays sizes in human-readable format (e.g., K, M, G).
- `-t`: Sorts files by modification time, newest first.
- `-r`: Reverses the order while sorting.
- `-R`: Lists subdirectories recursively.

**Example:**
```bash
ls -lah
# Shows all files (including hidden) in long, human-readable format
```

### File and Directory Management

#### `mkdir` - Make Directory
> The `mkdir` command creates new directories.

**Syntax:**
```bash
mkdir [OPTIONS] DIRECTORY...
```

**Options:**
- `-p`: Creates parent directories as needed; no error if directory already exists.
- `-m MODE`: Sets the file mode (permissions) for the new directory (e.g., `mkdir -m 777 newdir`).

**Example:**
```bash
mkdir project_files
mkdir -p path/to/nested/directory
```

#### `rmdir` - Remove Directory
> The `rmdir` command removes *empty* directories. It will fail if the directory contains any files or subdirectories.

**Syntax:**
```bash
rmdir [options] directory...
```

**Options:**
- `-p`: Removes the specified directory and its parent directories if they become empty after removal.

**Example:**
```bash
rmdir empty_dir
rmdir -p parent/child/grandchild # Removes grandchild, then child, then parent if they become empty
```

#### `touch` - Create or Update Files
> The `touch` command creates new empty files or updates the access and modification timestamps of existing files.

**Syntax:**
```bash
touch [OPTION]... FILE...
```

**Options:**
- `-a`: Changes only the access time.
- `-m`: Changes only the modification time.
- `-c`, `--no-create`: Does not create any files if they do not exist.
- `-t STAMP`: Uses `[[CC]YY]MMDDhhmm[.ss]` instead of the current time.

**Example:**
```bash
touch new_empty_file.txt
touch existing_file.txt # Updates timestamps of existing_file.txt
```

#### `cp` - Copy Files and Directories
> The `cp` command copies files and directories.

**Syntax:**
```bash
cp [options] source destination
cp [options] source... directory
```

**Options:**
- `-r`, `-R`, `--recursive`: Copies directories recursively.
- `-i`, `--interactive`: Prompts before overwriting an existing file.
- `-p`: Preserves file attributes like mode, ownership, and timestamps.
- `-v`, `--verbose`: Explains what is being done.

**Example:**
```bash
cp report.txt report_backup.txt
cp -r source_folder/ destination_folder/
cp file1.txt file2.txt documents/ # Copy multiple files into a directory
```

#### `mv` - Move or Rename Files
> The `mv` command moves files or directories from one location to another, or renames them if the source and destination are in the same directory.

**Syntax:**
```bash
mv [options] source destination
mv [options] source... directory
```

**Options:**
- `-i`, `--interactive`: Prompts before overwriting an existing file.
- `-f`, `--force`: Overwrites the destination file without prompting.
- `-n`, `--no-clobber`: Does not overwrite an existing file.
- `-v`, `--verbose`: Explains what is being done.

**Example:**
```bash
mv old_name.txt new_name.txt # Rename file
mv important_file.doc /mnt/backup/ # Move file to another location
mv file1 file2 folder/ # Move multiple files into a directory
```

#### `rm` - Remove Files and Directories
> The `rm` command removes (deletes) files and directories. **Use with caution**, as deleted files are generally not recoverable.

**Syntax:**
```bash
rm [options] [file...]
```

**Options:**
- `-r`, `-R`, `--recursive`: Removes directories and their contents recursively. **Essential for removing directories.**
- `-f`, `--force`: Ignores nonexistent files and arguments, never prompts.
- `-i`: Prompts before every removal.
- `-v`, `--verbose`: Explains what is being done.

**Example:**
```bash
rm temporary_file.tmp
rm -rf old_project/ # Forcefully remove directory and all its contents (use carefully!)
rm -i *.log # Prompt before removing each log file
```

#### `ln` - Create Links
> The `ln` command creates links between files. Links provide alternative names for files.

**Syntax:**
```bash
ln [options] target link_name
```

**Options:**
- `-s`, `--symbolic`: Creates a symbolic (soft) link instead of a hard link. Symbolic links can cross file systems and link to directories.
- `-f`, `--force`: Removes existing destination files.

**Types of Links:**
- **Hard Link:** A directory entry that associates a name with a file on a file system. All hard links are equally valid ways to access the file. Cannot link across file systems or to directories.
- **Symbolic (Soft) Link:** A special type of file that contains a path to another file or directory. Can link across file systems and to directories. If the target is moved or deleted, the link becomes broken.

**Example:**
```bash
ln existing_file hard_link # Create a hard link
ln -s /path/to/original/file symbolic_link # Create a symbolic link
ln -s /var/log /home/user/logs # Link a directory
```

## Text Processing and Editing

### Basic Text Commands

#### `cat` - Concatenate and Display Files
> The `cat` command reads files sequentially, writing them to standard output. It's commonly used to display file contents or combine files.

**Syntax:**
```bash
cat [options] [file...]
```

**Options:**
- `-n`, `--number`: Numbers all output lines.
- `-b`, `--number-nonblank`: Numbers only non-empty output lines.
- `-s`, `--squeeze-blank`: Suppresses repeated empty output lines.

**Example:**
```bash
cat config.txt
cat header.txt body.txt footer.txt > complete_document.txt
cat -n script.sh
```

#### `less` - View File Contents Page by Page
> The `less` command allows you to view text files one screen at a time. It's more feature-rich than `more` and more practical than `cat` for large files, allowing forward/backward scrolling and searching.

**Syntax:**
```bash
less [options] file
```

**Navigation within `less`:**
- `Space` / `f`: Scroll forward one screen.
- `b`: Scroll backward one screen.
- `d`: Scroll forward half a screen.
- `u`: Scroll backward half a screen.
- `G`: Go to the end of the file.
- `g`: Go to the beginning of the file.
- `/pattern`: Search forward for `pattern`.
- `?pattern`: Search backward for `pattern`.
- `n`: Repeat the previous search.
- `N`: Repeat the previous search in the opposite direction.
- `q`: Quit `less`.

**Example:**
```bash
less /var/log/syslog
```

#### `head` - Display Beginning of Files
> The `head` command outputs the first part (by default, 10 lines) of files.

**Syntax:**
```bash
head [options] [file...]
```

**Options:**
- `-n NUMBER`, `--lines=NUMBER`: Displays the first `NUMBER` lines instead of the default 10.
- `-c BYTES`, `--bytes=BYTES`: Displays the first `BYTES` bytes.

**Example:**
```bash
head /etc/passwd
head -n 20 large_file.csv
head -c 1024 data.bin
```

#### `tail` - Display End of Files
> The `tail` command outputs the last part (by default, 10 lines) of files. It's very useful for monitoring log files.

**Syntax:**
```bash
tail [options] [file...]
```

**Options:**
- `-n NUMBER`, `--lines=NUMBER`: Displays the last `NUMBER` lines instead of the default 10.
- `-c BYTES`, `--bytes=BYTES`: Displays the last `BYTES` bytes.
- `-f`, `--follow`: Outputs appended data as the file grows. Essential for monitoring logs in real-time.

**Example:**
```bash
tail /var/log/messages
tail -n 50 error.log
tail -f /var/log/apache2/access.log # Monitor web server access log
```

### Text Processing Tools

#### `grep` - Search for Patterns
> The `grep` command searches for `PATTERNS` in each `FILE`. It's an extremely powerful tool for finding text within files or filtering output from other commands.

**Syntax:**
```bash
grep [OPTIONS] PATTERN [FILE...]
```

**Options:**
- `-i`, `--ignore-case`: Ignores case distinctions in patterns and input data.
- `-r`, `-R`, `--recursive`: Searches directories recursively.
- `-v`, `--invert-match`: Selects non-matching lines.
- `-n`, `--line-number`: Prefixes each line of output with the 1-based line number within its input file.
- `-l`, `--files-with-matches`: Prints only the names of files containing matches.
- `-E`, `--extended-regexp`: Interprets `PATTERN` as an extended regular expression.
- `-F`, `--fixed-strings`: Interprets `PATTERN` as a list of fixed strings, separated by newlines.

**Example:**
```bash
grep "error" /var/log/syslog
ps aux | grep "httpd" # Find httpd processes
grep -r "DatabaseConnection" /var/www/my_app/
grep -i 'warning' *.log
grep -v '^#' config.conf # Show lines not starting with #
```

#### `sed` - Stream Editor
> The `sed` command is a stream editor for filtering and transforming text. It reads input line by line, applies specified operations, and writes the results to standard output.

**Syntax:**
```bash
sed [options] 'script' [file...]
sed [options] -f script_file [file...]
```

**Common Commands:**
- `s/regexp/replacement/flags`: Substitute `replacement` for `regexp`. Flags include `g` (global replace on the line), `i` (case-insensitive).
- `d`: Delete the pattern space (current line).
- `p`: Print the current pattern space.
- `i \text`: Insert `text` before the current line.
- `a \text`: Append `text` after the current line.

**Options:**
- `-i[SUFFIX]`, `--in-place[=SUFFIX]`: Edits files in place (makes backup if SUFFIX supplied).
- `-n`, `--quiet`, `--silent`: Suppresses automatic printing of pattern space.
- `-e script`, `--expression=script`: Adds the `script` to the commands to be executed.
- `-f script-file`, `--file=script-file`: Adds the contents of `script-file` to the commands.

**Example:**
```bash
sed 's/apple/orange/g' fruit.txt # Replace all 'apple' with 'orange'
sed '/^$/d' file.txt # Delete empty lines
sed -n '1,5p' file.txt # Print only the first 5 lines
sed -i '.bak' 's/old_setting/new_setting/' config.ini # Edit in place, create backup
```

#### `awk` - Text Processing Language
> The `awk` command is a versatile programming language designed for text processing, especially useful for pattern scanning and processing columnar data.

**Syntax:**
```bash
awk [options] 'program' [file...]
```

**Structure of `program`:**
- `pattern { action }`
- `BEGIN { action }` (Executed before processing input)
- `END { action }` (Executed after processing input)

**Common Variables:**
- `$0`: The entire input line.
- `$1`, `$2`, ...: The first, second, ... fields in the input line.
- `FS`: Field separator (default is whitespace).
- `NF`: Number of fields in the current record.
- `NR`: Number of the current record (line number).

**Options:**
- `-F fs`, `--field-separator=fs`: Specifies the input field separator.

**Example:**
```bash
awk '{print $1}' data.txt # Print the first column
awk -F':' '{print $1, $3}' /etc/passwd # Print username and UID from passwd file
awk '$3 > 100 {print $0}' scores.txt # Print lines where the third column is greater than 100
awk 'BEGIN { print "Report Start" } { sum += $1 } END { print "Total:", sum }' numbers.txt
```

#### `sort` - Sort Lines of Text
> The `sort` command sorts lines of text files or standard input.

**Syntax:**
```bash
sort [options] [file...]
```

**Options:**
- `-n`, `--numeric-sort`: Compares according to string numerical value.
- `-r`, `--reverse`: Reverses the result of comparisons.
- `-k POS1[,POS2]`, `--key=POS1[,POS2]`: Sorts via a key; key starts at `POS1` and ends at `POS2` (fields).
- `-t CHAR`, `--field-separator=CHAR`: Uses `CHAR` as the field separator.
- `-u`, `--unique`: Outputs only the first of an equal sequence.
- `-h`, `--human-numeric-sort`: Compares human-readable numbers (e.g., 2K, 1G).

**Example:**
```bash
sort names.txt
sort -r scores.txt # Sort in reverse order
sort -n -k 3 data.csv # Sort numerically based on the 3rd column
ls -l | sort -k 5 -h # Sort file listing by human-readable size (5th column)
sort -t: -k 3 -n /etc/passwd # Sort passwd file numerically by UID (3rd field, ':' separator)
```

#### `uniq` - Report or Filter Repeated Lines
> The `uniq` command filters adjacent matching lines from input, writing to output. Input needs to be sorted first for `uniq` to work effectively on all duplicate lines.

**Syntax:**
```bash
uniq [options] [input [output]]
```

**Options:**
- `-c`, `--count`: Prefixes lines by the number of occurrences.
- `-d`, `--repeated`: Only prints duplicate lines, one for each group.
- `-u`, `--unique`: Only prints unique lines (lines that are not repeated).
- `-i`, `--ignore-case`: Ignores differences in case when comparing.

**Example:**
```bash
sort access.log | uniq # Show unique lines from sorted log
sort names.txt | uniq -c # Count occurrences of each name
sort data.txt | uniq -d # Show only lines that were duplicated
```

## System Monitoring and Management

### System Information Commands

#### `uname` - Print System Information
> The `uname` command displays system information like kernel name, hostname, kernel release, processor type, etc.

**Syntax:**
```bash
uname [options]
```

**Options:**
- `-a`, `--all`: Prints all available information.
- `-s`, `--kernel-name`: Prints the kernel name (e.g., Linux).
- `-n`, `--nodename`: Prints the network node hostname.
- `-r`, `--kernel-release`: Prints the kernel release (e.g., 5.15.0-48-generic).
- `-v`, `--kernel-version`: Prints the kernel version.
- `-m`, `--machine`: Prints the machine hardware name (e.g., x86_64).
- `-o`, `--operating-system`: Prints the operating system (e.g., GNU/Linux).

**Example:**
```bash
uname -a
# Output might look like: Linux myhostname 5.15.0-48-generic #54-Ubuntu SMP Fri Aug 26 13:26:29 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
uname -r
# Output: 5.15.0-48-generic
```

#### `free` - Display Memory Usage
> The `free` command displays the total amount of free and used physical and swap memory in the system, as well as the buffers and caches used by the kernel.

**Syntax:**
```bash
free [options]
```

**Options:**
- `-h`, `--human`: Shows output in human-readable format (K, M, G).
- `-b`, `-k`, `-m`, `-g`: Shows output in Bytes, Kibibytes, Mebibytes, or Gibibytes.
- `-t`, `--total`: Displays a line containing the totals.
- `-s N`, `--seconds N`: Continuously displays the result every `N` seconds.

**Example:**
```bash
free -h
# Output shows Mem (RAM) and Swap usage
```

#### `uptime` - Show System Uptime and Load
> The `uptime` command shows how long the system has been running, the number of currently logged-in users, and the system load averages for the past 1, 5, and 15 minutes.

**Syntax:**
```bash
uptime [options]
```

**Options:**
- `-p`, `--pretty`: Shows uptime in a pretty format (e.g., "up 2 hours, 5 minutes").
- `-s`, `--since`: Shows the date and time since the system was booted.

**Example:**
```bash
uptime
# Output: 10:30:15 up 3 days, 1:15,  2 users,  load average: 0.05, 0.15, 0.10
uptime -p
# Output: up 3 days, 1 hour, 15 minutes
```

### Process Monitoring

#### `ps` - Process Status
> The `ps` command reports a snapshot of the current processes.

**Syntax:**
```bash
ps [options]
```

**Common Options (Syntax Styles Vary):**
- **BSD Style (no hyphen):**
  - `aux`: Shows processes for all users (`a`), including those without a controlling terminal (`x`), in user-oriented format (`u`).
- **System V Style (with hyphen):**
  - `-ef`: Shows all processes (`-e`) in full format (`-f`).
  - `-eLf`: Shows threads as well (`L`).

**Example:**
```bash
ps aux
ps -ef
ps aux | grep nginx # Find processes related to nginx
```

#### `top` - Monitor Processes Dynamically
> The `top` command provides a dynamic real-time view of running system processes. It displays system summary information and a list of processes managed by the kernel.

**Syntax:**
```bash
top [options]
```

**Interactive Commands within `top`:**
- `h` or `?`: Display help screen.
- `k`: Kill a process (prompts for PID and signal).
- `r`: Renice a process (prompts for PID and nice value).
- `P`: Sort by CPU usage (default).
- `M`: Sort by memory usage.
- `T`: Sort by time/cumulative time.
- `u`: Filter by user (prompts for username).
- `1`: Toggle display of individual CPU core stats.
- `q`: Quit `top`.

**Example:**
```bash
top
```

#### `htop` - Interactive Process Viewer (Enhanced)
> The `htop` command is an interactive process viewer and system monitor. It's considered an enhanced version of `top`, offering a more user-friendly interface with color, scrolling, easier process manipulation, and visual meters. (May need installation: `sudo apt install htop` or `sudo yum install htop`).

**Syntax:**
```bash
htop [options]
```

**Features:**
- Color-coded display.
- Vertical and horizontal scrolling for process list and command lines.
- Easier process sorting (click on headers or use function keys).
- Kill, renice processes directly using function keys (e.g., F9 for Kill).
- Tree view (F5).
- Setup screen (F2) for customization.

**Example:**
```bash
htop
```

### System Logs

#### `dmesg` - Display Kernel Ring Buffer Messages
> The `dmesg` command prints or controls the kernel ring buffer. It's useful for examining kernel boot messages and hardware detection/error messages logged during system operation.

**Syntax:**
```bash
dmesg [options]
```

**Options:**
- `-H`, `--human`: Produces human-readable output (uses `less`).
- `-T`, `--ctime`: Prints human-readable timestamps (may not be accurate for old messages).
- `-l level`, `--level=level`: Restricts output to specified levels (e.g., `err`, `warn`, `info`).
- `-f facility`, `--facility=facility`: Restricts output to specified facilities (e.g., `kern`, `user`).
- `-w`, `--follow`: Waits for new messages.

**Example:**
```bash
dmesg
dmesg | grep -i usb # Search for USB related messages
dmesg -l err,warn # Show only error and warning messages
sudo dmesg -c # Clear the ring buffer after printing (requires root)
```

#### `journalctl` - Query the systemd Journal
> The `journalctl` command queries and displays logs from `journald`, the systemd logging service. It provides advanced filtering and viewing options for system, service, and kernel logs on modern systemd-based distributions.

**Syntax:**
```bash
journalctl [options] [MATCHES...]
```

**Options:**
- `-u UNIT`, `--unit=UNIT`: Shows messages from the specified systemd unit (service).
- `-f`, `--follow`: Shows the most recent journal entries and continuously prints new entries.
- `-b [ID]`, `--boot[=ID]`: Shows messages from a specific boot (0 is current, -1 previous, etc.).
- `-k`, `--dmesg`: Shows only kernel messages (similar to `dmesg`).
- `--since "YYYY-MM-DD HH:MM:SS"`: Shows entries on or newer than the specified date.
- `--until "YYYY-MM-DD HH:MM:SS"`: Shows entries on or older than the specified date.
- `-p PRIORITY`, `--priority=PRIORITY`: Filters by message priority (e.g., `err`, `warning`, `info`, `debug` or 0-7).
- `-n LINES`, `--lines=LINES`: Shows the specified number of most recent lines.

**Example:**
```bash
journalctl # Show all logs
journalctl -u nginx.service # Show logs for nginx service
journalctl -f # Follow new log entries
journalctl -b -1 -p err # Show errors from the previous boot
journalctl --since "1 hour ago"
```

## User and Permission Management

### User Management

#### `useradd` / `adduser` - Add New User
> The `useradd` command is a low-level utility for creating new user accounts. `adduser` (common on Debian/Ubuntu) is a friendlier, interactive frontend to `useradd`.

**Syntax (`useradd`):**
```bash
useradd [options] username
```

**Common `useradd` Options:**
- `-m`, `--create-home`: Creates the user's home directory.
- `-d /path/to/home`, `--home /path/to/home`: Specifies the home directory path.
- `-s /path/to/shell`, `--shell /path/to/shell`: Specifies the user's login shell.
- `-g group`, `--gid group`: Specifies the user's primary group (name or GID).
- `-G group1,group2`, `--groups group1,group2`: Specifies supplementary groups.
- `-c "Comment"`, `--comment "Comment"`: Adds a comment (GECOS field), often the user's full name.

**Syntax (`adduser` - interactive):**
```bash
adduser username
```

**Example:**
```bash
sudo useradd -m -s /bin/bash -G sudo,dev newuser # Low-level command
sudo adduser anotheruser # Interactive command (Debian/Ubuntu)
# Don't forget to set a password!
sudo passwd newuser
```

#### `userdel` / `deluser` - Delete User
> The `userdel` command is a low-level utility for deleting user accounts. `deluser` (common on Debian/Ubuntu) is a frontend.

**Syntax (`userdel`):**
```bash
userdel [options] username
```

**Common `userdel` Options:**
- `-r`, `--remove`: Removes the user's home directory and mail spool.

**Syntax (`deluser`):**
```bash
deluser [--remove-home] username
```

**Example:**
```bash
sudo userdel -r olduser # Remove user and their home directory
sudo deluser --remove-home olduser # Debian/Ubuntu equivalent
```

#### `usermod` - Modify User Account
> The `usermod` command modifies existing user account attributes.

**Syntax:**
```bash
usermod [options] username
```

**Common Options:**
- `-d /path/to/home`, `--home /path/to/home`: Changes the user's home directory (use `-m` to move contents).
- `-s /path/to/shell`, `--shell /path/to/shell`: Changes the user's login shell.
- `-g group`, `--gid group`: Changes the user's primary group.
- `-G group1,group2`, `--groups group1,group2`: Sets the user's supplementary groups (overwrites existing list).
- `-aG group1,group2`, `--append --groups group1,group2`: Appends the user to supplementary groups (use with `-G`).
- `-l new_username`, `--login new_username`: Changes the username.
- `-L`, `--lock`: Locks the user's account.
- `-U`, `--unlock`: Unlocks the user's account.

**Example:**
```bash
sudo usermod -s /usr/bin/zsh jdoe # Change shell for jdoe
sudo usermod -aG sudo jdoe # Add jdoe to the sudo group
sudo usermod -L tempuser # Lock account
sudo usermod -l newsmith jsmith # Rename user jsmith to newsmith
```

### Group Management

#### `groupadd` - Add New Group
> The `groupadd` command creates a new group.

**Syntax:**
```bash
groupadd [options] groupname
```

**Options:**
- `-g GID`, `--gid GID`: Specifies the numeric group ID.

**Example:**
```bash
sudo groupadd developers
```

#### `groupdel` - Delete Group
> The `groupdel` command removes a group. You cannot remove the primary group of any existing user.

**Syntax:**
```bash
groupdel groupname
```

**Example:**
```bash
sudo groupdel testers
```

#### `groupmod` - Modify Group
> The `groupmod` command modifies group definitions (name or GID).

**Syntax:**
```bash
groupmod [options] groupname
```

**Options:**
- `-n new_group_name`, `--new-name new_group_name`: Changes the group name.
- `-g new_GID`, `--gid new_GID`: Changes the group ID.

**Example:**
```bash
sudo groupmod -n webdev developers # Rename group developers to webdev
```

### Permission Management

#### `chmod` - Change File Permissions
> The `chmod` command changes the access permissions (mode) of files and directories. Permissions control who can read, write, or execute a file.

**Syntax:**
```bash
chmod [options] mode file...
chmod [options] symbolic_mode file...
```

**Modes:**
- **Octal Mode:** Uses numbers (0-7) to represent permissions for Owner, Group, and Others.
  - `4`: Read (r)
  - `2`: Write (w)
  - `1`: Execute (x)
  - Example: `755` means `rwx` for Owner, `r-x` for Group, `r-x` for Others.
- **Symbolic Mode:** Uses letters to modify permissions.
  - `u` (user/owner), `g` (group), `o` (others), `a` (all)
  - `+` (add), `-` (remove), `=` (set exactly)
  - `r` (read), `w` (write), `x` (execute), `X` (execute only if directory or already executable), `s` (setuid/setgid), `t` (sticky bit)

**Options:**
- `-R`, `--recursive`: Changes permissions recursively for directories and their contents.

**Example:**
```bash
chmod 755 script.sh # Owner: rwx, Group: r-x, Others: r-x
chmod 644 data.txt # Owner: rw-, Group: r--, Others: r--
chmod u+x my_script.py # Add execute permission for the owner
chmod g-w shared_file # Remove write permission for the group
chmod o=r public_doc # Set others' permission to read-only
chmod -R 775 /var/www/html/project # Recursively set permissions
```

#### `chown` - Change File Owner and Group
> The `chown` command changes the user and/or group ownership of files and directories.

**Syntax:**
```bash
chown [options] owner[:group] file...
```

**Options:**
- `-R`, `--recursive`: Changes ownership recursively for directories and their contents.
- `--from=current_owner:current_group`: Changes ownership only if the file matches the current owner/group.

**Example:**
```bash
sudo chown jdoe report.txt # Change owner to jdoe
sudo chown jdoe:developers project_file # Change owner to jdoe and group to developers
sudo chown :admin config.ini # Change only the group to admin
sudo chown -R www-data:www-data /var/www/my_app # Recursively change ownership for web server
```

#### `chgrp` - Change Group Ownership
> The `chgrp` command changes the group ownership of files and directories. It's a subset of `chown`'s functionality.

**Syntax:**
```bash
chgrp [options] group file...
```

**Options:**
- `-R`, `--recursive`: Changes group ownership recursively.

**Example:**
```bash
sudo chgrp editors draft.doc
sudo chgrp -R developers /srv/git/project.git
```

## Networking and Communication

### Network Configuration

#### `ping` - Test Network Connectivity
> The `ping` command sends ICMP ECHO_REQUEST packets to network hosts to test reachability and measure round-trip time.

**Syntax:**
```bash
ping [options] host
```

**Options:**
- `-c count`: Stops after sending `count` packets.
- `-i interval`: Waits `interval` seconds between sending each packet (default is 1 second).
- `-s packetsize`: Specifies the number of data bytes to be sent.
- `-W timeout`: Time to wait for a response, in seconds.

**Example:**
```bash
ping google.com
ping -c 5 192.168.1.1 # Send 5 pings to the gateway
```

#### `ifconfig` - Configure Network Interfaces (Legacy)
> The `ifconfig` command displays or configures network interfaces. **Note:** It's considered legacy on many modern Linux systems, replaced by the `ip` command. However, it's still found and used. (May need installation: `sudo apt install net-tools` or `sudo yum install net-tools`).

**Syntax:**
```bash
ifconfig [interface] [options]
```

**Example:**
```bash
ifconfig # Display all active interfaces
ifconfig eth0 # Display configuration for eth0
sudo ifconfig eth0 192.168.1.100 netmask 255.255.255.0 up # Configure eth0 (temporary)
sudo ifconfig eth0 down # Disable eth0
```

#### `ip` - Show/Manipulate Routing, Devices, Policy Routing (Modern)
> The `ip` command is the modern, powerful tool for managing network interfaces, IP addresses, routing tables, ARP cache, and more. It replaces older tools like `ifconfig`, `route`, and `arp`.

**Syntax:**
```bash
ip [OPTIONS] OBJECT {COMMAND | help}
```

**Common Objects:**
- `link` (or `l`): Network device configuration (`ip link show`, `ip link set dev eth0 up`).
- `addr` (or `a`): Protocol (IP, IPv6) addresses on devices (`ip addr show`, `ip addr add 192.168.1.50/24 dev eth0`).
- `route` (or `r`): Routing table (`ip route show`, `ip route add default via 192.168.1.1`).
- `neigh` (or `n`): ARP or NDISC cache (`ip neigh show`).

**Example:**
```bash
ip addr show # Show IP addresses for all interfaces (similar to ifconfig)
ip link show # Show interface status
sudo ip link set eth0 up # Enable interface eth0
sudo ip link set eth0 down # Disable interface eth0
ip route show # Show the routing table (similar to route -n)
sudo ip addr add 10.0.0.10/24 dev eth1 # Add an IP address to eth1
sudo ip route add 192.168.5.0/24 via 10.0.0.1 # Add a static route
```

### Network Diagnostics

#### `netstat` - Network Statistics (Legacy)
> The `netstat` command displays network connections (incoming and outgoing), routing tables, interface statistics, masquerade connections, multicast memberships, etc. **Note:** Largely replaced by `ss` and `ip` on modern systems. (May need installation: `sudo apt install net-tools` or `sudo yum install net-tools`).

**Syntax:**
```bash
netstat [options]
```

**Common Options:**
- `-t`: Shows TCP connections.
- `-u`: Shows UDP connections.
- `-l`: Shows listening sockets.
- `-n`: Shows numerical addresses (doesn't resolve hostnames).
- `-p`: Shows the PID and name of the program to which each socket belongs (requires root).
- `-a`: Shows both listening and non-listening sockets.
- `-r`: Shows the kernel routing table (similar to `route -n`).
- `-i`: Shows network interface statistics.

**Example:**
```bash
netstat -tulnp # Show listening TCP/UDP ports and associated programs
netstat -rn # Show routing table
netstat -i # Show interface statistics
```

#### `ss` - Socket Statistics (Modern)
> The `ss` command is a utility to investigate sockets. It's the modern replacement for `netstat`, providing more detailed information and generally performing faster.

**Syntax:**
```bash
ss [options] [filter]
```

**Common Options:**
- `-t`: Display TCP sockets.
- `-u`: Display UDP sockets.
- `-l`: Display listening sockets.
- `-n`: Do not resolve service names (show port numbers).
- `-p`: Show process using socket.
- `-a`: Display all sockets (listening and established).
- `-r`: Resolve host names.
- `-e`: Show detailed socket information.
- `-i`: Show internal TCP information.

**Example:**
```bash
ss -tulnp # Show listening TCP/UDP ports and associated programs (similar to netstat -tulnp)
ss -tan # Show all TCP connections with numeric ports/addresses
ss -tun state established # Show established UDP connections
ss -tp | grep sshd # Show processes using SSH sockets
```

#### `traceroute` / `tracepath` - Trace Network Path
> The `traceroute` command prints the route packets trace to a network host. `tracepath` is a similar tool often available by default and doesn't usually require root privileges.

**Syntax (`traceroute`):**
```bash
traceroute [options] host
```
**Syntax (`tracepath`):**
```bash
tracepath [options] host
```

**Common `traceroute` Options:**
- `-n`: Do not resolve IP addresses to hostnames.
- `-I`: Use ICMP ECHO for probes (instead of UDP).
- `-T`: Use TCP SYN for probes.

**Example:**
```bash
traceroute google.com
tracepath example.org
sudo traceroute -T -p 80 www.example.com # Trace using TCP SYN packets to port 80
```

#### `dig` - DNS Lookup Utility
> The `dig` (Domain Information Groper) command is a flexible tool for interrogating DNS name servers. It performs DNS lookups and displays the answers.

**Syntax:**
```bash
dig [@server] [options] name [type]
```

**Common Options:**
- `+short`: Provides a short answer (just the IP address or record data).
- `+trace`: Traces the delegation path from the root name servers.
- `ANY`: Queries for any record type.
- `MX`: Queries for Mail Exchanger records.
- `NS`: Queries for Name Server records.
- `SOA`: Queries for Start of Authority records.
- `-x addr`: Performs a reverse DNS lookup (find hostname for an IP address).

**Example:**
```bash
dig example.com
dig example.com MX
dig @8.8.8.8 www.google.com A # Query Google's DNS server for A record
dig +short myip.opendns.com @resolver1.opendns.com # Find your public IP
dig -x 192.0.2.1 # Reverse lookup
dig example.com +trace
```

### File Transfer

#### `scp` - Secure Copy (Remote File Copy)
> The `scp` command securely copies files between hosts on a network using the SSH protocol for authentication and encryption.

**Syntax:**
```bash
scp [options] [[user@]host1:]file1 [[user@]host2:]file2
```

**Options:**
- `-r`: Recursively copies entire directories.
- `-P port`: Specifies the port to connect to on the remote host.
- `-p`: Preserves modification times, access times, and modes from the original file.
- `-C`: Enables compression.
- `-i identity_file`: Selects the file from which the identity (private key) for public key authentication is read.

**Example:**
```bash
# Copy local file to remote host
scp local_file.txt remote_user@remote_host:/remote/directory/

# Copy remote file to local host
scp remote_user@remote_host:/path/to/remote_file.zip .

# Copy directory recursively from local to remote
scp -r local_folder/ remote_user@remote_host:/remote/backup/

# Copy file using a specific port and private key
scp -P 2222 -i ~/.ssh/id_rsa data.csv user@server:/data/
```

#### `wget` - Non-interactive Network Downloader
> The `wget` command is a free utility for non-interactive download of files from the Web. It supports HTTP, HTTPS, and FTP protocols, as well as retrieval through HTTP proxies.

**Syntax:**
```bash
wget [options] [URL...]
```

**Options:**
- `-c`, `--continue`: Resumes getting a partially-downloaded file.
- `-r`, `--recursive`: Downloads recursively (follows links).
- `-l depth`, `--level=depth`: Specifies recursion maximum depth level.
- `-np`, `--no-parent`: Doesn't ascend to the parent directory when retrieving recursively.
- `-O file`, `--output-document=file`: Writes documents to `file`.
- `-P prefix`, `--directory-prefix=prefix`: Saves files to `prefix`/....
- `--limit-rate=amount`: Limits the download speed (e.g., `--limit-rate=100k`).
- `-U agent-string`, `--user-agent=agent-string`: Identifies as `agent-string` instead of Wget/version.

**Example:**
```bash
wget https://example.com/archive.zip
wget -c https://example.com/large_file.iso # Resume download
wget -r -np -l 1 https://example.com/docs/ # Download files from one directory level
wget -O webpage.html https://example.com/index.html
```

#### `curl` - Transfer Data with URLs
> The `curl` command is a versatile tool to transfer data from or to a server, using one of the many supported protocols (DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, POP3, POP3S, RTMP, RTSP, SCP, SFTP, SMB, SMBS, SMTP, SMTPS, TELNET, TFTP). Often used for testing APIs.

**Syntax:**
```bash
curl [options] [URL...]
```

**Options:**
- `-O`, `--remote-name`: Writes output to a local file named like the remote file.
- `-o file`, `--output file`: Writes output to `file` instead of stdout.
- `-L`, `--location`: Follows redirects.
- `-X METHOD`, `--request METHOD`: Specifies request method (e.g., GET, POST, PUT, DELETE).
- `-H "Header: Value"`, `--header "Header: Value"`: Passes custom header(s) to server.
- `-d 'data'`, `--data 'data'`: Sends the specified data in a POST request (HTTP).
- `-u user:password`, `--user user:password`: Specifies the user and password to use for server authentication.
- `-I`, `--head`: Fetches the headers only (HTTP/FTP/FILE).
- `-k`, `--insecure`: Allows insecure server connections when using SSL.

**Example:**
```bash
curl https://example.com # Display content of URL
curl -O https://example.com/file.tar.gz # Download file, save with remote name
curl -o local_name.jpg https://example.com/image.jpeg # Download and save with specific name
curl -L https://short.url/resource # Follow redirects
curl -X POST -H "Content-Type: application/json" -d '{"key":"value"}' https://api.example.com/submit
curl -I https://example.com # Show only headers
```

## Disk and File System Utilities

### File System Management

#### `mount` - Mount File Systems
> The `mount` command attaches a file system located on a device (like a hard drive partition, CD-ROM, or network share) to a specified directory (mount point) in the main file system hierarchy, making it accessible.

**Syntax:**
```bash
mount [options] device directory
mount -t type [options] device directory
```

**Options:**
- `-t type`, `--types type`: Specifies the file system type (e.g., `ext4`, `vfat`, `ntfs`, `nfs`, `cifs`). Often auto-detected.
- `-o options`, `--options options`: Specifies mount options (comma-separated, e.g., `ro` for read-only, `rw` for read-write, `uid=1000`, `gid=1000`).
- `-a`, `--all`: Mounts all file systems mentioned in `/etc/fstab`.

**Example:**
```bash
sudo mount /dev/sdb1 /mnt/usb_drive # Mount USB drive partition
sudo mount -t ntfs-3g /dev/sda5 /mnt/windows # Mount Windows NTFS partition (requires ntfs-3g)
sudo mount -t cifs //server/share /mnt/samba -o username=user,password=pass # Mount Samba/CIFS share
sudo mount -o remount,ro / # Remount root filesystem as read-only
mount # Display currently mounted filesystems
```

#### `umount` - Unmount File Systems
> The `umount` command detaches (unmounts) a mounted file system from the directory tree. It's crucial to unmount file systems before physically disconnecting the device to prevent data loss or corruption.

**Syntax:**
```bash
umount [options] directory
umount [options] device
```

**Options:**
- `-f`, `--force`: Forces unmount (e.g., in case of unresponsive NFS system). Use with caution.
- `-l`, `--lazy`: Lazy unmount. Detaches the filesystem now, and cleans up references later.

**Example:**
```bash
sudo umount /mnt/usb_drive
sudo umount /dev/sdb1
sudo umount -l /mnt/busy_mount # Lazy unmount if device is busy
```

#### `df` - Disk Free (Report File System Disk Space Usage)
> The `df` command reports the amount of disk space used and available on file systems.

**Syntax:**
```bash
df [options] [file...]
```

**Options:**
- `-h`, `--human-readable`: Prints sizes in powers of 1024 (e.g., 1K, 234M, 2G).
- `-H`, `--si`: Prints sizes in powers of 1000 (e.g., 1.1k, 245M, 2.2G).
- `-T`, `--print-type`: Prints the file system type.
- `-i`, `--inodes`: Lists inode information instead of block usage.
- `--total`: Produces a grand total.

**Example:**
```bash
df -h # Show usage for all mounted filesystems in human-readable format
df -hT # Include filesystem type
df -i /home # Show inode usage for the filesystem containing /home
```

#### `du` - Disk Usage (Estimate File Space Usage)
> The `du` command estimates file space usage for files and directories.

**Syntax:**
```bash
du [options] [file...]
```

**Options:**
- `-h`, `--human-readable`: Prints sizes in human-readable format.
- `-s`, `--summarize`: Displays only a total for each argument.
- `-c`, `--total`: Produces a grand total.
- `-a`, `--all`: Writes counts for all files, not just directories.
- `--max-depth=N`: Prints the total for a directory (or file, with `-a`) only if it is `N` or fewer levels below the command line argument. `--max-depth=1` summarizes usage in the current directory.

**Example:**
```bash
du -h /path/to/directory # Show disk usage for directory and subdirectories
du -sh /path/to/directory # Show summarized total size for the directory
du -h --max-depth=1 . # Show usage for files and directories in the current level
du -ah . # Show usage for all files and directories in current path
```

### Partition Management

#### `fdisk` - Manipulate Disk Partition Table
> The `fdisk` command is a dialog-driven program for creating and manipulating partition tables (MBR, GPT, etc.) on hard disk drives. **Use with extreme caution, as incorrect use can lead to data loss.**

**Syntax:**
```bash
fdisk [options] device
```

**Options:**
- `-l [device...]`, `--list [device...]`: Lists the partition tables for the specified devices and then exits.

**Interactive Commands (within `fdisk`):**
- `p`: Print the partition table.
- `n`: Add a new partition.
- `d`: Delete a partition.
- `t`: Change a partition's system ID.
- `w`: Write table to disk and exit.
- `q`: Quit without saving changes.
- `m`: Print help menu.

**Example:**
```bash
sudo fdisk -l # List partitions on all disks
sudo fdisk /dev/sda # Start interactive partitioning for /dev/sda
```

#### `mkfs` - Build a Linux File System
> The `mkfs` command is used to build (format) a Linux file system on a device, usually a disk partition. It's a frontend for various specific `mkfs.*` utilities (e.g., `mkfs.ext4`, `mkfs.xfs`, `mkfs.vfat`).

**Syntax:**
```bash
mkfs [options] [-t type] device [size]
mkfs.type [options] device [size] # Specific type syntax
```

**Options:**
- `-t type`, `--type type`: Specifies the type of file system to build (e.g., `ext4`, `xfs`, `vfat`).
- Specific options depend on the file system type (e.g., `-L label` for setting a volume label on ext*).

**Example:**
```bash
sudo mkfs -t ext4 /dev/sdb1 # Format /dev/sdb1 with ext4
sudo mkfs.ext4 -L DATA /dev/sdb1 # Format with ext4 and set label to DATA
sudo mkfs.vfat /dev/sdc1 # Format /dev/sdc1 with FAT32 (VFAT)
```

#### `fsck` - File System Check and Repair
> The `fsck` command checks and optionally repairs one or more Linux file systems. It's typically run automatically at boot time if errors are suspected, but can be run manually on unmounted file systems. **Never run `fsck` on a mounted file system.**

**Syntax:**
```bash
fsck [options] [-t type] device
```

**Options:**
- `-t type`, `--type type`: Specifies the file system type(s) to check.
- `-A`: Checks all file systems listed in `/etc/fstab`.
- `-y`: Assumes "yes" to all questions asked by `fsck`; use with caution.
- `-f`: Forces checking even if the file system seems clean.
- `-p`: Automatically repairs the file system without any questions (use carefully).

**Example:**
```bash
# First, ensure the filesystem is unmounted
sudo umount /dev/sdb1

# Then, check the filesystem
sudo fsck /dev/sdb1
sudo fsck -t ext4 /dev/sdb1 # Specify type
sudo fsck -y /dev/sdb1 # Check and automatically attempt repairs
```

## Compression and Archiving

#### `tar` - Tape Archive Utility
> The `tar` command creates, extracts, and manages archive files (often called tarballs). It can bundle multiple files and directories into a single file, optionally compressing it.

**Syntax:**
```bash
tar [options] [archive-file] [file or directory...]
```

**Common Operations (Mode Flags - only one):**
- `-c`, `--create`: Creates a new archive.
- `-x`, `--extract`, `--get`: Extracts files from an archive.
- `-t`, `--list`: Lists the contents of an archive.
- `-u`, `--update`: Appends files that are newer than those in the archive.
- `-r`, `--append`: Appends files to the end of an archive.

**Common Options:**
- `-f file`, `--file=file`: Specifies the archive file name. **Essential for most operations.**
- `-v`, `--verbose`: Lists files processed.
- `-z`, `--gzip`: Filters the archive through `gzip` for compression/decompression (`.tar.gz` or `.tgz`).
- `-j`, `--bzip2`: Filters the archive through `bzip2` for compression/decompression (`.tar.bz2`).
- `-J`, `--xz`: Filters the archive through `xz` for compression/decompression (`.tar.xz`).
- `-C directory`, `--directory=directory`: Changes to `directory` before performing operations.

**Example:**
```bash
# Create an uncompressed archive
tar -cvf archive.tar directory/ file1.txt

# List contents of an archive
tar -tvf archive.tar

# Extract files from an archive
tar -xvf archive.tar

# Create a gzip compressed archive
tar -czvf archive.tar.gz directory/

# Extract from a gzip compressed archive
tar -xzvf archive.tar.gz

# Create a bzip2 compressed archive
tar -cjvf archive.tar.bz2 directory/

# Extract from a bzip2 compressed archive
tar -xjvf archive.tar.bz2

# Extract specific files to a different directory
tar -xvf archive.tar -C /path/to/extract/to file1.txt path/in/archive/file2.txt
```

#### `gzip` / `gunzip` - Compress or Expand Files (GNU Zip)
> The `gzip` command compresses files using Lempel-Ziv (LZ77) coding. By default, it replaces the original file with a compressed version (`.gz` extension). `gunzip` decompresses `.gz` files.

**Syntax:**
```bash
gzip [options] [files...]
gunzip [options] [files...]
```

**Options:**
- `-d`, `--decompress`: Decompresses (same as `gunzip`).
- `-k`, `--keep`: Keeps (does not delete) input files during compression or decompression.
- `-r`, `--recursive`: Recursively compresses/decompresses files in directories.
- `-l`, `--list`: Lists compressed file contents (size, ratio, name).
- `-c`, `--stdout`: Writes output on standard output; keeps original files unchanged.

**Example:**
```bash
gzip large_log_file.log # Creates large_log_file.log.gz, deletes original
gunzip large_log_file.log.gz # Restores original, deletes .gz file
gzip -k data.txt # Creates data.txt.gz, keeps data.txt
cat file.txt | gzip -c > file.txt.gz # Compress using pipe, keep original
gunzip -c file.txt.gz > file.txt # Decompress using pipe, keep .gz file
```

#### `zip` / `unzip` - Package and Compress Files (ZIP format)
> The `zip` command packages and compresses files into a `.zip` archive, compatible with PKZIP (common on Windows). `unzip` extracts files from `.zip` archives. (May need installation: `sudo apt install zip unzip` or `sudo yum install zip unzip`).

**Syntax (`zip`):**
```bash
zip [options] zipfile files...
```
**Syntax (`unzip`):**
```bash
unzip [options] zipfile [files...] [-d exdir]
```

**Common `zip` Options:**
- `-r`: Recursively includes directories and their contents.
- `-e`: Encrypts the contents of the zip archive (prompts for password).
- `-9`: Use highest compression level.
- `-u`: Updates existing entries or adds new files.

**Common `unzip` Options:**
- `-l`: Lists archive contents without extracting.
- `-d exdir`: Extracts files into the specified directory `exdir`.
- `-o`: Overwrites existing files without prompting.
- `-n`: Never overwrites existing files.

**Example:**
```bash
zip archive.zip file1.txt file2.jpg # Create zip with specific files
zip -r documents.zip Documents/ # Recursively zip a directory
unzip archive.zip # Extract files to current directory
unzip documents.zip -d /path/to/extract # Extract to a specific directory
unzip -l archive.zip # List contents
```

## Process Management

### Process Control

#### `kill` - Send a Signal to a Process
> The `kill` command sends a specified signal to a process identified by its Process ID (PID). The default signal sent is SIGTERM (15), which requests graceful termination.

**Syntax:**
```bash
kill [options] pid...
```

**Options:**
- `-l [signal]`, `--list[=signal]`: Lists signal names, or converts signal number to name.
- `-s signal`, `--signal signal`: Specifies the signal to send (name or number).
- Common Signals:
  - `1` or `SIGHUP`: Hangup (often used to reload configuration).
  - `9` or `SIGKILL`: Kill (forceful, immediate termination; process cannot catch this).
  - `15` or `SIGTERM`: Terminate (graceful termination request; default).

**Example:**
```bash
kill 12345 # Send SIGTERM to process 12345
kill -9 12345 # Send SIGKILL (force kill) to process 12345
kill -HUP 54321 # Send SIGHUP (hangup) to process 54321
kill -l # List all available signals
```

#### `pkill` / `killall` - Send Signal Based on Name/Attributes
> The `pkill` command sends signals to processes based on name or other attributes. `killall` is similar but typically matches the exact command name.

**Syntax (`pkill`):**
```bash
pkill [options] pattern
```
**Syntax (`killall`):**
```bash
killall [options] name...
```

**Common `pkill` Options:**
- `-u user`, `--uid user`: Matches processes owned by the specified user.
- `-f`, `--full`: Matches the pattern against the full argument list (command + arguments).
- `-x`, `--exact`: Matches exactly with the process name.
- `-signal`: Specifies the signal to send (e.g., `-9` for SIGKILL).

**Common `killall` Options:**
- `-u user`: Kill processes owned by `user`.
- `-i`, `--interactive`: Ask for confirmation before killing.
- `-e`, `--exact`: Require exact match for very long names.
- `-signal`: Specifies the signal to send.

**Example:**
```bash
pkill firefox # Send SIGTERM to all processes matching "firefox"
pkill -9 -f "python backup_script.py" # Force kill process matching full command
pkill -u baduser # Kill all processes owned by baduser
killall nginx # Send SIGTERM to all processes named exactly "nginx"
sudo killall -HUP dnsmasq # Reload dnsmasq configuration
```

#### `nice` / `renice` - Run/Alter Process Scheduling Priority
> The `nice` command runs a command with a modified scheduling priority ("niceness"). Higher niceness values (up to 19) mean lower priority. `renice` alters the priority of running processes.

**Syntax (`nice`):**
```bash
nice [option] [command [arguments]]
```
**Syntax (`renice`):**
```bash
renice [-n] priority [-p pid...] [-g pgrp...] [-u user...]
```

**Options/Values:**
- **Niceness:** Ranges from -20 (highest priority, requires root) to 19 (lowest priority). Default is 0.
- `nice -n value`: Sets niceness value for the new command.
- `renice priority`: Sets the niceness for existing processes/groups/users.

**Example:**
```bash
nice -n 10 ./cpu_intensive_task # Run task with lower priority (niceness 10)
sudo nice -n -10 ./important_task # Run task with higher priority (niceness -10)
renice 15 -p 12345 # Lower priority of process 12345
sudo renice -5 -u apache # Increase priority for all processes owned by apache
```

### Job Control (Shell Built-ins)

> Job control allows you to manage multiple processes within a single shell session. These are typically shell built-in commands (bash, zsh, etc.).

#### `jobs` - List Active Jobs
> The `jobs` command lists the processes ("jobs") that have been started in the current shell session and are running in the background or stopped.

**Syntax:**
```bash
jobs [options] [jobspec...]
```

**Options:**
- `-l`: Lists process IDs in addition to the normal information.
- `-p`: Lists process IDs only.
- `-s`: Lists only stopped jobs.
- `-r`: Lists only running jobs.

**Example:**
```bash
# Start a job in the background
sleep 60 &
[1] 12345

# Stop a foreground job (Ctrl+Z)
vim large_file.txt
^Z
[2]+  Stopped                 vim large_file.txt

# List jobs
jobs
[1]-  Running                 sleep 60 &
[2]+  Stopped                 vim large_file.txt

jobs -l
[1]-  12345 Running                 sleep 60 &
[2]+  12346 Stopped                 vim large_file.txt
```

#### `bg` - Run Job in the Background
> The `bg` command resumes a stopped job and runs it in the background.

**Syntax:**
```bash
bg [jobspec]
```
- `jobspec`: Job identifier (e.g., `%1`, `%2`). If omitted, uses the most recently stopped job.

**Example:**
```bash
# Assuming job 2 (vim) is stopped
bg %2
[2]+ vim large_file.txt &
```

#### `fg` - Bring Job to the Foreground
> The `fg` command brings a background or stopped job to the foreground, making it the active process interacting with the terminal.

**Syntax:**
```bash
fg [jobspec]
```
- `jobspec`: Job identifier (e.g., `%1`, `%sleep`). If omitted, uses the most recently backgrounded/stopped job.

**Example:**
```bash
# Assuming job 1 (sleep) is running in the background
fg %1
sleep 60
# (Now running in foreground, Ctrl+C to interrupt)
```

## System Configuration and Settings

### Configuration Management

#### `crontab` - Schedule Periodic Tasks
> The `crontab` command manages crontab files, which contain schedules for running commands or scripts automatically at specified times or intervals. Each user can have their own crontab.

**Syntax:**
```bash
crontab [options] [file]
```

**Options:**
- `-e`: Edits the current user's crontab file (usually opens in the default editor).
- `-l`: Lists the current user's crontab entries.
- `-r`: Removes the current user's crontab file.
- `-u user`: Specifies the user whose crontab is to be managed (requires root).

**Crontab Format (Fields):**
```
# ┌───────────── minute (0 - 59)
# │ ┌───────────── hour (0 - 23)
# │ │ ┌───────────── day of month (1 - 31)
# │ │ │ ┌───────────── month (1 - 12)
# │ │ │ │ ┌───────────── day of week (0 - 6) (Sunday=0 or 7)
# │ │ │ │ │
# * * * * * command_to_execute
```
- `*`: Matches any value.
- `,`: Separates multiple values (e.g., `0,15,30,45`).
- `-`: Defines a range (e.g., `1-5`).
- `/`: Specifies step values (e.g., `*/15` for every 15 minutes).

**Example:**
```bash
# Edit your crontab
crontab -e

# Example crontab entry: Run backup script every day at 2:30 AM
# 30 2 * * * /home/user/scripts/backup.sh

# List your crontab
crontab -l

# Remove your crontab
crontab -r

# Edit crontab for user 'www-data' (as root)
sudo crontab -u www-data -e
```

#### `systemctl` - Control the systemd System and Service Manager
> The `systemctl` command is the primary tool for introspecting and controlling the state of the `systemd` system and service manager. Used for managing services (starting, stopping, enabling, disabling), viewing logs, system state, etc.

**Syntax:**
```bash
systemctl [options] command [unit...]
```

**Common Commands:**
- `start unit`: Starts (activates) one or more units.
- `stop unit`: Stops (deactivates) one or more units.
- `restart unit`: Stops and then starts one or more units.
- `reload unit`: Asks units to reload their configuration.
- `status [unit...]`: Shows runtime status information about one or more units.
- `enable unit`: Enables one or more units to start on boot.
- `disable unit`: Disables one or more units from starting on boot.
- `is-active unit`: Checks if a unit is currently active.
- `is-enabled unit`: Checks if a unit is enabled for startup on boot.
- `list-units [--type=service|socket...] [--all]`: Lists loaded units.
- `list-unit-files`: Lists installed unit files and their enablement state.
- `daemon-reload`: Reloads the systemd manager configuration (needed after modifying unit files).

**Example:**
```bash
sudo systemctl start nginx.service # Start nginx
sudo systemctl stop apache2.service # Stop apache2
sudo systemctl restart sshd.service # Restart sshd
sudo systemctl status cron.service # Check status of cron
sudo systemctl enable ufw.service # Enable firewall on boot
sudo systemctl disable bluetooth.service # Disable bluetooth on boot
systemctl is-active httpd # Check if httpd is running
systemctl list-units --type=service --state=running # List running services
```

#### `timedatectl` - Control System Time and Date
> The `timedatectl` command allows you to query and change the system clock and its settings. It interacts with `systemd-timesyncd` or other NTP services.

**Syntax:**
```bash
timedatectl [options] [command]
```

**Commands:**
- `status`: Shows current time settings (time, timezone, NTP sync status).
- `set-time "YYYY-MM-DD HH:MM:SS"`: Sets the system clock (requires NTP sync off).
- `set-timezone TIMEZONE`: Sets the system timezone (e.g., `America/New_York`, `Europe/London`). List with `timedatectl list-timezones`.
- `set-ntp true|false`: Enables or disables network time synchronization.

**Example:**
```bash
timedatectl status # Show current settings
timedatectl list-timezones | grep London # Find timezone
sudo timedatectl set-timezone Europe/London # Set timezone
sudo timedatectl set-ntp true # Enable NTP synchronization
# sudo timedatectl set-time "2023-10-27 10:00:00" # Manually set time (if NTP is off)
```

## Package Management

### Debian-based Systems (Ubuntu, Debian, Mint)

#### `apt` - Advanced Package Tool (High-Level)
> The `apt` command is the recommended high-level command-line interface for managing packages on Debian-based systems. It provides necessary options for package installation, removal, updates, and queries.

**Syntax:**
```bash
apt [options] command [package...]
```

**Common Commands:**
- `update`: Retrieves updated package lists from repositories. Run this before `upgrade` or `install`.
- `upgrade`: Installs the newest versions of all packages currently installed.
- `full-upgrade`: Performs `upgrade` but may remove installed packages if required to upgrade the system as a whole.
- `install package...`: Installs one or more packages.
- `remove package...`: Removes packages but leaves configuration files.
- `purge package...`: Removes packages and their configuration files.
- `autoremove`: Removes packages that were automatically installed to satisfy dependencies for other packages and are now no longer needed.
- `search term...`: Searches for packages containing `term` in their name or description.
- `show package`: Shows detailed information about a package.
- `list [--installed | --upgradable]`: Lists packages.

**Example:**
```bash
sudo apt update
sudo apt upgrade
sudo apt install curl git vim
sudo apt remove old-package
sudo apt purge unused-config-package
sudo apt autoremove
apt search web server
apt show nginx
apt list --installed
```

#### `apt-get` - Package Handling Utility (Lower-Level)
> The `apt-get` command is another command-line tool for handling packages. It's older than `apt` and often used in scripts due to its stable interface, but `apt` is generally preferred for interactive use. Functionality largely overlaps with `apt`.

**Syntax:**
```bash
apt-get [options] command [package...]
```

**Common Commands:** (Similar to `apt`: `update`, `upgrade`, `install`, `remove`, `purge`, `autoremove`)

**Example:**
```bash
sudo apt-get update
sudo apt-get install htop
sudo apt-get remove nano
```

#### `dpkg` - Debian Package Manager (Lowest-Level)
> The `dpkg` command is the low-level tool that forms the base of the Debian package management system. It directly installs, removes, and provides information about `.deb` packages but doesn't handle dependencies automatically.

**Syntax:**
```bash
dpkg [options] action
```

**Common Actions:**
- `-i file.deb`, `--install file.deb`: Installs a package file.
- `-r package`, `--remove package`: Removes an installed package (leaves config files).
- `-P package`, `--purge package`: Purges an installed package (removes config files).
- `-l [pattern]`, `--list [pattern]`: Lists installed packages matching `pattern`.
- `-s package`, `--status package`: Shows the status of a package.
- `-L package`, `--listfiles package`: Lists files installed by `package`.
- `-S pattern`, `--search pattern`: Searches for a filename within installed packages.
- `--configure package | -a`: Configures an unpacked but unconfigured package (or all such packages with `-a`).

**Example:**
```bash
sudo dpkg -i downloaded_package.deb # Install a downloaded .deb file
dpkg -l | grep zip # List installed packages related to zip
dpkg -s bash # Show status of the bash package
dpkg -L coreutils # List files installed by coreutils
sudo dpkg -r old-app # Remove package
sudo dpkg --configure -a # Fix potentially broken installs
```

### Red Hat-based Systems (CentOS, Fedora, RHEL)

#### `dnf` - Dandified Yum (Modern Default)
> The `dnf` command is the modern package manager for RPM-based distributions like Fedora, CentOS 8+, and RHEL 8+. It's the successor to `yum` with improved dependency resolution and performance.

**Syntax:**
```bash
dnf [options] command [package...]
```

**Common Commands:**
- `install package...`: Installs one or more packages.
- `remove package...`: Removes packages.
- `update [package...]`: Updates specified packages or all packages if none specified.
- `upgrade [package...]`: Similar to `update`, but may handle obsoletes differently. Often used interchangeably.
- `check-update`: Checks if updates are available.
- `autoremove`: Removes unused dependency packages.
- `search term...`: Searches package names and summaries for `term`.
- `info package`: Shows detailed information about a package.
- `list [installed | available | updates]`: Lists packages.
- `provides file_path`: Finds which package provides a specific file.
- `history`: Shows transaction history. `dnf history undo <id>` can revert transactions.

**Example:**
```bash
sudo dnf update
sudo dnf install httpd php
sudo dnf remove mariadb-server
sudo dnf autoremove
dnf search ftp server
dnf info openssh-server
dnf list installed
sudo dnf provides /usr/bin/vim
sudo dnf history
```

#### `yum` - Yellowdog Updater Modified (Older Default)
> The `yum` command was the default package manager for older RPM-based systems like CentOS 7 and earlier RHEL versions. While largely replaced by `dnf`, it shares many similar commands.

**Syntax:**
```bash
yum [options] command [package...]
```

**Common Commands:** (Very similar to `dnf`: `install`, `remove`, `update`, `search`, `info`, `list`, `provides`, `history`)

**Example:**
```bash
sudo yum update
sudo yum install wget
sudo yum remove telnet
yum search mail server
yum list available
```

#### `rpm` - RPM Package Manager (Low-Level)
> The `rpm` command is the low-level utility for managing `.rpm` package files directly. Like `dpkg`, it doesn't handle dependencies automatically.

**Syntax:**
```bash
rpm [options] [package...]
```

**Common Modes/Options:**
- `-i file.rpm`, `--install file.rpm`: Installs an RPM file. Use `-U` (upgrade) generally, as it installs or upgrades.
- `-U file.rpm`, `--upgrade file.rpm`: Upgrades or installs an RPM file.
- `-e package_name`, `--erase package_name`: Uninstalls (erases) a package.
- `-q package_name`, `--query package_name`: Queries if a package is installed.
- `-qa`, `--query --all`: Lists all installed packages.
- `-qi package_name`: Shows information about an installed package.
- `-ql package_name`: Lists files owned by an installed package.
- `-qf /path/to/file`, `--query --file /path/to/file`: Finds which installed package owns a file.
- `-V package_name`, `--verify package_name`: Verifies an installed package against the RPM database (checks for changed files).

**Example:**
```bash
sudo rpm -Uvh downloaded_package.rpm # Install or upgrade RPM with verbose output and hash marks
rpm -qa | grep kernel # List installed kernel packages
rpm -qi bash # Show info about bash package
rpm -ql coreutils # List files in coreutils package
rpm -qf /etc/hosts # Find package owning /etc/hosts
sudo rpm -e old-software # Uninstall package
```

### Arch Linux

#### `pacman` - Package Manager
> The `pacman` command is the package manager for Arch Linux and its derivatives (like Manjaro). It combines a simple binary package format with an easy-to-use build system (ABS).

**Syntax:**
```bash
pacman <operation> [options] [targets...]
```

**Common Operations:**
- `-S`, `--sync`: Synchronizes packages. Used with targets to install or upgrade.
  - `pacman -S package...`: Installs specific package(s).
  - `pacman -Syu`: Synchronizes repositories and upgrades all outdated packages. (**Standard update command**).
  - `pacman -Ss term...`: Searches repositories for packages matching `term`.
  - `pacman -Si package`: Shows detailed info about a repository package.
- `-R`, `--remove`: Removes package(s).
  - `pacman -R package`: Removes package, keeping dependencies.
  - `pacman -Rs package`: Removes package and its unneeded dependencies.
  - `pacman -Rns package`: Removes package, unneeded dependencies, and configuration files (`n`).
- `-Q`, `--query`: Queries the local package database.
  - `pacman -Q [package]`: Checks if package is installed (or lists all if no package given).
  - `pacman -Qi package`: Shows info about an installed package.
  - `pacman -Ql package`: Lists files owned by an installed package.
  - `pacman -Qo /path/to/file`: Shows which package owns a file.
  - `pacman -Qdt`: Lists orphaned packages (installed as dependencies but no longer needed).
- `-U`, `--upgrade`: Installs a downloaded `.pkg.tar.xz` package file.

**Example:**
```bash
sudo pacman -Syu # Update system (IMPORTANT: Always sync before install)
sudo pacman -S firefox neovim
sudo pacman -Ss browser # Search for browsers
pacman -Qi bash # Show info about installed bash package
sudo pacman -Rsn $(pacman -Qdtq) # Remove orphaned packages and their configs (be careful)
sudo pacman -U /path/to/downloaded.pkg.tar.xz # Install local package file
```

## Scripting and Programming

### Shell Scripting

#### `bash` - Bourne Again SHell
> The `bash` command invokes the Bourne Again Shell, the default command-line interpreter on most Linux distributions. It executes commands read from the terminal or from a file (script).

**Syntax:**
```bash
bash [options] [file [arguments...]]
```

**Options:**
- `-c string`: Reads commands from `string`.
- `-x`: Prints commands and their arguments as they are executed (debug mode).
- `-n`: Reads commands but does not execute them (syntax checking).

**Example:**
```bash
bash # Start an interactive bash session
bash my_script.sh # Execute a shell script
bash -x setup.sh # Execute script in debug mode
bash -c 'echo "Hello from Bash"' # Execute command string
```

#### `sh` - Standard Shell Command Language Interpreter
> The `sh` command invokes the system's standard POSIX-compliant shell. On many Linux systems, `/bin/sh` is a symbolic link to `bash` (often running in POSIX compatibility mode) or another shell like `dash`. Scripts written for `sh` aim for portability across Unix-like systems.

**Syntax:**
```bash
sh [options] [file [arguments...]]
```
(Options are generally similar to `bash` but may be more limited).

**Example:**
```bash
sh portable_script.sh # Execute a POSIX-compliant script
```

### Programming Languages (Commonly Available)

#### `perl` - Practical Extraction and Report Language
> The `perl` command executes Perl programs. Perl is a high-level, interpreted language known for its powerful text processing capabilities and regular expression engine.

**Syntax:**
```bash
perl [options] [programfile] [arguments...]
```

**Options:**
- `-e 'command'`: Executes one line of program `command`.
- `-c`: Checks syntax of the script without executing.
- `-w`: Enables warnings.
- `-d`: Runs the script under the Perl debugger.

**Example:**
```bash
perl my_script.pl argument1
perl -e 'print "Hello, Perl!\n";' # Execute one-liner
perl -cw check_script.pl # Check syntax with warnings
```

#### `python` / `python3` - Python Language Interpreter
> The `python` command runs Python programs. Python is a versatile, high-level, interpreted language emphasizing code readability. `python3` typically invokes Python version 3.x, while `python` might invoke Python 2.x (legacy) or 3.x depending on the system setup. Prefer `python3` for modern development.

**Syntax:**
```bash
python[3] [options] [script.py | -c command | -m module] [arguments...]
```

**Options:**
- `-c command`: Executes Python code from `command`.
- `-m module`: Runs library module as a script (e.g., `python3 -m http.server`).
- `-V`, `--version`: Prints the Python version number.

**Example:**
```bash
python3 my_app.py
python3 -c 'import sys; print(f"Hello, Python {sys.version_info.major}.{sys.version_info.minor}!")'
python3 -m venv my_virtual_env # Create a virtual environment
python3 --version
```

#### `gcc` / `g++` - GNU Compiler Collection
> The `gcc` command is the GNU C compiler; `g++` is the GNU C++ compiler. They compile source code written in C, C++, Objective-C, Fortran, Ada, Go, and D into executable programs or object files.

**Syntax:**
```bash
gcc [options] file...
g++ [options] file...
```

**Common Options:**
- `-o output_file`: Specifies the name for the output executable.
- `-c`: Compiles source files into object files (`.o`) without linking.
- `-Wall`: Enables most common compiler warnings.
- `-g`: Includes debugging information in the executable.
- `-O[level]`: Sets optimization level (e.g., `-O2`, `-O3`).
- `-l library`: Links with the specified library (e.g., `-lm` for math library).
- `-I /path/to/include`: Adds a directory to search for header files.
- `-L /path/to/lib`: Adds a directory to search for libraries.

**Example:**
```bash
# Compile C program
gcc hello.c -o hello_world

# Compile C++ program
g++ main.cpp utils.cpp -o my_program -Wall -O2

# Compile C file into an object file
gcc -c helper.c -o helper.o

# Link object files into an executable
gcc main.o helper.o -o final_app -lm
