<p align="center">
  <img src="Images/Linux Logo.webp" width="90" height="90" />
</p>

# Linux
- Linux is a free and open-source operating system based on Unix.
- Created by Linus Torvalds in 1991.
- It uses a monolithic kernel, meaning the core of the OS handles CPU, memory, device drivers, and system calls.
- Linux powers:
  - Servers (most web servers)
  - Smartphones (Android)
  - Supercomputers
  - IoT devices

### Key Features of Linux
- Open Source: Source code is freely available for anyone to view, modify, and distribute.
- Multi-user: Supports multiple users accessing the system at the same time.
- Multitasking: Run multiple programs simultaneously.
- Security: Based on file permissions, user roles, and tools like SELinux.
- Stability & Performance: Common in critical systems due to reliability.

### Linux Architecture
<p align="center">
  <img src="Images/Linux Architecture.jpg" width="800" height="700" />
</p>

#### 1. The Linux Kernel
The kernel is the core of the Linux operating system, acting as an interface between the hardware and software components. It manages system resources such as CPU, memory, and input/output devices.

#### Key Responsibilities of the Kernel:
- Process Management: Handling the creation, scheduling, and termination of processes.
- Memory Management: Efficiently allocating and managing memory (RAM) for processes.
- Device Drivers: Facilitating communication between hardware devices (such as printers, hard drives, and keyboards) and software.
- Filesystem Management: Ensuring proper access and management of data stored on disk drives.
- System Calls: Providing an interface through which user programs can interact with the kernel.

#### Subcomponents of the Kernel:
- Process Scheduler: Manages the execution of processes by deciding which process to run next.
- Memory Management Unit (MMU): Handles memory allocation, paging, and virtual memory.
- Inter-process Communication (IPC): Allows processes to communicate with each other.
- Input/Output (I/O): Manages communication with peripheral devices.
- Networking: Implements network protocols for communication between systems.

#### 2. System Libraries
System libraries are a collection of functions or routines that applications can call upon to perform basic operations. These libraries provide an abstraction layer for various hardware and system resources, allowing programs to run independently of the underlying hardware.

#### Examples of System Libraries:
- C Standard Library (glibc): Provides standard functions like file manipulation, memory allocation, and string operations.
- POSIX (Portable Operating System Interface): A set of standards that define how the system and applications interact to ensure portability across different Unix-like systems.

#### 3. System Utilities
System utilities are programs that provide essential functionality and are responsible for performing basic system operations. These utilities are often included with the operating system and serve as a bridge between users and the kernel.

#### Key Utilities:
- Shell: A command-line interface that allows users to interact with the kernel through commands. Common shells include `bash`, `zsh`, `fish`, and others.
- File Management Utilities: Such as `ls`, `cp`, `mv`, `rm`, `cat`, `grep`, etc., that help in managing and manipulating files.
- Process Management Utilities: Tools like `ps`, `top`, `kill`, `nice`, and `htop` help monitor and control system processes.
- Package Management: Tools like `apt` (Debian-based), `yum` (Red Hat-based), or pacman (Arch-based) that manage software installation and updates.
- Networking Utilities: Tools such as `ping`, `ifconfig`, `netstat`, and `ssh` are used for managing and monitoring network connections.

#### 4. User Interface
Linux offers two main types of interfaces for user interaction:

##### a. Command Line Interface (CLI)
- The CLI is a text-based interface where users type commands to interact with the system. The shell (e.g., `bash`) interprets commands and executes them.
- This interface is lightweight and powerful, offering fine-grained control over the system.

##### b. Graphical User Interface (GUI)
The GUI provides a more user-friendly way to interact with the system through graphical elements like windows, buttons, and icons. The most common desktop environments in Linux are:
- GNOME: A popular, user-friendly environment.
- KDE Plasma: Known for its customizability and feature-rich nature.
- Xfce: A lightweight and resource-efficient environment.
- LXQt: Lightweight and minimalistic.
GUI elements are built on top of the X Window System (X11) or newer alternatives like Wayland.

#### 5. Filesystem
The filesystem is crucial for data storage and organization. Linux supports several types of filesystems, and the structure follows a unified hierarchy known as the Filesystem Hierarchy Standard (FHS).

