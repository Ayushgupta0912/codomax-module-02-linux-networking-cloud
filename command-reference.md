# Linux and networking command reference

A quick reference for the Module 02 lab. Run commands in your own VM and check the output before taking action.

## Identity and system

~~~bash
whoami
id
hostnamectl
uname -a
cat /etc/os-release
uptime
~~~

## Files and directories

~~~bash
pwd
ls -lah
cd ~/module02
mkdir -p practice
touch notes.txt
cat notes.txt
cp notes.txt backup.txt
mv backup.txt notes-backup.txt
rm notes-backup.txt
~~~

Use `rm` carefully. It deletes files and may not move them to a recycle bin.

## Permissions and ownership

~~~bash
ls -l
chmod 640 notes.txt
chmod u+x script.sh
chown USER:GROUP notes.txt
~~~

Replace USER and GROUP with valid names. Do not apply these to system files as a practice shortcut.

## Accounts and groups

~~~bash
id
groups
getent passwd USERNAME
getent group GROUPNAME
sudo adduser labuser
sudo groupadd labteam
sudo usermod -aG labteam labuser
~~~

## Processes and services

~~~bash
ps aux
top
pgrep -a nginx
systemctl status ssh
systemctl status nginx
sudo systemctl restart nginx
journalctl -u nginx -n 50 --no-pager
~~~

## Networking and DNS

~~~bash
ip -br address
ip route
hostname -I
resolvectl status
getent hosts ubuntu.com
ping -c 4 1.1.1.1
curl -I https://ubuntu.com
ss -tuln
sudo ss -tulpn
~~~

## Firewall

~~~bash
sudo ufw status verbose
sudo ufw app list
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw status numbered
~~~

Allow SSH before enabling UFW on a remote host. Delete a rule only after checking its number and purpose.

## Package management

~~~bash
sudo apt update
apt list --upgradable
sudo apt install PACKAGE_NAME
sudo apt remove PACKAGE_NAME
~~~

Replace `PACKAGE_NAME` with the package you intend to install or remove.

## Nginx test

~~~bash
sudo systemctl enable --now nginx
systemctl is-active nginx
curl -I http://127.0.0.1
~~~

## Safety

Never put passwords, tokens, private SSH keys, or sensitive personal information in this repository. Do not use destructive commands on your Windows host or an important production system.
