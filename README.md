# SSH-Honeypot-with-Cowrie
# SSH Honeypot with Cowrie

A medium-interaction SSH honeypot built with Cowrie and Docker, plus a Python
log parser that classifies attacker behaviour.

## Overview
- Deploys Cowrie in a Docker container exposed on port 2222
- Captures login attempts, commands and sessions as JSON logs
- Python script parses logs and classifies commands (reconnaissance,
  system info, network discovery, user enumeration, etc.)

## Setup
```bash
docker pull cowrie/cowrie:latest
docker run -d --name cowrie -p 2222:2222 cowrie/cowrie:latest
```

Connect to the honeypot:
```bash
ssh -p 2222 root@127.0.0.1
```

## Log Analysis
Copy the logs out of the container volume, then run:
```bash
python3 parser/analyse_logs.py


## Example Output
Successful logins: 2
Commands observed: 15
Unique source IPs: 1

## Command Classification
| Command | Category |
|---|---|
| whoami | Reconnaissance |
| ls | File/Directory Discovery |
| uname -a | System Information |
| ps | Process Discovery |
| ifconfig | Network Discovery |
| cat /etc/passwd | User Enumeration |
| history | Command History Discovery |

#

## What I Learned
- Deploying containerised services with Docker
- How honeypots emulate a real system to capture attacker behaviour
- Parsing JSON logs and mapping commands to attacker techniques

## Disclaimer
Built for educational purposes in an isolated lab environment.
