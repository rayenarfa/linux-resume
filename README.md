# Linux Exam Guide — Terminal & Commands

You have **no Linux experience**? Start here. This guide teaches **what the terminal is**, **how to type commands correctly**, then groups **every command you studied** into **4 big categories** with memorable examples.

---

## Table of contents

1. [What is the terminal?](#1-what-is-the-terminal)
2. [How to write a command (the correct way)](#2-how-to-write-a-command-the-correct-way)
3. [The 4 big categories (overview)](#3-the-four-big-categories-overview)
4. [Category 1 — Files & folders](#category-1--files--folders)
5. [Category 2 — Text, search & archives](#category-2--text-search--archives)
6. [Category 3 — System, hardware & processes](#category-3--system-hardware--processes)
7. [Category 4 — Disks, permissions, network & packages](#category-4--disks-permissions-network--packages)
8. [Quick exam cheat sheet](#quick-exam-cheat-sheet)

---

## 1. What is the terminal?

### Simple picture

```
YOU  →  type a command  →  SHELL (interpreter)  →  LINUX (does the job)  →  result on screen
```

| Word | Meaning |
|------|---------|
| **Terminal** | The black (or white) window where you type text commands |
| **Shell** | The program that reads your commands (usually **bash**) |
| **Command** | An instruction like `ls` or `cd Documents` |
| **Prompt** | The line waiting for you, often looks like: `user@computer:~$` |

### What you see

```bash
rayen@esip:~$ ls
Documents  Downloads  music.txt
rayen@esip:~$ _
```

- **`rayen@esip:~$`** = prompt (computer is ready)
- You type after `$`, press **Enter**
- Linux runs the command and shows the result
- **`_`** = cursor waiting for next command

### Important rules

| Rule | Example |
|------|---------|
| **Linux is case-sensitive** | `Documents` ≠ `documents` |
| **Spaces separate words** | `cd my folder` ❌ → use `cd "my folder"` or `cd my\ folder` |
| **Press Enter to run** | Typing alone does nothing until Enter |
| **Current folder = working directory** | Where you are right now |
| **`.`** = current folder | `find .` = search here |
| **`..`** = parent folder (go up) | `cd ..` = go up one level |
| **`~`** = your home folder | `cd ~` = go home |
| **`/`** = root (top of system) | `cd /` = go to root |

### How to get help when stuck

```bash
man ls        # full manual for ls (press q to quit)
ls --help     # short help for many commands
```

---

## 2. How to write a command (the correct way)

### Command structure

```
command   [options]   [arguments]
   │          │            │
   │          │            └── WHAT (file, folder, name...)
   │          └── HOW (-l, -a, -h = flags/modifiers)
   └── WHAT TO DO (ls, cd, cp...)
```

### Examples broken down

| Full command | Command | Option | Argument |
|--------------|---------|--------|----------|
| `ls` | ls | — | — |
| `ls -l` | ls | -l (long details) | — |
| `cd Documents` | cd | — | Documents |
| `cp file1 file2` | cp | — | file1, file2 |
| `find . -name "*.txt"` | find | -name | . and "*.txt" |

### Options (flags) — memory trick

- **Short options**: one dash + letter → `-l`, `-a`, `-h`
- **Combined**: `ls -lah` = `ls -l -a -h` (all three together)
- **Long options**: two dashes → `--help`

### Correct typing habits

```bash
# ✅ Good — one command per line
cd Documents
ls -l

# ✅ Good — full path when needed
cp /home/rayen/file.txt /home/rayen/backup/

# ❌ Wrong — spaces in names without quotes
cd my documents

# ✅ Fixed
cd "my documents"
```

### Output redirection (save to file)

```bash
echo "Hello" > file.txt     # write "Hello" INTO file.txt (overwrites)
cat file.txt                # shows: Hello
```

| Symbol | Meaning |
|--------|---------|
| `>` | Send output to file (**overwrite**) |
| `|` | Pipe — send output to **next command** |

**Pipe example (very common in exam):**

```bash
dmesg | grep usb    # kernel messages → filter only lines with "usb"
```

---

## 3. The four big categories (overview)

Think of Linux like a **house**:

```
┌─────────────────────────────────────────────────────────────┐
│  CATEGORY 1 — FILES & FOLDERS                               │
│  🗂️  Walk around the house: open doors, move boxes,         │
│      create/delete folders, list what's inside              │
├─────────────────────────────────────────────────────────────┤
│  CATEGORY 2 — TEXT, SEARCH & ARCHIVES                       │
│  📄  Read letters, search words, count lines,              │
│      zip/unzip files                                        │
├─────────────────────────────────────────────────────────────┤
│  CATEGORY 3 — SYSTEM, HARDWARE & PROCESSES                  │
│  🖥️  Check the engine: CPU, RAM, USB, PCI, logs,           │
│      running programs, boot mode                            │
├─────────────────────────────────────────────────────────────┤
│  CATEGORY 4 — DISKS, PERMISSIONS, NETWORK & PACKAGES        │
│  💾  Partition hard drive, who can open files,              │
│      internet, install software                             │
└─────────────────────────────────────────────────────────────┘
```

| # | Category | Main idea | Key commands |
|---|----------|-----------|--------------|
| **1** | Files & folders | Navigate & manage files | `ls`, `cd`, `pwd`, `cp`, `mv`, `rm`, `mkdir` |
| **2** | Text, search & archives | Read & process text | `cat`, `grep`, `head`, `tail`, `tar`, `gzip` |
| **3** | System, hardware & processes | Know your machine | `top`, `free`, `lspci`, `dmesg`, `systemctl` |
| **4** | Disks, permissions, network & packages | Storage & security | `fdisk`, `chmod`, `ssh`, `apt-get` |

---

# Category 1 — Files & Folders

> **Memory story:** You arrive at a building. First you check **where you are**, then **what rooms exist**, then you **enter**, **create**, **copy**, or **delete** things.

---

## Navigation & help

### `pwd` — **P**rint **W**orking **D**irectory (where am I?)

```bash
pwd
# Output: /home/rayen
```

**Exam memory:** "**P**where **W**here am I?" → `pwd`

---

### `cd` — **C**hange **D**irectory (go to a folder)

```bash
cd Documents          # go into Documents folder
cd ..                 # go UP one level (parent)
cd ~                  # go to home folder
cd /                  # go to root (top of system)
cd                    # also goes home
```

**Visual:**

```
/home/rayen/          ← you are here (pwd)
    ├── Documents/    ← cd Documents
    ├── Downloads/
    └── file.txt
```

**Exam memory:** `cd` = "**C**hange **D**oor" — walk into another room

---

### `ls` — **L**i**s**t (what's in this folder?)

```bash
ls                    # simple list
ls -l                 # long format (permissions, size, date)
ls -lh                # long + human-readable sizes (KB, MB)
ls -a                 # all files including hidden (.bashrc)
ls -lah               # combine all three
```

**Example output of `ls -lh`:**

```
-rw-r--r-- 1 rayen rayen  2.1K Jan 10  notes.txt
drwxr-xr-x 2 rayen rayen  4.0K Jan 10  Documents
```

| First char | Meaning |
|------------|---------|
| `-` | regular file |
| `d` | directory (folder) |

**Exam memory:** `ls` = "**L**ook **S**tuff" — list files

---

### `man` — **Man**ual (help for any command)

```bash
man ls        # how to use ls
man cp        # how to use cp
```

Press **`q`** to quit.  
**Exam memory:** `man` = "**Man**ual pages"

---

## Create, delete, copy, move

### `mkdir` — **M**a**k**e **Dir**ectory (create folder)

```bash
mkdir projet          # create folder "projet"
mkdir -p a/b/c        # create nested folders (a, then b inside, then c)
```

**Exam memory:** `mkdir` = "**M**a**k**e **dir**"

---

### `touch` — create empty file (or update date)

```bash
touch notes.txt       # creates empty notes.txt
touch file1 file2     # create two files at once
```

**Exam memory:** `touch` = touch a file so it **exists**

---

### `rm` — **R**e**m**ove file (delete file)

```bash
rm old.txt            # delete one file
rm file1 file2        # delete multiple files
```

⚠️ **No recycle bin!** Deleted = gone.

**Exam memory:** `rm` = "**R**e**m**ove"

---

### `rmdir` — remove **empty** directory only

```bash
rmdir empty_folder    # works only if folder is empty
```

**Exam memory:** `rmdir` = remove **dir** (must be empty)

---

### `cp` — **C**o**p**y (copy file or folder)

```bash
cp notes.txt backup.txt           # copy file → new name
cp notes.txt Documents/           # copy file INTO folder
cp -r projet/ projet_backup/      # -r = copy folder recursively
```

**Exam memory:** `cp` = "**C**o**p**y" — needs **source** then **destination**

```
cp  SOURCE   DESTINATION
    │            │
 notes.txt   backup.txt
```

---

### `mv` — **M**o**v**e or rename

```bash
mv old.txt new.txt              # rename file
mv file.txt Documents/          # move file into folder
mv projet/ /home/rayen/archive/ # move whole folder
```

**Exam memory:** `mv` = "**M**o**v**e" — also used to **rename**

---

## Category 1 — quick practice scenario

```bash
pwd                              # where am I?
mkdir exam_practice              # create folder
cd exam_practice                 # enter it
touch todo.txt                   # create file
echo "study linux" > todo.txt    # write text into file
cp todo.txt todo_backup.txt      # copy
mv todo_backup.txt backup.txt    # rename
ls -lh                           # see everything
cd ..                            # go back up
```

---

# Category 2 — Text, Search & Archives

> **Memory story:** You open documents, **read** them, **search** for words, **count** lines, and **pack** files into a zip-like archive.

---

## View file content

### `cat` — **cat**enate / show whole file

```bash
cat notes.txt         # print entire file on screen
cat file1 file2       # show two files one after another
```

**Exam memory:** `cat` = show file like a **cat** looking at the page

---

### `head` — first lines (head = top)

```bash
head notes.txt        # first 10 lines (default)
head -n 5 notes.txt   # first 5 lines only
```

**Exam memory:** `head` = **head** of the file (top)

---

### `tail` — last lines (tail = bottom)

```bash
tail log.txt          # last 10 lines
tail -n 3 log.txt     # last 3 lines
```

**Exam memory:** `tail` = **tail** of the file (bottom)

---

## Search & filter text

### `grep` — **G**lobal search **R**egular **E**xpression **P**rint (search text)

```bash
grep "error" log.txt              # lines containing "error"
grep -i "linux" file.txt           # -i = ignore case (Linux, LINUX...)
dmesg | grep usb                   # filter kernel messages for "usb"
```

**Exam memory:** `grep` = "**G**rab **r**elevant **e**xcerpt **p**attern"

---

### `find` — find files by name/location

```bash
find . -name "notes.txt"           # find file in current folder
find /home -name "*.txt"             # all .txt in /home
find . -type f -name "*.txt"         # -type f = files only (not folders)
```

| Part | Meaning |
|------|---------|
| `.` | start search here (current folder) |
| `-name` | match this name |
| `*.txt` | wildcard — any name ending in .txt |

**Exam memory:** `find` = **find** a needle in the filesystem

---

### `wc` — **W**ord **C**ount

```bash
wc notes.txt
# Output:  5  20  120 notes.txt
#         lines words characters
```

**Exam memory:** `wc` = **w**ord **c**ount

---

### `sort` — sort lines alphabetically

```bash
sort names.txt        # A → Z
```

---

### `uniq` — remove **adjacent** duplicate lines

```bash
sort names.txt | uniq    # sort FIRST, then remove duplicates
```

⚠️ `uniq` only removes duplicates **next to each other** — that's why we `sort` first.

---

### `tr` — **tr**anslate / replace characters

```bash
cat file.txt | tr 'a' 'A'     # replace lowercase a with A
cat file.txt | tr '[:lower:]' '[:upper:]'   # all to UPPERCASE
```

**Exam memory:** `tr` = **tr**ansform characters

---

## Output redirection

### `echo` + `>` — write text to file

```bash
echo "Hello" > file.txt       # create/overwrite with "Hello"
cat file.txt                  # Hello
```

**Exam memory:** `>` = **arrow into file** (overwrite)

---

## Archives & compression

### `tar` — **t**ape **ar**chive (bundle files into one .tar)

```bash
tar -cvf archive.tar folder/     # create archive
#  c = create
#  v = verbose (show files)
#  f = filename (archive.tar)
```

**Exam memory:** `tar -cvf` = "**c**reate **v**erbose **f**ile"

---

### `gzip` — compress a file (makes .gz)

```bash
gzip bigfile.txt        # creates bigfile.txt.gz, removes original
gzip -k bigfile.txt     # -k = keep original too
```

Often combined:

```bash
tar -cvf backup.tar myfolder/
gzip backup.tar          # → backup.tar.gz
```

**Exam memory:** `gzip` = **zip** (compress) to save space

---

## Category 2 — quick practice scenario

```bash
echo -e "banana\napple\nbanana\ncherry" > fruits.txt
cat fruits.txt
sort fruits.txt | uniq          # apple, banana, cherry
grep "banana" fruits.txt        # find banana
head -n 2 fruits.txt
wc fruits.txt
tar -cvf fruits.tar fruits.txt
gzip fruits.tar
```

---

# Category 3 — System, Hardware & Processes

> **Memory story:** You are the **technician** — check RAM, CPU, USB devices, kernel messages, running programs, and boot mode.

---

## System information (TP5)

### `uname -a` — **u**nix **name** — all system info

```bash
uname -a
# Linux esip-pc 5.15.0 ... x86_64 GNU/Linux
```

**Exam memory:** `uname -a` = "**u**niversal **name**" of the system

---

### `hostname` — computer name

```bash
hostname
# esip-pc
```

---

### `lsb_release -a` — Linux distribution (Ubuntu version, etc.)

```bash
lsb_release -a
# Distributor ID: Ubuntu
# Release: 22.04
```

**Exam memory:** which **Linux flavor** you have

---

### `uptime` — how long system has been running

```bash
uptime
# 10:30:00 up 2 days, 3:15, 2 users, load average: 0.50, 0.30, 0.20
```

**Exam memory:** "**up**" time = since last reboot

---

### `free -h` — **free** memory (RAM)

```bash
free -h
#               total   used   free
# Mem:           7.7Gi  2.1Gi  4.2Gi
```

**Exam memory:** `free -h` = how much RAM is **free** (**h** = human readable)

---

### `df -h` — **d**isk **f**ree — disk space usage

```bash
df -h
# Filesystem  Size  Used  Avail  Use%  Mounted on
# /dev/sda1   50G   20G   28G    42%   /
```

**Exam memory:** `df` = **d**isk **f**ull? check space

---

### `top` — live monitor (CPU, RAM, processes)

```bash
top
```

Press **`q`** to quit. Like Task Manager.  
**Exam memory:** `top` = what's on **top** (using most CPU)

---

## Hardware & kernel (TP1)

### `lspci` — list **PCI** devices (graphics card, network card…)

```bash
lspci
# 00:02.0 VGA compatible controller: Intel ...
# 03:00.0 Network controller: ...
```

**Exam memory:** **l**i**s**t **PCI** (internal hardware slots)

---

### `lsusb` — list **USB** devices

```bash
lsusb
# Bus 001 Device 002: ID 046d:c52b Logitech USB Receiver
```

**Exam memory:** **l**i**s**t **USB** (keyboard, mouse, flash drive)

---

### `dmesg` — **d**evice **mes**sa**g**es (kernel log)

```bash
dmesg                          # all kernel messages
dmesg | grep usb               # only USB-related messages
```

**Exam memory:** `dmesg` = kernel **mes**sa**g**es (hardware events at boot)

---

### `lsmod` — list loaded kernel **mod**ules

```bash
lsmod
# Module          Size  Used by
# usb_storage     ...   ...
```

**Exam memory:** **l**i**s**t **mod**ules (drivers loaded in kernel)

---

### `modprobe` — load a kernel module

```bash
sudo modprobe usb_storage    # load USB storage driver
```

**Exam memory:** **mod**ule — **probe** (load) it

---

## Block devices & BIOS (TP2)

### `lsblk` — list **block** devices (disks & partitions)

```bash
lsblk
# NAME   MAJ:MIN RM  SIZE  RO TYPE MOUNTPOINT
# sda      8:0    0   50G   0 disk
# ├─sda1   8:1    0   49G   0 part /
# └─sda2   8:2    0    1G   0 part [SWAP]
```

With filesystem info:

```bash
lsblk -f    # shows UUID, filesystem type (ext4, ntfs...)
```

**Exam memory:** **l**i**s**t **block** devices = hard drives

---

### `journalctl` — system **journal** (logs)

```bash
journalctl                     # all logs
journalctl -b                  # logs since last boot
```

**Exam memory:** **journal** = system diary / logs

---

### `dmidecode` — BIOS / hardware info from firmware

```bash
sudo dmidecode
# BIOS version, RAM slots, manufacturer...
```

**Exam memory:** **DMI** = desktop management info (deep hardware)

---

## Process management

### `ps` — **p**rocess **s**tatus (running programs)

```bash
ps                # your processes
ps aux            # all processes (detailed)
```

**Exam memory:** `ps` = **p**rocess **s**napshot

---

### `kill` — stop a process by PID

```bash
ps aux | grep firefox    # find PID (e.g. 4521)
kill 4521                # stop it
kill -9 4521             # force kill if normal kill fails
```

**Exam memory:** `kill` = kill process number (**PID**)

---

## Systemd boot targets (TP3)

### What is a target?

A **target** = boot **mode** (like choosing GUI or recovery at startup).

| Target | Mode |
|--------|------|
| `graphical.target` | Normal desktop with **GUI** |
| `multi-user.target` | **CLI** only (no GUI) — text mode |
| `rescue.target` | **Recovery** mode (minimal, for fixing) |

---

### `systemctl set-default` — set default boot mode

```bash
sudo systemctl set-default multi-user.target    # boot to CLI by default
sudo systemctl set-default graphical.target     # boot to GUI by default
```

**Exam memory:** **set-default** = what mode at **next reboot**

---

### `systemctl isolate` — switch mode **right now**

```bash
sudo systemctl isolate multi-user.target    # switch to CLI now
sudo systemctl isolate graphical.target     # switch to GUI now
sudo systemctl isolate rescue.target        # enter rescue mode now
```

**Exam memory:** **isolate** = switch **immediately** (not waiting for reboot)

---

## Category 3 — quick practice scenario

```bash
uname -a && hostname && uptime
free -h
df -h
lsusb
lspci
lsblk
ps aux | head
systemctl get-default          # see current default target
```

---

# Category 4 — Disks, Permissions, Network & Packages

> **Memory story:** You are the **admin** — partition the hard drive, control who can read/write files, connect to network, install software.

---

## Disk partitioning (TP4)

### Identify disks first

```bash
lsblk -f          # disks + filesystem labels
sudo fdisk -l     # list all partitions (detailed)
```

---

### `fdisk` — partition tool (interactive)

Enter fdisk on a disk:

```bash
sudo fdisk /dev/sdb
```

**Inside fdisk — commands you must know:**

| Command | Action | Memory trick |
|---------|--------|--------------|
| `g` | Create **G**PT partition table | **G**PT table |
| `n` | **N**ew partition | **N**ew |
| `t` | Change partition **t**ype | **T**ype |
| `p` | **P**rint table (show partitions) | **P**rint |
| `w` | **W**rite changes and quit | **W**rite (save!) |
| `q` | Quit **without** saving | **Q**uit |

**Example session:**

```bash
sudo fdisk /dev/sdb
g          # create GPT
n          # new partition → enter sizes
t          # change type if needed
p          # verify table
w          # save and exit
```

---

### `parted` — another partition tool

```bash
sudo parted /dev/sdb
```

**parted commands:**

| Command | Action |
|---------|--------|
| `mklabel gpt` | Create GPT label |
| `mkpart primary fat32 1MiB 512MiB` | Create partition |
| `set 1 esp on` | Set partition 1 as EFI System Partition |
| `print` | Show partition table |
| `quit` | Exit |

**Exam memory:** `mklabel gpt` → `mkpart` → `set 1 esp on` → `print` → `quit`

---

### `gparted` — graphical version of parted

GUI tool — same idea as `parted` but with mouse. Exam may ask the name only.

---

## Permissions

### `chmod` — **ch**ange **mod**e (file permissions)

Linux permissions: **read (r)**, **write (w)**, **execute (x)**

```bash
chmod 755 script.sh       # rwxr-xr-x
chmod +x script.sh        # add execute for everyone
chmod 644 file.txt        # rw-r--r-- (owner read/write, others read)
```

**Number trick (exam):**

| Number | Permission |
|--------|------------|
| 4 | read (r) |
| 2 | write (w) |
| 1 | execute (x) |
| 7 = 4+2+1 | rwx |
| 5 = 4+1 | r-x |
| 6 = 4+2 | rw- |

**Exam memory:** `chmod 755` = owner full, group/others read+execute

---

## Package management

### `apt-get install` — install software (Debian/Ubuntu)

```bash
sudo apt-get update                    # refresh package list
sudo apt-get install tree              # install "tree" program
```

**Exam memory:** `apt-get install` = **get** and **install** a package

---

## Networking

### `ip a` — show **IP** **a**ddresses (modern command)

```bash
ip a
# inet 192.168.1.50/24 ...  ← your IP address
```

**Exam memory:** `ip a` = show **IP** **a**ddresses

---

### `ifconfig` — old way to show network (deprecated)

```bash
ifconfig
```

Still mentioned in exams but **`ip a`** is preferred today.

---

### `ssh` — **S**ecure **Sh**ell (connect to remote computer)

```bash
ssh rayen@192.168.1.10
# connects to computer 192.168.1.10 as user "rayen"
```

**Exam memory:** `ssh user@host` = remote login securely

```
ssh  USER  @  HOST
     │        │
   rayen   192.168.1.10
```

---

## Category 4 — quick practice scenario

```bash
lsblk -f
sudo fdisk -l
ip a
chmod 644 myfile.txt
sudo apt-get install htop
```

---

# Quick exam cheat sheet

## The 4 categories in one glance

```
1. FILES & FOLDERS     →  ls, cd, pwd, cp, mv, rm, mkdir, touch, man
2. TEXT & ARCHIVES      →  cat, grep, find, head, tail, wc, tar, gzip, >
3. SYSTEM & HARDWARE    →  top, free, df, ps, kill, lspci, lsusb, dmesg,
                           lsblk, systemctl, journalctl, uname
4. DISKS & ADMIN        →  fdisk, parted, chmod, ip a, ssh, apt-get
```

## Most tested patterns

| Pattern | Meaning |
|---------|---------|
| `command --help` | Quick help |
| `man command` | Full manual |
| `cmd1 \| cmd2` | Pipe output to next command |
| `echo "text" > file` | Write to file |
| `sudo command` | Run as administrator |
| `ls -lah` | List all, detailed, human sizes |
| `find . -name "*.txt"` | Find txt files here |
| `dmesg \| grep usb` | USB kernel messages |
| `systemctl isolate rescue.target` | Enter rescue mode now |
| `fdisk`: g, n, t, p, w | GPT, new, type, print, write |
| `ssh user@host` | Remote connection |

## fdisk vs parted — don't mix up

| Tool | Style | Key commands |
|------|-------|--------------|
| **fdisk** | Interactive letters | `g`, `n`, `t`, `p`, `w` |
| **parted** | Text commands | `mklabel gpt`, `mkpart`, `set 1 esp on`, `print`, `quit` |

## systemd targets — don't mix up

| Command | When |
|---------|------|
| `set-default graphical.target` | Next **reboot** → GUI |
| `isolate rescue.target` | **Now** → recovery mode |

---

## 5-day study plan (for beginners)

| Day | Study | Practice |
|-----|-------|----------|
| **1** | Sections 1–2 + Category 1 | `pwd`, `cd`, `ls -lah`, `mkdir`, `touch`, `cp`, `mv` |
| **2** | Category 2 | `cat`, `grep`, `find`, `head`, `tail`, `tar`, `gzip` |
| **3** | Category 3 (system info) | `free -h`, `df -h`, `top`, `uname`, `uptime` |
| **4** | Category 3 (hardware) + 4 (network) | `lsusb`, `lspci`, `dmesg`, `ip a`, `chmod`, `ssh` |
| **5** | Category 4 (disks) + cheat sheet | `lsblk`, `fdisk -l`, fdisk commands, `systemctl` targets |

---

## Final tip for the exam

Read the question and ask yourself **which category**:

- Moving/copying a file? → **Category 1**
- Searching text in a log? → **Category 2**
- How much RAM is free? → **Category 3**
- Create a partition? → **Category 4**

Good luck on your Linux exam.