##### Common Filesystem Types:
- ext4 (Fourth Extended File System): The most common filesystem used in modern Linux systems.
- Btrfs: A newer filesystem offering advanced features like snapshots and subvolumes.
- XFS: A high-performance filesystem often used for large-scale data storage.
- F2FS: Optimized for flash-based storage devices like SSDs.

##### Key Directories in Linux Filesystem:
- `/`: Root directory, the top-level directory in the file hierarchy.
- `/bin`: Essential binaries (commands required for system boot and repair).
- `/etc`: Configuration files for the system and software.
- `/home`: Home directories for users.
- `/var`: Variable data such as logs and mail.
- `/tmp`: Temporary files.
- `/dev`: Device files representing hardware devices.
- `/proc`: Virtual filesystem that provides process and kernel information.
- `/sys`: Kernel-related files, such as device info and system state.

#### 6. Shells
A shell is a command-line interpreter that allows users to execute commands in Linux. The most common shells are:
- Bash (Bourne Again Shell): The default and most popular shell in many distributions.
- Zsh (Z Shell): An extended version of the Bourne shell with many additional features.
- Fish (Friendly Interactive Shell): Known for its user-friendly nature and auto-suggestions.
Shells allow scripting (e.g., Bash scripts) to automate tasks, manipulate files, and manage processes.

#### 7. Hardware Abstraction Layer (HAL)
The Hardware Abstraction Layer (HAL) provides an interface between the kernel and hardware. It ensures that the kernel can communicate with different hardware components (e.g., CPUs, memory, storage devices) without needing to know the specifics of each device. HAL helps in maintaining compatibility across various devices.

#### 8. Boot Process
The Linux boot process is the sequence of steps that the system follows from power-up to being fully operational. It involves several stages:
1. BIOS/UEFI: The first software that runs when the system is powered on, initializing hardware components.
2. Bootloader (GRUB): A program that loads the Linux kernel into memory.
3. Kernel Initialization: The kernel takes control, initializes hardware, and mounts the root filesystem.
4. Init System (Systemd): The first process (`PID 1`) that starts user-space processes and services.

#### 9. Process Management
The Linux kernel uses process scheduling to ensure fair and efficient execution of processes. Key concepts include:
- Process: A running instance of a program.
- PID: Process ID, a unique identifier for each process.
- Forking: A system call that creates a new process.
- Signals: Mechanism for processes to communicate (e.g., `SIGKILL`, `SIGTERM`).
- Scheduling Algorithms: The kernel uses algorithms like Completely Fair Scheduler (CFS) for managing process execution.

#### 10. Networking
Linux has powerful networking capabilities and supports multiple network protocols, such as:
- TCP/IP: The foundational protocol suite for networking.
- Socket Programming: Linux allows the creation of network sockets for inter-process communication and data exchange.

##### Key Network Tools and Utilities:
- ifconfig: To configure network interfaces.
- ping: To test network connectivity.
- iptables: Firewall utility for packet filtering.
- netstat: To view network connections and statistics.

#### 11. Security
Security in Linux is enforced by several components and techniques:
- User Authentication: Ensures users are who they say they are (via passwords, keys, etc.).
- File Permissions: Each file has permissions that determine who can read, write, or execute it.
- SELinux (Security-Enhanced Linux): A set of kernel security modules that enforce access control policies.
- AppArmor: A security module similar to SELinux, used for restricting programs’ capabilities.

### Linux Distribution
- A Linux distribution (or distro) is a packaged version of Linux, including the kernel + tools + software.
- Common distros:
  - Ubuntu (Beginner-friendly)
  - Debian (Stable and secure)
  - Fedora (Cutting edge)
  - CentOS / AlmaLinux / Rocky Linux (Enterprise use)
  - Arch Linux (For advanced users)
  - Kali Linux (Security testing)
  - Linux Mint (User-friendly desktop)

### Linux Boot Process
<p align="center">
  <img src="Images/Boot Process.gif" width="800" height="800" />
</p>

