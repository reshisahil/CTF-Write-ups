# Boot2Root Labs — Learning & Write-ups

A hands-on cybersecurity learning repository documenting my journey into **Boot2Root challenges, network enumeration, Linux privilege escalation, and penetration testing fundamentals**.

I'm building practical skills through intentionally vulnerable machines, documenting my methodology, commands, observations, mistakes, and lessons learned along the way.

> **Learning approach:** Understand the methodology, investigate the evidence, and learn why a technique works—not just how to execute a command.

## Objectives

- Learn network discovery and target identification.
- Understand TCP port scanning and service enumeration.
- Investigate exposed services and common security misconfigurations.
- Practise initial access and Linux privilege escalation.
- Develop a structured penetration-testing workflow.
- Maintain clear, reproducible notes for future reference.

## My Boot2Root Methodology

### 1. Target Setup and Network Configuration

For local Boot2Root challenges, the vulnerable machine is supplied as a VM image, such as an OVA file.

- Import the target into VirtualBox.
- Configure the attacker and target machines on the same isolated lab network.
- Start the machines and verify their network interfaces.
- Identify the subnet assigned to the attacker machine.

Check network interfaces and routes:

```bash
ip -br addr
ip route
```

### 2. Host Discovery

When the target IP is unknown, discover active hosts on the confirmed lab subnet.

```bash
sudo nmap -sn <LAB_SUBNET>
```

Example:

```bash
sudo nmap -sn 192.168.56.0/24
```

**Important:** Replace the example subnet with the actual lab subnet. Identify the target by correlating scan results with VM network configuration or console information. Do not assume every responding host is a target.

### 3. Port Scanning

Once the target IP is confirmed, scan its TCP ports.

```bash
sudo nmap -Pn -p- -T3 <TARGET_IP>
```

- `-Pn`: Skip host discovery and proceed as though the host is online.
- `-p-`: Scan all TCP ports.
- `-T3`: Use Nmap's normal timing template.

If a scan reports filtered ports or no open ports, verify the target IP, network configuration, target state, and scan scope before drawing conclusions.

### 4. Service Enumeration

Investigate discovered ports to identify services and versions.

```bash
sudo nmap -Pn -sC -sV -p <OPEN_PORTS> <TARGET_IP>
```

- `-sC`: Run Nmap's default scripts.
- `-sV`: Attempt service-version detection.
- `-p`: Specify the discovered ports.

The output guides the next stage of investigation.

### 5. Initial Access

Investigate each exposed service based on the evidence collected.

Examples include:

- HTTP/HTTPS: page source, application behavior, directories, and exposed files.
- SSH: authentication configuration and available credentials.
- FTP: anonymous access and exposed files.
- Telnet: login behavior and insecure configurations.

The goal is to identify a valid, lab-authorized path to initial access—not to assume every exposed service is vulnerable.

### 6. Privilege Verification and Escalation

After obtaining a shell, determine the current user's privileges.

```bash
whoami
id
pwd
```

If the account is not privileged, investigate the system for legitimate privilege-escalation opportunities within the lab.

### 7. Flag Retrieval and Documentation

Once the required access is obtained, locate and read the designated flag.

Document the complete path from discovery to access, including the evidence that justified each decision.

---

## Completed Labs

### 01 — Hack The Box: Meow

**Platform:** Hack The Box — Starting Point  
**Category:** Telnet / Linux fundamentals  
**Difficulty:** Very Easy

#### Objective

Obtain access to the target and retrieve the flag stored in the root user's home directory.

#### Reconnaissance

An Nmap scan identified Telnet on TCP port 23.

```text
PORT   STATE SERVICE VERSION
23/tcp open  telnet  Linux telnetd
```

#### Enumeration

Connected to the exposed Telnet service:

```bash
telnet <TARGET_IP> 23
```

The service displayed a `Meow login:` prompt, identifying the available remote-login interface.

#### Initial Access

Testing the `root` username revealed an insecure authentication configuration: the service accepted the root login without requesting a password.

This provided privileged access without requiring a separate exploitation or privilege-escalation step.

#### Flag Retrieval

After login, inspected the current directory and read the designated flag file.

```bash
whoami
ls
cat flag.txt
```

The `whoami` command confirmed the current account. The `cat` command displayed the file's contents.

**Result:** Successfully obtained root access and retrieved the flag.

#### Key Lessons

- Enumerate exposed services before attempting exploitation.
- Telnet is an unencrypted remote-login protocol.
- Misconfigured authentication can expose privileged accounts.
- Root access and initial access are not always separate stages.
- Use `whoami` and `id` to verify the privileges of an obtained shell.
- A simple, evidence-driven investigation can be more effective than immediately attempting complex exploits.

---

## Lessons from My First Boot2Root Competition

My first Boot2Root competition highlighted an important difference between guided CTF challenges and standalone vulnerable machines.

In a guided challenge, the target IP or files may be supplied directly. In a standalone Boot2Root challenge, I may need to identify the target IP, verify the network configuration, enumerate exposed services, and determine the attack path independently.

The main lesson was to **verify the target and network before troubleshooting the scan results**.

When no ports appear open, possible causes include an incorrect target IP, a network mismatch, a stopped service, or filtering. The correct response is to verify the evidence rather than repeatedly running the same scan.

---

## Future Learning Roadmap

- [ ] Practise host discovery on local vulnerable VMs.
- [ ] Improve Nmap and service-enumeration skills.
- [ ] Complete more HTB Starting Point machines.
- [ ] Practise beginner-friendly VulnHub Boot2Root machines.
- [ ] Study Linux privilege escalation.
- [ ] Document each lab with clear findings and remediation notes.

## Disclaimer

All testing documented in this repository is intended for authorized cybersecurity labs, intentionally vulnerable machines, and environments where testing permission has been granted.

**This repository is a learning journal.** The objective is to develop sound methodology, technical understanding, and responsible security practices.
