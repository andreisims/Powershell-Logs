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

![Image](https://github.com/user-attachments/assets/da926cd1-8d16-47fe-a42f-06c039f19a2b)
- This command spawns a new Notepad process, a technique attackers often use to execute malware.
- Sysmon will log this under Event ID 1 (Process Creation).
### Step 3: Detect Process Execution Using Windows Event Viewer
1. Open Event Viewer (Win + R, type eventvwr.msc, press Enter).
2. Navigate to:
```
Applications and Services Logs → Microsoft → Windows → Sysmon → Operational
```
3. Click Filter Current Log and enter Event ID 1 (Process Creation).

4. ![Image](https://github.com/user-attachments/assets/2f42ba6e-f2c1-4de1-bcbc-db4bbc729613)
### Step 4: Retrieve Sysmon Process Logs Using PowerShell
Instead of using Event Viewer, use PowerShell to extract process execution logs:

**List All Processes Logged by Sysmon**
```
Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational" | Where-Object {$_.Id -eq 1} | Select-Object TimeCreated, Message | Format-Table -AutoSize
```

![Image](https://github.com/user-attachments/assets/68f9c765-975c-4de2-883f-45b48a86c44d)
- This command retrieves all process execution logs recorded by Sysmon.
**Filter for Notepad Execution**
```
Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational" | Where-Object {$_.Message -like "*notepad.exe*"} | Select-Object TimeCreated, Message | Format-Table -AutoSize
```

![Image](https://github.com/user-attachments/assets/8c6c6163-35fb-4d43-b9cc-024cad3c7ad2)
- This command extracts only Notepad execution events, mimicking how SOC analysts filter logs for specific process execution.

**Identify Suspicious Parent-Child Processes**
```
Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational" | Where-Object {$_.Message -like "*powershell.exe*"} | Select-Object TimeCreated, Message | Format-Table -AutoSize
```

![Image](https://github.com/user-attachments/assets/3aeaf720-f408-409f-8635-1ce47bb3cbd3)
- If a suspicious PowerShell script spawns a child process, it might indicate malware execution or persistence mechanisms.

## Results
<li>✅ Successfully installed Sysmon and enabled process tracking.</li>
<li>✅ Simulated a suspicious process execution using PowerShell.</li>
<li>✅ Detected and retrieved logs using Windows Event Viewer and PowerShell.</li>
<li>✅ Understood how SOC analysts can track process execution and identify malicious activity.</li>
