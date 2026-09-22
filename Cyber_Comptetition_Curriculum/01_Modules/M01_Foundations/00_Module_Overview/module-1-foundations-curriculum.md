# Instructor Guide & Lesson Plan: Module 1 — Foundations
**Course:** Cybersecurity Competition Training Curriculum
**Estimated Time:** 6 Hours (3 Hours Lecture, 3 Hours Hands-on Lab)
**Target Audience:** Community College Cybersecurity Students & Peer Faculty
**Created by:** Gemini Notebook (Collaborative Partner)

---

## 1. Module Overview & Metadata

### Description
Module 1 serves as the prerequisite foundation for all subsequent security, attack, investigation, and competition modules in this curriculum. The pedagogical core of this module is to teach students **how to operate and understand the environment before they are asked to secure, attack, investigate, or compete within it**. 

Students will build baseline competency in navigating Linux and Windows operating systems via Command Line Interfaces (CLI), understand fundamental networking architectures (the "plumbing" of the internet), establish isolated and safe virtual lab environments, and adopt industry-standard version control and technical documentation practices.

### Prerequisites
*   **Academic Prerequisites:** None. This is an entry-level gateway module.
*   **Technical Prerequisites:** Basic computer literacy (file management, web browsing).

### Competition Mapping
*   **National Cyber League (NCL):** Maps directly to **Open Source Intelligence (OSINT)** (basic networking/DNS queries) and builds the absolute baseline OS command skills needed for **Log Analysis**, **Network Traffic Analysis**, and **Web Application Security**.
*   **NCAE Cyber Games:** Prepares students for the **Infrastructure/Triage Phase** by teaching them how to log in, navigate, and run commands on unfamiliar systems under time constraints.

---

## 2. Learning Objectives
By the end of this module, students will be able to:
1.  **OS-LO-1:** Navigate both Linux and Windows file systems and perform file operations using CLI (bash) and PowerShell/CMD.
2.  **OS-LO-2:** Explain, configure, and troubleshoot basic user accounts, system permissions, active processes, and background services on Linux and Windows systems.
3.  **NET-LO-1:** Define and explain the relationship between MAC addresses, IP addresses (IPv4/IPv6), subnet masks, ports, and protocols (TCP/UDP).
4.  **NET-LO-2:** Query and troubleshoot core network services (DNS, DHCP, routing) using diagnostic utilities (`ping`, `traceroute`/`tracert`, `nslookup`, `netstat`/`ss`).
5.  **VIR-LO-1:** Install, configure, and manage virtual machines (VMs) using a Type-2 Hypervisor, utilizing snapshots and virtual host-only/NAT networks to maintain lab safety.
6.  **DOC-LO-1:** Utilize Git and GitHub for basic version control workflows (clone, add, commit, push) and format technical findings into professional markdown writeups.

---

## 3. Recommended Lab Environment & Tools
To successfully deliver this module, the department must provide or have students configure:
*   **Host System Requirements:** Intel i5/AMD Ryzen 5 (or better), 16GB RAM, 100GB free SSD space, virtualization enabled in BIOS/UEFI.
*   **Hypervisor:** VirtualBox (7.x+) or VMware Workstation Player (17.x+).
*   **Linux Virtual Machine:** Ubuntu Desktop 22.04 LTS or Debian 12 (configured with 2 vCPUs, 4GB RAM, 20GB Disk).
*   **Windows Virtual Machine:** Windows 10/11 Evaluation ISO or Windows Server 2022 Evaluation (configured with 2 vCPUs, 4GB RAM, 40GB Disk).
*   **Software Utilities:** Git CLI, VS Code (or a markdown editor of choice), and a GitHub account.

---

## 4. Complete Unit-by-Unit Lesson Plan

```
┌────────────────────────────────────────────────────────────────────────┐
│                      MODULE 1 TIME ALLOCATION                          │
│                                                                        │
│  Unit 1: Intro to Cyber Competitions (20m)                             │
│  Unit 2: Linux Fundamentals (50m)                                      │
│  Unit 3: Windows Fundamentals (50m)                                    │
│  Unit 4: Networking Fundamentals (60m)                                 │
│  Unit 5: Virtualization & Lab Safety (30m)                             │
│  Unit 6: Git & Documentation (30m)                                     │
│  Unit 7: Foundations Blue Team Lab (120m)                              │
│  Unit 8: Foundations Assessment (40m)                                  │
│  Unit 9: Module Review & Prep for Mod 2 (20m)                          │
└────────────────────────────────────────────────────────────────────────┘
```

---

