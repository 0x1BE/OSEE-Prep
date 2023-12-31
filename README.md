<p align="center" dir="auto">
  <a target="_blank" rel="noopener noreferrer" href="https://www.offsec.com/wp-content/themes/OffSecChildTheme/assets/course-icons/optimized/EXP-401_Fill.svg"><img width="300" height="300" src="https://www.offsec.com/wp-content/themes/OffSecChildTheme/assets/course-icons/optimized/EXP-401_Fill.svg" style="max-width: 100%;"></a>
</p>

# EXP-401: Advanced Windows Exploitation - OSEE Certification

This repository is dedicated to my self-study journey towards the Offensive Security Exploit Developer (OSEE) certification. I am planning to attend the course in 2025 or 2026, and this is part of my preparation. I believe in the power of open learning and therefore, I am sharing the materials that I am using for my studies.

# OSEE 401 Exam Preparation Guide

This repository serves as a structured guide for preparing for the Offensive Security Exploitation Expert (OSEE) 401 exam. It is meticulously crafted based on the [EXP401 Syllabus](https://www.offsec.com/awe/EXP401_syllabus.pdf) and focuses on the major topics essential for mastering advanced Windows exploitation techniques.

## Introduction

The OSEE certification is recognized in the cybersecurity industry for its rigor and emphasis on practical, hands-on skills. This guide aligns with the official syllabus and is designed to provide learners with detailed resources, clear explanations, and practical exercises for each major module.

## Prerequisites

- Solid understanding of Windows operating systems at both the administrative and kernel level. Familiarity with Windows internals, system architecture, and subsystems.
- Advanced programming skills in languages such as C, Python, and Assembly, especially as they relate to system-level programming and exploit development in Windows environments.
- Substantial experience in penetration testing and security research, particularly in identifying and exploiting Windows-based vulnerabilities.
- Proficiency with a wide range of security tools specific to Windows, including debuggers (such as WinDbg), disassemblers/decompilers (like IDA Pro, Ghidra), and virtualization software (VMware, Hyper-V).
- Strong background in reverse engineering Windows applications and binaries, with the ability to analyze and understand complex code structures.
- Prior experience in developing and exploiting advanced vulnerabilities such as buffer overflows, heap overflows, use-after-free vulnerabilities, and other complex Vulns. in Windows environments.

## Key Vulnerabilities Covered

### VMware Workstation Guest-To-Host Escape
- **CVE-2017-4901**: Bug in Drag and Drop RPCI

### Microsoft Edge Type Confusion
- **CVE-2019-0567**: Type confusion vulnerability in Microsoft Edge


## Table of Contents

- [2 Custom Shellcode Creation](#2-custom-shellcode-creation)
- [3 VMware Workstation Guest-To-Host Escape](#3-vmware-workstation-guest-to-host-escape)
- [4 Microsoft Edge Type Confusion](#4-microsoft-edge-type-confusion)
- [Future Modules](#future-modules)

(Note: Content for each section, along with additional sections, will be updated regularly.)

### Note on Content
This guide intentionally focuses on the main topics from the syllabus. Some specific topics have been omitted to ensure the guide remains concise and directed towards the primary learning objectives. For comprehensive coverage, learners are encouraged to refer to the official syllabus alongside this guide.

### Stay Connected
Follow my journey and share your experiences on Twitter: [0x1BE](https://twitter.com/0x1BE).

### Future Modules
More modules and sections will be added to this guide as I continue through the course. This includes an in-depth exploration of advanced topics, each accompanied by practical examples and resources for thorough study.


## Disclaimer

This repository is intended solely for educational purposes in preparation for the OSEE 401 exam. All materials and exercises are structured to align with the [EXP401 Syllabus](https://www.offsec.com/awe/EXP401_syllabus.pdf). This guide is not affiliated with or endorsed by Offensive Security.

---

Let's embark on this challenging yet rewarding journey together. Happy hacking!


## Table of Contents

- [2 Custom Shellcode Creation](#2-custom-shellcode-creation)
- [3 VMware Workstation Guest-To-Host Escape](#3-vmware-workstation-guest-to-host-escape)
- [4 Microsoft Edge Type Confusion](#4-microsoft-edge-type-confusion)
- [5 Driver Callback Overwrite](#5-driver-callback-overwrite)
- [6 Unsanitized User-mode Callback](#6-unsanitized-user-mode-callback)


### [2 Custom Shellcode Creation](#2-custom-shellcode-creation)
Custom shellcode creation is a critical skill for exploit developers. This module covers various aspects of shellcode development, including understanding 64-bit architectures and the intricacies of Win32 APIs.

#### 2.1 64-bit Architecture
The shift to 64-bit architecture brings several changes in how systems handle memory and execute code. This section delves into these changes and their impact on exploit development.
- **2.1.1 64-bit Memory Enhancements**
  - Description: An exploration of the enhancements in memory management in 64-bit systems and their implications on security.
  - Resources: [64-bit Memory Management](https://placeholder-link.com)
- **2.1.2 Calling Conventions**
  - Description: Understanding the calling conventions in 64-bit systems and how they differ from 32-bit systems.
  - Resources: [64-bit Calling Conventions](https://placeholder-link.com)
- **2.1.3 Win32 APIs**
  - Description: Leveraging Win32 APIs for exploitation in a 64-bit environment.
  - Resources: [Win32 APIs in 64-bit Exploitation](https://placeholder-link.com)

#### 2.2 Writing Exploit Code
A deep dive into the best practices and methodologies for writing effective and reliable exploit code.
- **2.2.1 Position-Independent-Code**
  - Description: Strategies for writing position-independent code, a crucial aspect for successful exploitation.
  - Resources: [Position-Independent Code Techniques](https://placeholder-link.com)
- **2.2.2 Visual Studio**
  - Description: Utilizing Visual Studio for developing and debugging exploit code.
  - Resources: [Exploit Development with Visual Studio](https://placeholder-link.com)

#### 2.3 Shellcode Framework Creation
- Description: Techniques for building a versatile and effective shellcode framework.
- Resources: [Building Shellcode Frameworks](https://placeholder-link.com)

#### 2.4 Reverse Shell
- Description: Crafting reverse shellcode for establishing remote connections post-exploitation.
- Resources: [Reverse Shellcode Development](https://placeholder-link.com)

### [3 VMware Workstation Guest-To-Host Escape](#3-vmware-workstation-guest-to-host-escape)
This module covers the techniques and vulnerabilities associated with escaping from a VMware Workstation guest environment to the host, a critical aspect of virtual machine security.

#### 3.1 Vulnerability Classes
- Description: An overview of different classes of vulnerabilities commonly found in virtualized environments like VMware.
- Resources: [VMware Vulnerability Classes](https://placeholder-link.com)

#### 3.2 Data Execution Prevention (DEP)
- **3.2.1 DEP Theory**
  - Description: Understanding the role and mechanism of Data Execution Prevention in Windows security.
  - Resources: [Data Execution Prevention Explained](https://placeholder-link.com)
- **3.2.2 Ret2Lib Attacks and Their Evolution**
  - Description: The evolution and mechanics of Return-to-Library attacks in the context of modern security defenses.
  - Resources: [Ret2Lib Attack Techniques](https://placeholder-link.com)
- **3.2.3 Return Oriented Programming**
  - Description: Advanced exploitation techniques using Return Oriented Programming to bypass security mechanisms.
  - Resources: [ROP Techniques](https://placeholder-link.com)

#### 3.3 Address Space Layout Randomization
- Description: Techniques for bypassing ASLR, a common memory protection mechanism.
- Resources: [Bypassing ASLR](https://placeholder-link.com)

#### 3.4 VMware Workstation Internals
- Description: Deep dive into VMware Workstation's internal mechanisms.
- Resources: [Exploring VMware Internals](https://vmware.com/internals), [VMware Architecture Course](https://pluralsight.com/vmware-internals)

#### 3.5 UaF Case Study: VMware Workstation Drag & Drop Vulnerability
- Description: Case study of a use-after-free vulnerability in VMware.
- Resources: [UaF Vulnerability Analysis](https://example.com/uaf-vmware), [Exploiting VMware Drag & Drop](https://youtube.com/vmware-dragdrop-vuln)

#### 3.6 The Windows Heap Memory Manager
- Description: Understanding the intricacies of Windows heap memory management.
- Resources: [Heap Memory Management in Windows](https://docs.microsoft.com/windows-heap-management), [Windows Heap Exploitation Techniques](https://example.com/windows-heap-exploits)

#### 3.7 Low Fragmentation Heap
- Description: Delving into the Low Fragmentation Heap mechanism in Windows.
- Resources: [Understanding LFH](https://example.com/low-fragmentation-heap), [Exploiting LFH Vulnerabilities](https://youtube.com/lfh-exploitation)

#### 3.8 UaF Case Study
- Description: Detailed case study on exploiting use-after-free vulnerabilities.
- Resources: [UaF Exploitation Guide](https://example.com/uaf-case-study), [Use-After-Free Exploits in Practice](https://youtube.com/uaf-exploits)

#### 3.9 UaF Case Study: Reallocation Control
- Description: Techniques for controlling memory reallocation in UaF vulnerabilities.
- Resources: [Memory Reallocation in UaF](https://example.com/uaf-reallocation), [Reallocation Control Techniques](https://youtube.com/uaf-memory-control)

#### 3.10 UaF Case Study: Fake Virtual Table
- Description: Strategies for crafting and exploiting fake virtual tables in UaF scenarios.
- Resources: [Fake Virtual Table Exploitation](https://example.com/fake-vtable), [Creating Fake Virtual Tables for UaF](https://youtube.com/fake-vtable-uaf)

#### 3.11 UaF Case Study: ROP Storage
- Description: Using Return-Oriented Programming in the context of UaF vulnerabilities.
- Resources: [ROP in UaF Exploits](https://example.com/uaf-rop-storage), [ROP Techniques for UaF](https://youtube.com/uaf-rop)

#### 3.12 UaF Case Study: Bypassing ASLR
- Description: Techniques to bypass Address Space Layout Randomization in UaF exploits.
- Resources: [Bypassing ASLR in UaF](https://example.com/bypass-aslr-uaf), [ASLR Bypass Techniques](https://youtube.com/aslr-bypass-uaf)

#### 3.13 UaF Case Study: Stack Pivoting
- Description: Utilizing stack pivoting techniques in UaF exploitation.
- Resources: [Stack Pivoting in Exploitation](https://example.com/stack-pivoting), [UaF and Stack Pivoting](https://youtube.com/stack-pivoting-uaf)

#### 3.14 UaF Case Study: Defeating DEP
- Description: Strategies to defeat Data Execution Prevention in UaF scenarios.
- Resources: [Defeating DEP in UaF](https://example.com/defeat-dep-uaf), [DEP Bypass Techniques](https://youtube.com/dep-bypass-uaf)

#### 3.15 Restoring the Execution Flow
- Description: Techniques for restoring execution flow after exploitation.
- Resources: [Execution Flow Restoration](https://example.com/restoring-execution-flow), [Post-Exploitation Flow Techniques](https://youtube.com/execution-flow-restoration)

#### 3.16 Executing Shellcode
- Description: Strategies and methods for executing shellcode post-exploitation.
- Resources: [Executing Shellcode](https://example.com/executing-shellcode), [Shellcode Execution Techniques](https://youtube.com/shellcode-execution)

#### 3.17 Windows Defender Exploit Guard
- Description: Understanding and bypassing Windows Defender Exploit Guard.
- Resources: [Exploit Guard Analysis](https://example.com/windows-defender-exploit-guard), [Bypassing Windows Defender Exploit Guard](https://youtube.com/exploit-guard-bypass)

#### 3.18 Testing the WDEG Protections
- Description: Methods for testing the effectiveness of Windows Defender Exploit Guard.
- Resources: [Testing WDEG](https://example.com/testing-wdeg), [Penetration Testing WDEG](https://youtube.com/testing-wdeg)

#### 3.19 ROP Mitigations
- Description: Techniques for mitigating Return-Oriented Programming attacks.
- Resources: [ROP Mitigation Strategies](https://example.com/rop-mitigations), [Mitigating ROP Attacks](https://youtube.com/rop-mitigation)


### [4 Microsoft Edge Type Confusion](#4-microsoft-edge-type-confusion)
This module focuses on exploring and exploiting type confusion vulnerabilities specifically in the Microsoft Edge browser, emphasizing the internal mechanisms of Edge, advanced exploitation techniques, and practical case studies.

#### 4.1 Edge Internals
- Description: An in-depth look at the architecture and internal components of the Microsoft Edge browser.
- Resources: [Inside Microsoft Edge](https://placeholder-link.com)

#### 4.2 Type Confusion Case Study
- Description: Analyzing real-world type confusion vulnerabilities in Edge and understanding their exploitation.
- Resources: [Edge Type Confusion Exploits](https://placeholder-link.com)

#### 4.3 Exploiting Type Confusion
- Description: Techniques and strategies for exploiting type confusion vulnerabilities in web browsers.
- Resources: [Exploiting Type Confusion](https://placeholder-link.com)

#### 4.4 Going for RIP
- Description: Methods to control the instruction pointer (RIP) in exploitation scenarios, a crucial step in gaining execution control.
- Resources: [Controlling the RIP in Exploits](https://placeholder-link.com)

#### 4.5 CFG Bypass
- Description: Strategies for bypassing Control Flow Guard (CFG) in Windows, a security feature to prevent memory corruption vulnerabilities.
- Resources: [Bypassing CFG](https://placeholder-link.com)

#### 4.6 Data Only Attack
- Description: Techniques for executing data-only attacks, where the attacker manipulates the data without changing the code.
- Resources: [Data Only Attacks in Depth](https://placeholder-link.com)

#### 4.7 Arbitrary Code Guard (ACG)
- Description: Understanding and bypassing Arbitrary Code Guard, a security feature in modern Windows environments.
- Resources: [ACG Exploitation Techniques](https://placeholder-link.com)

#### 4.8 Advanced Out-of-Context Calls
- Description: Techniques for making out-of-context function calls in exploitation scenarios.
- Resources: [Advanced Out-of-Context Call Techniques](https://placeholder-link.com)

#### 4.9 Remote Procedure Calls
- Description: Exploiting vulnerabilities in remote procedure call mechanisms.
- Resources: [Remote Procedure Call Exploits](https://placeholder-link.com)

#### 4.10 Browser Sandbox
- Description: Techniques to escape browser sandboxes, with a focus on Microsoft Edge.
- Resources: [Escaping Browser Sandboxes](https://placeholder-link.com)

### Future Modules
More modules and sections will be added to this guide as I continue through the course. This includes detailed exploration of topics such as driver callback overwrite, unsanitized user-mode callbacks, and more, each accompanied by practical examples and resources for in-depth study.


