# Users, groups, processes, and services

## Goal

Learn how Linux accounts and groups control access, how to inspect running processes, and how to manage systemd services.

## 1. Inspect the current user

~~~bash
whoami
id
groups
~~~

## 2. Create a practice user and group

Run these commands only on your own disposable lab VM. Choose a test username such as `labuser`.

~~~bash
sudo adduser labuser
sudo groupadd labteam
sudo usermod -aG labteam labuser
id labuser
getent group labteam
~~~

The `-aG` option appends the user to the supplementary group list. Do not omit `-a` when adding a user to an additional group, because that can replace existing supplementary group membership.

To verify the new group in a fresh login session:

~~~bash
su - labuser
groups
exit
~~~

Remove the test account only if you no longer need it:

~~~bash
sudo deluser labuser
sudo groupdel labteam
~~~

Do not remove your own administrator account.

## 3. Inspect processes

~~~bash
ps aux
top
pgrep -a ssh
~~~

- `ps aux` gives a snapshot of processes.
- `top` displays a live, updating process view.
- `pgrep` searches for processes by name.

If you must stop a test process, prefer a normal termination signal:

~~~bash
kill -15 PROCESS_ID
~~~

Replace `PROCESS_ID` with the actual process ID. Do not terminate an unfamiliar system process. Avoid `kill -9` unless normal shutdown has failed and you understand the impact.

## 4. Inspect and manage services

Ubuntu Server uses systemd on standard installations.

~~~bash
systemctl status ssh
sudo systemctl restart ssh
sudo systemctl enable ssh
journalctl -u ssh -n 50 --no-pager
~~~

For the web service used later in this module:

~~~bash
systemctl status nginx
~~~

A service may not exist until its package is installed. If systemctl reports that a unit cannot be found, check whether the related package has been installed.

## Lab record

- Test username created:
- Test group created:
- Group membership verified with:
- Process command used:
- Service inspected:
- Service status observed:
- Any issue and how it was resolved:
- Screenshot filenames:
