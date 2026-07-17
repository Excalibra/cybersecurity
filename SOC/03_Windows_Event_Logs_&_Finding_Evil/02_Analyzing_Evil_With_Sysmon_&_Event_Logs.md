# Analyzing Evil With Sysmon & Event Logs

In our pursuit of robust cybersecurity, it is crucial to understand how to identify and analyze malicious events effectively. Building upon our previous exploration of benign events, we will now delve into the realm of malicious activities and discover techniques for detection.

---

## Sysmon Basics

When investigating malicious events, several event IDs serve as common indicators of compromise. For instance, `Event ID 4624` provides insights into new logon events, enabling us to monitor and detect suspicious user access and logon patterns. Similarly, `Event ID 4688` furnishes information about newly created processes, aiding the identification of unusual or malicious process launches. To enhance our event log coverage, we can extend the capabilities by incorporating Sysmon, which offers additional event logging capabilities.

`System Monitor (Sysmon)` is a Windows system service and device driver that remains resident across system reboots to monitor and log system activity to the Windows event log. Sysmon provides detailed information about process creation, network connections, changes to file creation time, and more.

Sysmon's primary components include:

- A Windows service for monitoring system activity.
- A device driver that assists in capturing the system activity data.
- An event log to display captured activity data.

Sysmon's unique capability lies in its ability to log information that typically doesn't appear in the Security Event logs, and this makes it a powerful tool for deep system monitoring and cybersecurity forensic analysis.

Sysmon categorizes different types of system activity using event IDs, where each ID corresponds to a specific type of event. For example, `Event ID 1` corresponds to "Process Creation" events, and `Event ID 3` refers to "Network Connection" events. The full list of Sysmon event IDs can be found [here](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon).

For more granular control over what events get logged, Sysmon uses an XML-based configuration file. The configuration file allows you to include or exclude certain types of events based on different attributes like process names, IP addresses, etc. We can refer to popular examples of useful Sysmon configuration files:

- For a comprehensive configuration, we can visit: [https://github.com/SwiftOnSecurity/sysmon-config](https://github.com/SwiftOnSecurity/sysmon-config). <-- `We will use this one in this section!`
- Another option is: [https://github.com/olafhartong/sysmon-modular](https://github.com/olafhartong/sysmon-modular), which provides a modular approach.

To get started, you can install Sysmon by downloading it from the official Microsoft documentation ([https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon)). Once downloaded, open an administrator command prompt and execute the following command to install Sysmon.

```cmd
C:\Tools\Sysmon> sysmon.exe -i -accepteula -h md5,sha256,imphash -l -n
```

<img width="1402" height="508" alt="image" src="https://github.com/user-attachments/assets/041a8530-64ae-415d-80e8-2dd83f80a46d" />


To utilize a custom Sysmon configuration, execute the following after installing Sysmon.

```shell
C:\Tools\Sysmon> sysmon.exe -c filename.xml
```

**Note**: It should be noted that [Sysmon for Linux](https://github.com/Sysinternals/SysmonForLinux) also exists.

---

## Detection Example 1: Detecting DLL Hijacking

In our specific use case, we aim to detect a DLL hijack. The Sysmon event log IDs relevant to DLL hijacks can be found in the Sysmon documentation ([https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon)). To detect a DLL hijack, we need to focus on `Event Type 7`, which corresponds to module load events. To achieve this, we need to modify the `sysmonconfig-export.xml` Sysmon configuration file we downloaded from [https://github.com/SwiftOnSecurity/sysmon-config](https://github.com/SwiftOnSecurity/sysmon-config).

By examining the modified configuration, we can observe that the "include" comment signifies events that should be included.

<img width="1926" height="222" alt="image" src="https://github.com/user-attachments/assets/51167b00-2432-4502-ad37-fff877d46423" />

In the case of detecting DLL hijacks, we change the "include" to "exclude" to ensure that nothing is excluded, allowing us to capture the necessary data.

<img width="1820" height="200" alt="image" src="https://github.com/user-attachments/assets/5b3749aa-e678-4f94-b6f3-97c40c25be2b" />

To utilize the updated Sysmon configuration, execute the following.

```cmd
C:\Tools\Sysmon> sysmon.exe -c sysmonconfig-export.xml
```

<img width="1450" height="436" alt="image" src="https://github.com/user-attachments/assets/18e8f721-19f6-4fdc-9f05-c4a29460bc91" />

With the modified Sysmon configuration, we can start observing image load events. To view these events, navigate to the Event Viewer and access "Applications and Services" -> "Microsoft" -> "Windows" -> "Sysmon." A quick check will reveal the presence of the targeted event ID.

<img width="1000" height="468" alt="image" src="https://github.com/user-attachments/assets/27ae948c-f280-4fc5-aa08-4a17ef0469a5" />

Let's now see how a Sysmon event ID 7 looks like.

<img width="2124" height="588" alt="image" src="https://github.com/user-attachments/assets/3e7672bb-a65c-4e52-ab83-bfd919173592" />

The event log contains the DLL's signing status (in this case, it is Microsoft-signed), the process or image responsible for loading the DLL, and the specific DLL that was loaded. In our example, we observe that "MMC.exe" loaded "psapi.dll", which is also Microsoft-signed. Both files are located in the System32 directory.

Now, let's proceed with building a detection mechanism. To gain more insights into DLL hijacks, conducting research is paramount. We stumble upon an informative [blog post](https://www.wietzebeukema.nl/blog/hijacking-dlls-in-windows) that provides an exhaustive list of various DLL hijack techniques. For the purpose of our detection, we will focus on a specific hijack involving the vulnerable executable calc.exe and a list of DLLs that can be hijacked.

<img width="1000" height="550" alt="image" src="https://github.com/user-attachments/assets/82ff5d53-8966-4516-9acd-56d2654b74b3" />

Let's attempt the hijack using "calc.exe" and "WININET.dll" as an example. To simplify the process, we can utilize Stephen Fewer's "hello world" [reflective DLL](https://github.com/stephenfewer/ReflectiveDLLInjection/tree/master/bin). It should be noted that DLL hijacking does not require reflective DLLs.

By following the required steps, which involve renaming `reflective_dll.x64.dll` to `WININET.dll`, moving `calc.exe` from `C:\Windows\System32` along with `WININET.dll` to a writable directory (such as the `Desktop` folder), and executing `calc.exe`, we achieve success. Instead of the Calculator application, a [MessageBox](https://learn.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-messageboxa) is displayed.

<img width="1008" height="592" alt="image" src="https://github.com/user-attachments/assets/83bb9dce-ad7e-4a32-b28a-43c04479cf7f" />

Next, we analyze the impact of the hijack. First, we filter the event logs to focus on `Event ID 7`, which represents module load events, by clicking "Filter Current Log...".

<img width="1090" height="1106" alt="image" src="https://github.com/user-attachments/assets/4671d423-5ea5-4d80-abda-feb4f11bb8db" />

Subsequently, we search for instances of "calc.exe", by clicking "Find...", to identify the DLL load associated with our hijack.

<img width="2136" height="836" alt="image" src="https://github.com/user-attachments/assets/e04f15ef-1878-462c-a44f-57abbebaabcb" />

The output from Sysmon provides valuable insights. Now, we can observe several indicators of compromise (IOCs) to create effective detection rules. Before moving forward though, let's compare this to an authenticate load of "wininet.dll" by "calc.exe".

<img width="1000" height="466" alt="image" src="https://github.com/user-attachments/assets/cde35902-b31a-49e9-ab8e-12674716bc78" />

Let's explore these IOCs:

1. "calc.exe", originally located in System32, should not be found in a writable directory. Therefore, a copy of "calc.exe" in a writable directory serves as an IOC, as it should always reside in System32 or potentially Syswow64.
2. "WININET.dll", originally located in System32, should not be loaded outside of System32 by calc.exe. If instances of "WININET.dll" loading occur outside of System32 with "calc.exe" as the parent process, it indicates a DLL hijack within calc.exe. While caution is necessary when alerting on all instances of "WININET.dll" loading outside of System32 (as some applications may package specific DLL versions for stability), in the case of "calc.exe", we can confidently assert a hijack due to the DLL's unchanging name, which attackers cannot modify to evade detection.
3. The original "WININET.dll" is Microsoft-signed, while our injected DLL remains unsigned.

These three powerful IOCs provide an effective means of detecting a DLL hijack involving calc.exe. It's important to note that while Sysmon and event logs offer valuable telemetry for hunting and creating alert rules, they are not the sole sources of information.

---

## Detection Example 2: Detecting Unmanaged PowerShell/C-Sharp Injection

Before delving into detection techniques, let's gain a brief understanding of C# and its runtime environment. C# is considered a "managed" language, meaning it requires a backend runtime to execute its code. The [Common Language Runtime (CLR)](https://docs.microsoft.com/en-us/dotnet/standard/clr) serves as this runtime environment. [Managed code](https://docs.microsoft.com/en-us/dotnet/standard/managed-code) does not directly run as assembly; instead, it is compiled into a bytecode format that the runtime processes and executes. Consequently, a managed process relies on the CLR to execute C# code.

As defenders, we can leverage this knowledge to detect unusual C# injections or executions within our environment. To accomplish this, we can utilize a useful utility called [Process Hacker](https://processhacker.sourceforge.io/).

<img width="1000" height="899" alt="image" src="https://github.com/user-attachments/assets/08b0032c-5262-49c1-b621-1dd55ae67749" />

By using Process Hacker, we can observe a range of processes within our environment. Sorting the processes by name, we can identify interesting color-coded distinctions. Notably, "powershell.exe", a managed process, is highlighted in green compared to other processes. Hovering over powershell.exe reveals the label "Process is managed (.NET)," confirming its managed status.

<img width="1000" height="386" alt="image" src="https://github.com/user-attachments/assets/43232646-9655-4cac-8523-8853a7b8dd70" />

Examining the module loads for `powershell.exe`, by right-clicking on `powershell.exe`, clicking "Properties", and navigating to "Modules", we can find relevant information.

<img width="1000" height="63" alt="image" src="https://github.com/user-attachments/assets/dc27d77c-b29e-4682-b75e-5822c3347ee0" />

The presence of "Microsoft .NET Runtime...", `clr.dll`, and `clrjit.dll` should attract our attention. These 2 DLLs are used when C# code is ran as part of the runtime to execute the bytecode. If we observe these DLLs loaded in processes that typically do not require them, it suggests a potential [execute-assembly](https://www.cobaltstrike.com/blog/cobalt-strike-3-11-the-snake-that-eats-its-tail/) or [unmanaged PowerShell injection](https://www.youtube.com/watch?v=7tvfb9poTKg&ab_channel=RaphaelMudge) attack.

To showcase unmanaged PowerShell injection, we can inject an [unmanaged PowerShell-like DLL](https://github.com/leechristensen/UnmanagedPowerShell) into a random process, such as `spoolsv.exe`. We can do that by utilizing the [PSInject project](https://github.com/EmpireProject/PSInject) in the following manner.

```powershell
 powershell -ep bypass
 Import-Module .\Invoke-PSInject.ps1
 Invoke-PSInject -ProcId [Process ID of spoolsv.exe] -PoshCode "V3JpdGUtSG9zdCAiSGVsbG8sIEd1cnU5OSEi"
```

<img width="904" height="390" alt="image" src="https://github.com/user-attachments/assets/60380fb5-1565-449b-9fd7-df7a0cb20f47" />

After the injection, we observe that "spoolsv.exe" transitions from an unmanaged to a managed state.

<img width="742" height="416" alt="image" src="https://github.com/user-attachments/assets/50142c2f-025a-43db-8461-35ab0d579aef" />

Additionally, by referring to both the related "Modules" tab of Process Hacker and Sysmon `Event ID 7`, we can examine the DLL load information to validate the presence of the aforementioned DLLs.

<img width="1000" height="617" alt="image" src="https://github.com/user-attachments/assets/e3c8c80f-6dd7-40f7-8a48-a90e068fe9ae" />

<img width="1000" height="479" alt="image" src="https://github.com/user-attachments/assets/bf8df8b5-9771-4a7c-b5f6-89adbd5f2df9" />

---

## Detection Example 3: Detecting Credential Dumping

Another critical aspect of cybersecurity is detecting credential dumping activities. One widely used tool for credential dumping is [Mimikatz](https://github.com/gentilkiwi/mimikatz), offering various methods for extracting Windows credentials. One specific command, "sekurlsa::logonpasswords", enables the dumping of password hashes or plaintext passwords by accessing the [Local Security Authority Subsystem Service (LSASS)](https://en.wikipedia.org/wiki/Local_Security_Authority_Subsystem_Service). LSASS is responsible for managing user credentials and is a primary target for credential-dumping tools like Mimikatz.

The attack can be executed as follows.

```cmd
C:\Tools\Mimikatz> mimikatz.exe

  .#####.   mimikatz 2.2.0 (x64) #18362 Feb 29 2020 11:13:36
 .## ^ ##.  "A La Vie, A L'Amour" - (oe.eo)
 ## / \ ##  /*** Benjamin DELPY `gentilkiwi` ( benjamin@gentilkiwi.com )
 ## \ / ##       > http://blog.gentilkiwi.com/mimikatz
 '## v ##'       Vincent LE TOUX             ( vincent.letoux@gmail.com )
  '#####'        > http://pingcastle.com / http://mysmartlogon.com   ***/

mimikatz # privilege::debug
Privilege '20' OK

mimikatz # sekurlsa::logonpasswords

Authentication Id : 0 ; 1128191 (00000000:001136ff)
Session           : RemoteInteractive from 2
User Name         : Administrator
Domain            : DESKTOP-NU10MTO
Logon Server      : DESKTOP-NU10MTO
Logon Time        : 5/31/2023 4:14:41 PM
SID               : S-1-5-21-2712802632-2324259492-1677155984-500
        msv :
         [00000003] Primary
         * Username : Administrator
         * Domain   : DESKTOP-NU10MTO
         * NTLM     : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
         * SHA1     : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX0812156b
        tspkg :
        wdigest :
         * Username : Administrator
         * Domain   : DESKTOP-NU10MTO
         * Password : (null)
        kerberos :
         * Username : Administrator
         * Domain   : DESKTOP-NU10MTO
         * Password : (null)
        ssp :   KO
        credman :
```

As we can see, the output of the "sekurlsa::logonpasswords" command provides powerful insights into compromised credentials.

To detect this activity, we can rely on a different Sysmon event. Instead of focusing on DLL loads, we shift our attention to process access events. By checking `Sysmon event ID 10`, which represents "ProcessAccess" events, we can identify any suspicious attempts to access LSASS.

<img width="1000" height="271" alt="image" src="https://github.com/user-attachments/assets/4ca38ea4-8550-456e-ad70-913b70dced7b" />

<img width="1000" height="397" alt="image" src="https://github.com/user-attachments/assets/948b392f-e0ab-490d-8af4-4421951dfab2" />

For instance, if we observe a random file ("AgentEXE" in this case) from a random folder ("Downloads" in this case) attempting to access LSASS, it indicates unusual behavior. Additionally, the `SourceUser` being different from the `TargetUser` (e.g., "waldo" as the `SourceUser` and "SYSTEM" as the `TargetUser`) further emphasizes the abnormality. It's also worth noting that as part of the mimikatz-based credential dumping process, the user must request [SeDebugPrivileges](https://devblogs.microsoft.com/oldnewthing/20080314-00/?p=23113). As the name suggests, it's primarily used for debugging. This can be another Indicator of Compromise (IOC).

Please note that some legitimate processes may access LSASS, such as authentication-related processes or security tools like AV or EDR.

---

