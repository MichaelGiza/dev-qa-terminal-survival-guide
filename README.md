# 🐧 🪟 🍏 Terminal Cheat Sheet for Dev & QA

A practical breakdown of essential terminal commands for **Linux**, **macOS**, and **Windows (PowerShell)**. 

This cheat sheet isn't an encyclopedia. It contains only the commands that developers and QA engineers use in 95% of their daily commercial work.

---

## 📊 1. Main commands comparison

Modern Windows PowerShell comes with built-in *aliases* (shortcuts) that mimic Linux commands. This allows you to use the same intuitive commands on Windows.

| Action | Linux / macOS | Windows PowerShell (Alias) |
| :--- | :--- | :--- |
| **Who am I? (Current user)** | `whoami` | `whoami` |
| **View command history** | `history` *(persistent)* | `history` *(current session only)* |
| **Check active network connections / occupied ports** | `netstat -tuln` or `lsof -i` | `netstat -ano` |
| **List ALL running processes (for debugging)** | `ps aux` | `ps` |
| **Filter processes by name (e.g., Chrome)** | `ps aux \| grep chrome` | `ps chrome` |
| **Close process (Graceful)** | `kill PID` | `kill id` |
| **Kill process (Force)** | `kill -9 PID` | `kill id -fo` |
| **Where am I?** | `pwd` | `pwd` |
| **Clear console** | `clear` | `clear` or `cls` |
| **List files in folder (Names only in Unix)** | `ls` | `ls` or `dir` *(detailed by default)* |
| **List files with specific extension (e.g., .txt)** | `ls *.txt` | `ls *.txt` or `dir *.txt` |
| **List files in folder (Long / Detailed)** | `ls -l` | `ls` or `dir` *(detailed by default)* |
| **List files in folder (Hidden files / Names only)** | `ls -a` | `ls -Force` or `dir -Force` *(detailed by default)* |
| **List files in folder (Long / Detailed & Hidden)** | `ls -la` | `ls -Force` or `dir -Force` *(detailed by default)* |
| **Change directory (Enter folder)** | `cd folder1` | `cd folder1` |
| **Change directory (Two levels deep)** | `cd folder1/folder2` | `cd folder1\folder2` or `cd folder1/folder2` |
| **Go up one folder** | `cd ..` | `cd ..` |
| **Go up two folders** | `cd ../..` | `cd ../..` |
| **Go to Home directory** | `cd ~` or `cd` | `cd ~` |
| **Go to Root directory (Main drive)** | `cd /` | `cd \` *or `cd /`* |
| **Copy file (Create a duplicate)** | `cp file1.txt file1_copy.txt` | `cp file1.txt file1_copy.txt` |
| **Copy folder (with contents)** | `cp -r folder1 folder1_copy` | `cp -r folder1 folder1_copy` |
| **Create folder** | `mkdir folder_name` | `mkdir folder_name` |
| **Create empty file** | `touch file.txt` | `ni file.txt` |
| **Delete file** | `rm file.txt` | `rm file.txt` or `del file.txt` |
| **Delete file (force)** | `rm -f file.txt` | `rm -force file.txt` |
| **Delete folder** | `rm -r folder_name` | `rm -r folder_name` |
| **Delete folder (force)** | `rm -rf folder_name` | `rm -r -fo folder_name` |
| **Rename file/folder** | `mv folder_name new_name` | `mv folder_name new_name` |
| **Move file/folder to directory** | `mv file.txt folder_name/` | `mv file.txt folder_name/` |
| **Display file content** | `cat file.txt` | `cat file.txt` |
| **Display file last lines** | `tail file.txt` *(default 10)*| `Get-Content file.txt -Tail 10` *(define lines)* |
| **Display file last lines in real time** | `tail file.txt`| `Get-Content file.txt -Wait` |
| **Display file first lines** | `head -n 10 file.txt` *(e.g., 10)*| `Get-Content file.txt -TotalCount 10` *(e.g., 10)* |
| **Search text in a file** | `grep "text" file.txt`| `Select-String "text" file.txt`|
| **Search text in a file (ignore case)** | `grep -i "text" file.txt`| `Select-String "text" file.txt` *(ignore default)*|
| **Display all variables** | `printenv`| `dir env:`|
| **Compress folder** | `tar -czvf arc.tar.gz folder_name/`| `Compress-Archive -Path folder_name -DestinationPath arc.zip`|

---

## 📝 2. Terminal File Editors (Vim & Nano Survival Guide)

Here is how to quickly handle file editing inside the terminal when GUI tools are not available.
> ⚠️ Do not expect `nano` to be everywhere.

### 📝 Quick Text Editing (Vim & Nano)

* **Problem:** I need to quickly edit a configuration file directly in the terminal.
    * *Solution (Nano):*
      ```bash
        nano config.txt
        ```
    * *Nano Survival Guide:*
        * **Edit:** Just start typing.
        * **Save:** Press `Ctrl + O`, then `Enter`.
        * **Exit:** Press `Ctrl + X`.

* **Problem:** I need to edit a file on a remote production server where Nano is not available.
    * *Solution (Vim):*
      ```bash
        vim config.txt
        ```
    *  Vim starts in **Normal Mode** (you cannot type text immediately). You must switch modes to do anything.

---

### 🧗 Vim Essentials (How to Actually Use It)

* **Problem:** I opened Vim, but I cannot type any text.
    * *Action:* Press **`i`** on your keyboard to enter **Insert Mode**. You will see `-- INSERT --` at the bottom. Now you can type normally.

* **Problem:** I finished editing and I want to save or exit, but typing just adds characters to the file.
    * *Action:* Press **`Esc`** to leave Insert Mode and return to **Normal Mode**.

* **Problem:** I am in Normal Mode (after pressing Esc), and I want to save my changes and close the editor.
    * *Action:* Type **`:wq`** and press **`Enter`** *(write and quit)*.

* **Problem:** I messed up the configuration file, and I want to exit immediately WITHOUT saving anything.
    * *Action:* Type **`:q!`** and press **`Enter`** *(force quit)*.

---

### 💡 Summary of Terminal Editor Commands

| Intended Goal | Vim Command (In Normal Mode) | Nano Shortcut |
| :--- | :--- | :--- |
| **Open File** | `vim filename` | `nano filename` |
| **Start Typing** | Press `i` | Just start typing |
| **Stop Typing / Change Mode** | Press `Esc` | *Not applicable* |
| **Save Changes** | Type `:w` + `Enter` | `Ctrl + O` + `Enter` |
| **Save & Exit** | Type `:wq` + `Enter` | `Ctrl + O` then `Ctrl + X` |
| **Exit Without Saving** | Type `:q!` + `Enter` | `Ctrl + X` then type `n` |

---

## 🐧🔒 3. Linux Permissions (File Access Control)

In Linux, every file and directory is assigned to one specific **Owner** and one specific **Group**. You can control who can **Read (r)**, **Write (w)**, and **Execute (x)** based on three target categories.

### 📋 Security Groups

* **👤 Owner (User):** The specific user account that owns the file (usually its creator).
* **👥 Group:** A collection of users (e.g., `qa-team`, `developers`). Any member of this group inherits these permissions.
* **🌍 Others (World):** Everyone else who has an account on the system (neither the owner nor part of the group).

#### 🚦 How Linux Checks Identity (The Hierarchy)
When you try to access a file, Linux resolves your identity in a strict top-down order. **It stops checking the moment it finds the first match:**

```text
 👤 ARE YOU THE OWNER?
   ├──► YES: System applies OWNER permissions. (Checks stop here)
   └──► NO: 
         ▼
 👥 ARE YOU A MEMBER OF THE FILE'S GROUP?
   ├──► YES: System applies GROUP permissions. (Checks stop here)
   └──► NO: 
         ▼
 🌍 OTHERS: System applies OTHERS permissions to everyone else.
