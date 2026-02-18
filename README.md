# cloud-production-monitoring-lab
## What OS you launched
Amazon Linux 2023
## Instance type
T3.micro
## Default disk size
30G
## Instance Memory
~1 GB RAM
- Memory available: 618 MB
## Why not to use root in production
It is Safer to create a non-root user and grant sudo access, so that accidental or malicious actions do not compromise the entire system. for as we create cloudadmin.
## Linux directory structure summary
- '/'       → Root directory, top of filesystem
- '/home'   → User directories
- '/etc'    → Configuration files
- '/var'    → Logs and variable data
- '/usr'    → Installed software and binaries
- '/boot'   → Kernel and bootloader files
- '/dev'    → Device files
- '/tmp'    → Temporary files