#### 🔌 1. BIOS/UEFI (Firmware Initialization)
  - Runs immediately after powering on the system.
  - Performs POST (Power-On Self Test) to check hardware (CPU, RAM, keyboard, etc.).
  - Initializes hardware components and configures the system.
  - Looks for a bootable device (hard disk, USB, etc.).
- BIOS (Basic Input/Output System) is older; UEFI (Unified Extensible Firmware Interface) is the modern replacement.
- Once a boot device is found, BIOS/UEFI loads the Bootloader into memory.

#### 🚀 2. Bootloader (GRUB, LILO, etc.)
  - Loads the Linux kernel into memory and passes control to it.
  - Allows users to select from multiple OSes or kernel versions (in dual-boot systems).
  - Initializes basic kernel parameters (e.g., root filesystem, initrd).
- Popular Bootloaders:
  - GRUB (GRand Unified Bootloader) – most common.
  - LILO (Linux Loader) – legacy, rarely used today.
  - Syslinux/Isolinux – lightweight loaders often used for live systems.
- Loads the initrd or initramfs, a temporary root filesystem needed to prepare the real root filesystem.

#### 🧬 3. Kernel Initialization
  - Takes over from the bootloader.
  - Initializes hardware using built-in and loaded drivers.
  - Mounts the root filesystem (may first use initrd/initramfs).
  - Sets up memory management, process scheduler, and other subsystems.
- The kernel eventually executes the init process, typically `/sbin/init` or its modern replacements.

#### 🔁 4. Init System (PID 1)
  - It's the first user-space process started by the kernel.
  - Responsible for starting all background services (daemons), mounting disks, network setup, and more.
- Popular Init Systems:
  - Systemd (modern and widely used in major distros like Ubuntu, Fedora, Arch).
  - SysVinit (older, script-based init system).
  - Upstart (used in older Ubuntu versions).
  - In Systemd, the process starts as `/lib/systemd/systemd` or `/sbin/init`.

#### 🗂️ 5. Services & Target (Runlevels)
  - Starts system services according to a target (in Systemd) or runlevel (in SysVinit).
  - Examples of services: network manager, SSH, display manager, etc.
- Systemd Targets:
  - `default.target` → usually points to `graphical.target` or `multi-user.target`.
  - `rescue.target`, `emergency.target` → recovery modes.
- SysVinit Runlevels:
  - `0`: Halt
  - `1`: Single user mode
  - `3`: Multi-user (non-GUI)
  - `5`: Multi-user with GUI
  - `6`: Reboot

#### 👤 6. Login Prompt (Shell or GUI)
- Presents the login prompt:
  - CLI login (via `getty` or similar terminal service).
  - GUI login (via a Display Manager, e.g., GDM, LightDM, SDDM).
- After login:
  - Loads user profile and desktop environment or shell session.

### Linux File System Structure (Folder Hierarchy)
Linux uses a tree-like hierarchical file system that starts at the root directory `/`.

- `/`	        Root directory of the entire file system
- `/bin`	    Essential binary executables (e.g., `ls`, `cp`)
- `/boot`	    Bootloader files (like `grub`, `vmlinuz`)
- `/dev`	    Device files (e.g., `/dev/sda`)
- `/etc`	    Configuration files for the system and applications
- `/home`	    User home directories (e.g., `/home/username`)
- `/lib`	    Essential shared libraries
- `/media`	Mounted media like USB drives
- `/mnt`	    Temporarily mounted filesystems
- `/opt`	    Optional or third-party software
- `/proc`	    Virtual filesystem for system information (e.g., `/proc/cpuinfo`)
- `/root`	    Home directory for root user
- `/run`	    Runtime data for processes
- `/sbin`	    System binaries used by root/admin
- `/srv`	    Data for services like FTP, HTTP
- `/sys`	    Interface to kernel devices
- `/tmp`	    Temporary files (auto-deleted)
- `/usr`	    User programs and utilities
- `/var`	    Variable data like logs, mail, spool files

### Linux Command Line
- The command line interface (CLI) is a text-based interface for interacting with the operating system.
- The most common shell is Bash (`Bourne Again SHell`).
- It's more powerful and flexible than the GUI for many tasks, especially system administration.

### 🐧 Linux Commands Cheat Sheet

### 🗂️ 1. File & Directory Management

