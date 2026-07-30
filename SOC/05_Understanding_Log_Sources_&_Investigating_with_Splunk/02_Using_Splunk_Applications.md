# Using Splunk Applications

---

## Splunk Applications

Splunk applications, or apps, are packages that we add to our Splunk Enterprise or Splunk Cloud deployments to extend capabilities and manage specific types of operational data. Each application is tailored to handle data from specific technologies or use cases, effectively acting as a pre-built knowledge package for that data. Apps can provide capabilities ranging from custom data inputs, custom visualizations, dashboards, alerts, reports, and more.

Splunk Apps enable the coexistence of multiple workspaces on a single Splunk instance, catering to different use cases and user roles. These ready-made apps can be found on Splunkbase.

As an integral part of our cybersecurity operations, the Splunk apps designed for Security Information and Event Management (SIEM) purposes provide a range of capabilities to enhance our ability to detect, investigate, and respond to threats. They are designed to ingest, analyze, and visualize security-related data, enabling us to detect complex threats and perform in-depth investigations.

When using these apps in our Splunk environment, we need to consider factors such as data volume, hardware requirements, and licensing. Many apps can be resource-intensive, so we must ensure our Splunk deployment is sized correctly to handle the additional workload. Further, it's also important to ensure we have the correct licenses for any premium apps, and that we are aware of the potential for increased license usage due to the added data inputs.

In this segment, we'll be leveraging the `Sysmon App for Splunk` developed by Mike Haag.

To download, add, and use this application, follow the steps delineated below:

1. Sign up for a free account at [splunkbase](https://splunkbase.splunk.com/)
   
   <img width="2091" height="969" alt="image" src="https://github.com/user-attachments/assets/70fece4a-c0d9-428f-a792-2915f147b667" />

2. Once registered, log into your account

3. Head over to the [Sysmon App for Splunk](https://splunkbase.splunk.com/app/3544) page to download the application.
   
   <img width="2085" height="1339" alt="image" src="https://github.com/user-attachments/assets/2c6cbabb-5765-4331-b693-4b557b436f8c" />

4. Add the application as follows to your search head.
   
   <img width="2085" height="727" alt="image" src="https://github.com/user-attachments/assets/2c7b778f-fce9-4a95-9e9c-f9c560d9720b" />

   <img width="2089" height="583" alt="image" src="https://github.com/user-attachments/assets/f6cd4e88-fcba-41fa-a6c2-4e38989f8375" />

   <img width="2087" height="797" alt="image" src="https://github.com/user-attachments/assets/096c90e0-77ff-4c06-90a1-c8442d411462" />

   
5. Adjust the application's [macro](https://docs.splunk.com/Documentation/Splunk/latest/Knowledge/Definesearchmacros) so that events are loaded as follows.
   
   <img width="2155" height="897" alt="image" src="https://github.com/user-attachments/assets/8488b0b5-c5fe-4abb-84fc-dd0656c9effe" />

   <img width="2159" height="517" alt="image" src="https://github.com/user-attachments/assets/2f6a0526-4a72-4c9f-aabb-1aa77ea3a6c6" />

   <img width="2157" height="501" alt="image" src="https://github.com/user-attachments/assets/2d9e718e-bbbc-404a-aa5a-4e24f97ee51d" />

   <img width="2159" height="1053" alt="image" src="https://github.com/user-attachments/assets/e0a59739-515f-4ed3-89c6-837d878eff23" />


Let's access the Sysmon App for Splunk by locating it in the "Apps" column on the Splunk home page and head over to the `File Activity` tab.

<img width="2155" height="1257" alt="image" src="https://github.com/user-attachments/assets/39d9730c-4f3e-4c44-b867-b270112ffe90" />

Let's now specify "All time" on the time picker and click "Submit". Results are generated successfully; however, no results are appearing in the "Top Systems" section.

<img width="2159" height="1743" alt="image" src="https://github.com/user-attachments/assets/b8927048-1481-4285-a48a-fe0411a72320" />

We can fix that by clicking on "Edit" (upper right hand corner of the screen) and editing the search.

<img width="2157" height="1663" alt="image" src="https://github.com/user-attachments/assets/c4e2af77-e700-43ee-896e-63a8fbd566f3" />

The Sysmon Events with ID 11 do not contain a field named `Computer`, but they do include a field called `ComputerName`. Let's fix that and click "Apply"

<img width="2157" height="1477" alt="image" src="https://github.com/user-attachments/assets/12d63348-3156-4639-a2cf-c93cc7686bf7" />

Results should now be generated successfully in the "Top Systems" section.

<img width="2161" height="1645" alt="image" src="https://github.com/user-attachments/assets/e5158f0f-673b-4a39-a51c-8a09b3be598e" />

> Feel free to explore and experiment with this Splunk application. An excellent exercise is to modify the searches when no results are generated due to non-existent fields being specified, continuing until the desired results are obtained.

---
