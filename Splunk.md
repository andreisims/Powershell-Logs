## Task #4: Use Splunk to Search for Login Attempts
### Objective
The objective of this task is to help users learn how to search and analyze login attempts using Splunk. We will ingest Windows Security logs into Splunk, identify successful and failed login events, and create a basic search query to extract relevant security insights.
## **Preparation**
### Step 1: Install Splunk
1. Download **Splunk Enterprise** from the official website:  
![https://www.splunk.com/en_us/download.html](https://www.splunk.com/en_us/download.html)
![Image](https://github.com/user-attachments/assets/83dde0d0-4659-468b-b1cb-992f50d3a057)
![Image](https://github.com/user-attachments/assets/a1f7439d-e6da-44ad-8a6e-b2dc2ec6d170)
![Image](https://github.com/user-attachments/assets/e7f046f7-9e5e-4776-844a-304436e9d6ad)
2. Install Splunk with the default settings.
3. Open **Splunk Web Interface** (`http://localhost:8000`) and log in.
4. Navigate to **Settings → Add Data → Monitor → Local event Logs → Add All →Next**. 
5. Select **Security Event Logs** to ingest logs into Splunk.
6. Click **Save & Index the data**.

### Step 2: Search for Login Events in Splunk
1. Open Splunk Web Interface.
2. Run the following search query to find all successful login attempts:
```
index=* EventCode=4624 | table _time, User, Source_Network_Address, Logon_Type
```
This filters and displays login attempts with timestamps, usernames, and source IPs.
![Image](https://github.com/user-attachments/assets/4e78a6c2-8dfd-4b8c-ba68-61f918dad5ec)
![Image](https://github.com/user-attachments/assets/0eeb7d22-3cbb-440c-9b94-666d97f32aee)
3. Run the following query to find all failed login attempts:
```
index=* EventCode=4625 | table _time, User, Source_Network_Address, Failure_Reason
```
- This displays failed login attempts, including the reason for failure.
- ![Image](https://github.com/user-attachments/assets/3979fa6d-76cf-4845-817b-c28dfb0173be)
- ![Image](https://github.com/user-attachments/assets/250fd9a5-fcea-4744-8ec2-7ef317b61e01)
- 4. To detect multiple failed login attempts from a single source (potential brute-force attack), use:
```
index=windows_logs EventCode=4625 | stats count by User, Source_Network_Address | where count > 5
```
- This highlights accounts with five or more failed attempts, a possible brute-force attack indicator. (no results)
![Image](https://github.com/user-attachments/assets/d40b0dda-50ef-4eb9-816d-d4e57972e21f)
## Results
<li>✅ Successfully ingested Windows Security logs into Splunk.</li>
<li>✅ Simulated successful and failed login attempts.</li>
<li>✅ Used Splunk queries to extract and analyze login activities.</li>
<li>✅ Learned how SOC analysts detect brute-force attacks using Splunk.</li>
