## Cheatsheet

| Command / Query | Description |
|-----------------|-------------|
| `event.code:4625` | Filter for Windows failed login attempts (Event ID 4625) |
| `event.code:4625 AND winlog.event_data.SubStatus:0xC0000072` | Filter for failed login attempts against disabled accounts |
| `event.code:4625 AND user.name: admin*` | Filter for failed login attempts where username starts with "admin" |
| `event.code:4625 AND winlog.event_data.SubStatus:0xC0000072 AND @timestamp >= "2023-03-03T00:00:00.000Z" AND @timestamp <= "2023-03-06T23:59:59.999Z"` | Filter for failed login attempts against disabled accounts within specific time window (March 3-6, 2023) |
| `event.code:4624` | Filter for successful Windows login events (Event ID 4624) |
| `event.code:4732` | Filter for user additions to security-enabled local groups (Event ID 4732) |
| `event.code:4733` | Filter for user removals from security-enabled local groups (Event ID 4733) |
| `event.code:4732 OR event.code:4733` | Filter for both user additions and removals from local groups |
| `(event.code:4732 OR event.code:4733) AND group.name:administrators` | Filter for additions/removals to/from local Administrators group |
| `NOT user.name: *$` | Exclude computer accounts (accounts ending with $) from results |
| `NOT user.name: *$ AND winlog.channel.keyword: Security` | Exclude computer accounts and filter only Windows Security channel logs |
| `user.name: svc-*` | Search for all service accounts (starting with "svc-") |
| `"svc-sql1"` | Free text search across all indexed fields for the string "svc-sql1" |
| `process.name:MSBuild.exe` | Filter for MSBuild.exe process execution events |
| `process.name:MSBuild.exe AND process.parent.name:(excel.exe OR winword.exe)` | Detect MSBuild started by Office applications (potential Living-off-the-land binary abuse) |
| `user.name.keyword` | Field reference - username (use .keyword for aggregations/exact match) |
| `user.name` | Field reference - username (use without .keyword for wildcard searches in KQL) |
| `host.hostname.keyword` | Field reference - hostname of the machine generating the log |
| `host.name.keyword` | Field reference - name of the host |
| `related.ip.keyword` | Field reference - related IP addresses in the event |
| `winlog.event_data.SubStatus` | Field reference - Windows event substatus code (0xC0000072 = disabled account) |
| `winlog.event_data.MemberSid.keyword` | Field reference - Security Identifier of group member |
| `winlog.logon.type.keyword` | Field reference - Windows logon type |
| `event.action.keyword` | Field reference - action that occurred |
| `group.name.keyword` | Field reference - name of the group |
| `process.name.keyword` | Field reference - name of the process (use .keyword for aggregations) |
| `process.name` | Field reference - name of the process (use without .keyword in KQL queries) |
| `process.parent.name.keyword` | Field reference - name of the parent process (use .keyword for aggregations) |
| `process.parent.name` | Field reference - name of the parent process (use without .keyword in KQL queries) |
| `@timestamp` | Field reference - timestamp extracted from the original event |
| `event.created` | Field reference - timestamp when event was created in Elasticsearch |
| `event.code` | Field reference - event code/ID (ECS standardized field) |
| `winlog.event_id` | Field reference - Windows event ID (Winlogbeat native field) |
| `winlog.channel.keyword` | Field reference - Windows event log channel (e.g., Security) |
