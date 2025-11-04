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


#!/bin/bash
 
LOGFILE="healthlog.txt"
TIMESTAMP=$(date +"%Y-%m-%d %H:%M:%S")


 
echo "==================== HEALTH CHECK REPORT ====================" >> $LOGFILE

echo "Timestamp: $TIMESTAMP" >> $LOGFILE
          
echo "--------------------------------------------------------------" >> $LOGFILE
 
2. Make the Script Executable
Open the terminal in VS Code (Ctrl + ~) and run:

bash
Copy code
chmod +x healthcheck.sh
echo "System Date & Time: $(date)" >> $LOGFILE

echo "--------------------------------------------------------------" >> $LOGFILE


uptime_formatted=$(awk '{print int($1/3600)" hours "int(($1%3600)/60)" minutes"}' /proc/uptime) >> $LOGFILE
echo "System Uptime: $uptime_formatted" >> $LOGFILE

echo "--------------------------------------------------------------" >> $LOGFILE

echo "Memory Usage (MB):" >> $LOGFILE
total_mem=$(grep MemTotal /proc/meminfo | awk '{print $2}') >> $LOGFILE
free_mem=$(grep MemAvailable /proc/meminfo | awk '{print $2}') >> $LOGFILE
total_mem_mb=$((total_mem / 1024)) >> $LOGFILE
free_mem_mb=$((free_mem / 1024)) >> $LOGFILE
used_mem_mb=$((total_mem_mb - free_mem_mb)) >> $LOGFILE
echo "Total: ${total_mem_mb} MB" >> $LOGFILE
echo "Used: ${used_mem_mb} MB" >> $LOGFILE
echo "Free: ${free_mem_mb} MB" >> $LOGFILE


echo "--------------------------------------------------------------" >> $LOGFILE


echo "CPU Load (1, 5, 15 min): $(cut -d ' ' -f 1-3 /proc/loadavg)" >> $LOGFILE

echo "--------------------------------------------------------------" >> $LOGFILE

echo -e "\nDisk Usage:" >> $LOGFILE
df -h >> $LOGFILE
echo "" >> $LOGFILE

echo "--------------------------------------------------------------" >> $LOGFILE

echo -e "\nService Status:" >> $LOGFILE
sc query sshd > /dev/null 2>&1 && echo "SSH: Running " || echo "SSH: Not Running " >> $LOGFILE
sc query nginx > /dev/null 2>&1 && echo "Nginx: Running " || echo "Nginx: Not Running " >> $LOGFILE

echo "--------------------------------------------------------------" >> $LOGFILE

echo -e "\nTop 5 Memory Consuming Processes:" >> $LOGFILE
wmic process get Name,WorkingSetSize | sort -k2 -n | tail -n 5 >> $LOGFILE

echo "-------------------------------------------------------------" >> $LOGFILE