| Command     | Description                              | Example                                |
|-------------|------------------------------------------|----------------------------------------|
| `ls`        | List directory contents                  | `ls -l`                                |
| `cd`        | Change directory                         | `cd /home/user/Documents`              |
| `pwd`       | Print working directory                  | `pwd`                                  |
| `mkdir`     | Make new directory                       | `mkdir myfolder`                       |
| `rmdir`     | Remove empty directory                   | `rmdir emptyfolder`                    |
| `rm`        | Remove files or directories              | `rm file.txt`, `rm -r dir/`            |
| `cp`        | Copy files or directories                | `cp file1.txt backup/`                 |
| `mv`        | Move or rename files                     | `mv old.txt new.txt`                   |
| `touch`     | Create empty file                        | `touch newfile.txt`                    |
| `find`      | Search files in directory tree           | `find / -name "*.log"`                 |
| `locate`    | Find files using indexed database        | `locate bashrc`                        |
| `tree`      | Visual directory tree                    | `tree /etc`                            |

---

### 📄 2. File Viewing & Editing

| Command     | Description                              | Example                                |
|-------------|------------------------------------------|----------------------------------------|
| `cat`       | View file content                        | `cat file.txt`                         |
| `more`      | View large files page-by-page            | `more file.txt`                        |
| `less`      | Scrollable file viewer                   | `less /var/log/syslog`                 |
| `head`      | Show beginning of file                   | `head -n 10 file.txt`                  |
| `tail`      | Show end of file                         | `tail -f /var/log/syslog`              |
| `nano`      | Command-line text editor                 | `nano file.txt`                        |
| `vim`/`vi`  | Advanced text editor                     | `vi script.sh`                         |

---

### 🔧 3. File Permissions & Ownership

| Command     | Description                              | Example                                |
|-------------|------------------------------------------|----------------------------------------|
| `chmod`     | Change permissions                       | `chmod 755 script.sh`                  |
| `chown`     | Change file owner                        | `chown user:group file.txt`            |
| `umask`     | Set default permissions                  | `umask 022`                            |
| `ls -l`     | View file permissions                    | `ls -l file.txt`                       |

---

### 🧠 4. Process Management

| Command     | Description                              | Example                                |
|-------------|------------------------------------------|----------------------------------------|
| `ps`        | Show running processes                   | `ps aux`                               |
| `top`       | Real-time process viewer                 | `top`                                  |
| `htop`      | Enhanced top (if installed)              | `htop`                                 |
| `kill`      | Terminate process by PID                 | `kill 1234`                            |
| `killall`   | Kill processes by name                   | `killall firefox`                      |
| `nice`      | Set process priority                     | `nice -n 10 command`                   |
| `renice`    | Change running process priority          | `renice +5 1234`                       |
| `jobs`      | Show background jobs                     | `jobs`                                 |
| `fg`/`bg`   | Bring job to foreground/background       | `fg %1`, `bg %2`                       |

---

### 💾 5. Disk Management

| Command     | Description                              | Example                                |
|-------------|------------------------------------------|----------------------------------------|
| `df -h`     | Disk space (human-readable)              | `df -h`                                |
| `du -sh`    | Directory/file size                      | `du -sh /home/user`                    |
| `mount`     | Mount filesystem                         | `mount /dev/sdb1 /mnt`                 |
| `umount`    | Unmount filesystem                       | `umount /mnt`                          |
| `lsblk`     | List block devices                       | `lsblk`                                |
| `fdisk`     | Partition disk (interactive)             | `fdisk /dev/sda`                       |
| `mkfs`      | Format partition                         | `mkfs.ext4 /dev/sdb1`                  |

---

### 🌐 6. Networking

| Command     | Description                              | Example                                |
|-------------|------------------------------------------|----------------------------------------|
| `ip a`      | Show IP addresses                        | `ip a`                                 |
| `ifconfig`  | Legacy interface (deprecated)            | `ifconfig`                             |
| `ping`      | Test connectivity                        | `ping google.com`                      |
| `netstat`   | Show network connections                 | `netstat -tuln`                        |
| `ss`        | Faster, modern netstat replacement       | `ss -tuln`                             |
| `curl`      | Transfer data via HTTP/FTP               | `curl https://example.com`             |
| `wget`      | Download files from the web              | `wget http://file.zip`                 |
| `scp`       | Secure copy over SSH                     | `scp file.txt user@host:/dir/`         |
| `ssh`       | Secure remote login                      | `ssh user@host`                        |
| `traceroute`| Trace route to host                      | `traceroute google.com`                |

