## Task #2: Identify Failed and Successful Logins

### Step 1: Simulate Login Events
Successful Login:
<li>Lock your machine `(Win + L)` and log in with the correct password.</li>
<li>This will generate a successful login event (Event ID 4624).</li>

![Image](https://github.com/user-attachments/assets/98c088db-cbd6-4348-af6a-e23278bdf5e2)

Failed Login Attempt:
<li>Lock your machine again and try logging in with the wrong password at least three times.</li>
<li>This will generate failed login events (Event ID 4625).</li>

 ![Image](https://github.com/user-attachments/assets/7655ea39-5589-4d0d-ad37-e4067349785b)
 ![Image](https://github.com/user-attachments/assets/841af92e-238b-4082-8271-2bc6c566cd94)

### Step 2: Detect Login Events using Windows Event Viewer
<li>Open Event Viewer (Win + R, type eventvwr.msc, press Enter).</li>
<li>Click Filter Current Log and enter the following Event IDs: 4624 → Successful login, 4625 → Failed login</li>

![Image](https://github.com/user-attachments/assets/a43b64ea-c447-41a4-b4ff-33e1b79ebd4f)
![Image](https://github.com/user-attachments/assets/eb67c335-8161-414f-b680-f07f26385409)

### Step 3: Retrieve Login Events using PowerShell
Check for Successful Logins
<li>Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4624} | Select-Object TimeCreated, Message | Format-Table -AutoSize</li> 

![Image](https://github.com/user-attachments/assets/cb47e48d-69eb-473a-b747-c68288e264ff)

Check for Failed Logins
<li>Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4625} | Select-Object TimeCreated, Message | Format-Table -AutoSize</li> 

![Image](https://github.com/user-attachments/assets/9d6b4e4a-a109-4ebb-a5cd-c3e23c05ddfd)
