# Windows Event Logs & Finding Evil

## Module Description

This module covers the exploration of Windows Event Logs and their significance in uncovering suspicious activities. Throughout the course, we delve into the anatomy of Windows Event Logs and highlight the logs that hold the most valuable information for investigations. The module also focuses on utilizing Sysmon and Event Logs for detecting and analyzing malicious behavior. Additionally, we delve into Event Tracing for Windows (ETW), explaining its architecture and components, and provide ETW-based detection examples. To streamline the analysis process, we introduce the powerful Get-WinEvent cmdlet.

## Module Summary

This module focuses on exploring `Windows Event Logs` and their role in identifying suspicious activities.

- We dive into the intricacies of Windows Event Logs, examining their anatomy and highlighting the most valuable logs for investigation purposes.
- We provide practical insights on how to effectively investigate these logs to uncover potential security breaches. One key aspect we cover is the utilization of `Sysmon` and Event Logs to detect and analyze malicious activities.
- We guide you through the process of installing or updating Sysmon and present real-world examples of detection, including identifying `DLL hijacking`, `unmanaged PowerShell/C-Sharp injection`, and `credential dumping`.
- We also delve into `Event Tracing for Windows (ETW)` and its architecture, explaining its components and showcasing how to interact with it.
- We introduce useful ETW providers and offer `ETW-based detection` examples like identifying `unusual parent-child relationships` and `malicious .NET assembly loading`.
- Furthermore, we introduce the powerful `Get-WinEvent cmdlet` for streamlined analysis of Windows Event Logs. We demonstrate various examples of retrieving events from specific logs and provide techniques for efficient event filtering.

---

`CREST CPSA/CRT`-related Sections:

- Analyzing Evil With Sysmon & Event Logs
- Tapping Into ETW

---

This module is broken into sections with accompanying hands-on exercises to practice the techniques we cover. The module ends with a practical hands-on skills assessment to gauge your understanding of the various topic areas.

As you work through the module, you will see detection examples for the topics introduced. It is worth reproducing as many of these examples as possible to reinforce further the concepts presented in each section. You can do this in the target host provided in the interactive sections or your virtual machine.

You can start and stop the module anytime and pick up where you left off. There is no time limit or "grading," but you must complete all of the exercises and the skills assessment to receive the maximum number of cubes and have this module marked as complete in any paths you have chosen.

The module is classified as "medium" and assumes basic knowledge of how Windows operate and common attack principles.

A firm grasp of the following modules can be considered prerequisites for successful completion of this module:

- Penetration Testing Process
- Incident Handling Process