---

### 👤 7. User Management

| Command     | Description                              | Example                                |
|-------------|------------------------------------------|----------------------------------------|
| `whoami`    | Show current user                        | `whoami`                               |
| `id`        | User/group info                          | `id`                                   |
| `adduser`   | Add a new user                           | `adduser alice`                        |
| `userdel`   | Delete a user                            | `userdel alice`                        |
| `passwd`    | Change user password                     | `passwd alice`                         |
| `groupadd`  | Add a new group                          | `groupadd devs`                        |
| `usermod`   | Modify user account                      | `usermod -aG devs alice`               |

---

### 🔐 8. Security & Permissions

| Command     | Description                              | Example                                |
|-------------|------------------------------------------|----------------------------------------|
| `sudo`      | Run command as root                      | `sudo apt update`                      |
| `su`        | Switch user                              | `su -`                                 |
| `ufw`       | Simple firewall for Ubuntu               | `sudo ufw enable`                      |
| `iptables`  | Complex firewall settings                | `iptables -L`                          |

---

### 📦 9. Package Management

#### Debian/Ubuntu:

| Command          | Description                        |
|------------------|------------------------------------|
| `apt update`     | Update package list                |
| `apt upgrade`    | Upgrade all packages               |
| `apt install`    | Install a package                  |
| `apt remove`     | Remove a package                   |

#### RHEL/CentOS:

| Command          | Description                        |
|------------------|------------------------------------|
| `yum install`    | Install a package                  |
| `dnf install`    | (Newer) Install a package          |

#### Arch Linux:

| Command          | Description                        |
|------------------|------------------------------------|
| `pacman -S`      | Install package                    |
| `pacman -Syu`    | Sync and upgrade system            |

---

### 📜 10. System Information

| Command     | Description                              | Example                                |
|-------------|------------------------------------------|----------------------------------------|
| `uname -a`  | System/kernel info                       | `uname -a`                             |
| `hostname`  | View/modify hostname                     | `hostname`                             |
| `uptime`    | Show how long system has been up         | `uptime`                               |
| `free -h`   | Memory usage                             | `free -h`                              |
| `top`       | Real-time performance                    | `top`                                  |
| `vmstat`    | System performance summary               | `vmstat`                               |
| `lscpu`     | CPU architecture                         | `lscpu`                                |
| `lsblk`     | Block device info                        | `lsblk`                                |

---

#### ✅ Tips

- Use `man command` to see manual/help for any command.
- Combine with `|`, `>`, `&&`, `;` for powerful command chaining.
---

### Navigation Commands
`pwd`	Print current directory
`ls`	List files in a directory
`cd`	Change directory
`clear`	Clear the terminal screen
`exit`	Exit the shell session

### File and Directory Commands
- `mkdir dirname`	    Create a directory
- `touch filename`	Create an empty file
- `cp src dest`	    Copy files or directories
- `mv src dest`	    Move or rename files/directories
- `rm file`	        Remove a file
- `rm -r folder`	    Remove a directory recursively
- `rmdir folder`	    Remove an empty directory

### Viewing Files
- `cat file`	    Print entire file
- `less file`	    Scrollable view
- `more file`	    Page-by-page display
- `head file`	    Show first 10 lines
- `tail file`	    Show last 10 lines
- `tail -f file`	Live update view (great for logs)

### CLI Tips
- Tab Autocomplete: Press `Tab` to auto-complete files/commands.
- Command History: Use the `↑` and `↓` arrows to scroll through history.
- Reuse Previous Commands:
  - `!!` – last command
  - `!n` – nth command in history
  - `!grep` – last command starting with `grep`

### Getting Help
- `man command`	    Manual page
- `command --help`	Quick help
- `info command`	    More detailed help pages

