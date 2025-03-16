## Task #3: Extract and Analyze Sysmon Logs for Process Creation  

Objective
<li>The goal of this task is to introduce students to Sysmon (System Monitor) for process tracking and security monitoring. By completing this task, students will learn how to detect malicious process execution, investigate suspicious activity, and analyze Sysmon logs using Event Viewer and PowerShell.</li>

### **Step 1: Install Sysmon**
If Sysmon is not installed, download and install it using the following steps:
1. Download **Sysmon** from Microsoft Sysinternals:  
   [https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon)

   ![Image](https://github.com/user-attachments/assets/dee4db3e-f13e-4043-9d27-27b9464d204d)
3. Extract the Sysmon ZIP file.  
4. Open a **Command Prompt (Run as Administrator)** and install Sysmon with basic logging:  
   ```powershell
   sysmon -accepteula -i
   ```
5. Verify installation by checking for Sysmon logs in Event Viewer:
   ```
   Applications and Services Logs → Microsoft → Windows → Sysmon → Operational
    ```