### Unit 1: Introduction to Cyber Competition (20 Minutes)
*   **Objective:** Demystify cybersecurity competitions, define their rules, and establish motivation for technical foundational training.
*   **Lecture Slides Outline:**
    *   **Slide 1: Title & Welcome** (Course context, instructor info).
    *   **Slide 2: What is a CTF?** (Jeopardy-style vs. Attack-Defense; what are flags, how are points scored).
    *   **Slide 3: The NCL & NCAE Landscapes** (NCL individual categories, NCAE team infrastructure defense).
    *   **Slide 4: Why "Foundations First"?** (The absolute necessity of knowing the operating system before you can secure or attack it).
*   **Discussion Hook:** "Has anyone here ever played a video game where you had to find hidden secrets (easter eggs) or complete puzzles under pressure? How did you learn the controls before you tried the boss fights?"
*   **Common Misconceptions:**
    *   *Misconception:* "I need to learn how to hack immediately to compete."
    *   *Correction:* Competitions are won by teams who can quickly fix basic configuration errors, analyze logs, and understand system basics. Tools are secondary to fundamental comprehension.

---

### Unit 2: Linux Fundamentals (50 Minutes)
*   **Objective:** Enable students to confidently log into a Linux system, navigate directories, edit files, manage users/permissions, and identify running processes using the command line.
*   **Lecture Slides Outline:**
    *   **Slide 1: The Linux Philosophy & Architecture** (Kernel, Shell, Userspace; "Everything is a file" concept).
    *   **Slide 2: File System Navigation** (`pwd`, `ls -la`, `cd`, absolute vs. relative paths).
    *   **Slide 3: File Manipulation** (`touch`, `mkdir`, `cp`, `mv`, `rm`, `nano`/`vim`).
    *   **Slide 4: Reading and Searching Files** (`cat`, `less`, `head`, `tail`, `grep`, pipeline `|`).
    *   **Slide 5: Users, Groups, and Permissions** (File permissions `rwxrwxrwx`, `chmod` symbolic/octal, `chown`, `sudo`, `/etc/passwd`).
    *   **Slide 6: Process Management & Services** (`ps aux`, `top`, `kill`, `systemctl start/stop/status`).
*   **Class Demonstration Steps:**
    1. Open terminal on Ubuntu VM.
    2. Navigate to `/var/log` and use `tail -n 20 syslog` combined with `grep` to find system events.
    3. Create a new text file using `touch test.txt`, modify its permissions using `chmod 700 test.txt`, and show how non-root users are blocked.
    4. Start and stop the `ssh` service using `systemctl` and verify its state.
*   **Whiteboard Prompt:** Draw a standard Linux file system tree (`/`, `/home`, `/etc`, `/var`, `/bin`) and trace the path from `/home/user` to `/etc/passwd`.
*   **Common Misconceptions:**
    *   *Misconception:* Running `rm -rf` is safe if you are not root.
    *   *Correction:* It will still delete everything in your home directory that you own. Stress the importance of checking commands before pressing Enter under administrative rights (`sudo`).

---

### Unit 3: Windows Fundamentals (50 Minutes)
*   **Objective:** Familiarize students with Windows administrative paradigms, CLI (cmd.exe), PowerShell, the Registry, file permissions (NTFS/ACLs), and service management.
*   **Lecture Slides Outline:**
    *   **Slide 1: Inside Windows OS** (The hybrid kernel, GUI vs. CLI focus, User Account Control (UAC)).
    *   **Slide 2: Windows Command Prompt vs. PowerShell** (cmd.exe legacy shell vs. PowerShell object-oriented environment and Cmdlets).
    *   **Slide 3: Navigation & File Operations** (`dir`, `cd`, `copy`, `move`, `del`, `mkdir`, PowerShell equivalents like `Get-ChildItem`).
    *   **Slide 4: Windows Security & Access Control** (Users & Groups, local accounts vs. Active Directory, NTFS Permissions, ACLs).
    *   **Slide 5: Windows Services and Processes** (Task Manager, Services.msc, CLI tools: `tasklist`, `taskkill`, `Get-Process`, `Get-Service`).
    *   **Slide 6: The Windows Registry** (Purpose, structure: HKLM, HKCU, and its role as a configuration database).
*   **Class Demonstration Steps:**
    1. Open PowerShell as Administrator.
    2. Run `Get-Service | Where-Object {$_.Status -eq "Running"}` to display running services.
    3. Demonstrate creating a local user using `net user competition_user Password123! /add`.
    4. Explore the Registry using `regedit` (read-only demonstration of `HKLM\Software\Microsoft\Windows\CurrentVersion\Run` to explain startup persistence).
*   **Whiteboard Prompt:** Draw a comparison table showing equivalent CLI commands: e.g., Linux (`ls`, `cat`, `ps`, `ifconfig`) vs. Windows CMD (`dir`, `type`, `tasklist`, `ipconfig`) vs. PowerShell Cmdlets (`Get-ChildItem`, `Get-Content`, `Get-Process`, `Get-NetIPAddress`).
*   **Common Misconceptions:**
    *   *Misconception:* Windows Administrator accounts have unlimited privilege silently.
    *   *Correction:* User Account Control (UAC) prompts even administrators to confirm high-privilege activities, isolating the administrative token until approved.