### Understanding File Permissions
In Linux, every file and directory has permissions for:
- Owner (u)
- Group (g)
- Others (o)
`ls -l` 
```
-rw-r--r-- 1 user group  1024 Apr 26  notes.txt
```
- `-`	    Regular file (`d` for directory)
- `rw`-	Owner: read & write
- `r--`	Group: read-only
- `r--`	Others: read-only

### Changing Permissions – `chmod`
Numeric mode
0	    ---
1	    --x
2	    -w-
4	    r--

```
chmod 755 script.sh     # rwxr-xr-x
chmod 644 notes.txt     # rw-r--r--
```
### File and Directory Types
- `-`	Regular file
- `d`	Directory
- `l`	Symbolic link
- `b`	Block device
- `c`	Character device
- `s`	Socket
- `p`	Named pipe (FIFO)

### Working with Links
- Hard Link `ln original.txt hardlink.txt`
- Symbolic(Soft)Link `ln -s original.txt symlink.txt`
- Soft links can link to directories
- Hard links can’t span file systems or point to directories

### File Compression
-`tar -cvf file.tar dir/` Create archive
- `tar -xvf file.tar`	     Extract archive
- `gzip file`	             Compress file (creates file.gz)
- `gunzip file.gz`	     Decompress
- `zip file.zip file`	     Create zip
- `unzip file.zip`	     Extract zip

### Viewing and Displaying Text Files
- `cat file.txt`	    Print file contents to terminal
- `less file.txt`	    Scrollable view (use q to quit)
- `more file.txt`	    View page by page
- `head file.txt`	    Show first 10 lines
- `tail file.txt`	    Show last 10 lines
- `tail -f file.txt`	Real-time updates (log files)

### Editing Text Files
- Nano: A simple, user-friendly text editor suitable for beginners. Straightforward and intuitive.
`nano filename.txt`
- Use arrow keys to move
- Save: `Ctrl + O`
- Exit: `Ctrl + X`
#### Nano Keyboard Shortcuts
- `Ctrl + O`	Write file (save)
- `Ctrl + X`	Exit Nano
- `Ctrl + K`	Cut line
- `Ctrl + U`	Paste line
- `Ctrl + W`	Search
- `Ctrl + G`	Help
- `Ctrl + _`	Go to line

Vim Editor (Powerful, but advanced)
- Vim: A powerful, modal, highly configurable text editor based on vi. Ideal for advanced users.
`vim filename.txt`
- `i`  → Insert mode
- `Esc` → Exit insert mode
- `:w`  → Save
- `:q`  → Quit
- `:wq` → Save and quit
- `:q!` → Quit without saving

#### Vim Basic Commands
🖊️ Enter Insert Mode
```
i        → Insert before cursor  
a        → Append after cursor  
o        → Open new line below
```
⌨️ Exit Insert Mode
`ESC`

💾 Save & Exit
- `:w`	         Save (write)
- `:q`	         Quit
- `:wq` or `ZZ`	 Save and quit
- `:q!`	         Quit without saving

📦 Navigation in Normal Mode
- `h` `j` `k` `l`	 Move left, down, up, right
- `gg`	         Go to beginning of file
- `G`	             Go to end of file
- `:n`	         Go to line `n`
- `/word`	         Search for `word`
- `n`	             Next search result

✂️ Editing Text
- `dd`	    Delete current line
- `yy`	    Yank (copy) current line
- `p`	        Paste below cursor
- `x`	        Delete character under cursor
- `u`	        Undo last change
- `Ctrl + r`	Redo

### Searching with `grep`
```
grep "error" /var/log/syslog
grep -i "user" users.txt    # Case-insensitive
grep -r "main()" ./         # Recursive search
```
Common flags
- `-i`: case-insensitive
- `-r`: recursive
- `-n`: show line number
- `--color`: highlight matches

### Sorting and Filtering
`sort`
```
sort names.txt
sort -r names.txt         # Reverse
sort -n numbers.txt       # Numeric sort
```
`uniq`
```
uniq items.txt            # Remove duplicates (must be sorted)
sort items.txt | uniq     # Combined usage
```
`cut`
```
cut -d ':' -f1 /etc/passwd
```
- `-d` sets delimiter
- `-f` chooses field

