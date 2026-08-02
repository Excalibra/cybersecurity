# Detecting Attacker Behavior With Splunk Based On Analytics

As previously mentioned, the second approach leans heavily on statistical analysis and anomaly detection to identify abnormal behavior. By profiling `normal` behavior and identifying deviations from this baseline, we can uncover suspicious activities that may signify an intrusion. These statistical detection models, although driven by data, are invariably shaped by the broader understanding of attacker techniques, tactics, and procedures (TTPs).

A good example of this approach in Splunk is the use of the `streamstats` command. This command allows us to perform real-time analytics on the data, which can be useful for identifying unusual patterns or trends.

Consider a scenario where we are monitoring the number of network connections initiated by a process within a certain time frame.

```shellsession
index="main" sourcetype="WinEventLog:Sysmon" EventCode=3 | bin _time span=1h | stats count as NetworkConnections by _time, Image | streamstats time_window=24h avg(NetworkConnections) as avg stdev(NetworkConnections) as stdev by Image | eval isOutlier=if(NetworkConnections > (avg + (0.5*stdev)), 1, 0) | search isOutlier=1
```

In this search:

- We start by focusing on network connection events (`EventCode=3`), and then group these events into hourly intervals (`bin` can be seen as a `bucket` alias). For each unique process image (`Image`), we calculate the number of network connection events per time bucket.
- We then use the `streamstats` command to calculate a rolling average and standard deviation of the number of network connections over a 24-hour period for each unique process image. This gives us a dynamic baseline to compare each data point to.
- The `eval` command is then used to create a new field, `isOutlier`, and assigns it a value of `1` for any event where the number of network connections is more than 0.5 standard deviations away from the average. This labels these events as statistically anomalous and potentially indicative of suspicious activity.
- Lastly, the `search` command filters our results to only include the outliers, i.e., the events where `isOutlier` equals `1`.

By monitoring for anomalies in network connections initiated by processes, we can detect potentially malicious activities such as command-and-control communication or data exfiltration attempts. However, as with any anomaly detection method, it's important to remember that it may yield false positives and should be calibrated according to the specifics of your environment.

<img width="1423" height="1377" alt="image" src="https://github.com/user-attachments/assets/a14bc4bd-9310-483a-8958-ea88b023b79f" />


Upon closer examination of the results, we observe the presence of numerous suspicious processes that were previously identified, although not all of them are evident.

## Crafting SPL Searches Based On Analytics

Below are some more detection examples that follow this approach.

1. **Example: Detection Of Abnormally Long Commands**

    Attackers frequently employ excessively long commands as part of their operations to accomplish their objectives.

    ```shellsession
    index="main" sourcetype="WinEventLog:Sysmon" Image=*cmd.exe | eval len=len(CommandLine) | table User, len, CommandLine | sort - len
    ```

    After reviewing the results, we notice some benign activity that can be filtered out to reduce noise. Let's apply the following modifications to the search.

    ```shellsession
    index="main" sourcetype="WinEventLog:Sysmon" Image=*cmd.exe ParentImage!="*msiexec.exe" ParentImage!="*explorer.exe" | eval len=len(CommandLine) | table User, len, CommandLine | sort - len
    ```

    <img width="1933" height="963" alt="image" src="https://github.com/user-attachments/assets/e8f9fed2-de8f-4227-907a-2b6dceb901bc" />


    Once again, we observe the recurrence of malicious activity that we previously identified during our investigation.

2. **Example: Detection Of Abnormal cmd.exe Activity**

    The following search identifies unusual `cmd.exe` activity within a certain time range. It uses the `bucket` command to group events by hour, calculates the `count`, `average`, and `standard deviation` of `cmd.exe` executions, and flags outliers.

    ```shellsession
    index="main" EventCode=1 (CommandLine="*cmd.exe*") | bucket _time span=1h | stats count as cmdCount by _time User CommandLine | eventstats avg(cmdCount) as avg stdev(cmdCount) as stdev | eval isOutlier=if(cmdCount > avg+1.5*stdev, 1, 0) | search isOutlier=1
    ```

    <img width="1425" height="1413" alt="image" src="https://github.com/user-attachments/assets/834276a1-3763-4edc-a91c-6313a0115b21" />


    Upon closer examination of the results, we observe the presence of suspicious commands that were previously identified, although not all of them are evident.

