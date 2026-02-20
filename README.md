# cloud-production-monitoring-lab
## Week 1 — Linux Foundations
## Day 1 — System & Linux Basics
### What OS you launched
Amazon Linux 2023
### Instance type
T3.micro
### Default disk size
30G
### Instance Memory
~1 GB RAM
- Memory available: 618 MB
### Why not to use root in production
It is Safer to create a non-root user and grant sudo access, so that accidental or malicious actions do not compromise the entire system. for as we create cloudadmin.
### Linux directory structure summary
- '/'       → Root directory, top of filesystem
- '/home'   → User directories
- '/etc'    → Configuration files
- '/var'    → Logs and variable data
- '/usr'    → Installed software and binaries
- '/boot'   → Kernel and bootloader files
- '/dev'    → Device files
- '/tmp'    → Temporary files

## Day 2 — Networking & Service Management
  🌐 Network Inspection
- Private IP: 172.31.24.47
- Environment: EC2 (Private subnet range 172.31.x.x)
- Web Server: Nginx
- Default HTTP Port: 80
🔎 Networking Commands Used
- ip a
- ss -tulnp
- curl localhost
- sudo systemctl start nginx
- sudo systemctl stop nginx
- sudo systemctl status nginx
- sudo systemctl enable nginx
## Key Learning:
ip a → Shows network interfaces and private IP.

ss -tulnp → Shows listening ports and associated processes.

Port 22 → SSH service.

Port 80 → Nginx HTTP service.

Observations:

When Nginx is running → curl localhost returns HTML page.

When Nginx is stopped → connection refused on port 80.

This demonstrates service dependency and availability concepts.

📂 Logs Location

/var/log/nginx/

    access.log

    error.log

Used:

tail -f access.log

Learned how to monitor logs in real time.

## Cloud Engineering Reflection

Even if Nginx runs successfully:

External access may fail due to Security Group rules.

Network-layer security is separate from OS-layer service status.
## Day 3 — Process & System Monitoring
🎯 Objective

Understand Linux process management, CPU usage, load average, memory analysis, and disk inode monitoring from a production perspective.

🖥 System Monitoring Commands Used
ps aux
top
uptime
nproc
free -m
df -h
df -i

🔍 Load Average Analysis

Command:

uptime


Output:

load average: 0.00, 0.00, 0.00


Instance CPU cores:

2 vCPUs

Interpretation

Load < number of CPU cores → system healthy

Load = CPU cores → fully utilized

Load > CPU cores → overloaded system
⚡ CPU Stress Simulation

Command used to simulate CPU load:

yes > /dev/null &

Observations

The yes process consumed high CPU.

CPU usage increased significantly in top.

Demonstrated how runaway processes impact system performance.

Stopped the process using:

killall yes

💾 Disk & Inode Monitoring

Checked disk usage:

df -h


Checked inode usage:

df -i

Important Concept

Even if disk space is available,
if inodes are exhausted (100%),
the system cannot create new files.

This is critical for:

Log-heavy systems

Web servers

Monitoring systems

## 🔴 Day 4 — Log Analysis & Production Troubleshooting
🎯 Objective

Simulate real-world production failures and practice structured troubleshooting using:

Service status inspection

Port verification

Configuration validation

Log analysis

Disk usage simulation

🧪 Scenario 1 — Service Failure Investigation
Step 1 — Check Service Status
sudo systemctl status nginx

Verified:

Whether the service was active or failed

Observed error messages if present

Step 2 — Check Listening Ports
ss -tulnp | grep 80

Confirmed whether Nginx was listening on port 80.

Step 3 — Local Connectivity Test
curl localhost

Observed:

HTML response when service running

Connection refused when service stopped

🧨 Scenario 2 — Intentional Configuration Error

To simulate a deployment mistake:

Edited nginx config file:

sudo nano /etc/nginx/nginx.conf

Added invalid directive to break configuration.

Tested configuration before restart:

sudo nginx -t

Result:

Configuration test failed.

Error message displayed with line number.

Attempted restart:

sudo systemctl restart nginx

Service failed as expected.

Checked error logs:

tail -n 20 /var/log/nginx/error.log
🔎 Key Learning

Always validate configuration before restart.

Error logs provide precise failure details.

Blind restarts in production can cause outages.

💾 Scenario 3 — Disk Usage Simulation

Created large file to simulate disk pressure:

fallocate -l 500M bigfile

Checked disk usage:

df -h

Observed increase in used space.

Removed file:

rm bigfile

Verified disk recovery.

🔎 Key Learning

Disk monitoring is critical in production.

Log-heavy systems can fill storage quickly.

Disk full situations can stop services.

🌐 Scenario 4 — Traffic Simulation

Generated multiple HTTP requests:

for i in {1..50}; do curl localhost > /dev/null; done

Checked access logs:

tail -n 20 /var/log/nginx/access.log

Observed increased log entries.

🔎 Key Learning

Logs grow proportionally with traffic.

Monitoring log growth is important.

High traffic can impact system resources.



