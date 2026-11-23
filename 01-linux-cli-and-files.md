# Linux CLI, navigation, files, and permissions

## Goal

Practise moving around the Linux file system, creating and inspecting files, and understanding Linux permissions.

## 1. Identify the current environment

~~~bash
whoami
hostname
pwd
uname -a
cat /etc/os-release
~~~

- `whoami` prints the current account name.
- `hostname` displays the machine name.
- `pwd` prints the current working directory.
- `uname -a` displays kernel and system details.
- `/etc/os-release` identifies the Linux distribution and release.

## 2. Navigate the file system

~~~bash
pwd
ls
ls -lah
cd /etc
pwd
cd ~
pwd
~~~

Useful paths: `/` is the root of the Linux directory tree; `/home` contains ordinary users' home directories; `/etc` stores system-wide configuration; `/var/log` commonly stores logs; `/tmp` is used for temporary files.

## 3. Create, copy, move, and inspect files

~~~bash
mkdir -p ~/module02/practice
cd ~/module02/practice
touch notes.txt
printf 'Linux Module 02 practice\n' > notes.txt
cat notes.txt
cp notes.txt notes-backup.txt
mv notes-backup.txt backup.txt
ls -l
~~~

The `>` operator replaces a file's contents. The `>>` operator appends to a file. Check the target path before using either operator.

## 4. Understand permissions

Run `ls -l notes.txt`. A permission string such as `-rw-r--r--` shows the file type followed by permissions for the owner, group, and others.

- `r` = read
- `w` = write
- `x` = execute
- Numeric values: read = 4, write = 2, execute = 1

Example: `640` means owner can read/write, group can read, and others have no permissions.

~~~bash
chmod 640 notes.txt
ls -l notes.txt
chmod u+x notes.txt
ls -l notes.txt
~~~

Do not make files executable unless they need to be executed. Avoid using `chmod 777` as a general fix.

## 5. Ownership

Inspect ownership with `ls -l notes.txt`. A privileged administrator can change ownership on a test file:

~~~bash
sudo chown USERNAME:GROUPNAME notes.txt
~~~

Replace `USERNAME` and `GROUPNAME` with real accounts that exist on your VM. Do not copy the placeholders literally.

## Lab record

- Date:
- Ubuntu version:
- Working directory used:
- File created:
- Permission before and after `chmod`:
- What the permission change meant:
- Screenshot filename:
- What I learned:
