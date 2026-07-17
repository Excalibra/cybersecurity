# Skills Assessment

---

## Dashboard Review & Critical Thinking Exercise

Congratulations,

You have been hired in Eagle as a SOC Tier 1 analyst. Yesterday was your on-boarding day with the company, and today you will be familiarized with the SOC. Your day will begin by meeting up with a senior analyst, who will provide insights into the environment, and afterwards, you are expected to begin monitoring alerts and security events in our home-cooked SOC dashboards.

The following are your notes after meeting the senior analyst, who provided insights into the environment:

- The organization has moved all hosting to the cloud; the old DMZ network is closed down, so no more servers exist there.
- The IT operation team (the core IT admins) consists of four people. They are the only ones with high privileges in the environment.
- The IT operation team often tends to use the default administrator account(s) even if they are told otherwise.
- All endpoint devices are hardened according to CIS hardening baselines. Whitelisting exists to a limited extent.
- IT security has created a privileged admin workstation (PAW) and requires that all admin activities be performed on this machine.
- The Linux environment is primarily 'left over' servers from back in the day, which have very little, if any, activity on a regular day. The root user account is not used; due to audit findings, the account was blocked from connecting remotely, and users who require those rights will need to escalate via the sudo command.
- Naming conventions exist and are strictly followed; for example, service accounts contain '-svc' as part of their name. Service accounts are created with long, complex passwords, and they perform a very specific task (most likely running services locally on machines).

---


Now you are free to take your seat and start monitoring. Navigate to `http://[Target IP]:5601`, click on the side navigation toggle, and click on "Dashboard". Review the `SOC-Alerts` dashboard.

- `Visualization 1: Failed logon attempts (All users)`  
  Such a visualization might reveal potential brute force attacks. It's important to identify any single user with numerous failed attempts or perhaps, various users connecting to (or from) the same endpoint device. However, the current data does not point towards any such scenario. One anomaly is noticeable though. **Hint**: It is related to the "sql-svc1" account.

- `Visualization 2: Failed logon attempts (Disabled user)`  
  It seems that there is one incident where the user "Anni" has tried to authenticate, despite the account being disabled.

- `Visualization 3: Failed logon attempts (Admin users only)`  
  **Hint**: Check if all events took place on either Privileged Access Workstations (PAWs) or Domain Controllers.

- `Visualization 4: RDP logon for service account`  
  Service accounts in this environment serve a very specialized function. Do you notice anything that warrants suspicion?

- `Visualization 5: User added or removed from a local group`  
  An administrator has incorporated an individual (who is only represented by the SID value) into the "Administrators" group. Should you escalate to a Tier 2/3 analyst or consult with the IT Operations department first?

- `Visualization 6: Admin logon not from PAW`  
  Administrators should exclusively utilize PAWs for server remote connections. Should you escalate to a Tier 2/3 analyst or consult with the IT Operations department first?

- `Visualization 7: SSH Logins`  
  Be reminded that the root user account is not typically in use.