---

### Unit 4: Networking Fundamentals (60 Minutes)
*   **Objective:** Explain network layer architectures, naming conventions, address resolutions, and essential diagnostic commands.
*   **Lecture Slides Outline:**
    *   **Slide 1: The Local Network** (What is a LAN? MAC Addresses vs. IP Addresses, Subnet Masks).
    *   **Slide 2: The TCP/IP Model vs. OSI Model** (Simplified layer explanation: Physical, Network, Transport, Application).
    *   **Slide 3: Ports and Protocols** (What is a socket? TCP vs. UDP, Common Ports: 22 SSH, 80 HTTP, 443 HTTPS, 53 DNS).
    *   **Slide 4: Key Network Services** (DHCP for address leasing, DNS for domain-to-IP resolution).
    *   **Slide 5: Troubleshooting Utilities** (`ping` for echo, `traceroute`/`tracert` for path analysis, `nslookup`/`dig` for name queries, `netstat`/`ss` for open ports).
*   **Class Demonstration Steps:**
    1. Run `ping 8.8.8.8` to show layer-3 IP connectivity.
    2. Run `nslookup google.com` to show DNS resolution.
    3. Run `netstat -ano` (Windows) and `ss -tulpn` (Linux) to display all currently open sockets and listening ports.
*   **Whiteboard Prompt:** Trace a packet from a browser entering `http://example.com` to the server: DNS resolution -> ARP request for Gateway MAC -> TCP Handshake -> HTTP GET request.
*   **Common Misconceptions:**
    *   *Misconception:* "Ping" uses TCP.
    *   *Correction:* `ping` utilizes ICMP (Internet Control Message Protocol), which runs directly on top of the Network Layer (IP) without utilizing TCP or UDP ports.

---

### Unit 5: Virtualization & Lab Safety (30 Minutes)
*   **Objective:** Instruct students on how to safely build, configure, isolate, and save their lab environments using Type-2 Hypervisors.
*   **Lecture Slides Outline:**
    *   **Slide 1: What is Virtualization?** (Type-1 Bare Metal vs. Type-2 Hosted Hypervisors).
    *   **Slide 2: VM Configuration Baselines** (vCPUs, RAM allocation, Guest Additions/Tools).
    *   **Slide 3: Virtual Networking Modes** (Bridged = Public exposed, NAT = Outbound only, Host-Only = Isolated lab LAN).
    *   **Slide 4: Snapshots: Your Lab Undo Button** (When to take snapshots, how to restore them, snapshot storage implications).
    *   **Slide 5: Cybersecurity Lab Safety Rules** (Never run offensive tools on bridged networks; isolate malware analysis; trust no external USB in labs).
*   **Class Demonstration Steps:**
    1. Show VirtualBox/VMware interface.
    2. Modify a VM's network adapter settings from NAT to Host-Only.
    3. Take a snapshot called "Pre-Hardening", delete a crucial system folder on the VM to crash it, and then cleanly restore the snapshot in under 30 seconds.
*   **Discussion Hook:** "If you are experimenting with a security script that might accidentally scan your local home router or smart TV, which VM network adapter mode should you use and why?"

---

### Unit 6: Git & Documentation (30 Minutes)
*   **Objective:** Teach version control fundamentals and professional technical writing structure for CTF writeups and competition forensics.
*   **Lecture Slides Outline:**
    *   **Slide 1: What is Version Control?** (Why tracking changes matters in code, configurations, and team notes).
    *   **Slide 2: Basic Git Workflow** (Initializing, Clones, Working Directory -> Staging Area -> Local Repository -> Remote Repository).
    *   **Slide 3: The Git Command Suite** (`git init`, `git clone`, `git status`, `git add`, `git commit -m`, `git push`).
    *   **Slide 4: Writing in Markdown** (Syntaxes for headers, lists, code blocks, tables, images).
    *   **Slide 5: Anatomy of a Security Writeup** (Executive Summary, Vulnerability/Problem, Step-by-Step Proof of Concept (PoC) with commands/screenshots, Remediation/Mitigation).
*   **Class Demonstration Steps:**
    1. Initialize a Git repository locally: `git init`.
    2. Create a markdown file: `README.md`.
    3. Add headers, code blocks with `bash` syntax, and bullet points.
    4. Run `git status`, `git add README.md`, `git commit -m "Initial commit of foundations guide"`.
*   **Common Misconceptions:**
    *   *Misconception:* Git and GitHub are the same thing.
    *   *Correction:* Git is the local CLI tool that tracks changes; GitHub is the remote cloud-hosted repository where teams push their local Git histories.

