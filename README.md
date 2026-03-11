<p align="center">
  <img width="200" height="200" src="https://www.offsec.com/wp-content/themes/OffSecChildTheme/assets/course-icons/optimized/EXP-401_Fill.svg">
</p>

<h1 align="center">OSEE / EXP-401: Advanced Windows Exploitation</h1>
<h3 align="center">Self-Study Preparation Guide</h3>

<p align="center">
  <img src="https://img.shields.io/badge/OffSec-EXP--401-red?style=flat-square">
  <img src="https://img.shields.io/badge/Level-Expert-black?style=flat-square">
  <img src="https://img.shields.io/badge/Focus-Windows%20Exploitation-blue?style=flat-square">
  <img src="https://img.shields.io/badge/Resources-Free%20%26%20Public-green?style=flat-square">
</p>

<br>

> This is an independent, community-built prep guide for the OSEE (EXP-401) certification. Not affiliated with or endorsed by Offensive Security. Every resource linked here is free and publicly available. 
<br>

---

## Table of Contents

- [Official References](#-official-references)
- [Module 1 - Prerequisites, Tools and Environment](#module-1---prerequisites-tools-and-environment)
- [Module 2 - Custom Shellcode Creation](#module-2---custom-shellcode-creation)
- [Module 3 - VMware Guest-to-Host Escape](#module-3---vmware-workstation-guest-to-host-escape)
- [Module 4 - Microsoft Edge Type Confusion](#module-4---microsoft-edge-type-confusion)
- [Module 5 - Windows Kernel Exploitation](#module-5---windows-kernel-exploitation)
- [Module 6 - Hyper-V Bonus](#module-6---hyper-v-bonus)
- [Module 7 - Exam Prep and Strategy](#module-7---exam-prep-and-strategy)
- [Module 8 - Tools Reference](#module-8---tools-reference)
- [Module 9 - Papers and Conference Talks](#module-9---papers-and-conference-talks)
- [CVE Reference Table](#cve-reference-table)

---

## 📌 Official References

### OffSec Links

| Resource | Link |
|----------|------|
| EXP-401 Course Page | [offsec.com](https://www.offsec.com/courses/exp-401/) |
| OSEE Exam Guide | [help.offsec.com](https://help.offsec.com/hc/en-us/articles/360046458732-EXP-401-Advanced-Windows-Exploitation-OSEE-Exam-Guide) |
| EXP-401 Syllabus PDF | [appliedtechnologyacademy.com](https://appliedtechnologyacademy.com/wp-content/uploads/2024/06/exp-401-course-outline.pdf) |

### Community Prep Repos

These are the best community resources that already exist. Start here before anything else.

- [PwnAwan/EXP-401-OSEE](https://github.com/PwnAwan/EXP-401-OSEE) - curated resources and PoC exploits
- [gscamelo/OSEE](https://github.com/gscamelo/OSEE) - another solid prep collection
- [yeyintminthuhtut/Awesome-Advanced-Windows-Exploitation-References](https://github.com/yeyintminthuhtut/Awesome-Advanced-Windows-Exploitation-References) - the most comprehensive link dump available
- [FULLSHADE/WindowsExploitationResources](https://github.com/FULLSHADE/WindowsExploitationResources)
- [MustafaNafizDurukan/WindowsKernelExploitationResources](https://github.com/MustafaNafizDurukan/WindowsKernelExploitationResources)
- [FuzzySecurity Tutorials](https://www.fuzzysecurity.com/tutorials.html) - the classic series, still relevant
- [Corelan Exploit Writing Tutorials Parts 1-11](https://www.corelan.be/index.php/articles/) - required reading for user-mode foundations

### Course Reviews Worth Reading

- ["My AWE Experience!!!" by Hemali](https://infosecflash.com/2018/11/04/my-awe-experience/)
- ["AWE Course Review" by Trickster0](https://trickster0.wordpress.com/2018/10/27/awe-course-review-by-offensive-security/)
- ["Advanced Windows Exploitation 2018 Review" by tekman](https://www.oppositionsecurity.com/advanced-windows-exploitation-2018-review/)

---

## Module 1 - Prerequisites, Tools and Environment

Before you write a single line of shellcode, make sure these fundamentals are solid. The course assumes you already know x64 assembly, Windows internals, the PE format, and can navigate a debugger comfortably.

### 1.1 Required Reading

- [Windows Internals Part 1 (Microsoft Press)](https://learn.microsoft.com/en-us/sysinternals/resources/windows-internals) - read this cover to cover
- [Intel x86-64 Software Developer Manual](https://www.intel.com/content/www/us/en/developer/articles/technical/intel-sdm.html)
- [x64 Architecture Overview (Microsoft Docs)](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/x64-architecture)
- [x64 Calling Conventions (Microsoft Docs)](https://learn.microsoft.com/en-us/cpp/build/x64-calling-convention)
- [PE Format Reference (Microsoft Docs)](https://learn.microsoft.com/en-us/windows/win32/debug/pe-format)
- [EPROCESS and Kernel Structure Reference (CodeMachine)](https://www.codemachine.com/article_kernelstruct.html)

### 1.2 Tools You Will Use Every Day

| Tool | What it's for | Link |
|------|--------------|------|
| WinDbg Preview | Primary kernel and user-mode debugger | [Microsoft Store](https://apps.microsoft.com/detail/9pgjgd53tn86) |
| IDA Pro Freeware | Disassembler and decompiler | [hex-rays.com](https://hex-rays.com/ida-free/) |
| Ghidra | Free RE tool from NSA | [ghidra-sre.org](https://ghidra-sre.org/) |
| x64dbg | Open-source user-mode debugger | [x64dbg.com](https://x64dbg.com/) |
| rp++ | ROP gadget finder | [GitHub](https://github.com/0vercl0k/rp) |
| Ropper | ROP chain builder | [GitHub](https://github.com/sashs/Ropper) |
| ROPgadget | Python ROP gadget tool | [GitHub](https://github.com/JonathanSalwan/ROPgadget) |
| mona.py | Exploit dev plugin for Immunity/WinDbg | [GitHub](https://github.com/corelan/mona) |
| Process Hacker | Process and memory inspector | [processhacker.sourceforge.io](https://processhacker.sourceforge.io/) |
| HEVD | Intentionally vulnerable kernel driver | [GitHub](https://github.com/hacksysteam/HackSysExtremeVulnerableDriver) |
| Sickle | Shellcode and opcode generation | [GitHub](https://github.com/wetw0rk/Sickle) |

### 1.3 Setting Up Kernel Debugging

You need two VMs talking to each other over serial or KDNET. One is your debugger, one is your target. Get this working before anything else in Module 5.

- [hasherezade - Part 1: Setting Up the Environment](https://hshrzd.wordpress.com/2017/05/28/starting-with-windows-kernel-exploitation-part-1-setting-up-the-environment/)
- [Setting Up Kernel Mode Debugging over KDNET (Microsoft Docs)](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection)
- [Introduction to Windows Kernel Exploitation - Environment Setup (wetw0rk)](https://wetw0rk.github.io/posts/0x00-introduction-to-windows-kernel-exploitation/)
- [WinDbg Kernel Debugging Cheat Sheet (OSR Online)](https://www.osronline.com/article.cfm%5Eid=576.htm)
- [Remote Kernel Debugging Over TCP/IP (Microsoft Docs)](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/setting-up-kernel-mode-debugging-over-a-network-cable-in-visual-studio)

---

## Module 2 - Custom Shellcode Creation

This module is about writing shellcode that works anywhere, without hardcoded addresses or assumptions about the target environment. You need to understand PIC, PEB walking, and how to resolve Win32 APIs at runtime.

### 2.1 64-bit Architecture

The jump from 32-bit to 64-bit changes a lot: register widths, calling conventions, shadow space, RSP alignment requirements, and how the PEB is accessed.

- [x64 Architecture Overview (Microsoft Docs)](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/x64-architecture)
- [x64 Calling Convention (Microsoft Docs)](https://learn.microsoft.com/en-us/cpp/build/x64-calling-convention)
- [Windows x64 Shellcode Differences (Topher Timzen)](https://www.tophertimzen.com/blog/windowsx64Shellcode/)
- [NASM x64 Assembly Tutorial](https://cs.lmu.edu/~ray/notes/nasmtutorial/)
- [Bridging C++ and x64 Shellcode Development (Red Teaming Dojo)](https://mohamed-fakroud.gitbook.io/red-teamings-dojo/shellcoding/bridging-c++-and-x64-shellcode-development-windows)
- [Corelan ROP and DEP Notes (64-bit context)](https://www.corelan.be/index.php/2011/05/12/hack-notes-rop-retn-rop-retn-and-rop-retn/)

### 2.2 Position-Independent Code and PEB Walking

Every shellcode starts the same way: find `kernel32.dll` without any hardcoded base address. You do this by walking the PEB, parsing the export table, and resolving functions by hash. This is the foundation.

- [x64 Find and Execute WinAPI via PEB (Print3M)](https://print3m.github.io/blog/x64-winapi-shellcoding)
- [Shellcoding a Reverse Shell via PEB from C (0xEct0)](https://0xect0.github.io/2024-07-28-shellcoding-rev-shell-from-c/)
- [PE Parsing Technique for x86 Shellcode (Red Teaming Dojo)](https://mohamed-fakroud.gitbook.io/red-teamings-dojo/shellcoding/leveraging-from-pe-parsing-technique-to-write-x86-shellcode)
- [Windows Shellcode Introduction Part 1 (SecurityCafe, archived)](https://web.archive.org/web/20230331070657/https://securitycafe.ro/2015/10/30/introduction-to-windows-shellcode-development-part1/)
- [ShellcodeStdio - Compiler-Optimized PIC Framework](https://winternl.com/shellcodestdio/)
- [PIC Bindshell with RSP Alignment (mattifestation)](https://github.com/mattifestation/PIC_Bindshell)
- [Shellcode in .NET and PEB Changes (Topher Timzen)](https://www.tophertimzen.com/blog/shellcodeDotNetPEB/)
- [Export Directory Table Reference (Microsoft Docs)](https://learn.microsoft.com/en-us/windows/win32/debug/pe-format#export-directory-table)

### 2.3 Building a Shellcode Framework

Once you can resolve APIs, the next step is packaging everything into a reusable framework: find the base, walk the export table, resolve functions by hash, then run whatever payload you want.

- [Windows Shellcoding Step by Step Part 1 (cocomelonc)](https://cocomelonc.github.io/tutorial/2021/10/27/windows-shellcoding-1.html)
- [Malware Development and Shellcoding Series (0xPat)](https://0xpat.github.io/Malware_development_part_1/)
- [Sickle - Payload Development Framework](https://github.com/wetw0rk/Sickle)
- [OWASP Introduction to Shellcode Development (PDF, archived)](https://web.archive.org/web/20230902090123/https://owasp.org/www-pdf-archive/Introduction_to_shellcode_development.pdf)
- [Win32 API List (Microsoft Docs)](https://learn.microsoft.com/en-us/windows/win32/apiindex/windows-api-list)

### 2.4 Writing a Reverse Shell

The end goal of most shellcode: connect back to your machine over TCP and drop a shell. Write this from scratch in PIC assembly or PIC C. Do not use msfvenom for this exercise.

- [Reverse Shell Shellcode Part 2 (cocomelonc)](https://cocomelonc.github.io/tutorial/2021/11/09/windows-shellcoding-2.html)
- [Writing a Reverse Shell from C (0xect0)](https://0xect0.github.io/2024-07-28-shellcoding-rev-shell-from-c/)
- [WinSock2 API Reference (Microsoft Docs)](https://learn.microsoft.com/en-us/windows/win32/winsock/windows-sockets-start-page-2)
- [Msfvenom Reference (for comparison only)](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfvenom)

### 2.5 Visual Studio for Exploit Development

Use Visual Studio to write and compile shellcode in C, then extract raw opcodes from the Release build. You need to disable `/GS`, runtime checks, and optimizations that break PIC code.

- [Custom Windows Shellcode with Visual Studio (xacone)](https://xacone.github.io/custom_shellcode.html)
- [ShellcodeStdio via Visual Studio (winternl.com)](https://winternl.com/shellcodestdio/)
- [Disabling /GS Stack Security Check (Microsoft Docs)](https://learn.microsoft.com/en-us/cpp/build/reference/gs-buffer-security-check)
- [Executing Shellcode Directly (Osanda Malith)](https://osandamalith.com/2017/04/11/executing-shellcode-directly/)

---

## Module 3 - VMware Workstation Guest-to-Host Escape

> **CVE-2017-4901** | Use-After-Free in the Drag-and-Drop RPCI mechanism

This is the hardest module in the course. You are exploiting a use-after-free in `vmware-vmx.exe` and chaining it with heap grooming, ASLR bypass, a ROP chain, and shellcode execution to break out of the VM entirely. Every technique from Module 2 gets used here.

### 3.1 Vulnerability Overview

- [CVE-2017-4901 (CVE Details)](https://www.cvedetails.com/cve/CVE-2017-4901/)
- [vmware_escape PoC by rip1s (GitHub)](https://github.com/rip1s/vmware_escape)
- [How to Exploit CVE-2017-4901 (rip1s Wiki)](https://github.com/rip1s/vmware_escape/wiki/How-to-exploit-cve-2017-4901) - read this multiple times
- [Awesome VM Escape Exploits (WinMin)](https://github.com/WinMin/awesome-vm-exploit)
- [The Great Escapes of VMware (BlackHat EU 2017 PDF)](https://www.blackhat.com/docs/eu-17/materials/eu-17-Mandal-The-Great-Escapes-Of-Vmware-A-Retrospective-Case-Study-Of-Vmware-G2H-Escape-Vulnerabilities.pdf)

### 3.2 VMware Internals

You need to understand how the backdoor I/O port works, what RPCI is, and how the DnD (drag-and-drop) subsystem interacts with `vmware-vmx.exe` on the host.

- [Open-VM-Tools Source (Backdoor I/O Port)](https://github.com/vmware/open-vm-tools)
- [Backdoor Library Source Code](https://github.com/vmware/open-vm-tools/tree/master/open-vm-tools/lib/backdoor)
- [ESXi VM Escape PoC Analysis (Huntress 2025)](https://www.huntress.com/blog/esxi-vm-escape-exploit)

### 3.3 DEP Theory and Bypass

DEP marks memory pages as non-executable. The standard bypass is a ROP chain that calls `VirtualProtect` to flip the execute bit, then jumps to your shellcode.

- [DEP Overview (Microsoft Docs)](https://learn.microsoft.com/en-us/windows/win32/memory/data-execution-prevention)
- [Bypassing Hardware-Enforced DEP (Skape and Skywing, 2005)](https://web.archive.org/web/20210516224622/http://www.uninformed.org/?v=2&a=4) - the original paper
- [DEP/ASLR Bypass Whitepaper (Exploit-DB)](https://www.exploit-db.com/docs/english/17914-bypassing-aslrdep.pdf)
- [Step-by-Step ROP to Bypass DEP (CyberGeeks)](https://cybergeeks.tech/a-step-by-step-introduction-to-the-use-of-rop-gadgets-to-bypass-dep/)
- [Corelan Part 10: Chaining DEP with ROP](https://www.corelan.be/index.php/2010/06/16/exploit-writing-tutorial-part-10-chaining-dep-with-rop-the-rubik%c2%b3s-cube/)
- [Universal DEP/ASLR Bypass with msvcr71.dll and mona.py (Corelan)](https://www.corelan.be/index.php/2011/07/03/universal-depaslr-bypass-with-msvcr71-dll-and-mona-py/)
- [Modern Windows Memory Corruption Exploits Part 1 (CyberArk)](https://www.cyberark.com/resources/threat-research-blog/a-modern-exploration-of-windows-memory-corruption-exploits-part-i-stack-overflows)

### 3.4 Return-Oriented Programming

ROP is how you bypass DEP. You chain together small instruction sequences already present in loaded modules, each ending in a `ret`, to build a fake call stack that does what you want.

- [Return-Oriented Programming (Hovav Shacham, 2007)](https://dl.acm.org/doi/10.1145/1315245.1315313) - the foundational paper
- [ROP Emporium (practical x64 ROP challenges)](https://ropemporium.com/) - do all of these
- [rp++ Multi-architecture ROP Gadget Finder](https://github.com/0vercl0k/rp)
- [ROPgadget Python Tool](https://github.com/JonathanSalwan/ROPgadget)
- [Ropper ROP Chain Builder](https://github.com/sashs/Ropper)
- [Corelan Part 9: Introduction to Win32 Shellcoding](https://www.corelan.be/index.php/2010/02/25/exploit-writing-tutorial-part-9-introduction-to-win32-shellcoding/)

### 3.5 ASLR Bypass

ASLR randomizes base addresses. You defeat it through info leaks, finding non-ASLR modules, heap spraying, or partial overwrites depending on what the target gives you.

- [Corelan Part 6: Bypassing ASLR, SafeSEH, SEHOP, DEP](https://www.corelan.be/index.php/2009/09/21/exploit-writing-tutorial-part-6-bypassing-stack-cookies-safeseh-sehop-hw-dep-and-aslr/)
- [Windows 10 KASLR Bypass in One WinDbg Command (CoreSecurity)](https://www.coresecurity.com/core-labs/articles/windows-10-kaslr-bypass-windbg)
- [Bypassing ASLR/DEP Whitepaper (Exploit-DB)](https://www.exploit-db.com/docs/english/17914-bypassing-aslrdep.pdf)

### 3.6 Windows Heap Internals

Before you can groom the heap you need to understand it. How the allocator works, what a chunk looks like, how the free lists are managed, and where your data lands after each alloc and free.

- [Windows 8 Heap Internals (Valasek and Metz, BlackHat 2012 PDF)](https://illmatics.com/Windows%208%20Heap%20Internals.pdf)
- [Understanding the LFH (Valasek PDF)](https://www.illmatics.com/Understanding_the_LFH.pdf)
- [Project Heapbleed: Reusable Heap Primitives (census-labs)](https://census-labs.com/news/2014/12/04/project-heapbleed/)
- [Corelan Part 11: Heap Spraying Demystified](https://www.corelan.be/index.php/2011/12/31/exploit-writing-tutorial-part-11-heap-spraying-demystified/)

### 3.7 Low Fragmentation Heap

The LFH is the front-end allocator that handles commonly-sized objects. Exploiting bugs near LFH-managed memory means you need to control which bucket your allocation lands in and what neighbors it.

- [Understanding the LFH (Valasek PDF)](https://www.illmatics.com/Understanding_the_LFH.pdf)
- [Heap Feng Shui in JavaScript (Alexander Sotirov, BlackHat 2007 PDF)](https://www.blackhat.com/presentations/bh-europe-07/Sotirov/Presentation/bh-eu-07-sotirov-apr19.pdf)

### 3.8 Use-After-Free Case Studies

UAF is the bug class behind both the VMware and Edge exploits. You free an object, control what gets allocated in its place, and then trigger the stale pointer to corrupt that new object.

- [Exploiting CVE-2017-4901 Full Analysis (rip1s)](https://github.com/rip1s/vmware_escape/wiki/How-to-exploit-cve-2017-4901)
- [Browser UAF Exploitation (Connor McGarr, MS13-055 IE8)](https://connormcgarr.github.io/browser1/)
- [Use-After-Free Exploit Development (Exploit-DB PDF)](https://www.exploit-db.com/docs/english/44463-use-after-free-exploitation.pdf)
- [Exploiting HEVD UAF x64 with Non-Paged Pool Feng-Shui](https://securityinsecurity.github.io/exploiting-hevd-use-after-free/)
- [CVE-2015-0057: win32k UAF (Exploit-DB)](https://www.exploit-db.com/exploits/36974)

### 3.9 Stack Pivoting

When your overflow does not land on a stack you control, you use a stack pivot gadget to redirect RSP to attacker-controlled memory where you have already staged your ROP chain.

- [FuzzySecurity Tutorial Part 13: Stack Pivoting](https://www.fuzzysecurity.com/tutorials/expDev/13.html)
- [FuzzySecurity Tutorial Part 7: ROP Gadgets](https://www.fuzzysecurity.com/tutorials/expDev/7.html)
- [SMEP Bypass via Stack Pivoting (Connor McGarr)](https://connormcgarr.github.io/x64-Kernel-Shellcode-Revisited-and-SMEP-Bypass/)

### 3.10 Windows Defender Exploit Guard

The host process `vmware-vmx.exe` has WDEG mitigations enabled including ROP mitigations, export address filtering, and import address filtering. You need to understand what each one does before you can bypass them.

- [Windows Defender Exploit Guard (Microsoft Docs)](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/exploit-protection)
- [Exploit Protection Reference (Microsoft Docs)](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/exploit-protection-reference)

---

## Module 4 - Microsoft Edge Type Confusion

> **CVE-2019-0567** | Type Confusion in the Chakra JavaScript Engine

Three-stage exploit chain. Stage 1 gets a read/write primitive in the renderer. Stage 2 defeats CFG and ACG. Stage 3 escapes the AppContainer sandbox. Each stage builds on the last and all of them are defeated by techniques unique to modern browsers.

### 4.1 Chakra Internals

You need to understand how ChakraCore represents JavaScript objects, how the JIT compiler works, what auxSlots are, how NaN boxing works, and the difference between inline and auxiliary property storage.

- [ChakraCore Open-Source JS Engine (GitHub)](https://github.com/chakra-core/ChakraCore)
- [CVE-2019-0567 Part 1: Environment Setup and Vulnerability Analysis (Connor McGarr)](https://connormcgarr.github.io/type-confusion-part-1/)
- [Attacking Edge Through the JavaScript Compiler (Bruno Keith)](https://github.com/bkth/Attacking-Edge-Through-the-JavaScript-Compiler)
- [Project Zero Issue for CVE-2019-0567](https://issues.chromium.org/issues/40066595)

### 4.2 Root Cause Analysis

`InitProto` is incorrectly marked side-effect-free by the JIT. When this assumption is violated during a type transition, the optimizer corrupts the `auxSlots` pointer, giving you a type confusion.

- [CVE-2019-0567 Part 1: Vulnerability Analysis (Connor McGarr)](https://connormcgarr.github.io/type-confusion-part-1/)
- [DayZeroSec: CVE-2019-0567 Summary](https://dayzerosec.com/vulns/2022/04/19/microsoft-edge-type-confusion-vulnerability-part-2-cve-2019-0567.html)
- [Perception Point: CVE-2019-0539 Sister Vulnerability Analysis](https://perception-point.io/cve-2019-0539/)

### 4.3 Building the Read/Write Primitive

Corrupt the `auxSlots` pointer to point to a second object. Use two `DataView` instances to turn the type confusion into a stable arbitrary read and write primitive. NaN boxing lets you read 64-bit pointers correctly.

- [CVE-2019-0567 Part 2: R/W Primitive Development (Connor McGarr)](https://connormcgarr.github.io/type-confusion-part-2/)
- [DataView API (MDN Web Docs)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DataView)
- [Attacking Edge Through the JS Compiler (Bruno Keith)](https://github.com/bkth/Attacking-Edge-Through-the-JavaScript-Compiler)

### 4.4 Controlling RIP

Use your read/write primitive to leak a vtable pointer, calculate module offsets, and then overwrite the vtable to redirect execution into your ROP chain.

- [CVE-2019-0567 Part 3: RIP Control and Defeating Mitigations (Connor McGarr)](https://connormcgarr.github.io/type-confusion-part-3/)

### 4.5 Control Flow Guard Bypass

CFG validates the target of every indirect call. You bypass it by finding a call target that is not protected, or by corrupting a pointer that CFG does not check.

- [Bypassing CFG on Windows 10 (BlackHat 2014 PDF)](https://www.blackhat.com/docs/us-14/materials/us-14-Zhang-Bypassing-Control-Flow-Guard-On-Windows-10-And-Windows-8-1.pdf)
- [Bypassing Control Flow Guard in Windows 10 (Improsec)](https://improsec.com/tech-blog/bypassing-control-flow-guard-in-windows-10)
- [Cross The Wall: Bypass All Mitigations in Edge (BlackHat 2017 PDF)](https://www.blackhat.com/docs/us-17/thursday/us-17-Chen-CROSS-WALL-Bypass-All-Modern-Mitigations-of-Microsoft-Edge.pdf)

### 4.6 Arbitrary Code Guard Bypass

ACG prevents the content process from mapping new executable memory or modifying existing code pages. The bypass abuses the out-of-process JIT server using RPC calls from the content process.

- [CVE-2019-0567 Part 3: ACG Bypass via RPC (Connor McGarr)](https://connormcgarr.github.io/type-confusion-part-3/)
- [ACG Reference (Microsoft Docs)](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/exploit-protection-reference)
- [CVE-2017-8637: ACG Bypass via Edge Out-of-Process JIT (MSRC)](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2017-8637)
- [Attacking Edge Through the JS Compiler (Bruno Keith)](https://github.com/bkth/Attacking-Edge-Through-the-JavaScript-Compiler)

### 4.7 Data-Only Attacks

Sometimes you cannot execute code at all. Instead you use your read/write primitive to directly modify security-relevant data: flags, tokens, ACL entries, or dispatch tables, without ever running your own shellcode.

- [Non-Control-Data Attacks Are Realistic Threats (Chen et al., 2005)](https://dl.acm.org/doi/10.1145/1102120.1102148)
- [yeyintminthuhtut: Data-Only Attack References](https://github.com/yeyintminthuhtut/Awesome-Advanced-Windows-Exploitation-References)

### 4.8 Sandbox Escape

The Edge renderer runs inside an AppContainer. Getting code execution in the renderer is not enough. You need to abuse the JIT server or broker process, which runs with more privilege, to fully escape the sandbox.

- [Chromium Sandbox Architecture](https://chromium.googlesource.com/chromium/src/+/main/sandbox/)
- [Cross The Wall: Bypass All Mitigations in Edge (BlackHat 2017 PDF)](https://www.blackhat.com/docs/us-17/thursday/us-17-Chen-CROSS-WALL-Bypass-All-Modern-Mitigations-of-Microsoft-Edge.pdf)
- [Project Zero Blog: Edge and Chrome Sandbox Research](https://googleprojectzero.blogspot.com/)

---

## Module 5 - Windows Kernel Exploitation

Kernel exploitation means running code at ring 0. A single mistake crashes the machine. You need to understand pool internals, how the kernel handles user-mode interactions, and how to manipulate kernel data structures like tokens and callbacks without triggering any of the hardware mitigations (SMEP, SMAP, KVAS).

### 5.1 Kernel Architecture

Understand the full picture: ring 0 vs ring 3, IRQL levels, how syscalls work, how IOCTLs reach driver handlers, and what the `KPCR/KTHREAD/EPROCESS` chain looks like in memory.

- [Windows Kernel Driver Programming Overview (Microsoft Docs)](https://learn.microsoft.com/en-us/windows-hardware/drivers/kernel/)
- [EPROCESS and Kernel Structure Reference (CodeMachine)](https://www.codemachine.com/article_kernelstruct.html)
- [Alex Ionescu Windows Internals Talks (YouTube)](https://www.youtube.com/results?search_query=alex+ionescu+windows+internals)
- [Windows Internals Part 1 (Mark Russinovich)](https://learn.microsoft.com/en-us/sysinternals/resources/windows-internals)

### 5.2 HEVD Lab Setup

HackSys Extreme Vulnerable Driver is the standard training target. It has every major kernel bug class implemented intentionally in both x86 and x64. Start every technique here before touching real targets.

- [HEVD Repository (GitHub)](https://github.com/hacksysteam/HackSysExtremeVulnerableDriver)
- [HEVD Pre-compiled Releases (x86/x64)](https://github.com/hacksysteam/HackSysExtremeVulnerableDriver/releases)
- [Introduction to Windows Kernel Exploitation with HEVD (wetw0rk)](https://wetw0rk.github.io/posts/0x00-introduction-to-windows-kernel-exploitation/)
- [HEVD Kernel Exploitation Saga Writeup](https://medium.com/@Achilles8284/windows-kernel-exploitation-the-saga-hevd-writeup-part-2-payloads-and-processes-5f783ff58812)
- [xct/windows-kernel-exploits (GitHub)](https://github.com/xct/windows-kernel-exploits)

### 5.3 Token Stealing

The classic kernel privilege escalation. Walk the `EPROCESS` list to find the `System` process, copy its token into your process's token field, and return to user mode as `NT AUTHORITY\SYSTEM`.

- [Token Stealing and SMEP Bypass on Windows 10 x64 (Connor McGarr)](https://connormcgarr.github.io/x64-Kernel-Shellcode-Revisited-and-SMEP-Bypass/)
- [Starting with Kernel Exploitation Part 3: Token Stealing (hasherezade)](https://hshrzd.wordpress.com/2017/06/22/starting-with-windows-kernel-exploitation-part-3-stealing-the-access-token/)
- [How Kernel Exploits Abuse Tokens (ired.team)](https://www.ired.team/miscellaneous-reversing-forensics/windows-kernel-internals/how-kernel-exploits-abuse-tokens-for-privilege-escalation)
- [PINKPANTHER: Handcrafted Token Stealing Shellcode (GitHub)](https://github.com/winterknife/PINKPANTHER)
- [Windows Kernel Exploitation Part 3: Arbitrary Memory Overwrite (Exploit-DB PDF)](https://www.exploit-db.com/docs/english/43527-windows-kernel-exploitation-tutorial-part-3-arbitrary-memory-overwrite-(write-what-where).pdf)

### 5.4 Kernel Stack Overflow

Overflow a kernel stack buffer to overwrite the return address. If GS cookies are present you need a way around them first. Then you either land on shellcode directly or use a kernel ROP chain.

- [Starting with Kernel Exploitation Part 2: Stack Overflows (hasherezade)](https://hshrzd.wordpress.com/2017/06/05/starting-with-windows-kernel-exploitation-part-2/)
- [HEVD x64 Stack Overflow (wetw0rk)](https://wetw0rk.github.io/posts/0x00-introduction-to-windows-kernel-exploitation/)
- [Kernel Stack Overflow Exploitation (Osanda Malith)](https://osandamalith.com/2017/04/05/windows-kernel-exploitation-stack-overflow/)

### 5.5 Arbitrary Memory Overwrite (Write-What-Where)

Overwrite `HalDispatchTable+0x8` with the address of your shellcode. Then call `NtQueryIntervalProfile` from user mode to trigger the overwritten pointer inside the kernel.

- [FuzzySecurity Tutorial Part 15: Write-What-Where via HalDispatchTable](https://fuzzysecurity.com/tutorials/expDev/15.html)
- [Kernel Write-What-Where via HalDispatchTable (rootkits.xyz)](https://rootkits.xyz/blog/2017/08/kernel-writing-what-where/)
- [Windows Kernel Exploitation Part 3: Write-What-Where (Exploit-DB PDF)](https://www.exploit-db.com/docs/english/43527-windows-kernel-exploitation-tutorial-part-3-arbitrary-memory-overwrite-(write-what-where).pdf)

### 5.6 Kernel Pool Exploitation

Pool overflows and UAF in the non-paged or paged pool. You need to groom the pool to get your target allocation in the right place before triggering the bug.

- [Exploiting HEVD UAF x64 with Pool Feng-Shui](https://securityinsecurity.github.io/exploiting-hevd-use-after-free/)
- [Pool Overflow Exploitation Since Windows 10 19H1 (SSTIC 2020 PDF)](https://www.sstic.org/media/SSTIC2020/SSTIC-actes/pool_overflow_exploitation_since_windows_10_19h1/SSTIC2020-Article-pool_overflow_exploitation_since_windows_10_19h1-2.pdf)
- [CVE-2021-21551: Dell BIOS Driver Pool Exploitation (CrowdStrike)](https://www.crowdstrike.com/blog/cve-2021-21551-learning-through-exploitation/)
- [Windows 10 Pool Memory Internals (windows-internals.com)](https://windows-internals.com/pool-overflow-exploitation-since-windows-10-19h1/)

### 5.7 SMEP Bypass

SMEP (CR4 bit 20) prevents the CPU from executing user-mode pages while in ring 0. The standard bypass is a ROP gadget that clears the bit before jumping to your shellcode. PTE manipulation is another option.

- [SMEP: What it is and How to Beat it (Andrea Fortuna)](https://www.andreafortuna.org/2017/09/28/smep-what-is-it-and-how-to-beat-it-on-windows/)
- [Token Stealing and SMEP Bypass on Windows 10 x64 (Connor McGarr)](https://connormcgarr.github.io/x64-Kernel-Shellcode-Revisited-and-SMEP-Bypass/)
- [HEVD x64 Stack Overflow with SMEP Bypass (rootkits.xyz)](https://rootkits.xyz/blog/2017/11/kernel-stack-overflow-smep/)
- [yeyintminthuhtut: SMEP Bypass References](https://github.com/yeyintminthuhtut/Awesome-Advanced-Windows-Exploitation-References)

### 5.8 Unsanitized User-Mode Callbacks

The `win32k` subsystem can call back into user mode during kernel execution. If the kernel does not re-validate object state after the callback returns, an attacker can corrupt that state during the window.

- [Kernel Attacks Through User-Mode Callbacks (Tarjei Mandt, BlackHat 2011 PDF)](https://www.blackhat.com/docs/us-11/materials/us-11-Mandt-Kernel-Attacks-Through-User-Mode-Callbacks.pdf) - essential reading
- [CVE-2011-1974: Win32k Callback Vulnerability (Exploit-DB)](https://www.exploit-db.com/exploits/17474)
- [MS15-061: Win32k UAF via xxxSetClassLong Callback (Exploit-DB)](https://www.exploit-db.com/exploits/37055)

### 5.9 Driver Callback Overwrite

Overwrite kernel callback pointers like `PsSetCreateProcessNotifyRoutine` entries or I/O completion callbacks. When the kernel triggers one of those callbacks your code runs in ring 0.

- [Windows Driver Kit (Microsoft Docs)](https://learn.microsoft.com/en-us/windows-hardware/drivers/download-the-wdk)
- [Vulnerable Driver Files (PwnAwan EXP-401 Repo)](https://github.com/PwnAwan/EXP-401-OSEE/tree/main/Driver%20Files)
- [Windows Kernel Security Mitigations (Microsoft MSRC Blog)](https://msrc.microsoft.com/blog/)

---

## Module 6 - Hyper-V Bonus

Not always on the main syllabus but directly relevant. Understanding the hypervisor layer helps with both kernel exploitation technique and with the VMware module.

- [Hyper-V Architecture (Microsoft Docs)](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/reference/hyper-v-architecture)
- [Advanced Windows 10 Kernel Exploitation (Morten Schenk, DEF CON 25)](https://www.youtube.com/watch?v=Gu_5kkErQ6Y)
- [WindowsExploitationResources Hyper-V Section (FULLSHADE)](https://github.com/FULLSHADE/WindowsExploitationResources)

---

## Module 7 - Exam Prep and Strategy

### 7.1 Exam Structure

- 72-hour exam with two assignments
- 75 points needed to pass (each assignment is worth up to 50 points, 25 for partial credit)
- Penetration test report in PDF format due within 24 hours after the exam window closes
- [Official OSEE Exam Guide](https://help.offsec.com/hc/en-us/articles/360046458732-EXP-401-Advanced-Windows-Exploitation-OSEE-Exam-Guide)

### 7.2 Practice CVEs

These are the targets the community recommends for building skills that directly apply to the exam.

| CVE | Description | Writeup |
|-----|-------------|---------|
| CVE-2021-21551 | Dell BIOS Driver pool LPE | [CrowdStrike](https://www.crowdstrike.com/blog/cve-2021-21551-learning-through-exploitation/) |
| CVE-2017-8601 | Windows JScript type confusion | [Exploit-DB](https://www.exploit-db.com/exploits/42479) |
| CVE-2015-5736 | Fortinet FortiClient | [Exploit-DB](https://www.exploit-db.com/exploits/41721) |
| CVE-2014-4113 | Win32k UAF (MS14-058) | [Exploit-DB](https://www.exploit-db.com/exploits/37064) |
| CVE-2011-2005 | NDIS LPE (MS11-080) | [Exploit-DB](https://www.exploit-db.com/exploits/18176) |
| CVE-2017-4901 | VMware guest-to-host escape | [rip1s GitHub](https://github.com/rip1s/vmware_escape) |
| CVE-2019-0567 | Edge Chakra type confusion | [Connor McGarr](https://connormcgarr.github.io/type-confusion-part-1/) |
| HEVD | All kernel bug classes | [GitHub](https://github.com/hacksysteam/HackSysExtremeVulnerableDriver) |

### 7.3 Recommended Study Path

Go through this in order. Do not skip ahead to the browser stuff until you can write a kernel exploit from scratch.

1. Complete Corelan exploit writing tutorials Parts 1 through 11
2. Exploit HEVD stack overflow on x86 then x64
3. Exploit HEVD write-what-where via `HalDispatchTable`
4. Exploit HEVD pool UAF with non-paged pool feng shui
5. Write a custom PIC reverse shell in x64 assembly
6. Read both Valasek heap internals PDFs cover to cover
7. Analyze CVE-2017-4901 (VMware) using the rip1s wiki and source code
8. Build CVE-2019-0567 by following all three Connor McGarr posts
9. Write a full penetration test report for each exploit you build
10. Read every AWE course review to calibrate your expectations for the exam

---

## Module 8 - Tools Reference

### 8.1 WinDbg

- [WinDbg Full Documentation (Microsoft Docs)](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/)
- [WinDbg Quick Reference (OSR Online)](https://www.osronline.com/article.cfm%5Eid=576.htm)
- [WinDbg Commands Cheat Sheet (briolidz)](https://briolidz.wordpress.com/2013/11/17/windbg-some-debugging-commands/)
- [Kernel Mode WinDbg Extensions (Microsoft Docs)](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/kernel-mode-extensions)

### 8.2 Scripting and Automation

- [pwntools (Linux-focused but useful for scaffolding)](https://github.com/Gallopsled/pwntools)
- [Sickle: Shellcode and Opcode Generation](https://github.com/wetw0rk/Sickle)
- [ctypes: Calling Windows APIs from Python](https://docs.python.org/3/library/ctypes.html)
- [Volatility3: Memory Analysis for Kernel Structure Research](https://github.com/volatilityfoundation/volatility3)

### 8.3 Fuzzing and Patch Diffing

- [WinAFL: Windows Fuzzing (Google Project Zero)](https://github.com/googleprojectzero/winafl)
- [AFL++: Modern Fuzzing Framework](https://github.com/AFLplusplus/AFLplusplus)
- [BinDiff: Binary Comparison and Patch Diffing](https://www.zynamics.com/bindiff.html)
- [Diaphora: IDA Pro Binary Diffing Plugin](https://github.com/joxeankoret/diaphora)

---

## Module 9 - Papers and Conference Talks

### 9.1 Papers You Should Actually Read

| Paper | Year | Link |
|-------|------|------|
| Return-Oriented Programming (Shacham) | 2007 | [ACM](https://dl.acm.org/doi/10.1145/1315245.1315313) |
| ROP Without Returns (Checkoway et al.) | 2010 | [ACM](https://dl.acm.org/doi/10.1145/1866307.1866370) |
| Non-Control-Data Attacks (Chen et al.) | 2005 | [ACM](https://dl.acm.org/doi/10.1145/1102120.1102148) |
| Bypassing Hardware-Enforced DEP (Skape, Skywing) | 2005 | [Archive](https://web.archive.org/web/20210516224622/http://www.uninformed.org/?v=2&a=4) |
| Heap Feng Shui in JavaScript (Sotirov) | 2007 | [BlackHat PDF](https://www.blackhat.com/presentations/bh-europe-07/Sotirov/Presentation/bh-eu-07-sotirov-apr19.pdf) |

### 9.2 Conference Talks

| Talk | Event | Link |
|------|-------|------|
| Kernel Attacks Through User-Mode Callbacks (Tarjei Mandt) | BlackHat 2011 | [PDF](https://www.blackhat.com/docs/us-11/materials/us-11-Mandt-Kernel-Attacks-Through-User-Mode-Callbacks.pdf) |
| The Great Escapes of VMware | BlackHat EU 2017 | [PDF](https://www.blackhat.com/docs/eu-17/materials/eu-17-Mandal-The-Great-Escapes-Of-Vmware-A-Retrospective-Case-Study-Of-Vmware-G2H-Escape-Vulnerabilities.pdf) |
| Cross The Wall: Bypass All Mitigations in Edge | BlackHat US 2017 | [PDF](https://www.blackhat.com/docs/us-17/thursday/us-17-Chen-CROSS-WALL-Bypass-All-Modern-Mitigations-of-Microsoft-Edge.pdf) |
| Bypassing Control Flow Guard on Windows 10 | BlackHat US 2014 | [PDF](https://www.blackhat.com/docs/us-14/materials/us-14-Zhang-Bypassing-Control-Flow-Guard-On-Windows-10-And-Windows-8-1.pdf) |
| Advanced Windows 10 Kernel Exploitation (Morten Schenk) | DEF CON 25 | [YouTube](https://www.youtube.com/watch?v=Gu_5kkErQ6Y) |

### 9.3 Free Training Platforms

| Platform | What it covers | Link |
|----------|---------------|------|
| ROP Emporium | Practical ROP x64 | [ropemporium.com](https://ropemporium.com/) |
| RET2 Wargames | Exploit development | [wargames.ret2.systems](https://wargames.ret2.systems/) |
| pwn.college | Binary and kernel exploitation | [pwn.college](https://pwn.college/) |
| OpenSecurityTraining2 | Architecture and exploitation, free | [ost2.fyi](https://ost2.fyi/) |
| Nightmare | Binary exploitation course | [guyinatuxedo.github.io](https://guyinatuxedo.github.io/) |
| LiveOverflow | Exploitation YouTube series | [YouTube](https://www.youtube.com/c/LiveOverflow) |
| exploit.education | Vulnerable VMs | [exploit.education](https://exploit.education/) |

---

## CVE Reference Table

| CVE | Application | Bug Class | Module |
|-----|-------------|-----------|--------|
| CVE-2017-4901 | VMware Workstation | Use-After-Free (DnD RPCI) | 3 |
| CVE-2019-0567 | Microsoft Edge / Chakra | Type Confusion (JIT) | 4 |
| CVE-2019-0539 | Microsoft Edge / Chakra | Type Confusion | 4 |
| CVE-2017-8637 | Microsoft Edge | ACG Bypass (JIT Server) | 4 |
| CVE-2017-8601 | Windows JScript | Type Confusion | 4 |
| CVE-2021-21551 | Dell BIOSConnect | Pool Overflow (LPE) | 5 |
| CVE-2014-4113 | win32k.sys | Use-After-Free | 5 |
| CVE-2015-0057 | win32k.sys | Use-After-Free (Callback) | 5 |
| CVE-2011-2005 | NDIS | Buffer Overflow | 5 |

---

<p align="center">
  <sub>Independent community resource. Not affiliated with Offensive Security.
</p>
