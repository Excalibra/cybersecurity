# SIEM Visualization Example 1: Failed Logon Attempts (All Users)

Dashboards in SIEM solutions serve as containers for multiple visualizations, allowing us to organize and display data in a meaningful way.

In this and the following sections, we will create a dashboard and some visualizations from scratch.

---

## Developing Our First Dashboard & Visualization


Now, navigate to `http://[Target IP]:5601`, click on the side navigation toggle, and click on "Dashboard".

Delete the existing "SOC-Alerts" dashboard as follows.

<img width="1337" height="559" alt="image" src="https://github.com/user-attachments/assets/64a8be6e-f27f-4a22-a4e0-9877b6bcab97" />


When visiting the Dashboard page again we will be presented with a message indicating that no dashboards currently exist. Additionally, there will be an option available to create a new Dashboard and its first visualization. To initiate the creation of our first dashboard, we simply have to click on the "Create new dashboard" button.

<img width="1913" height="1169" alt="image" src="https://github.com/user-attachments/assets/692a630a-6321-4e53-9114-1c6966859c8f" />


Now, to initiate the creation of our first visualization, we simply have to click on the "Create visualization" button.

<img width="1096" height="928" alt="image" src="https://github.com/user-attachments/assets/26498c74-ef65-45e5-828e-5fa0db50d47b" />


Upon initiating the creation of our first visualization, the following new window will appear with various options and settings.

Before proceeding with any configuration, it is important for us to first click on the calendar icon to open the time picker. Then, we need to specify the date range as "last 15 years". Finally, we can click on the "Apply" button to apply the specified date range to the data.

<img width="1030" height="638" alt="image" src="https://github.com/user-attachments/assets/3a5b68db-5c0e-4b5b-8771-a64cc3ed22d7" />


There are four things for us to notice on this window:

1. A filter option that allows us to filter the data before creating a graph. For example, if our goal is to display failed logon attempts, we can use a filter to only consider event IDs that match `4625 – Failed logon attempt on a Windows system`. The following image demonstrates how we can specify such a filter.
   <img width="1029" height="637" alt="image" src="https://github.com/user-attachments/assets/05fb3284-0084-4267-b80c-e7de1ee9c263" />

2. This field indicates the data set (index) that we are going to use. It is common for data from various infrastructure sources to be separated into different indices, such as network, Windows, Linux, etc. In this particular example, we will specify `windows*` in the "Index pattern".

