# Powershell Logs
This brief tutorial demonstrates how attackers misuse PowerShell for reconnaissance and how SOC teams can detect and track such activities. By default, PowerShell logging is disabled, so the first step is to enable key logging features like Script Block Logging, Module Logging, and Transcription via Group Policy. These logs provide visibility into PowerShell commands and scripts executed on a system. The tutorial simulates an attacker using a PowerShell command (Get-LocalUser) to enumerate local user accounts, a common reconnaissance technique. By enabling and analyzing PowerShell logs, SOC teams can effectively detect malicious activities, integrate logs into SIEM tools for centralized monitoring, and respond to threats proactively.

## Requirements
<li>System: Windows 10/11 or Windows Server 2019/2022</li>
<li>PowerShell (Pre-installed)</li>
<li>Windows Event Viewer</li>
<li>Notepad or Excel (for documentation)</li>

## 1. Environment
<h4>- create VM on Azure or using a virual machine on your desktop</h4>
<li>I'm using Azure and have connected via RDP</li>

![Image](https://github.com/user-attachments/assets/74c50a82-5479-4d6d-b0b9-abd08f6cdce7)
## Enable Logging for PowerShell Execution
<li>Press Win + R to open the Run dialog. Type gpedit.msc and press Enter to open the Group Policy Editor.</li>
<li>or search for group policy and select 'edit group policy'</li>

![Image](https://github.com/user-attachments/assets/7842649e-be13-4b8d-8a40-a526e9da935e)
<li>Navigate to the following path: Computer Configuration > Administrative Templates > Windows Components > Windows PowerShell and turn on the following: Module Logging, Powershell Script Block Logging, Script Execution, Powershell Transcription. hit apply </li>

![Image](https://github.com/user-attachments/assets/ca1e1795-2ed8-4e89-b2de-d9a0768559c5)
## Attack Simulation & Detection Using Powershell
<li>Run the following command in an elevated PowerShell session: Get-LocalUser | Select-Object Name, Enabled</li>
<li>This command lists all local user accounts on the system along with their status (enabled/disabled). Attackers use similar commands post-exploitation to enumerate users before escalating privileges.</li>

![Image](https://github.com/user-attachments/assets/177d028c-6c35-4210-8573-a53bddfa22a4)
## Detect the Attack using Windows Event Viewer
<li>Open Event Viewer (Win + R, type eventvwr.msc, press Enter) or search for event and select 'event viewer'</li>

![Image](https://github.com/user-attachments/assets/6db10b34-bc81-4679-bc2a-6725aef2675d)
<li>in event viewer, Applications and Services Logs → Microsoft → Windows → PowerShell → Operational</li>

![Image](https://github.com/user-attachments/assets/970c4a08-2469-4071-95b2-b3981986381b)
<li>Click Filter Current Log and enter Event ID 4104 (Execute a Remote Command)</li>

![Image](https://github.com/user-attachments/assets/773fe8b5-e68b-4381-a1d8-a91179e7fc9f)

![Image](https://github.com/user-attachments/assets/3d1e4ba2-d62f-4e98-820f-9fcb1db1e610)
## Retrieve Logs using PowerShell (Alternative Detection Method)
<li>Instead of using Event Viewer, use PowerShell to directly extract the event:
Get-WinEvent -LogName "Microsoft-Windows-PowerShell/Operational" | Where-Object {$_.Id -eq 4104} | Select-Object TimeCreated, Message</li>

![Image](https://github.com/user-attachments/assets/14cc6654-00f3-48de-9a69-09df893a9945)
<li>This command fetches all script block executions from PowerShell logs and filters them by Event ID 4104. Look for the command Get-LocalUser in the output</li>

## Conclusion
<li>✅ Successfully simulated an attacker’s reconnaissance technique using PowerShell</li>
<li>✅ Detected the suspicious command execution via Windows Event Viewer and PowerShell log extraction.</li>
<li>✅ Understood how SOC analysts can detect and investigate PowerShell-based attacks in real-world scenarios.</li>

