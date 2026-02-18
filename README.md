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
