SSH Honeypot with Cowrie

An SSH honeypot built with Cowrie and Docker. It emulates a Debian server, accepts any login, and records everything an attacker does.

What I Did
Pulled the Cowrie image and ran it in a Docker container on port 2222
Connected to the honeypot over SSH as root (any password is accepted)
Ran typical attacker reconnaissance commands inside the fake server
Checked the Cowrie logs to confirm the logins and commands were captured
Setup
bash
docker pull cowrie/cowrie:latest
docker run -d --name cowrie -p 2222:2222 cowrie/cowrie:latest

Check that it's running:

bash
docker ps
Connecting to the Honeypot
bash
ssh -p 2222 root@127.0.0.1

Commands I ran inside the session:

whoami
pwd
ls
uname -a
ps
ifconfig
cat /etc/passwd
history
exit

Cowrie responds as a fake Debian server (svr04) with realistic output for each command.

Viewing the Logs
bash
docker logs --tail 100 cowrie

The logs show the connection, the SSH client fingerprint, the successful login, and every command entered.

What I Learned
Running containerised services with Docker
How honeypots emulate a real system to capture attacker behaviour
Reading Cowrie logs to see logins, commands and session deta