---

### Unit 7: Foundations Blue Team Lab (120 Minutes)
*   *Refer to the full Student Lab Guide for extensive details. Instructors should monitor student progress and provide hints on basic CLI syntax issues.*

### Unit 8: Foundations Assessment (40 Minutes)
*   *Refer to the Module 1 Assessment documentation for the written knowledge check and practical challenge parameters.*

### Unit 9: Module Review (20 Minutes)
*   **Objective:** Consolidate learnings from Module 1, answer outstanding questions, and preview how these operating system and network concepts are required for Module 2: Defensive Operations (Blue Teaming).
*   **Discussion Hook:** "Now that we can navigate Linux and Windows systems and see open ports, how do we start closing those ports and stopping unauthorized services next week?"

---

## 5. Peer Faculty Teaching Tips & Pedagogical Strategies
*   **The "I Do, We Do, You Do" Approach:** Operating system command line skills are best retained through immediate muscle memory. Encourage instructors to run CLI commands, have students type them simultaneously (We Do), and then assign minor independent command variants (You Do) before moving to the next slide.
*   **Overcoming Terminal Fear:** Many introductory community college students are intimidated by a blank, black command prompt. Instructors should emphasize that "command lines are just text-based search bars that have highly specific vocabulary." Frame commands as plain English requests (e.g., `cat` = "show me this," `grep` = "find this keyword").
*   **Emphasis on Lab Snapshots:** Force students to take a snapshot at the *beginning* of Unit 7's lab. If a student destroys their VM configuration (which is expected during early hardening attempts), the instructor should point out that restoration is a learning experience, not a failure.


================================================================================

# Student Lab Guide: Module 1 — Unit 7: Foundations Blue Team Lab
**Course:** Cybersecurity Competition Training Curriculum
**Focus:** Operating System & Networking Auditing, Hardening, and Technical Documentation

---

## 1. Lab Overview & Scenario

### The Scenario
You have been brought in as a junior cybersecurity consultant for **SudoCorp**, a small regional business. Their IT administrator recently set up two virtual machines (one Linux server and one Windows workstation) for testing but left them with several out-of-the-box configurations, insecure default user accounts, open legacy services, and weak file protections. 

Your mission is to perform a systematic **security audit** of these two systems, **harden** them against basic entry-level attacks, and **document** your discoveries and remediations in a professional Markdown format.

```
                  ┌──────────────────────────────┐
                  │      Host Hypervisor         │
                  │  (VirtualBox / VMware)       │
                  └──────────────┬───────────────┘
                                 │
                  ┌──────────────┴───────────────┐
                  │    Virtual Host-Only Network  │
                  │      Subnet: 192.168.56.0/24 │
                  └──────────┬──────────────┬────┘
                             │              │
    ┌────────────────────────┴──┐        ┌──┴────────────────────────┐
    │    Linux Server VM        │        │   Windows Workstation VM  │
    │  IP: 192.168.56.10        │        │   IP: 192.168.56.20       │
    │  OS: Ubuntu/Debian        │        │   OS: Windows 10 / 11     │
    └───────────────────────────┘        └───────────────────────────┘
```

### Objectives
*   Configure VM network interfaces for secure, isolated communication (Host-Only Network).
*   Conduct diagnostic network checks to map the virtual lab space.
*   Audit and remediate administrative permissions, user accounts, and credentials on Linux and Windows.
*   Identify, stop, and disable unauthorized or insecure active processes and listening network services.
*   Apply basic file permissions to protect confidential data.
*   Author a structured, professional Markdown writeup tracking your actions.

### Prerequisites
*   Successfully completed Unit 1 through Unit 6 lectures.
*   Your host system running a hypervisor (VirtualBox or VMware Player).
*   Both Linux and Windows VMs imported and powered on.

---

## 2. Lab Setup & Configuration
Before starting your audit, you must configure both virtual machines to run inside an **isolated local area network** to prevent traffic leakage to the public internet or your host system's primary interface.

### Step 1: Virtual Network Configuration (In the Hypervisor)
1.  **Shut down** both of your Virtual Machines if they are currently running.
2.  In your hypervisor settings (VirtualBox: *File* -> *Tools* -> *Network Manager*; VMware: *Virtual Network Editor*), verify that a **Host-Only Network Adapter** exists (typically named `vboxnet0` or `VMnet1` with IP range `192.168.56.0/24`).
3.  Right-click your **Linux Server VM**, select **Settings** -> **Network**.
    *   Change Adapter 1 from "NAT" to **Host-Only Adapter**.
    *   Select your host-only network name (e.g., `vboxnet0`).
4.  Right-click your **Windows Workstation VM**, select **Settings** -> **Network**.
    *   Change Adapter 1 from "NAT" to **Host-Only Adapter**.
    *   Select your host-only network name (e.g., `vboxnet0`).
