## Task #3: Extract and Analyze Sysmon Logs for Process Creation  

Objective
<li>The goal of this task is to introduce students to Sysmon (System Monitor) for process tracking and security monitoring. By completing this task, students will learn how to detect malicious process execution, investigate suspicious activity, and analyze Sysmon logs using Event Viewer and PowerShell.</li>

### **Step 1: Install Sysmon**
If Sysmon is not installed, download and install it using the following steps:
i. Download **Sysmon** from Microsoft Sysinternals:  
   [https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon)

   ![Image](https://github.com/user-attachments/assets/dee4db3e-f13e-4043-9d27-27b9464d204d)
ii. Extract the Sysmon ZIP file.  
iii. Open a **Command Prompt (Run as Administrator)** and install Sysmon with basic logging:  
   ```powershell
   sysmon64 -accepteula -i
   ```
   ![Image](https://github.com/user-attachments/assets/ddbe20e0-0a7c-4f77-8fe0-c632391bea61)
iv. Verify installation by checking for Sysmon logs in Event Viewer:
   ```
   Applications and Services Logs → Microsoft → Windows → Sysmon → Operational
   ```
   ![Image](https://github.com/user-attachments/assets/b94b8a9d-ba32-4a7a-a9ee-6f4046e4377a)
## Attack Simulation & Detection Using Sysmon
We will now simulate a suspicious process execution and detect it using Sysmon logs.
### Step 2: Simulate Suspicious Process Execution
1. Open PowerShell (Run as Administrator).
2. Execute a command that mimics an attacker running a new process:
```
Start-Process notepad.exe
```
- This command spawns a new Notepad process, a technique attackers often use to execute malware.
- Sysmon will log this under Event ID 1 (Process Creation).