`awk`
```
awk '{print $1}' file.txt        # Print first column
awk -F ':' '{print $1, $3}' /etc/passwd
```
`sed`
```
sed 's/old/new/' file.txt        # Replace first occurrence
sed 's/old/new/g' file.txt       # Replace all occurrences
```
### Redirection and Pipes
- `>`	    Redirect output to a file (overwrite)
- `>>`	Append output to file
- `<`	    Use file as input
```
ls -l > files.txt
cat files.txt | grep ".sh" | sort
```

## User & Group Management

### User Management Basics
Linux is a multi-user operating system, and every user has:
- A username
- A UID (User ID)
- A GID (Group ID)
- A home directory
- A default shell

### Adding and Managing Users
- `adduser username`	Add a new user (Debian/Ubuntu)
- `useradd username`	Add user (low-level, needs manual setup)
- `passwd username`	Set or change a user’s password
- `deluser username`	Delete a user (Ubuntu/Debian)
- `userdel username`	Delete a user (RHEL/CentOS)

### Modifying Users
- `usermod -aG group user`	    Add user to group
- `usermod -d /new/home user`	    Change home directory
- `usermod -l newname oldname`	Change username

### Group Management
Groups allow multiple users to share permissions.
- `groupadd groupname`	         Create a new group
- `groupdel groupname`	         Delete a group
- `groupmod -n newgroup oldgroup`	 Rename a group
- `gpasswd -a user group`	         Add user to a group
- `groups username`	             Show groups of a user

### User Information Files
- `/etc/passwd`	Stores user account info
- `/etc/shadow`	Stores encrypted passwords
- `/etc/group`	Stores group info
- `/etc/gshadow`	Stores secure group info

### Switching Users and Becoming Root
- `su`	        Switch to another user
- `su - username`	Login as user with their environment
- `sudo command`	Run a command as another user (usually root)

- `sudo` is safer and preferred over `su` in modern distros.
- Add user to sudoers:
```
usermod -aG sudo username
```

## Process Management
### Process
A process is any program or command being executed. Each process has a:
- PID (Process ID)
- PPID (Parent Process ID)
- User
- Priority (nice value)
- State (running, sleeping, zombie, etc.)

### Viewing Processes
- `ps`	                Show running processes
- `ps aux`	            Detailed list of all running processes
- `top`	                Real-time process monitor
- `htop`	                Enhanced top (interactive, requires install)
- `pidof process_name`	Find PID of a process
- `pgrep name`	        Find PID by name

### Killing Processes
- `kill PID`	    Send termination signal to process
- `kill -9 PID`	Force kill a process
- `pkill name`	Kill by process name
- `killall name`	Kill all processes with the given name

### Priority & Niceness
- Nice value: Controls process priority (range: `-20` to `19`, lower = higher priority)

- `nice -n 10 command`	Start a command with lower priority
- `renice -n 5 -p 1234`	Change priority of running process

## Package Management
### Package
A package is a bundle containing compiled software, configuration files, and metadata.
- Each Linux distro uses its own package manager:

|Distro	            | Package Manager	       |File Extension  |
|-------------------|------------------------|----------------|
|Ubuntu/Debian	    |`apt`, `dpkg`	         | `.deb`         |
|RHEL/CentOS/Fedora	|`yum`, `dnf`, `rpm`	   |  `.rpm`        |
|Arch Linux	        |`pacman`	               |`.pkg.tar.zst`  |
|OpenSUSE	          |`zypper`	               |`.rpm`          |


#### Debian/Ubuntu-Based Systems – `apt`
- `sudo apt update`	    Refresh package index
- `sudo apt upgrade`	    Upgrade all packages
- `sudo apt install pkg`	Install a package
- `sudo apt remove pkg`	Remove a package
- `sudo apt purge pkg`	Remove with config files
- `sudo apt autoremove`	Remove unused dependencies
- `apt list --installed`	Show installed packages
- `apt search name`	    Search for a package
Similarly for Red Hat/CentOS-Based Systems – `yum` and `dnf`
- `yum` is traditional; `dnf` is the newer default in Fedora and RHEL 8