5.  Power on **both** virtual machines.

### Step 2: System Credentials
Log into the virtual machines using the following default system credentials:
*   **Linux Server:** Username: `admin_user` | Password: `ChangeMe123!`
*   **Windows Workstation:** Username: `LocalAdmin` | Password: `ChangeMe123!`

---

## 3. Step-by-Step Lab Tasks

### Task 1: Virtual Network Mapping & Troubleshooting
Before securing the machines, you must establish that they can see and talk to each other on the local network.

1.  **Find the IP Address on Linux:**
    *   Open a terminal on your Linux VM.
    *   Run the command:
        ```bash
        ip address show
        ```
    *   Identify the interface name (e.g., `eth0` or `enp0s3`) and record the IPv4 address assigned to it. It should be in the `192.168.56.x` range.
2.  **Find the IP Address on Windows:**
    *   Open PowerShell as an Administrator on your Windows VM.
    *   Run the command:
        ```powershell
        Get-NetIPAddress -AddressFamily IPv4 -InterfaceAlias "Ethernet"
        ```
        *(Or run `ipconfig` in standard Command Prompt).*
    *   Record the IPv4 address. It should be in the `192.168.56.x` range.
3.  **Perform Connectivity Checks (Ping):**
    *   From your Linux Terminal, run a ping check to your Windows VM IP (replace with your actual Windows IP):
        ```bash
        ping -c 4 192.168.56.20
        ```
    *   *Note:* If the ping requests timeout, do not panic! Windows systems block incoming ICMP echo requests by default via their local firewall. We will address this soon.
    *   From your Windows PowerShell, ping your Linux VM IP (replace with your actual Linux IP):
        ```powershell
        ping 192.168.56.10
        ```
        This check should succeed. If it fails, double-check that both network adapters are mapped to the exact same host-only interface.

---

### Task 2: Linux System Audit & Hardening

Now you will analyze the security health of the Linux VM, delete unnecessary accounts, stop insecure legacy services, and lock down file permissions.

#### Subtask A: User Audit and Remediation
1.  **Identify accounts:** Linux stores local accounts in `/etc/passwd`. Review the active accounts on the system by executing:
    ```bash
    cat /etc/passwd | grep -E '/bin/bash|/bin/sh'
    ```
    This filters the file for users who have login shells.
2.  **Locate the intruder:** You will notice an unauthorized local account named `rogue_tester` with an active login shell.
3.  **Delete the rogue account:** Remove this user and delete their associated home directory by executing:
    ```bash
    sudo userdel -r rogue_tester
    ```
4.  **Harden administrative credentials:** The default administrative account `admin_user` has a weak password (`ChangeMe123!`). Change it to a strong, complex password using:
    ```bash
    sudo passwd admin_user
    ```
    *(Set a password with at least 12 characters, including numbers, uppercase, and special characters).*

#### Subtask B: Network Socket & Service Remediation
1.  **Scan active sockets:** Display all active, listening TCP and UDP connections along with their program names:
    ```bash
    sudo ss -tulpn
    ```
2.  **Analyze the results:**
    *   Look at the "Local Address:Port" column.
    *   You will find an active service listening on Port `23` (`*:23` or `0.0.0.0:23`). This is **Telnet**, an ancient, unencrypted, highly insecure protocol that transmits passwords in cleartext.
3.  **Kill the daemon:** Stop the active Telnet service and configure the system so it does not start automatically on boot:
    ```bash
    sudo systemctl stop inetd
    sudo systemctl disable inetd
    ```
    *(Note: On older Debian/Ubuntu systems, Telnet runs under the openbsd-inetd super-server).*
4.  **Verify shutdown:** Run `sudo ss -tulpn` again to confirm that Port 23 is no longer listening.

#### Subtask C: File System Security
1.  **Check weak file permissions:** The IT administrator left a backup file containing sensitive corporate records in `/home/admin_user/confidential_backups/company_secrets.txt`. Navigate to this directory and check its permissions:
    ```bash
    cd /home/admin_user/confidential_backups/
    ls -l company_secrets.txt
    ```
2.  **Assess the vulnerability:** You will see permissions of `-rwxrwxrwx` (octal `777`). This means *any* user on the Linux system can read, modify, or delete this file!
3.  **Apply restrictive permissions:** Restrict the permissions so that only the owner (`admin_user`) can read and write to the file, while groups and others have zero permissions:
    ```bash
    chmod 600 company_secrets.txt
    ```
4.  **Verify change:** Run `ls -l company_secrets.txt` to verify the permissions now display as `-rw-------`.

---

### Task 3: Windows System Audit & Hardening

Next, you will secure the Windows Workstation using PowerShell and native administrative consoles.

#### Subtask A: Windows User Accounts Review
1.  **Audit local accounts:** List all local user accounts registered on this computer using PowerShell:
    ```powershell
    Get-LocalUser
    ```
2.  **Analyze administrative group membership:** Check which accounts belong to the powerful Local Administrators group:
    ```powershell
    Get-LocalGroupMember -Group "Administrators"
    ```
3.  **Identify anomalies:** You will find an unauthorized user named `backdoor_user` inside the Administrators group.
4.  **Remediate user exposure:** Remove `backdoor_user` from the system entirely:
    ```powershell
    Remove-LocalUser -Name "backdoor_user"
    ```
5.  **Harden current administrator password:** Change the password for the default local account `LocalAdmin` to a secure, enterprise-grade password:
    ```powershell
    Set-LocalUser -Name "LocalAdmin" -Password (ConvertTo-SecureString "EnterpriseSecurePass987!" -AsPlainText -Force)
    ```

#### Subtask B: Insecure Windows Services Remediation
1.  **Query running services:** Search for services that are currently running but pose a known security risk. A major target is the outdated **Link-Local Multicast Name Resolution (LLMNR)** and unneeded remote administration tools. Let's find running services:
    ```powershell
    Get-Service | Where-Object {$_.Status -eq "Running"}
    ```
2.  **Stop unnecessary legacy service:** The legacy print spooler or unneeded sharing services may be active. Let's stop and disable the **Print Spooler** service (which has been the source of critical vulnerabilities like PrintNightmare):
    ```powershell
    Stop-Service -Name "Spooler" -Force
    Set-Service -Name "Spooler" -StartupType Disabled
    ```

#### Subtask C: Network Security & Firewall Hardening
1.  **Check firewall status:** Windows Defender Firewall is currently disabled across some network profiles. Check the status:
    ```powershell
    Get-NetFirewallProfile | Select-Object Name, Enabled
    ```
2.  **Enable Firewall globally:** Turn the Windows Defender Firewall ON for all profiles (Domain, Private, and Public) immediately to lock down the system:
    ```powershell
    Set-NetFirewallProfile -All -Enabled True
    ```
3.  **Verify changes:** Re-run `Get-NetFirewallProfile | Select-Object Name, Enabled` and verify that all profiles display `True`.

---

## 4. Documentation & Lab Submission (Markdown Writeup)

To complete this lab, you must write a comprehensive technical audit report in **Markdown format** and save it to your local Git directory. 

### Markdown Requirements
Your document must be saved as `module_1_lab_writeup.md` and contain the following structure:
1.  **Title and Author:** Module 1 Lab Writeup - [Your Name].
2.  **Task 1 Results:** A table recording the IP addresses and connectivity status of your virtual machines.
3.  **Task 2 (Linux Hardening Log):**
    *   State the command used to identify user accounts.
    *   State the command used to delete `rogue_tester`.
    *   State the port, protocol, and command used to identify and disable the Telnet daemon.
    *   Show before and after permission strings for `company_secrets.txt`.
4.  **Task 3 (Windows Hardening Log):**
    *   List the commands used to audit local administrative accounts and remove `backdoor_user`.
    *   List the commands used to stop and disable the Windows Print Spooler service.
    *   State the PowerShell command used to enable the Windows Firewall.
5.  **Executive Summary & Reflection:** Write a short, 3-4 sentence summary of what you learned and why performing an operating system audit is the mandatory starting point before running vulnerability scanners or offensive tools.

### Git Submission Steps
1. Navigate to your local git folder on your host machine or Linux VM.
2. Move your `module_1_lab_writeup.md` file into this folder.
3. Run the following Git commands to submit your writeup:
   ```bash
   git add module_1_lab_writeup.md
   git commit -m "Submit Module 1 Foundations Blue Team Lab Writeup"
   git push origin main
   ```


================================================================================

# Module 1 Assessment: Foundations Knowledge Check & Hands-on Challenge
**Course:** Cybersecurity Competition Training Curriculum
**Deliverable:** Written & Practical Assessment Bundle with Answer Key

---

## Part 1: Written Knowledge Check (10 Scenario-Based Questions)

These questions are designed to mimic the analytical thinking required in professional environments and cybersecurity competitions (such as the National Cyber League).

### Question 1 (Learning Objective: OS-LO-1)
A system administrator wants to find all instances of the word "vulnerability" inside a log file named `audit.log` located in `/var/log`, but only wants to display the first 5 matching occurrences. Which of the following commands accomplishes this task?
*   A) `grep -m 5 "vulnerability" /var/log/audit.log`
*   B) `head -n 5 /var/log/audit.log | grep "vulnerability"`
*   C) `cat /var/log/audit.log | tail -n 5 | grep "vulnerability"`
*   D) `less /var/log/audit.log | grep -n 5 "vulnerability"`

