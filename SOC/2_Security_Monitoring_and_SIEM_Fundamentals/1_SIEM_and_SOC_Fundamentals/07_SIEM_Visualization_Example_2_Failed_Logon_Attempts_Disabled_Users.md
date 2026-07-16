# SIEM Visualization Example 2: Failed Logon Attempts (Disabled Users)

In this SIEM visualization example we want to create visualization to monitor failed login attempts against disabled users.

We mention "failed" because it is not possible to log in with a disabled user, so it will never be successful even if the correct credentials are provided. In a scenario where the correct credentials are provided, the Windows logs will contain an additional SubStatus value of 0xC0000072, that indicates the reason of the failure.

Navigate to the bottom of this section and click on `Click here to spawn the target system!`.

Navigate to `http://[Target IP]:5601`, click on the side navigation toggle, and click on "Dashboard".

A prebaked dashboard should be visible. Let's click on the "pencil"/edit icon.

<img width="1888" height="652" alt="image" src="https://github.com/user-attachments/assets/8a221dc1-5386-414b-beb1-e1c3e901f7cd" />


Now, to initiate the creation of our first visualization, we simply have to click on the "Create visualization" button.

Upon initiating the creation of our first visualization, the following new window will appear with various options and settings.

<img width="1030" height="638" alt="image" src="https://github.com/user-attachments/assets/59c907ee-f50c-4d45-9fda-7a064f5afdf2" />

There are four things for us to notice on this window:

1. A filter option that allows us to filter the data before creating a graph. In this case our goal is to display failed logon attempts against disabled users only. We can use a filter to only consider event IDs that match `4625 – Failed logon attempt on a Windows system`, like we did in the previous visualization example. In this case though, we should also take into account the SubStatus (`winlog.event_data.SubStatus` field) that indicates, when set to 0xC0000072, that the failure is due to a logon with disabled user. The following image demonstrates how we can specify such a filter.
   <img width="1028" height="535" alt="image" src="https://github.com/user-attachments/assets/da0f7f1b-c8dd-4055-8b09-96f89781bfb7" />


2. This field indicates the data set (index) that we are going to use. It is common for data from various infrastructure sources to be separated into different indices, such as network, Windows, Linux, etc. In this particular example, we will specify `windows*` in the "Index pattern".

3. This search bar provides us with the ability to double-check the existence of a specific field within our data set, serving as another way to ensure that we are looking at the correct data. Like in the previous visualization, we are interested in the `user.name.keyword` field. We can use the search bar to quickly perform a search and verify if this field is present and discovered within our selected data set. This allows us to confirm that we are accessing the desired field and working with accurate data.
   <img width="460" height="1043" alt="image" src="https://github.com/user-attachments/assets/bc2844d1-167b-4da2-b579-da9604213524" />


4. Lastly, this drop-down menu enables us to select the type of visualization we want to create. The default option displayed in the earlier image is "Bar vertical stacked". If we click on that button, it will reveal additional available options (image redacted as not all options fit on the screen). From this expanded list, we can choose the desired visualization type that best suits our requirements and data presentation needs.
   <img width="1030" height="793" alt="image" src="https://github.com/user-attachments/assets/a6a84593-5719-4beb-8417-d445d45bcb56" />


---

For this visualization, let's select the "Table" option. After selecting the "Table", we can proceed to click on the "Rows" option. This will allow us to choose the specific data elements that we want to include in the table view.

<img width="711" height="712" alt="image" src="https://github.com/user-attachments/assets/8c2b4b87-594c-4904-a23e-98b697f887b9" />


Let's configure the "Rows" settings as follows.

<img width="728" height="935" alt="image" src="https://github.com/user-attachments/assets/c547c48a-8770-4d98-88b7-819ea3a19ec9" />


Moving forward, let's close the "Rows" window and proceed to enter the "Metrics" configuration.

<img width="703" height="839" alt="image" src="https://github.com/user-attachments/assets/2d64a1e6-0d66-4339-876d-c6bebeca6019" />


In the "Metrics" window, let's select "count" as the desired metric.

<img width="606" height="554" alt="image" src="https://github.com/user-attachments/assets/23bc9609-5dc2-4c10-9de2-f865596b787e" />


One final addition to the table is to include another "Rows" setting to show the machine where the failed logon attempt occurred. To do this, we will select the `host.hostname.keyword` field, which represents the computer reporting the failed logon attempt. This will allow us to display the hostname or machine name alongside the count of failed logon attempts, as shown in the image.

<img width="1027" height="281" alt="image" src="https://github.com/user-attachments/assets/8bcaae6c-2f08-4fd4-800c-4890aa493688" />


Now we can see three columns in the table, which contain the following information:

1. The disabled user whose credentials generated the failed logon attempt event.
2. The machine on which the logon attempt occurred.
3. The number of times the event has occurred (based on the specified time frame or the entire data set, depending on the settings).

Finally, click on "Save and return", and you will observe that the new visualization is added to the dashboard.
