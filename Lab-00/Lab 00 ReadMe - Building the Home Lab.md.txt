#### Lab 00 - Building the Home Lab & Portfolio Infrastructure - Read Me

> **Role:** Independent IT Professional
**Difficulty:** ⭐☆☆☆☆ (long, not hard)
**Time to Complete:** 5–7 hours (recommended: split across 2 sessions)
> 

---

## TL;DR

> Before solving any IT problems, I designed and built the entire
infrastructure from scratch — a virtualized network with five machines
running on VirtualBox, a functioning osTicket help desk system deployed
on a LAMP stack, and a documentation pipeline across GitHub and Hashnode.
Every lab going forward is logged as a real ticket with SLA tracking,
troubleshooting documentation, and STAR method write-ups.
> 

---

## Documentation

| Document | Description |
| --- | --- |
| 📋 [README.md](https://www.notion.so/README.md) | This file — overview, objectives, skills |
| 📖 [Full Lab](https://www.notion.so/lab-00-full.md) | Complete walkthrough with screenshots and explanations |
| ⚡ [Condensed Lab](https://www.notion.so/lab-00-condensed.md) | Quick reference runbook — steps only |
| 🌐 [Network Documentation](https://www.notion.so/documentation/network-documentation.md) | IP assignments and network diagram |

## Why This Lab Exists

The most common question I see in IT communities is: **"Where can I
find labs for my portfolio?"**

I couldn't find what I was looking for — labs that simulate real-world
incidents, document work through a ticketing system, and produce
portfolio-ready output. So I built my own environment to make that
possible.

Lab 00 is the foundation. Nothing else works without this.

---

## What Was Built

```
YOUR ALIENWARE 16 AURORA (Host)
│
├── VirtualBox 7.x (Hypervisor)
│   ├── NAT Network: "LabNAT" (10.0.2.0/24 — internet access)
│   ├── Host-Only Network: "LabLAN" (192.168.56.0/24 — internal)
│   │
│   ├── [VM] osTicket-Server (Ubuntu Server 22.04)
│   │     └── Apache + MySQL + PHP + osTicket
│   │     └── IP: 192.168.56.10
│   │     └── Status: RUNNING
│   │
│   ├── [VM] Win10-PC01 (Shell — empty, configured, not installed)
│   │     └── IP: 192.168.56.100 (future)
│   │
│   ├── [VM] Win11-PC01 (Shell — empty, configured, not installed)
│   │     └── IP: 192.168.56.101 (future)
│   │
│   ├── [VM] Ubuntu-PC01 (Shell — empty, configured, not installed)
│   │     └── IP: 192.168.56.102 (future)
│   │
│   └── [VM] Mint-PC01 (Shell — empty, configured, not installed)
│         └── IP: 192.168.56.103 (future)
│
├── Documentation (your choice of platform)
│   └── STAR method writeups for each lab
│
└── ISOs Folder
    ├── Windows 10 Enterprise Evaluation
    ├── Windows 11 Enterprise Evaluation
    ├── Ubuntu Desktop 22.04.x LTS
    ├── Linux Mint 21.x
    └── Ubuntu Server 22.04.x LTS
```

## **Objectives**

- [x] Install and configure **VirtualBox 7.x** with Extension Pack
- [x] Design and implement **dual-network architecture** (NAT + Host-Only)
- [x] Create **5 virtual machines** (1 server + 4 client shells)
- [x] Deploy **Ubuntu Server 22.04** with static IP configuration
- [x] Install and configure a full **LAMP stack** (Linux, Apache, MySQL, PHP)
- [x] Deploy and customize **osTicket** help desk ticketing system
- [x] Configure **SLA tiers, departments, help topics, and support teams**
- [x] Download and organize **5 operating system ISOs**
- [x] Create **VM snapshot** for clean-state recovery
- [x] Document **network architecture** and **credential management**
- [x] Establish a **documentation method** using the STAR framework

---

## **Environment Specs**

| **Component** | **Details** |
| --- | --- |
| **Host Machine** | Alienware 16 Aurora · 32GB RAM · 1TB Storage |
| **Hypervisor** | Oracle VirtualBox 7.x with Extension Pack |
| **Lab Network** | 192.168.56.0/24 (Host-Only) |
| **Internet Access** | 10.0.2.0/24 (NAT per VM) |
| **Server** | Ubuntu Server 22.04 · osTicket · LAMP Stack |
| **osTicket URL** | [**http://192.168.56.10/osticket/scp/**](http://192.168.56.10/osticket/scp/) |

---

## **Network Architecture**

### **IP Address Assignments**

| **Hostname** | **Role** | **IP Address** | **OS** | **Status** |
| --- | --- | --- | --- | --- |
| Host | Physical Machine | 192.168.56.1 | Windows | ✅ Active |
| osTicket-Server | Help Desk Server | 192.168.56.10 | Ubuntu Server 22.04 | ✅ Active |
| Win10-PC01 | Client Workstation | 192.168.56.100 | Windows 10 Enterprise | ⬜ Shell |
| Win11-PC01 | Client Workstation | 192.168.56.101 | Windows 11 Enterprise | ⬜ Shell |
| Ubuntu-PC01 | Client Workstation | 192.168.56.102 | Ubuntu Desktop 22.04 | ⬜ Shell |
| Mint-PC01 | Client Workstation | 192.168.56.103 | Linux Mint 21 | ⬜ Shell |

### **Network Diagram**

```
text
               ┌──────────────┐
               │   INTERNET   │
               └──────┬───────┘
                      │
          ┌───────────┴───────────┐
          │   NAT (10.0.2.0/24)   │   ← Each VM gets its own NAT
          │   Gateway: 10.0.2.2   │     for internet access
          └───────────┬───────────┘
                      │
    ┌─────┬─────┬─────┼─────┬─────┐
    │     │     │     │     │     │
  ┌─┴─┐┌─┴─┐┌─┴─┐┌──┴─┐┌─┴──┐┌─┴──┐
  │SVR ││W10 ││W11 ││UBU ││MINT││HOST│
  │ .10││.100││.101││.102││.103││ .1 │
  └─┬──┘└─┬──┘└─┬──┘└─┬──┘└─┬──┘└─┬──┘
    │     │     │     │     │     │
  ┌─┴─────┴─────┴─────┴─────┴─────┴──┐
  │   Host-Only (192.168.56.0/24)     │  ← All VMs + Host
  │   "Office LAN" simulation         │    communicate here
  └────────────────────────────────────┘
```

---

## **Virtual Machines**

### **osTicket-Server (Running)**

| **Setting** | **Value** |
| --- | --- |
| OS | Ubuntu Server 22.04 LTS |
| RAM | 2048 MB (2 GB) |
| CPU | 1 |
| Disk | 20 GB (dynamic) |
| Adapter 1 | NAT (internet) |
| Adapter 2 | Host-Only (192.168.56.10 static) |
| Services | Apache, MySQL, PHP, osTicket |
| Snapshot | "Clean-osTicket-Install" saved |

### **Win10-PC01 (Shell)**

| **Setting** | **Value** |
| --- | --- |
| OS | Windows 10 Enterprise (64-bit) |
| RAM | 4096 MB (4 GB) |
| CPU | 2 |
| Disk | 50 GB (dynamic) |
| Adapter 1 | NAT |
| Adapter 2 | Host-Only |
| Status | Configured, OS not installed (Lab 02) |

### **Win11-PC01 (Shell)**

| **Setting** | **Value** |
| --- | --- |
| OS | Windows 11 Enterprise (64-bit) |
| RAM | 4096 MB (4 GB) |
| CPU | 2 |
| Disk | 64 GB (dynamic) |
| Adapter 1 | NAT |
| Adapter 2 | Host-Only |
| EFI | ✅ Enabled |
| TPM | ✅ 2.0 |
| Status | Configured, OS not installed (Lab 02) |

### **Ubuntu-PC01 (Shell)**

| **Setting** | **Value** |
| --- | --- |
| OS | Ubuntu Desktop 22.04 (64-bit) |
| RAM | 4096 MB (4 GB) |
| CPU | 2 |
| Disk | 25 GB (dynamic) |
| Adapter 1 | NAT |
| Adapter 2 | Host-Only |
| Status | Configured, OS not installed (Lab 02) |

### **Mint-PC01 (Shell)**

| **Setting** | **Value** |
| --- | --- |
| OS | Linux Mint 21 (Ubuntu 64-bit) |
| RAM | 2048 MB (2 GB) |
| CPU | 2 |
| Disk | 25 GB (dynamic) |
| Adapter 1 | NAT |
| Adapter 2 | Host-Only |
| Status | Configured, OS not installed (Lab 02) |

---

## **osTicket Configuration**

### **SLA Plans**

| **Name** | **Grace Period** | **Schedule** |
| --- | --- | --- |
| **SEV-A (Critical)** | 1 hour | 24/7 |
| **SEV-B (High)** | 4 hours | 24/5 |
| **SEV-C (Normal)** | 8 hours | Monday–Friday 8am–5pm |
| **SEV-D (Low)** | 24 hours | Monday–Friday 8am–5pm |

### **Departments**

| **Department** | **Type** |
| --- | --- |
| IT Support | Public |
| System Administration | Public |
| Networking | Public |

### **Help Topics**

| **Help Topic** | **Department** | **SLA** |
| --- | --- | --- |
| Password Reset | IT Support | SEV-D |
| Hardware Issue | IT Support | SEV-C |
| Software Issue | IT Support | SEV-C |
| Network Connectivity | Networking | SEV-B |
| Access / Permissions | IT Support | SEV-C |
| Workstation Not Booting | IT Support | SEV-B |
| Malware / Security Incident | System Administration | SEV-A |
| New Employee Setup | IT Support | SEV-C |
| Printer Issue | IT Support | SEV-D |
| General Inquiry | IT Support | SEV-D |

### **Teams**

| **Team** | **Purpose** |
| --- | --- |
| Tier I Support | First-line response and triage |
| Tier II Support | Escalation and advanced troubleshooting |

---

## **What I Learned**

Building this lab isn't complicated, but it is labor intensive. The

VirtualBox setup and VM shells took about an hour. The Ubuntu Server,

LAMP stack, and osTicket configuration took the rest — easily 4-5 hours.

**Key takeaways:**

- **YAML is unforgiving.** The Netplan configuration for static IP
    
    assignment requires exact spacing — one wrong indent and the entire
    
    network config fails. This taught me to respect configuration file
    
    syntax and always test after applying changes.
    
- **Snapshots save hours.** Taking a clean snapshot after configuring
    
    osTicket means I can break things in future labs and roll back in
    
    seconds instead of rebuilding from scratch.
    
- **Documentation is the real skill.** Setting up VirtualBox is
    
    straightforward. Writing about it clearly enough that someone else
    
    could follow? That's the hard part — and the part employers actually
    
    care about.
    
- **The ticketing system changes everything.** Having osTicket forces
    
    me to document every lab like a real technician — opening tickets,
    
    writing resolution notes, tracking SLAs. This habit is more valuable
    
    than any single technical skill.
    

---

## **Skills Demonstrated**

| Skill | What I Did |
| --- | --- |
| **System Configuration** | Configured VirtualBox preferences, VM hardware specs, EFI/TPM settings |
| **Local Area Networks** | Designed and implemented virtual network with NAT + Host-Only adapters, assigned static IPs via Netplan |
| **Data Storage Technologies** | Created dynamically allocated virtual hard disks, planned storage allocation across 5 VMs |
| **Command-Line Interface** | Configured Ubuntu Server entirely via CLI — installed LAMP stack, edited YAML configs, managed services with systemctl |
| **Information Systems Security** | Secured MySQL installation, set Apache file permissions, established credential management practices |
| **System Support** | Built Linux server from scratch, installed and configured web application (osTicket) on LAMP stack |
| **Documentation** | Created network diagrams, IP tables, credential reference sheets, established STAR method as standard lab documentation framework |

## **Job Role Applicability**

### **🟢 Help Desk Tier 1**

Understanding how a ticketing system is structured — SLAs, departments,

help topics, escalation tiers — gives you context for how your tickets

are prioritized and routed. Most Tier 1 techs use ticketing systems

daily but never see how they're configured. You now understand both sides.

### **🔵 IT Support Specialist**

Building a virtual lab environment demonstrates that you can set up and

manage infrastructure independently. Deploying a LAMP stack, configuring

static IPs, and managing services via CLI are daily tasks for IT support

roles beyond basic help desk.

### **🟡 Desktop Support Technician**

Managing multiple operating systems (Windows 10, Windows 11, Ubuntu,

Linux Mint) across a network is core desktop support work. Understanding

VirtualBox networking modes prepares you for working with any

virtualization platform in production.

### **🟠 System Support Specialist**

Deploying a web application on a Linux server, configuring Apache,

securing MySQL, managing firewall rules, and planning network

architecture are system administration fundamentals. This lab

demonstrates you can build infrastructure, not just use it.

---

## **Tools & Technologies Used**

| **Tool** | **Purpose** |
| --- | --- |
| **Oracle VirtualBox 7.x** | Type 2 hypervisor for VM management |
| **VirtualBox Extension Pack** | USB 2.0/3.0, disk encryption, PXE boot support |
| **Ubuntu Server 22.04 LTS** | Server OS for hosting osTicket |
| **Apache 2** | Web server |
| **MySQL** | Database server for osTicket |
| **PHP 8.1** | Server-side scripting for osTicket |
| **osTicket** | Open-source help desk ticketing system |
| **Netplan** | Ubuntu network configuration (YAML-based) |

---

## **File Structure**

```
text
Lab-00/
├── README.md                          
├── screenshots/
│   ├── virtualbox-manager.png
│   ├── extension-pack-installed.png
│   ├── host-only-network-config.png
│   ├── dhcp-server-settings.png
│   ├── ipconfig-host-only.png
│   ├── netplan-config.png
│   ├── static-ip-configured.png
│   ├── ping-host-to-server.png
│   ├── apache-default-page.png
│   ├── osticket-install-success.png
│   ├── osticket-staff-panel.png
│   ├── osticket-help-topics.png
│   ├── osticket-sla-plans.png
│   ├── vm-snapshot-created.png
│   ├── all-vms-listed.png
│   └── isos-folder.png
└── documentation/
    └── network-documentation.md
```

---

## **What You'd Tell an Employer**

Before starting any labs, I designed and built the entire 
 infrastructure from scratch — a virtualized network with five 
machines and a help desk ticketing system running on a LAMP 
stack. Every lab I complete is logged as a real ticket with 
SLA tracking, troubleshooting documentation, and measurable 
outcomes."

---

## **What's Next**

Lab 00 is the foundation. The environment is built, the ticketing

system is configured, and the documentation pipeline is live.

In **Lab 01**, I step into the role of a technician at NovaBridge

Technologies, a managed service provider. The team needs bootable

USB toolkits for new client onboarding — and when one of them

won't boot at a client site, I diagnose why.

➡️ [**Lab 01: Creating Bootable USB Media**](https://arena.ai/Lab-01/)