# **Task #5: Detect Anomalies in Linux Auth Logs**

## **Objective**
The objective of this task is to help students analyze **Linux authentication logs** to detect **failed login attempts, privilege escalations, and unauthorized access**. Students will simulate login attempts, extract logs using **Linux commands**, and identify anomalies that indicate potential security threats.

---

## **Lab Setup**
### **Requirements**
- **System:** Linux (Ubuntu 22.04 / Debian / CentOS)  
- **Tools Required:**  
  - **Terminal**
  - **Syslog (Pre-installed)**
  - **grep, awk, cut** (Pre-installed)
  - **Notepad or Excel (for documentation)**  

---

## **Preparation**
### **Step 1: Verify Authentication Logging is Enabled**
Authentication logs are usually stored in `/var/log/auth.log` (Ubuntu/Debian) or `/var/log/secure` (CentOS/RHEL).  
To check if logs are available, run:  
```bash
ls -lh /var/log/auth.log
```