### Question 2 (Learning Objective: OS-LO-2)
An operator logs into a Linux machine and discovers that a file named `database.db` has permissions set to `rwsr-xr-x` (where the owner permissions include a SetUID bit). What is the security implication of this configuration?
*   A) The file is fully encrypted and can only be decrypted by the administrator.
*   B) Any user executing this file will run it with the permissions of the file's owner (typically root).
*   C) The file is a symbolic link pointing to a remote database server.
*   D) Only the owner is allowed to read and write to this database file.

### Question 3 (Learning Objective: OS-LO-2)
You need to stop a suspicious process on a Windows workstation immediately using PowerShell. You know the Process ID (PID) is `4512`. Which cmdlet should you execute?
*   A) `Stop-Service -Id 4512`
*   B) `Kill-Process -Name 4512`
*   C) `Stop-Process -Id 4512`
*   D) `Remove-Process -Pid 4512`

### Question 4 (Learning Objective: NET-LO-1)
A packet capture reveals communication occurring between a client machine and a server on Port `53` using UDP. Which service is most likely being utilized?
*   A) SSH (Secure Shell)
*   B) DNS (Domain Name System)
*   C) HTTP (Hypertext Transfer Protocol)
*   D) DHCP (Dynamic Host Configuration Protocol)

### Question 5 (Learning Objective: NET-LO-2)
While troubleshooting connectivity, a student notices that they can ping a public IP address (such as `1.1.1.1`), but when they enter `google.com` in their web browser, the page fails to load. Which of the following configurations is most likely broken or misconfigured on the workstation?
*   A) The local Subnet Mask.
*   B) The local MAC address routing table.
*   C) The local DNS Server setting.
*   D) The Default Gateway IP address.

### Question 6 (Learning Objective: NET-LO-2)
An operator wants to see all active TCP and UDP connections on a Windows Server, along with the process identifier (PID) responsible for hosting each port connection. Which command-line prompt achieves this?
*   A) `ipconfig /all`
*   B) `netstat -ano`
*   C) `route print`
*   D) `nslookup -type=any`

### Question 7 (Learning Objective: VIR-LO-1)
Before conducting a hazardous system update or testing a suspected malware sample, what is the best security practice for virtualized host environments?
*   A) Clone the VM, change its MAC address, and export it as an OVA.
*   B) Take a VM Snapshot so that the machine state can be instantly rolled back if a compromise occurs.
*   C) Reinstall the hypervisor to clear any cached data.
*   D) Switch the network interface card settings to Bridged mode.

### Question 8 (Learning Objective: VIR-LO-1)
Which VM network configuration allows a guest VM to access the internet through the host's physical network connection, while preventing any external internet devices from initiating direct inbound connections to the guest VM?
*   A) Bridged Adapter
*   B) Host-Only Adapter
*   C) NAT (Network Address Translation)
*   D) Internal Network

### Question 9 (Learning Objective: DOC-LO-1)
A student wants to copy a repository hosted on GitHub (`https://github.com/example/cyber-labs`) down to their local workstation to start working. What is the correct initial Git command?
*   A) `git init https://github.com/example/cyber-labs`
*   B) `git pull https://github.com/example/cyber-labs`
*   C) `git clone https://github.com/example/cyber-labs`
*   D) `git checkout https://github.com/example/cyber-labs`

### Question 10 (Learning Objective: DOC-LO-1)
In a professional Capture the Flag (CTF) writeup or incident response report, what is the primary purpose of including an "Executive Summary"?
*   A) To display the raw source code and scripts used during the challenge.
*   B) To provide a non-technical overview of the impact, scope, and key recommendations for business leaders.
*   C) To document every single unsuccessful CLI attempt in chronologically detailed logs.
*   D) To list the licensing credentials of the hypervisors used to host the test environment.

---

## Part 2: Written Knowledge Check Answer Key & Explanations

1.  **Correct Answer: A**
    *   *Explanation:* The `grep -m 5` option tells `grep` to stop reading a file after finding 5 matching lines. Option B is incorrect because `head -n 5` only checks the very first 5 lines of the log file for the keyword, which might miss matches later in the document.
2.  **Correct Answer: B**
    *   *Explanation:* SetUID (SUID) allows a binary file to be executed with the privileges of the file owner rather than the user executing it. If owned by root, this is a massive privilege escalation risk if the binary is writable or has vulnerabilities.
3.  **Correct Answer: C**
    *   *Explanation:* In PowerShell, `Stop-Process -Id <PID>` is the correct cmdlet to terminate a process by its process ID. `Stop-Service` is for background system services, not direct executables/processes.
4.  **Correct Answer: B**
    *   *Explanation:* Port 53 is reserved for the Domain Name System (DNS), which historically uses UDP for fast, lightweight lookups.