```

### 🔢 Quick Reference for `chmod` and `chown` (Octal Notation)

Each group's value is the sum of its active rights (r=4, w=2, x=1):

* **`r` (4):** Read
* **`w` (2):** Write
* **`x` (1):** Execute
* **`-` (0):** No Permission

#### Standard Combinations:
* **7 (4+2+1):** `rwx` – Read + Write + Execute *(Full permissions)*
* **6 (4+2+0):** `rw-` – Read + Write *(Modify without execution)*
* **5 (4+0+1):** `r-x` – Read + Execute *(Read and run, no modifying)*
* **4 (4+0+0):** `r--` – Read Only *(Strictly restricted)*
* **0 (0+0+0):** `---` – No Access *(Completely blocked)*

### 💡 Quick Tip:
* **`chmod`**: Changes the **rules** (what can be done with the file).
* **`chown`**: Changes the **owner** (who the file belongs to).

### 🛠️ Changing permissions (`chmod`)

```bash
# Add execute permission to a file (required for scripts)
chmod +x file.sh

# Owner gets full access (7); group & others get nothing (00)
chmod 700 file

# Owner gets full access (7); group & others get read/execute only (55)
chmod 755 dir

# Owner can read/write (6); group & others can only read (44)
chmod 644 file

```

### 🖥️ CLI Visual Layout - description of permissions (`chmod`)

#### 📄Case 1: Regular File 
When you run `ls -l`, the terminal removes all spaces to save screen real estate, displaying it as a solid string: `-rw-r--r--`. 
```text
CLI OUTPUT:    -rw-r--r--  1  user  group  1024  Nov 18 12:40  my_file.txt
                └─────────┘
                     │
                     ▼
 HOW THE SYSTEM PARSES IT (HIDDEN SECTIONS):
 
       TYPE      │  OWNER PERMISSIONS  │   GROUP PERMISSIONS   │   OTHERS PERMISSIONS
 ────────────────┼─────────────────────┼───────────────────────┼───────────────────────
        -        │   r     w     -     │   r     -     -       │   r     -     -
 ────────────────┼─────────────────────┼───────────────────────┼───────────────────────
        │        │   │     │     │     │   │     │     │       │   │     │     │
        ▼        │   ▼     ▼     ▼     │   ▼     ▼     ▼       │   ▼     ▼     ▼
 [Not directory] │ [Read][Write][EXEC] │ [Read][WRITE][EXEC]   │ [Read][WRITE][EXEC]
   (File Type)   │              (OFF)  │        (OFF) (OFF)    │        (OFF) (OFF)
