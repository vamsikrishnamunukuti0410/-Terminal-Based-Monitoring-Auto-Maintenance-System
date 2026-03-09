# 🖥️ Terminal-Based Intelligent Linux Monitoring & Auto-Maintenance System

A fully automated Linux monitoring system built entirely in **Bash** that provides real-time system visibility, automated alerting, self-healing, and production-grade maintenance.

---

# 📁 Project Structure

```
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
├── README.md
├── logs/
│   ├── health_history.log
│   ├── alerts.log
│   ├── self_heal.log
│   └── security_update.log
└── reports/
    └── system_YYYY-MM-DD.txt
```

---

# 🚀 Quick Start

### 1️⃣ Make scripts executable

```bash
chmod +x *.sh
```

### 2️⃣ Configure thresholds

Edit the configuration file:

```bash
nano config.conf
```

Configure thresholds, email settings, and critical services.

### 3️⃣ Launch the monitoring dashboard

```bash
bash monitor.sh
```

### 4️⃣ Install cron automation

```bash
sudo bash setup_cron.sh
```

---

# 📊 Phase 1: Core Monitoring Dashboard (`monitor.sh`)

Real-time terminal dashboard with color-coded metrics.

| Metric              | Source              | Color Coding         |
| ------------------- | ------------------- | -------------------- |
| CPU Usage           | /proc/stat / ps     | Green → Yellow → Red |
| Memory Usage        | free                | Green → Yellow → Red |
| Disk Usage          | df                  | Green → Yellow → Red |
| Disk I/O Latency    | iostat              | Magenta              |
| Network Speed       | /sys/class/net      | Green                |
| Network Connections | ss / netstat        | Cyan                 |
| Uptime              | uptime              | Cyan                 |
| Load Average        | /proc/loadavg       | Green → Yellow → Red |
| Error Rate          | journalctl / syslog | Magenta              |
| Top Processes       | ps aux              | White                |
| TCP Retransmissions | /proc/net/snmp      | Magenta              |

Features:

* Refresh interval: **5 seconds**
* Threshold labels: `NORMAL`, `WARNING`, `CRITICAL`
* Visual percentage bars

Example:

```
████░░░░░░
```

---

# 🔔 Phase 2: Threshold Alerting (`alerts.sh`)

Triggers alerts when system metrics exceed configured thresholds.

| Metric | Warning | Critical |
| ------ | ------- | -------- |
| CPU    | 70%     | 80%      |
| Memory | 65%     | 75%      |
| Disk   | 75%     | 85%      |
| Load   | 3       | 5        |

Alerts are written to:

```
logs/alerts.log
```

Optional email alerts can be enabled.

---

# 📈 Phase 3: Health History Logging

The monitoring dashboard logs system metrics every **5 minutes**.

Example log entry:

```
2025-01-15 14:30:00 | CPU: 45% | MEM: 62% | DISK: 55% | LOAD: 1.2
```

Log file:

```
logs/health_history.log
```

---

# 📝 Phase 4: Daily System Report (`report.sh`)

Generates a detailed daily system report including:

* System uptime
* CPU usage
* Memory usage
* Disk utilization
* Top processes
* Load average
* Network statistics
* Error summaries
* Alert summary

Run manually:

```bash
bash report.sh
```

Output:

```
reports/system_YYYY-MM-DD.txt
```

Compressed automatically.

---

# 🔄 Phase 5: Log Rotation (`log_rotation.sh`)

Enterprise-style log management.

Features:

* Deletes logs older than **30 days**
* Compresses logs larger than **50MB**
* Keeps maximum **10 rotated files**
* Cleans old system reports

Run:

```bash
bash log_rotation.sh
```

---

# 💊 Phase 6: Self-Healing System (`self_heal.sh`)

Automatically monitors and restarts critical services.

Features:

* Monitors services from configuration
* Auto restart if service fails
* Up to **3 restart retries**
* Escalates with alert if restart fails

Run:

```bash
sudo bash self_heal.sh
```

Logs stored in:

```
logs/self_heal.log
```

---

# 🔧 Phase 7: Weekly Maintenance (`maintenance.sh`)

Automates routine system maintenance.

Tasks performed:

* System package updates
* Temporary file cleanup
* Journal log vacuum
* Log rotation execution

Run:

```bash
sudo bash maintenance.sh
```

---

# 🔒 Phase 8: Security Updates (`security_update.sh`)

Applies **security-only patches** without major upgrades.

| Distribution    | Method                |
| --------------- | --------------------- |
| Ubuntu / Debian | unattended-upgrade    |
| RHEL / CentOS   | yum update --security |
| Fedora          | dnf update --security |

Run:

```bash
sudo bash security_update.sh
```

Logs stored in:

```
logs/security_update.log
```

---

# ⏰ Phase 9: Cron Automation (`setup_cron.sh`)

| Schedule    | Task                       |
| ----------- | -------------------------- |
| */5 * * * * | Health logging & self-heal |
| 59 23 * * * | Daily report               |
| 0 0 * * *   | Log rotation               |
| 0 2 * * 0   | Weekly maintenance         |
| 0 3 * * 0   | Security updates           |

Install cron jobs:

```bash
sudo bash setup_cron.sh
```

Verify:

```bash
crontab -l
```

---

# ⚙️ Configuration (`config.conf`)

All system settings are centralized in one configuration file.

Example:

```
# Thresholds
CPU_WARN=70
CPU_CRIT=80

MEMORY_WARN=65
MEMORY_CRIT=75

DISK_WARN=75
DISK_CRIT=85

LOAD_WARN=3
LOAD_CRIT=5

# Email alerts
EMAIL_ENABLED=false
EMAIL_RECIPIENT="admin@example.com"

# Critical services
CRITICAL_SERVICES="sshd nginx mysql"
MAX_RESTART_RETRIES=3

# Log rotation
LOG_RETENTION_DAYS=30
LOG_MAX_SIZE_MB=50
MAX_ROTATED_FILES=10
```

---

# 🛠️ Prerequisites

**Operating System**

* Linux (Ubuntu / Debian / RHEL / CentOS / Fedora)

**Shell**

* Bash 4.0+

**Required Tools**

* bc
* ps
* df
* free
* ss or netstat
* gzip
* zip

**Optional Tools**

* mail / sendmail
* iostat
* mpstat

**Permissions**

Some scripts require **sudo privileges**.

---

# 📌 Summary

This project provides a lightweight yet powerful **Linux monitoring and maintenance framework** using only Bash.

Capabilities include:

* Real-time monitoring
* Alerting system
* Historical logging
* Automated reports
* Self-healing services
* Log rotation
* Security patch management
* Cron-based automation

Designed for **servers, DevOps environments, and system administrators**.