5.  **Correct Answer: C**
    *   *Explanation:* Because the user can reach public IPs (`1.1.1.1`), basic routing (Default Gateway) and local networking (Subnet Mask) are working. The failure of names like `google.com` to resolve indicates a failure to translate domain names to IP addresses, which is the job of the DNS Server.
6.  **Correct Answer: B**
    *   *Explanation:* On Windows, `netstat -ano` displays active TCP/UDP connections, with `-a` showing all sockets, `-n` forcing numeric display of addresses and ports, and `-o` displaying the owning Process ID (PID).
7.  **Correct Answer: B**
    *   *Explanation:* Snapshots store the exact register, RAM, and disk state of a virtual machine, allowing immediate, non-destructive rollbacks to a clean baseline.
8.  **Correct Answer: C**
    *   *Explanation:* NAT acts as an outbound-only gateway, translating guest traffic behind the host's IP. Bridged (Option A) exposes the guest directly to the host's physical network, allowing inbound connections. Host-Only (Option B) prevents internet access entirely.
9.  **Correct Answer: C**
    *   *Explanation:* `git clone` copies an existing remote repository onto a local directory. `git init` is used only to create a brand-new local repository.
10. **Correct Answer: B**
    *   *Explanation:* Executive Summaries translate technical complexities into business risk and remediation priorities, allowing non-technical stakeholders (directors, clients, managers) to understand the security posture.

---

## Part 3: Practical Hands-on Challenge (The Validation Auditing Script)

To automate grading and teach students script validation, instructors can copy and run these validation commands on student VMs to instantly assess if they completed the Module 1 Unit 7 lab successfully.

### 1. Linux Validation Script (`validate_linux.sh`)
Instructors can save this script as `validate_linux.sh` on the student Linux VM and run it with root privileges (`sudo bash validate_linux.sh`) to print a report card.

```bash
#!/bin/bash
echo "=== SudoCorp Linux Audit Validation ==="
score=0
total=3

# Check 1: User rogue_tester deletion
if ! grep -q "rogue_tester" /etc/passwd; then
    echo "[PASS] rogue_tester account removed successfully."
    score=$((score + 1))
else
    echo "[FAIL] rogue_tester account still exists in /etc/passwd."
fi

# Check 2: Telnet (inetd) disabled
telnet_status=$(systemctl is-active inetd 2>/dev/null)
if [ "$telnet_status" != "active" ]; then
    echo "[PASS] Telnet daemon (inetd) stopped and disabled."
    score=$((score + 1))
else
    echo "[FAIL] Telnet daemon (inetd) is still active!"
fi

# Check 3: company_secrets.txt permissions
if [ -f /home/admin_user/confidential_backups/company_secrets.txt ]; then
    perms=$(stat -c "%a" /home/admin_user/confidential_backups/company_secrets.txt)
    if [ "$perms" -eq 600 ]; then
        echo "[PASS] company_secrets.txt permissions set to 600 (owner only)."
        score=$((score + 1))
    else
        echo "[FAIL] company_secrets.txt permissions are $perms (should be 600)."
    fi
else
    echo "[FAIL] company_secrets.txt file not found in path!"
fi

echo "======================================"
echo "Linux Audit Score: $score / $total"
```

### 2. Windows Validation Script (`validate_windows.ps1`)
Instructors can run this PowerShell script as Administrator on the student Windows VM to verify their hardening actions.

```powershell
Write-Host "=== SudoCorp Windows Audit Validation ===" -ForegroundColor Cyan
$score = 0
$total = 3

# Check 1: backdoor_user deletion
$user_check = Get-LocalUser | Where-Object {$_.Name -eq "backdoor_user"}
if ($null -eq $user_check) {
    Write-Host "[PASS] backdoor_user deleted successfully." -ForegroundColor Green
    $score++
} else {
    Write-Host "[FAIL] backdoor_user still exists on the system." -ForegroundColor Red
}

# Check 2: Print Spooler service disabled
$spooler_check = Get-Service -Name "Spooler"
if ($spooler_check.Status -eq "Stopped" -and $spooler_check.StartType -eq "Disabled") {
    Write-Host "[PASS] Print Spooler service stopped and disabled." -ForegroundColor Green
    $score++
} else {
    Write-Host "[FAIL] Print Spooler service is still running or enabled." -ForegroundColor Red
}

# Check 3: Firewall active on all profiles
$firewall_check = Get-NetFirewallProfile | Where-Object {$_.Enabled -eq $false}
if ($null -eq $firewall_check) {
    Write-Host "[PASS] Windows Defender Firewall enabled on all profiles." -ForegroundColor Green
    $score++
} else {
    Write-Host "[FAIL] Windows Firewall is still disabled on some profiles." -ForegroundColor Red
}

Write-Host "======================================" -ForegroundColor Cyan
Write-Host "Windows Audit Score: $score / $total" -ForegroundColor Cyan
```
