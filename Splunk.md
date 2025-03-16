## Task #4: Use Splunk to Search for Login Attempts
### Objective
The objective of this task is to help users learn how to search and analyze login attempts using Splunk. We will ingest Windows Security logs into Splunk, identify successful and failed login events, and create a basic search query to extract relevant security insights.
## **Preparation**
### **Step 1: Install Splunk**
1. Download **Splunk Enterprise** from the official website:  
   [https://www.splunk.com/en_us/download.html](https://www.splunk.com/en_us/download.html)

![Image](https://github.com/user-attachments/assets/83dde0d0-4659-468b-b1cb-992f50d3a057)
![Image](https://github.com/user-attachments/assets/a1f7439d-e6da-44ad-8a6e-b2dc2ec6d170)
![Image](https://github.com/user-attachments/assets/e7f046f7-9e5e-4776-844a-304436e9d6ad)
3. Install Splunk with the default settings.
4. Open **Splunk Web Interface** (`http://localhost:8000`) and log in.
5. Navigate to **Settings → Add Data → Monitor Windows Logs**. (Settings>add data>monitor>>local event logs >add all>.and next)
6. Select **Security Event Logs** to ingest logs into Splunk.
7. Click **Save & Index the data**.
### Step 2: Search for Login Events in Splunk
1. Open Splunk Web Interface.
2. Run the following search query to find all successful login attempts:
```
index=* EventCode=4624 | table _time, User, Source_Network_Address, Logon_Type
```
This filters and displays login attempts with timestamps, usernames, and source IPs.
![Image](https://github.com/user-attachments/assets/4e78a6c2-8dfd-4b8c-ba68-61f918dad5ec)
![Image](https://github.com/user-attachments/assets/0eeb7d22-3cbb-440c-9b94-666d97f32aee)