## Networking Basics
### Understanding Networking in Linux
Linux is widely used for networking tasks, whether it's for web servers, routers, or simple networking configuration on a local machine.

### Basic Networking Concepts
- IP Address: Identifies a device on a network.
  - IPv4: 192.168.1.1
  - IPv6: fe80::1
- Subnet Mask: Defines the network portion of an IP address.
- Default Gateway: The device that forwards traffic from your local network to other networks (usually a router).
- DNS (Domain Name System): Resolves domain names to IP addresses.

### Checking Network Configuration
- `ifconfig`	    Display network interfaces (older, replaced by ip)
- `ip a`	        Show all network interfaces
- `ip link`	    Display network interfaces and their status
- `hostname`	    Show or set system hostname
- `hostname -I`	Display IP address
- `nmcli`	        Network manager command-line tool (Ubuntu)

### Testing Network Connectivity
- `ping host`	        Test connectivity to a host
- `ping 8.8.8.8`	    Test connectivity to Google's DNS server
- `traceroute host`	Show the path packets take to a destination
- `curl url`	        Fetch content from a URL (can check connectivity to websites)
- `nslookup domain`	Query DNS server for domain info

### Troubleshooting Network Issues
- `netstat -tuln`	Show listening ports and connections
- `ss -tuln`	    Show socket statistics (more modern than `netstat`)
- `ufw status`	Check firewall status (for systems using `ufw`)
- `iptables -L`	List iptables firewall rules (more advanced)

### Basic Firewall Configuration – `ufw`
- `sudo ufw enable`	Enable the firewall
- `sudo ufw disable`	Disable the firewall
- `sudo ufw allow 22`	Allow SSH (port 22)
- `sudo ufw deny 80`	Deny HTTP (port 80)
- `sudo ufw status`	Check firewall status

## System Monitoring & Performance Tuning

### System Monitoring
Monitoring is crucial to ensure that your system is performing optimally and to quickly identify and resolve issues. Common metrics to monitor include:
- CPU usage
- Memory usage
- Disk I/O
- Network activity
- System load

`top` – command provides a real-time overview of system resources.
- `PID`: Process ID
- `USER`: User running the process
- `%CPU`: CPU usage by the process
- `%MEM`: Memory usage by the process
- `TIME+`: Total CPU time used by the process
- `COMMAND`: The command that started the process
To quit `top`, press `q`.

- `htop` is a more user-friendly version of `top` with a colorful, interactive interface.
- `vmstat` command provides insights into system memory, processes, and CPU performance.
- `iostat` Used to monitor CPU performance and I/O statistics

`df` command shows the amount of disk space used and available on mounted filesystems.
```
df -h
```
`-h` (human-readable) will show sizes in a more user-friendly format (e.g., GB, MB).

### Managing System Services with `systemd`
Most modern Linux distributions use systemd as their init system, which is responsible for booting the system and managing services.

- To check if a service is running `systemctl status <service-name>`
- Start a service `sudo systemctl start <service-name>`
- Stop a service `sudo systemctl stop <service-name>`
- Restart a service `sudo systemctl restart <service-name>`
- Reload a service `sudo systemctl reload <service-name>`
- Viewing All Active Services `systemctl list-units --type=service`

### Common Services and Daemons
Here are some common services and daemons you may encounter:
- Apache (httpd): Web server
- Nginx: Web server/reverse proxy
- MySQL/MariaDB: Database server
- PostgreSQL: Database server
- SSH (sshd): Secure shell server for remote access
- Cron: Task scheduler
- NetworkManager: Manages network connections
- Docker: Container management service

### Cron Jobs
Cron is a Linux utility used to schedule jobs (tasks) to run at specific intervals
- Viewing Cron Jobs `crontab -l`
- view the system-wide cron jobs `cat /etc/crontab`
- edit the cron jobs for the current user `crontab -e`
syntax for adding a cron job
```
* * * * * /path/to/command
```
Each `*` represents a time unit:
- First `*` : Minute (0-59)
- Second `*`: Hour (0-23)
- Third `*` : Day of the month (1-31)
- Fourth `*`: Month (1-12)
- Fifth `*` : Day of the week (0-6, Sunday=0)
