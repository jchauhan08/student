---
layout: post
title: "Setup Blog"
date: 2025-09-09
categories: [Foundation, B-tools_and_equipment]
tags: [setup, blog, tools, equipment]
author: "Jaynee Chauhan"
summary: "A brief summary of the blog post goes here."
permalink: /tools/setup-blog/
---

# 🛠️ Windows (WSL) Operating System and Tools Setup

Welcome! This guide will help you set up your development environment using **Windows Subsystem for Linux (WSL)** with **Ubuntu**, along with useful tools like Git and VS Code.

---

## 📌 What You’ll Learn

- Installing WSL and Ubuntu
- Setting up developer tools
- Using Linux commands
- Working with Git (version control)
- Installing packages using apt
- Getting started with Visual Studio Code (VS Code)

---

## 🧠 Visual Workflow Overview

Here’s a simple step-by-step visual of how everything fits together:

```
💻 Open Windows Terminal
💻 Install WSL → wsl --install
💻 Launch Ubuntu Terminal → wsl
📁 Linux Commands → mkdir, cd, ls
📁 Clone Project → git clone https://...
🛠️ Activate Tools → Ruby, Python, Git
🔄 Work Cycle → code → make → test → commit
```



## 🧰 Windows Setup

### ✅ Install Visual Studio Code (VS Code)

1. Go to [https://code.visualstudio.com](https://code.visualstudio.com)
2. Download the installer for **Windows**
3. Install it using the default options

### ✅ Install Git Credential Manager (GCM)

1. Download from [https://aka.ms/gcm](https://aka.ms/gcm)
2. Run the installer and select default options


## 🐧 WSL Setup (Windows Subsystem for Linux)

### 💾 Install WSL and Ubuntu

1. Open **Windows Terminal** and pin it to your taskbar
2. Run this command to install WSL with Ubuntu 24.04:

    ```bash
    wsl --install -d Ubuntu-24.04
    ```

    When asked, create a username and password

    > **Note:** When typing the password, nothing will show—this is normal.

3. Once Ubuntu starts, exit the terminal:

    ```bash
    exit
    ```

4. Set Ubuntu 24.04 as default:

    ```bash
    wsl --set-default Ubuntu-24.04
    ```

5. To reopen Ubuntu later, just run:

    ```bash
    wsl
    ```


### 🛠️ First-Time Ubuntu Setup

Open Ubuntu by right-clicking the terminal and choosing Ubuntu 24.04

Run these commands to set up your dev environment:

```bash
mkdir opencs
cd opencs
git config --global credential.helper "/mnt/c/Program Files/Git/mingw64/bin/git-credential-manager.exe"
git clone https://github.com/Open-Coding-Society/student.git
cd student/
./scripts/activate_ubuntu.sh
./scripts/activate.sh
./scripts/venv.sh
```

These scripts will ask for your WSL password, GitHub username, and email.

---

### 🐚 Common Shell Commands

| Action         | Command                |
| -------------- | --------------------- |
| Make folder    | `mkdir folder-name`    |
| Change folder  | `cd folder-name`       |
| List files     | `ls`                   |
| Go back        | `cd ..`                |

---

### 🔧 Git (Version Control) Commands

| Purpose        | Command                        |
| -------------- | ----------------------------- |
| Clone repo     | `git clone <repo-url>`         |
| Pull updates   | `git pull`                     |
| Save changes   | `git commit -m "your message"` |
| Push changes   | `git push`                     |

---

### 📦 Package Management with apt (Ubuntu)

| Purpose                | Command                          |
| ---------------------- | -------------------------------- |
| Update package list    | `sudo apt update`                |
| Upgrade all packages   | `sudo apt upgrade`               |
| Install a package      | `sudo apt install <package>`     |
| Remove a package       | `sudo apt remove <package>`      |
| Search for a package   | `apt search <package>`           |
| List installed packages| `apt list --installed`           |

---

### 🧪 System Checks (Optional)

To check your system and tool versions, run:

```bash
python --version
pip --version
ruby -v
bundle -v
gem --version
git config --global --list
```

---

### 🔁 Restarting Your Development Terminal

Each time you open a new terminal:

Open Ubuntu 24.04 from your pinned terminal

Run:

```bash
cd opencs/student
source venv/bin/activate
code .
```

---

### ✅ Helpful WSL Commands

| Purpose                    | Command                          |
| -------------------------- | -------------------------------- |
| WSL help menu              | `wsl --help`                     |
| List all installed distros | `wsl -l -v`                      |
| Shutdown WSL               | `wsl --shutdown`                 |
| Unregister/remove a distro | `wsl --unregister <name>`        |

---

You're all set! 🎉  
You now have a basic Linux development environment running inside Windows. Start coding!
```
---

## 🙋 Frequently Asked Questions (FAQ)

<details>
<summary><strong>Do I need to pay for any of these tools?</strong></summary>

No, all tools listed (WSL, Ubuntu, Git, VS Code) are free and open source.
</details>

<details>
<summary><strong>What if I already have WSL or Ubuntu installed?</strong></summary>

You can skip the installation steps and proceed to setting up your development environment.
</details>

<details>
<summary><strong>How do I update my tools later?</strong></summary>

Use `sudo apt update && sudo apt upgrade` in Ubuntu, and check for updates in VS Code and Git as needed.
</details>

<details>
<summary><strong>Where can I get help if I’m stuck?</strong></summary>

- Check the [official WSL documentation](https://learn.microsoft.com/en-us/windows/wsl/)
- Visit [GitHub Discussions](https://github.com/Open-Coding-Society/student/discussions)
- Ask your peers or mentors
</details>

---

## 📝 Tips for Success

- **Bookmark this guide** for quick reference.
- **Practice using the terminal**—the more you use it, the easier it gets.
- **Keep your system updated** for security and new features.
- **Don’t be afraid to experiment**—mistakes are part of learning!

---

## 📚 Additional Resources

- [WSL Official Documentation](https://learn.microsoft.com/en-us/windows/wsl/)
- [Ubuntu Manual](https://help.ubuntu.com/)
- [GitHub Learning Lab](https://lab.github.com/)
- [VS Code Docs](https://code.visualstudio.com/docs)

---

Happy coding! 🚀 If you have suggestions to improve this guide, feel free to contribute or open an issue on the project repository.