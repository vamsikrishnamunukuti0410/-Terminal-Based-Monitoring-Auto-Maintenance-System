🖥️ Terminal-Based Intelligent Linux Monitoring & Auto-Maintenance System
A fully automated Linux monitoring system built entirely in Bash that provides real-time system visibility, automated alerting, self-healing, and production-grade maintenance.

📁 Project Structure
linux-monitoring-system/
├── monitor.sh            # Phase 1: Real-time colored terminal dashboard
├── alerts.sh             # Phase 2: Threshold-based alerting system
├── report.sh             # Phase 4: Daily compressed report generator
├── log_rotation.sh       # Phase 5: Log rotation & cleanup
├── self_heal.sh          # Phase 6: Self-healing service monitor
├── maintenance.sh        # Phase 7: Weekly maintenance automation
├── security_update.sh    # Phase 8: Security-only patch updates
├── setup_cron.sh         # Phase 9: Cron job installer
├── config.conf           # Central configuration file
├── README.md             # This file
├── logs/
│   ├── health_history.log   # Phase 3: Health history (auto-generated)
│   ├── alerts.log           # Alert events
│   ├── self_heal.log        # Service restart log
│   └── security_update.log  # Security update log
└── reports/
    └── system_YYYY-MM-DD.txt  # Daily reports (auto-generated)
🚀 Quick Start
1. Make scripts executable
chmod +x *.sh
2. Configure thresholds
Edit config.conf to set your thresholds, email settings, and critical services:

nano config.conf
3. Launch the dashboard
bash monitor.sh
4. Install cron automation
sudo bash setup_cron.sh
📊 Phase 1: Core Monitoring Dashboard (monitor.sh)
Real-time terminal dashboard with color-coded metrics:

Metric	Source	Color Coding
CPU Usage	/proc/stat / ps	Green → Yellow → Red
Memory Usage	free / vm_stat	Green → Yellow → Red
Disk Usage	df	Green → Yellow → Red
Disk I/O Latency	iostat	Magenta
Network Speed	/sys/class/net/	Green (DL/UL KB/s)
Network Connections	ss / netstat	Cyan
Uptime	uptime	Cyan
Load Average	/proc/loadavg	Green → Yellow → Red
Error Rate	journalctl / syslog	Magenta
Top 5 Processes	ps aux	White
TCP Retransmissions	/proc/net/snmp	Magenta
Refreshes every 5 seconds (configurable)
Threshold labels: NORMAL, WARNING, CRITICAL
Visual bars: ████░░░░░░ for percentage metrics
🔔 Phase 2: Threshold Alerting (alerts.sh)
Triggers when metrics exceed thresholds in config.conf:

Metric	Warning	Critical
CPU	70%	80%
Memory	65%	75%
Disk	75%	85%
Load	3	5
Logs to logs/alerts.log
Sends email via mail/sendmail (when EMAIL_ENABLED=true)
📈 Phase 3: Health History Logging
The dashboard automatically logs metrics every 5 minutes to logs/health_history.log:

2025-01-15 14:30:00 | CPU: 45% | MEM: 62% | DISK: 55% | LOAD: 1.2
📝 Phase 4: Daily Report (report.sh)
Generates a comprehensive daily report:

System uptime, CPU, memory, disk stats
Top 5 processes by CPU
Load average, network stats
Error summary, TCP statistics
Alert summary for the day
bash report.sh
# Output: reports/system_2025-01-15.txt + .zip
🔄 Phase 5: Log Rotation (log_rotation.sh)
Enterprise-grade log management:

Deletes logs older than 30 days
Compresses logs larger than 50 MB
Prunes excess rotated files (keeps max 10)
Cleans old reports
bash log_rotation.sh
💊 Phase 6: Self-Healing (self_heal.sh)
Automatic restart of critical services:

Monitors services listed in CRITICAL_SERVICES config
Auto-restarts failed services (up to 3 retries)
Escalates with email alert after exhausting retries
Logs all actions to logs/self_heal.log
sudo bash self_heal.sh
🔧 Phase 7: Weekly Maintenance (maintenance.sh)
Automated weekly system tasks:

Package update (apt/yum/dnf/pacman)
Temp file cleanup (/tmp, /var/tmp, thumbnail cache)
Journal log vacuum (keep 7 days)
Log rotation (invokes log_rotation.sh)
sudo bash maintenance.sh
🔒 Phase 8: Security Updates (security_update.sh)
Security-only patching (no major version upgrades):

Distro	Method
Ubuntu/Debian	unattended-upgrade -d or apt-get upgrade
RHEL/CentOS	yum update --security
Fedora	dnf update --security
Logs to logs/security_update.log
Alerts on failure
Verifies kernel version unchanged
sudo bash security_update.sh
⏰ Phase 9: Cron Automation (setup_cron.sh)
Schedule	Task
*/5 * * * *	Health logging & self-heal
59 23 * * *	Daily report
0 0 * * *	Log rotation
0 2 * * 0	Weekly maintenance (Sun 2AM)
0 3 * * 0	Security updates (Sun 3AM)
sudo bash setup_cron.sh    # Install
crontab -l                 # Verify
⚙️ Configuration (config.conf)
All settings are centralized in config.conf:

# Thresholds
CPU_WARN=70     CPU_CRIT=80
MEMORY_WARN=65  MEMORY_CRIT=75
DISK_WARN=75    DISK_CRIT=85
LOAD_WARN=3     LOAD_CRIT=5

# Email
EMAIL_ENABLED=false
EMAIL_RECIPIENT="admin@example.com"

# Services
CRITICAL_SERVICES="sshd nginx mysql"
MAX_RESTART_RETRIES=3

# Log Rotation
LOG_RETENTION_DAYS=30
LOG_MAX_SIZE_MB=50
MAX_ROTATED_FILES=10
🛠️ Prerequisites
OS: Linux (Ubuntu/Debian, RHEL/CentOS, Fedora)
Shell: Bash 4.0+
Tools: bc, ps, df, free, ss/netstat, gzip, zip
Optional: mail/sendmail (for email alerts), iostat (for disk I/O), mpstat (for CPU stats)
Permissions: sudo required for maintenance, security updates, and self-healing
