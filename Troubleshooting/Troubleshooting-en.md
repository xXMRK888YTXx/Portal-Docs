# Portal Troubleshooting Guide

This guide provides solutions for common issues encountered while using **Portal**.

---

## 🛰 Network & Connectivity Issues

### 1. Port Availability (Port 29170)
Portal uses port **29170** for communication. If another application is already using this port, Portal will not be able to start its network services.

#### Step A: Identify if the port is busy
1. Open **Command Prompt (CMD)** as Administrator.
2. Type the following command and press Enter:
   `netstat -ano | findstr :29170`
3. If the port is busy, you will see a line like this:
   `TCP    0.0.0.0:29170    0.0.0.0:0    LISTENING    1234`
   *(Where **1234** is the PID - Process ID)*.

#### Step B: Identify the Program Name
Once you have the PID, you can find the program name using one of these methods:

* **Method 1 (Command Prompt):**
  Run this command (replace `1234` with your actual PID):
  `tasklist /fi "pid eq 1234"`
* **Method 2 (Task Manager):**
    1. Press `Ctrl + Shift + Esc`.
    2. Go to the **Details** tab.
    3. Find the **PID** column and look for your number to see which `.exe` is holding the port.

**Solution:** Close the conflicting application or end the process in Task Manager.

---

### 2. Windows Firewall Blocking
The Windows Defender Firewall may block incoming connections (WiFi/WebSockets) from your mobile device.

#### Solution: Add an Inbound Rule
1. Press `Win + R`, type `control firewall.cpl` and hit **Enter**.
2. Click on **Advanced settings** on the left sidebar.
3. Select **Inbound Rules** in the left pane and click **New Rule...** in the right pane.
4. **Rule Type:** Select `Program` and click **Next**.
5. **Program Path:** Browse and select the `Portal` executable file and click **Next**.
6. **Action:** Select `Allow the connection` and click **Next**.
7. **Profile:** Ensure **Domain**, **Private**, and **Public** are all checked and click **Next**.
8. **Name:** Enter `Portal_Access_Rule` and click **Finish**.

---

### 3. Third-Party Antivirus & Firewalls
If you are using third-party security software (**Kaspersky, Avast, ESET, Norton, etc.**), the standard Windows Firewall settings might be overridden.

#### How to fix:
* **Add to Exclusions:** Open your antivirus settings and add the `Portal` installation folder or the `.exe` file to the **Exclusions** (or Trusted Applications) list.
* **Check Sandbox/Gaming Mode:** Some antiviruses block unknown network activity if "Gaming Mode" or "Silent Mode" is active.
* **Network Monitor:** Ensure that traffic for the local network (specifically for port **29170**) is allowed.

---

### 4. Network Profile Type
Windows often blocks incoming connections if your network is set to **Public**.

1. Go to **Settings** > **Network & Internet** > **Status**.
2. Click on **Properties** for your current connection.
3. Change the Network Profile from **Public** to **Private**.

---

## 🛠 Technical Support
If the steps above did not solve your issue:
* Ensure both devices are on the same local network.
* **Check Router Settings (Client Isolation):** Log into your Wi-Fi router's admin panel and check if a feature called **"AP Isolation"**, **"Client Isolation"**, or **"Guest Network"** is enabled. This security feature prevents devices connected to the same Wi-Fi from communicating with each other. It must be **disabled** for Portal to work.