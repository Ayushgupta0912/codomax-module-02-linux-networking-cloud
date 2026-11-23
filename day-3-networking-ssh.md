# Day 3 — Networking, DNS, ports, firewall, and SSH

**Date performed:** Not recorded yet  
**Status:** Not started

## Objective

Inspect the server's network configuration and practise secure SSH access.

## Suggested commands

~~~bash
ip -br address
ip route
resolvectl status
getent hosts ubuntu.com
ss -tuln
sudo ufw status verbose
sudo systemctl status ssh
~~~

Follow `docs/04-ssh-security.md` to create and test key-based SSH access.

## My actual observations

- Interface and IP:
- Default gateway:
- DNS resolver:
- DNS lookup result:
- Listening ports:
- UFW status and rules:
- SSH service status:
- SSH key login tested:
- Any issue and resolution:

## Security note

Do not add private keys or passwords to this repository. Restrict SSH access and do not expose the VM to the public internet for this lab.

## Evidence

List genuine screenshots here.