3. This search bar provides us with the ability to double-check the existence of a specific field within our data set, serving as another way to ensure that we are looking at the correct data. For example, let's say we are interested in the `user.name.keyword` field. We can use the search bar to quickly perform a search and verify if this field is present and discovered within our selected data set. This allows us to confirm that we are accessing the desired field and working with accurate data.
   <img width="460" height="1043" alt="image" src="https://github.com/user-attachments/assets/4dcbf54a-63a7-40d1-9c3c-4bb8af1b6669" />

   "Why `user.name.keyword` and not `user.name`?", you may ask. We should use the `.keyword` field when it comes to aggregations. Please refer to this [stackoverflow question](https://stackoverflow.com/questions/48869795/difference-between-a-field-and-the-field-keyword) for a more elaborate answer.

4. Lastly, this drop-down menu enables us to select the type of visualization we want to create. The default option displayed in the earlier image is "Bar vertical stacked". If we click on that button, it will reveal additional available options (image redacted as not all options fit on the screen). From this expanded list, we can choose the desired visualization type that best suits our requirements and data presentation needs.
   <img width="1030" height="793" alt="image" src="https://github.com/user-attachments/assets/40e11265-061f-4f87-8039-e92d016eabcc" />

---

For this visualization, let's select the "Table" option. After selecting the "Table", we can proceed to click on the "Rows" option. This will allow us to choose the specific data elements that we want to include in the table view.

<img width="711" height="712" alt="image" src="https://github.com/user-attachments/assets/78c8bcbe-7c39-443b-9225-529675ff971d" />

Let's configure the "Rows" settings as follows.

<img width="728" height="935" alt="image" src="https://github.com/user-attachments/assets/12cc8cac-de3b-4c84-b07c-07722e794607" />

**Note**: You will notice `Rank by Alphabetical` and not `Rank by Count of records` like in the screenshot above. This is OK. By the time you perform the next configuration below, `Count of records` will become available.

Moving forward, let's close the "Rows" window and proceed to enter the "Metrics" configuration.

<img width="703" height="839" alt="image" src="https://github.com/user-attachments/assets/63ff063b-e338-4f1b-8ad7-faffe16898c1" />

In the "Metrics" window, let's select "count" as the desired metric.

<img width="606" height="554" alt="image" src="https://github.com/user-attachments/assets/0775e972-6d70-4ff2-b527-52fe8390025d" />

As soon as we select "Count" as the metric, we will observe that the table gets populated with data (assuming that there are events present in the selected data set)

<img width="1029" height="504" alt="image" src="https://github.com/user-attachments/assets/afb36c58-3ee5-4ab2-8727-d9042b2bb22d" />


One final addition to the table is to include another "Rows" setting to show the machine where the failed logon attempt occurred. To do this, we will select the `host.hostname.keyword` field, which represents the computer reporting the failed logon attempt. This will allow us to display the hostname or machine name alongside the count of failed logon attempts, as shown in the image.

<img width="1033" height="398" alt="image" src="https://github.com/user-attachments/assets/dd40831c-c39a-4b1f-9329-125cb4f34e24" />


Now we can see three columns in the table, which contain the following information:

1. The username of the individuals logging in (Note: It currently displays both users and computers. Ideally, a filter should be implemented to exclude computer devices and only display users).
2. The machine on which the logon attempt occurred.
3. The number of times the event has occurred (based on the specified time frame or the entire data set, depending on the settings).

Finally, click on "Save and return", and you will observe that the new visualization is added to the dashboard, appearing as shown in the following image.

<img width="1030" height="761" alt="image" src="https://github.com/user-attachments/assets/f360527c-7a7f-49e8-953e-ae6ae9a46d23" />


Let's not forget to save the dashboard as well. We can do so by simply clicking on the "Save" button.

<img width="1917" height="1053" alt="image" src="https://github.com/user-attachments/assets/3dea55c0-ff67-49fd-81a8-7957b9217c1b" />


---

## Refining The Visualization

Suppose the SOC Manager suggested the following refinements:

- Clearer column names should be specified in the visualization
- The Logon Type should be included in the visualization
- The results in the visualization should be sorted
- The DESKTOP-DPOESND, WIN-OK9BH1BCKSD, and WIN-RMMGJA7T9TC usernames should not be monitored
- [Computer accounts](https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/service-accounts-computer) should not be monitored (not a good practice)

Let's refine the visualization we created, so that it fulfills the suggestions above.

Navigate to `http://[Target IP]:5601`, click on the side navigation toggle, and click on "Dashboard".

The dashboard we previously created should be visible. Let's click on the "pencil"/edit icon.

<img width="1888" height="652" alt="image" src="https://github.com/user-attachments/assets/165d5733-b528-446f-a8c7-865447746508" />


Let's now click on the "gear" button at the upper-right corner of our visualization, and then click on "Edit lens".

<img width="1913" height="985" alt="image" src="https://github.com/user-attachments/assets/3c0de2a0-ec91-4a47-8ed1-b8d64a529514" />


"Top values of user.name.keyword" should be changed as follows.

<img width="433" height="873" alt="image" src="https://github.com/user-attachments/assets/001b7d8e-cf71-4b68-b076-2eaa21dafe47" />

<img width="476" height="801" alt="image" src="https://github.com/user-attachments/assets/8b7e675c-c465-4cf9-ba68-47d7826298c2" />

"Top values of host.hostname.keyword" should be changed as follows.

<img width="473" height="789" alt="image" src="https://github.com/user-attachments/assets/17a3516f-af5e-4880-a5f8-8db61d1db055" />


The "Logon Type" can be added as follows (we will use the `winlog.logon.type.keyword` field).

<img width="432" height="842" alt="image" src="https://github.com/user-attachments/assets/34977029-287e-4396-874b-3ba538646e42" />

<img width="456" height="791" alt="image" src="https://github.com/user-attachments/assets/84b1bd72-8cc5-4fea-879d-02998a1559a0" />

"Count of records" should be changed as follows.
<img width="459" height="1062" alt="image" src="https://github.com/user-attachments/assets/c85a6e5b-b51d-4f0f-baa2-fe85e5f84b96" />

We can introduce result sorting as follows.
<img width="1915" height="1196" alt="image" src="https://github.com/user-attachments/assets/c37558cb-4106-41fb-8822-cdcf27e2edce" />


All we have to do now is click on "Save and return".

The DESKTOP-DPOESND, WIN-OK9BH1BCKSD, and WIN-RMMGJA7T9TC usernames can be excluded by specifying additional filters as follows.

<img width="1430" height="1046" alt="image" src="https://github.com/user-attachments/assets/93028065-4731-441d-a505-348578e0a4e5" />


Computer accounts can be excluded by specifying the following KQL query and clicking on the "Update" button.

```shell
NOT user.name: *$ AND winlog.channel.keyword: Security
```

The `AND winlog.channel.keyword: Security` part is to ensure that no unrelated logs are accounted for.

<img width="1919" height="1063" alt="image" src="https://github.com/user-attachments/assets/3098ccce-0009-44e3-9c57-d91cab64dca3" />


This is our visualization after all the refinements we performed.

<img width="1917" height="1071" alt="image" src="https://github.com/user-attachments/assets/bb5d49ef-d1c4-4aa4-80c2-358330d2b405" />


Finally, let's give our visualization a title by clicking on "No Title".

<img width="1917" height="1059" alt="image" src="https://github.com/user-attachments/assets/9c887780-6072-4dfa-9de9-7961146dc3f8" />


Don't forget to click on the "Save" button (the one on the upper-right hand side of the window).

