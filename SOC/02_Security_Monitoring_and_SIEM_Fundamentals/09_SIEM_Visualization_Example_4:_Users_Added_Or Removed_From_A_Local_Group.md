# SIEM Visualization Example 4: Users Added Or Removed From A Local Group (Within A Specific Timeframe)

In this SIEM visualization example, we aim to create a visualization to monitor user additions or removals from the local "Administrators" group from March 5th 2023 to date.

Our visualization will be based on the following Windows event logs.

- [4732: A member was added to a security-enabled local group](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4732)
- [4733: A member was removed from a security-enabled local group](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4733)

Navigate to the bottom of this section and click on `Click here to spawn the target system!`.

Navigate to `http://[Target IP]:5601`, click on the side navigation toggle, and click on "Dashboard".

A prebaked dashboard should be visible. Let's click on the "pencil"/edit icon.

<img width="1888" height="652" alt="image" src="https://github.com/user-attachments/assets/2c71167c-8e66-47e6-85c1-ac5a556211a8" />


Now, to initiate the creation of our first visualization, we simply have to click on the "Create visualization" button.

Upon initiating the creation of our first visualization, the following new window will appear with various options and settings.

<img width="1030" height="638" alt="image" src="https://github.com/user-attachments/assets/cf182a55-f4d5-42ca-b11f-180a4803ee74" />


There are four things for us to notice on this window:

1. A filter option that allows us to filter the data before creating a graph. In this case our goal is to display user additions or removals from the local "Administrators" group. We can use a filter to only consider event IDs that match `4732 – A member was added to a security-enabled local group` and `4733 – A member was removed from a security-enabled local group`. We can also use a filter to only consider 4732 and 4733 events where the local group is the "Administrators" one.
   <img width="1030" height="473" alt="image" src="https://github.com/user-attachments/assets/04ef06cc-8946-49e4-b1b5-e7c31cd46152" />


2. This field indicates the data set (index) that we are going to use. It is common for data from various infrastructure sources to be separated into different indices, such as network, Windows, Linux, etc. In this particular example, we will specify `windows*` in the "Index pattern".

3. This search bar provides us with the ability to double-check the existence of a specific field within our data set, serving as another way to ensure that we are looking at the correct data. We are interested in the `user.name.keyword` field. We can use the search bar to quickly perform a search and verify if this field is present and discovered within our selected data set. This allows us to confirm that we are accessing the desired field and working with accurate data.
   <img width="460" height="1043" alt="image" src="https://github.com/user-attachments/assets/8baff8db-99a5-417b-935b-1638c670f0d3" />


4. Lastly, this drop-down menu enables us to select the type of visualization we want to create. The default option displayed in the earlier image is "Bar vertical stacked". If we click on that button, it will reveal additional available options (image redacted as not all options fit on the screen). From this expanded list, we can choose the desired visualization type that best suits our requirements and data presentation needs.
   <img width="1030" height="793" alt="image" src="https://github.com/user-attachments/assets/21720a23-fe18-4ff2-8659-f179b5064de6" />


---

For this visualization, let's select the "Table" option. After selecting the "Table", we can proceed to click on the "Rows" option. This will allow us to choose the specific data elements that we want to include in the table view.

<img width="711" height="712" alt="image" src="https://github.com/user-attachments/assets/5eb5bd2c-78d5-4c5f-8218-54459e6325aa" />


Let's configure the "Rows" settings as follows.

<img width="728" height="935" alt="image" src="https://github.com/user-attachments/assets/9f9f1606-cb6c-425d-8c57-236fbbc27e97" />


Moving forward, let's close the "Rows" window and proceed to enter the "Metrics" configuration.

<img width="703" height="839" alt="image" src="https://github.com/user-attachments/assets/65a427b1-7149-43e9-913d-38f438844ee0" />


In the "Metrics" window, let's select "count" as the desired metric.

<img width="606" height="554" alt="image" src="https://github.com/user-attachments/assets/aab8d3a5-9a27-4244-ae68-1ff33fce0baf" />


One final addition to the table is to include some more "Rows" settings to enhance our understanding.

- Which user was added to or removed from the group? (`winlog.event_data.MemberSid.keyword` field)
- To which group was the addition or the removal performed? (double-checking that it is the "Administrators" one) (`group.name.keyword` field)
- Was the user added to or removed from the group? (`event.action.keyword` field)
- On which machine did the action occur? (`host.name.keyword` field)
  <img width="1169" height="332" alt="image" src="https://github.com/user-attachments/assets/fb3e4bc6-e2c0-48ab-b67b-6bf30c00df18" />


Click on "Save and return", and you will observe that the new visualization is added to the dashboard.

As discussed, we want to monitor user additions or removals from the local "Administrators" group *within a specific timeframe (March 5th 2023 to date)*.

We can narrow the scope of our visualization as follows.

<img width="1917" height="1413" alt="image" src="https://github.com/user-attachments/assets/7675ca25-03b5-422d-8b9c-e70d7bc290bf" />


<img width="1921" height="1409" alt="image" src="https://github.com/user-attachments/assets/5eccfe84-702f-410c-ba76-9ed60c199891" />


<img width="1923" height="1403" alt="image" src="https://github.com/user-attachments/assets/1dd7f0d0-898e-44e6-ac45-f285bf38b90f" />


Finally, let's click on the "Save" button so that all our edits persist.
