# 📊 Splunk Dashboard for SSH Login Monitoring

## 📌 Project Overview
This project demonstrates how to **create a Splunk Dashboard to monitor SSH login attempts**, detect failed logins, identify top users, and analyze potential **brute-force attacks**.

---

## 🛠 Technology Stack
- **Operating System:** Ubuntu 22.04
- **SIEM Tool:** Splunk Enterprise
- **Log Forwarding Tool:** Splunk Universal Forwarder
- **Authentication Logs:** `/var/log/auth.log`

---

## 📥 Steps to Create an SSH Login Monitoring Dashboard in Splunk

### **Step 1: Access the Splunk Web Interface**
Open a browser and go to:

http://<splunk-server-ip>:8000


Log in with **admin credentials**.

---

### **Step 2: Create a New Dashboard**
1️⃣ Navigate to **Dashboards** → Click **Create New Dashboard**.  
2️⃣ Name the dashboard: **SSH Login Monitoring**.  
3️⃣ Select **Private** or **Shared** (if needed).  
4️⃣ Click **Create Dashboard**.

---

### **Step 3: Add Panels for SSH Monitoring**

#### **🔹 Panel 1: Total SSH Login Attempts (Success & Failed)**
Click **Add Panel** → **New Search** and enter:

```splunk
index=main sourcetype=ssh_logs ("Failed password" OR "Accepted password") 
| stats count by message

✅ Panel Name: Total SSH Login Attempts


🔹 Panel 2: SSH Successful vs. Failed Logins (Timechart)
Click Add Panel → New Search and enter:
index=main sourcetype=ssh_logs ("Failed password" OR "Accepted password") 
| timechart span=5m count by message
✅ Panel Name: SSH Login Trends


🔹 Panel 3: Top SSH Users by Login Attempts
Click Add Panel → New Search and enter:
index=main sourcetype=ssh_logs ("Failed password" OR "Accepted password") 
| stats count by user 
| sort -count
✅ Panel Name: Top SSH Users by Login Attempts



🔹 Panel 4: Top Brute Force Attackers (IPs with Most Failed Logins)
Click Add Panel → New Search and enter:
index=main sourcetype=ssh_logs "Failed password" 
| stats count by src_ip 
| sort -count
✅ Panel Name: Top Brute Force Attackers


🔹 Panel 5: Users with Most Failed Logins
Click Add Panel → New Search and enter:
index=main sourcetype=ssh_logs "Failed password" 
| stats count by user 
| sort -count
✅ Panel Name: Top Users with Failed Logins



Step 4: Save and View the Dashboard
Click Save on the dashboard.
Open the dashboard to view real-time SSH login monitoring.


📸 Screenshots
SSH Login Monitoring Dashboard

Timechart of SSH Login Trends

Top SSH Users by Login Attempts

Top Brute Force IPs & Users with Most Failed Logins


🎯 Key Learnings
✔ Hands-on experience with SIEM log analysis & dashboard creation.
✔ Detecting brute-force attacks in Splunk.
✔ Visualizing security trends in a real-time dashboard.
✔ Creating custom Splunk search queries for security monitoring.
