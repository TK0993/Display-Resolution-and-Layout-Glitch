# IT-Support-Portfolio
A log of real-world IT support tickets, troubleshooting scripts, and root-cause analyses.
# IT Support Ticket: INC-84920 (Display Resolution & Layout Glitch)

## 📌 Ticket Overview
* **Ticket ID:** INC-84920  
* **Priority:** P3 (Medium/Low - Non-critical usability issue)  
* **Category:** Software / OS Customization / Display  
* **Component:** Windows 11 Desktop Environment / Third-Party Application Conflict  

## 🔍 User Issue Description
User reported that immediately after signing into a full-screen gaming client (EA App), the desktop background turned blank/black, and desktop shortcut icons significantly decreased in size.

### Before Resolution:
![Before Fix](YOUR_BEFORE_IMAGE_NAME_HERE.png)

---

## 🛠️ Root Cause Analysis (RCA)
* **Trigger:** Launching full-screen gaming clients (EA, Steam, Ubisoft Connect) forces temporary hardware resolution changes on the primary monitor.
* **Mechanism:** When the application hooks into the display driver, Windows refreshes the File Explorer (`explorer.exe`) process. If the application handles the resolution hand-back improperly, Windows defaults desktop icons to their smallest grid layout and drops the wallpaper cache.
* **Log Verification:** Audited Windows System Logs via Event Viewer and located **Event ID 4101**: *"Display driver stopped responding and has successfully recovered,"* matching the exact timestamp of the application initialization.

---

## 🚀 Resolution & Automation
Instead of performing a time-consuming system reboot, the issue was solved instantly using a targeted administration script to restart the Windows graphical shell.
Image 1 shows black desktop background with desktop icons resized due app conflict (1.black screen and small desktop icons)
### PowerShell Automation Used:
```powershell
# Step 1: Forcefully stop the Windows graphical shell interface
Stop-Process -Name "explorer" -Force

# Step 2: Restart the Windows graphical shell interface to rebuild cache
Start-Process "explorer.exe"
```

### After Resolution:
![After Fix](2.background restored and desktop items resorted)

---

## 🧠 Summary of Learning & Takeaways
* **Efficiency Over Reboots:** Preserved user uptime and active application data by targeting the specific failing process (`explorer.exe`) instead of restarting the entire system hardware.
* **Data Privacy Compliance:** Handled sensitive personal data in accordance with IT support best practices by reviewing and protecting personal/family photography on the user endpoint before finalizing public documentation.