```

#### 📁 Case 2: Directory 
When you run `ls -l`, the terminal removes all spaces to save screen real estate, displaying it as a solid string: `drwxr-xr-x`. 

However, the operating system strictly parses this string into separate, hidden columns of **fixed positions**. 

 ```text
 CLI OUTPUT:    drwxr-xr-x  2  user  group  4096  Nov 18 12:40  my_folder/
                └─────────┘
                     │
                     ▼
 HOW THE SYSTEM PARSES IT (HIDDEN SECTIONS):
 
     TYPE    │  OWNER PERMISSIONS  │   GROUP PERMISSIONS   │   OTHERS PERMISSIONS
 ────────────┼─────────────────────┼───────────────────────┼───────────────────────
      d      │   r     w     x     │   r     -     x       │   r     -     x
 ────────────┼─────────────────────┼───────────────────────┼───────────────────────
      │      │   │     │     │     │   │     │     │       │   │     │     │
      ▼      │   ▼     ▼     ▼     │   ▼     ▼     ▼       │   ▼     ▼     ▼
 [Directory] │ [Read][Write][Exec] │ [Read][WRITE][Exec]   │ [Read][WRITE][Exec]
 (File Type) │                     │        (OFF)          │        (OFF)
```

### 🛠️ Changing Ownership (`chown`)

```bash
# Change the owner of a file
sudo chown user_name file.txt

