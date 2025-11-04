# Bash-scripting-

📘 Project Overview:

The System Health Check Script (healthcheck.sh) is a Bash script that monitors key system metrics like uptime, CPU load, memory and disk usage, and service status.
It generates a full system report and saves it into a log file named healthlog.txt with a timestamp.

This script is useful for system administrators, DevOps engineers, or anyone who wants to perform periodic health checks on their system.

🚀 Features:

✅ Displays current date and time
✅ Shows system uptime
✅ Reports CPU load (from uptime)
✅ Displays memory usage (free -m)
✅ Lists disk usage (df -h)
✅ Shows top 5 memory-consuming processes
✅ Checks if certain services (like nginx and ssh) are running
✅ Logs all information into healthlog.txt

📂 Project Structure:

SystemHealthCheck/ │ 
├── healthcheck.sh # Main Bash script 
├── healthlog.txt # Output log file (auto-generated) 
└── README.md # Project documentation

bash Copy code

⚙️ Prerequisites:

Before running the script, make sure your system has:

Bash shell (Linux, macOS, or WSL)
Common system commands:
uptime
free
df
ps
awk
systemctl (for checking service status)

🧑‍💻 How to Run the Project in VS Code:

1. Create and Save the Script:

Make sure you have this script in your workspace as healthcheck.sh:


