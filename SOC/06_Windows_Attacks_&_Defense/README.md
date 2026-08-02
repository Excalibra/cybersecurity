# Windows Attacks & Defense

## Module Description

Microsoft Active Directory (AD) has been, for the past 20+ years, the leading enterprise domain management suite, providing identity and access management, centralized domain administration, authentication, and much more. Throughout those years, the more integrated our applications and data have become with AD, the more exposed to a large-scale compromise we have become. In this module, we will walk through the most commonly abused and fruitful attacks against Active Directory environments that allow threat actors to perform horizontal and vertical privilege escalations in addition to lateral movement.

One of the module's core goals is to showcase prevention and detection methods against the covered Active Directory attacks.

## Module Summary

This module will walk you through the most commonly abused and fruitful attacks against Active Directory, allowing horizontal and vertical privilege escalations as well as lateral movement. For each of the following attacks, we will outline different prevention techniques, showcase detection methods, and implement honeypots (if possible) to trap attackers:

- `Kerberoasting`
- `Asreproasting`
- `GPP Passwords`
- `Misconfigured GPO Permissions (or GPO-deployed files)`
- `Credentials in Network Shares`
- `Credentials in User Attributes`
- `DCSync`
- `Kerberos Golden Ticket`
- `Kerberos Constrained Delegation Attack`
- `Print Spooler & NTLM Relaying`
- `Coercing attacks & Kerberos Unconstrained Delegation`
- `Object ACLs`
- `PKI Misconfigurations` - `ESC1`
- `PKI Misconfigurations` - `ESC8` (`Coercing` + `Certificates`)

---

This module is broken into sections with accompanying hands-on exercises to practice the tactics and techniques we cover. The module ends with a practical hands-on skills assessment to gauge your understanding of the various topic areas.

As you work through the module, you will see example commands and command output for the topics introduced. It is worth reproducing as many of these examples as possible to reinforce further the concepts presented in each section. You can do this in the target host provided in the interactive sections or your virtual machine.

You can start and stop the module anytime and pick up where you left off. There is no time limit or "grading," but you must complete all of the exercises and the skills assessment to receive the maximum number of cubes and have this module marked as complete in any paths you have chosen.

The module is classified as "medium" and assumes basic knowledge of how Windows operate and common AD attack principles.

A firm grasp of the following modules can be considered prerequisites for successful completion of this module:

- Introduction to Windows Command Line
- Introduction to Active Directory
- Password Attacks
- Active Directory Enumeration & Attacks
- Windows Event Logs & Finding Evil
