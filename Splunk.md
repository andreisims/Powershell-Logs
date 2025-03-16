## Task #4: Use Splunk to Search for Login Attempts
### Objective
The objective of this task is to help users learn how to search and analyze login attempts using Splunk. We will ingest Windows Security logs into Splunk, identify successful and failed login events, and create a basic search query to extract relevant security insights.
## **Preparation**
### **Step 1: Install Splunk**
1. Download **Splunk Enterprise** from the official website:  
   [https://www.splunk.com/en_us/download.html](https://www.splunk.com/en_us/download.html)
2. Install Splunk with the default settings.
3. Open **Splunk Web Interface** (`http://localhost:8000`) and log in.
4. Navigate to **Settings → Add Data → Monitor Windows Logs**.
5. Select **Security Event Logs** to ingest logs into Splunk.
6. Click **Save & Index the data**.