# Change both the owner and the group simultaneously
sudo chown user_name:group_name file.txt

# Recursively change ownership of a directory and all its contents (-R)
sudo chown -R user_name:group_name /path/to/folder/

```

#### 🖥️ CLI Visual Layout - description of owners  (`chown`)

To understand who owns a file and how it is linked, we look at the full long-format output.

#### 📄 Case 1: Regular File (Hard Link Count = 1)

```text
 -rw-r--r--  1  john  developers  1024  Nov 18 12:40  my_file.txt
 └────────┘  │  └──┘  └────────┘  └──┘  └──────────┘  └─────────┘
     │       │   │        │         │         │            │
     │       │   │        │         │         │            └── Resource Name
     │       │   │        │         │         └─────────────── Last Modified Time
     │       │   │        │         └───────────────────────── File Size (Bytes)
     │       │   │        └─────────────────────────────────── GROUP (Team Access)
     │       │   └──────────────────────────────────────────── OWNER (User Account)
     │       └──────────────────────────────────────────────── HARD LINKS (1 = Just this file)
     └──────────────────────────────────────────────────────── File Type & Permissions (description in section above)
```
#### 📁 Case 2: Empty Directory (Hard Link Count = 2)

```text
drwxr-xr-x  2  john  developers  4096  Nov 18 12:40  my_folder
 └────────┘  │  └──┘  └────────┘  └──┘  └──────────┘  └────────┘
     │       │   │        │         │         │            │
     │       │   │        │         │         │            └── Folder Name
     │       │   │        │         │         └─────────────── Last Modified Time
     │       │   │        │         └───────────────────────── Folder Metadata Size
     │       │   │        └─────────────────────────────────── GROUP (Team Access)
     │       │   └──────────────────────────────────────────── OWNER (User Account)
     │       └──────────────────────────────────────────────── HARD LINKS (2 = Folder + "." shortcut)
     └──────────────────────────────────────────────────────── File Type & Permissions (description in section above)

```

#### 📂 Case 3: Directory with Content (e.g., containing 3 Subfolders)

If a directory contains regular files, the link count **does not change**. However, every time you create a **subfolder** inside it, the parent directory's link count increases by 1.

```text
 drwxr-xr-x  5  john  developers  4096  Nov 18 12:40  my_folder
 └────────┘  │  └──┘  └────────┘  └──┘  └──────────┘  └────────┘
     │       │   │        │         │         │            │
     │       │   │        │         │         │            └── Folder Name
     │       │   │        │         │         └─────────────── Last Modified Time
     │       │   │        │         └───────────────────────── Folder Metadata Size
     │       │   │        └─────────────────────────────────── GROUP (Team Access)
     │       │   └──────────────────────────────────────────── OWNER (User Account)
     │       └──────────────────────────────────────────────── HARD LINKS (2 base links + 3 subfolders)
     └──────────────────────────────────────────────────────── File Type & Permissions (description in section above)
```
---

## 🪟🔒 4. What about Windows Permissions?

In daily Dev/QA work, **almost nobody manages Windows permissions via the CLI**. 

1. **GUI over CLI:** Windows uses complex ACLs (Access Control Lists). Modifying them via terminal commands like `icacls` or `Set-Acl` is extremely verbose and non-intuitive. If you ever need to change permissions on Windows, everyone just uses the right-click menu: `Properties ──► Security tab`.
2. **The Deployment Reality:** Production servers, Docker containers, and CI/CD pipelines run almost exclusively on **Linux**. This is why mastering `chmod` and `chown` is critical for deployment and debugging, while Windows permissions are usually left to the operating system's defaults.
