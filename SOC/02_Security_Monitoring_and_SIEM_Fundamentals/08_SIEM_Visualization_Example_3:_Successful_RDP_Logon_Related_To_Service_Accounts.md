# SIEM Visualization Example 3: Successful RDP Logon Related To Service Accounts

In this SIEM visualization example, we aim to create a visualization to monitor successful RDP logons specifically related to service accounts. Service account credentials are never used for RDP logons in corporate/real-world environments. We have been informed by the IT Operations department that all service accounts on the environment start with `svc-`.

The motivation for this visualization stems from the fact that service accounts often possess exceptionally high privileges. We need to keep a close eye on how service accounts are used.

Our visualization will be based on the following Windows event log.

- [4624: An account was successfully logged on](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4624)

Navigate to the bottom of this section and click on `Click here to spawn the target system!`.

Navigate to `http://[Target IP]:5601`, click on the side navigation toggle, and click on "Dashboard".

A prebaked dashboard should be visible. Let's click on the "pencil"/edit icon.

<img width="1888" height="652" alt="image" src="https://github.com/user-attachments/assets/19b88f31-905d-464f-b0f1-36dc4bce09dc" />


Now, to initiate the creation of our first visualization, we simply have to click on the "Create visualization" button.

Upon initiating the creation of our first visualization, the following new window will appear with various options and settings.

<img width="1030" height="638" alt="image" src="https://github.com/user-attachments/assets/59df92bc-f981-4a31-8242-cf59f9e493c7" />


There are five things for us to notice on this window:

1. A filter option that allows us to filter the data before creating a graph. In this case our goal is to display successful RDP logons specifically related to service accounts. We can use a filter to only consider event IDs that match `4624 – An account was successfully logged on`. In this case though, we should also take into account the logon type which should be `RemoteInteractive` (`winlog.logon.type` field). The following images demonstrates how we can specify such filters.
   <img width="1427" height="802" alt="image" src="https://github.com/user-attachments/assets/ca209f17-c78c-4464-96d2-e544281decd6" />

   <img width="1426" height="809" alt="image" src="https://github.com/user-attachments/assets/8aaa7d28-4e4b-4013-80cd-3fa245a42b98" />


2. This field indicates the data set (index) that we are going to use. It is common for data from various infrastructure sources to be separated into different indices, such as network, Windows, Linux, etc. In this particular example, we will specify `windows*` in the "Index pattern".

3. This search bar provides us with the ability to double-check the existence of a specific field within our data set, serving as another way to ensure that we are looking at the correct data. We are interested in the `user.name.keyword` field. We can use the search bar to quickly perform a search and verify if this field is present and discovered within our selected data set. This allows us to confirm that we are accessing the desired field and working with accurate data.
   <img width="460" height="1043" alt="image" src="https://github.com/user-attachments/assets/a379f5c4-febc-4ca8-92aa-9aba123cd9a8" />


4. Lastly, this drop-down menu enables us to select the type of visualization we want to create. The default option displayed in the earlier image is "Bar vertical stacked". If we click on that button, it will reveal additional available options (image redacted as not all options fit on the screen). From this expanded list, we can choose the desired visualization type that best suits our requirements and data presentation needs.
   <img width="1030" height="793" alt="image" src="https://github.com/user-attachments/assets/c310f5a4-4ea7-4d80-b54c-fbbf357e6502" />


---

For this visualization, let's select the "Table" option. After selecting the "Table", we can proceed to click on the "Rows" option. This will allow us to choose the specific data elements that we want to include in the table view.

<img width="711" height="712" alt="image" src="https://github.com/user-attachments/assets/93e54957-a14b-4f46-95f9-205fa5e5c6ab" />


Let's configure the "Rows" settings as follows.

<img width="728" height="935" alt="image" src="https://github.com/user-attachments/assets/fbde304f-e139-4ab3-bd2e-2409a0b0395f" />


Moving forward, let's close the "Rows" window and proceed to enter the "Metrics" configuration.

<img width="703" height="839" alt="image" src="https://github.com/user-attachments/assets/4b64cf55-96d1-4476-8888-878e575178b1" />


In the "Metrics" window, let's select "count" as the desired metric.

<img width="606" height="554" alt="image" src="https://github.com/user-attachments/assets/aa3434fa-4342-4499-bfbb-f9f4aac52977" />


One final addition to the table is to include two more "Rows" settings to show the machine where the successful RDP logon attempt occurred and the machine that initiated the successful RDP logon attempt. To do this, we will select the `host.hostname.keyword` field that represents the computer reporting the successful RDP logon attempt and the `related.ip.keyword` field that represents the IP of the computer initiating the succsessful RDP logon attempt. This will allow us to display the involved machines alongside the count of successful logon attempts, as shown in the image.

<img width="458" height="875" alt="image" src="https://github.com/user-attachments/assets/0c866c89-7e7d-44d7-b966-c660e7a4516d" />

<img width="458" height="821" alt="image" src="https://github.com/user-attachments/assets/b7a85771-7aa3-4eaa-a8ce-d641c7e8f90e" />


As discussed, we want to monitor successful RDP logons specifically related to service accounts, knowing for a fact that all service accounts of the environment start with `svc-`. So, to conclude our visualization we need to specify the following KQL query.

```shell
user.name: svc-*
```

**Note**: As you can see we don't use the `.keyword` field in KQL queries.

<img width="1800" height="1218" alt="image" src="https://github.com/user-attachments/assets/c659ba46-a699-43c9-8700-0d0cb4242239" />


Now we can see four columns in the table, which contain the following information:

1. The service account whose credentials generated the successful RDP logon attempt event.
2. The machine on which the logon attempt occurred.
3. The IP of the machine that initiated the logon attempt.
4. The number of times the event has occurred (based on the specified time frame or the entire data set, depending on the settings).

Finally, click on "Save and return", and you will observe that the new visualization is added to the dashboard.