3. **Example: Detection Of Processes Loading A High Number Of DLLs In A Specific Time**

    It is not uncommon for malware to load multiple DLLs in rapid succession. The following SPL can assist in monitoring this behavior.

    ```shellsession
    index="main" EventCode=7 | bucket _time span=1h | stats dc(ImageLoaded) as unique_dlls_loaded by _time, Image | where unique_dlls_loaded > 3 | stats count by Image, unique_dlls_loaded
    ```

    After reviewing the results, we notice some benign activity that can be filtered out to reduce noise. Let's apply the following modifications to the search.

    ```shellsession
    index="main" EventCode=7 NOT (Image="C:\\Windows\\System32*") NOT (Image="C:\\Program Files (x86)*") NOT (Image="C:\\Program Files*") NOT (Image="C:\\ProgramData*") NOT (Image="C:\\Users\\waldo\\AppData*")| bucket _time span=1h | stats dc(ImageLoaded) as unique_dlls_loaded by _time, Image | where unique_dlls_loaded > 3 | stats count by Image, unique_dlls_loaded | sort - unique_dlls_loaded
    ```

    - `index="main" EventCode=7 NOT (Image="C:\\Windows\\System32*") NOT (Image="C:\\Program Files (x86)*") NOT (Image="C:\\Program Files*") NOT (Image="C:\\ProgramData*") NOT (Image="C:\\Users\\waldo\\AppData*")`: This part of the query is responsible for fetching all the events from the `main` index where `EventCode` is `7` (Image loaded events in Sysmon logs). The `NOT` filters are excluding events from known benign paths (like "Windows\System32", "Program Files", "ProgramData", and a specific user's "AppData" directory).
    - `| bucket _time span=1h`: This command is used to group the events into time buckets of one hour duration. This is used to analyze the data in hourly intervals.
    - `| stats dc(ImageLoaded) as unique_dlls_loaded by _time, Image`: The `stats` command is used to perform statistical operations on the events. Here, `dc(ImageLoaded)` calculates the distinct count of DLLs loaded (`ImageLoaded`) for each process image (`Image`) in each one-hour time bucket.
    - `| where unique_dlls_loaded > 3`: This filter excludes the results where the number of unique DLLs loaded by a process within an hour is `3 or less`. This is based on the assumption that legitimate software usually loads DLLs at a moderate rate, whereas malware might rapidly load many different DLLs.
    - `| stats count by Image, unique_dlls_loaded`: This command calculates the number of times each process (`Image`) has loaded `more than 3 unique DLLs` in an hour.
    - `| sort - unique_dlls_loaded`: Finally, this command sorts the results in descending order based on the number of unique DLLs loaded (`unique_dlls_loaded`).

    <img width="1943" height="1343" alt="image" src="https://github.com/user-attachments/assets/a6b1686a-6c7b-4fb6-80ea-6e22607fe27b" />


    Upon closer examination of the results, we observe the presence of suspicious processes that were previously identified, although not all of them are evident.

    It's important to note that this behavior can also be exhibited by legitimate software in numerous cases, so context and additional investigation would be necessary to confirm malicious activity.

4. **Example: Detection Of Transactions Where The Same Process Has Been Created More Than Once On The Same Computer**

    We want to correlate events where the same process (`Image`) is executed on the same computer (`ComputerName`) since this might indicate abnormalities depending on the nature of the processes involved. As always, context and additional investigation would be necessary to confirm if it's truly malicious or just a benign occurrence. The following SPL can assist in monitoring this behavior.

    ```shellsession
    index="main" sourcetype="WinEventLog:Sysmon" EventCode=1 | transaction ComputerName, Image | where mvcount(ProcessGuid) > 1 | stats count by Image, ParentImage
    ```

    - `index="main" sourcetype="WinEventLog:Sysmon" EventCode=1`: This part of the query fetches all the Sysmon process creation events (`EventCode=1`) from the `main` index. Sysmon event code 1 represents a process creation event, which includes details such as the process that was started, its command line arguments, the user that started it, and the process that it was started from.
    - `| transaction ComputerName, Image`: The transaction command is used to group related events together based on shared field values. In this case, events are being grouped together if they share the same `ComputerName` and `Image` values. This can help to link together all the process creation events associated with a specific program on a specific computer.
    - `| where mvcount(ProcessGuid) > 1`: This command filters the results to only include transactions where more than one unique process GUID (`ProcessGuid`) is associated with the same program image (`Image`) on the same computer (`ComputerName`). This would typically represent instances where the same program was started more than once.
    - `| stats count by Image, ParentImage`: Finally, this stats command is used to count the number of such instances by the program image (`Image`) and its parent process image (`ParentImage`).

    <img width="1943" height="1365" alt="image" src="https://github.com/user-attachments/assets/ba455b6f-0fc3-4b70-b00e-8fc43c0a0b42" />


    Let's dive deeper into the relationship between `rundll32.exe` and `svchost.exe` (since this pair has the highest `count` number).

    ```shellsession
    index="main" sourcetype="WinEventLog:Sysmon" EventCode=1  | transaction ComputerName, Image  | where mvcount(ProcessGuid) > 1 | search Image="C:\\Windows\\System32\\rundll32.exe" ParentImage="C:\\Windows\\System32\\svchost.exe" | table CommandLine, ParentCommandLine
    ```

    <img width="1891" height="1525" alt="image" src="https://github.com/user-attachments/assets/677d68a9-07e9-4bca-be21-10005689c107" />


    After careful scrutiny of the results, it becomes apparent that we not only identify the presence of previously identified suspicious commands but also new ones.

---

> By establishing a profile of "normal" behavior and utilizing a statistical model to identify deviations from a baseline, we could have detected the compromise of our environment more rapidly, especially with a thorough understanding of attacker tactics, techniques, and procedures (TTPs). However, it is important to acknowledge that relying solely on this approach when crafting queries is inadequate.

---
