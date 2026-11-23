# Deploy an Ubuntu Server and a web service

## Goal

Create a local Linux server VM, configure secure access, deploy a simple HTTP service, and prepare it for connectivity testing.

## 1. Create the VM

In Oracle VirtualBox on Windows:

1. Download an Ubuntu Server LTS ISO from the official Ubuntu website: https://ubuntu.com/download/server
2. Create a new VM named `Ubuntu-Server-Module-02`.
3. Select the downloaded ISO and choose Ubuntu (64-bit) where a version selector is shown.
4. If offered, skip unattended installation so the steps below can be followed.
5. Suggested resources: 2 GB RAM if available, 1–2 CPUs, and a dynamically allocated 25 GB virtual disk. Reduce resource allocation if the Windows host is under memory pressure.
6. Set Adapter 1 to NAT.
7. Start the VM and follow the installer.

During installation:
- Select the appropriate language and keyboard.
- Use the default network DHCP configuration unless your lab requires otherwise.
- Use the VM's virtual disk for installation. Do not select or format the Windows host drive.
- Create a normal administrator user with a strong password.
- Select Install OpenSSH Server when offered.
- Finish installation and reboot.

After reboot, log in and verify:

~~~bash
whoami
hostnamectl
ip -br address
sudo apt update
~~~

## 2. Install Nginx

~~~bash
sudo apt install nginx
sudo systemctl enable --now nginx
systemctl status nginx
~~~

Nginx is a web server. The default HTTP page should be available locally from the VM:

~~~bash
curl -I http://127.0.0.1
~~~

A successful HTTP response shows that the local web server answered. Record the actual status line from your output.

## 3. Allow HTTP in UFW

If you are using UFW, inspect existing rules and allow only the web traffic required for this exercise:

~~~bash
sudo ufw status verbose
sudo ufw allow 80/tcp
sudo ufw status numbered
~~~

If SSH administration is required, make sure OpenSSH is allowed before enabling UFW. See `docs/03-networking-and-firewall.md`.

## 4. Open the service from Windows using VirtualBox NAT

To view the Nginx page from the Windows host:

1. Shut down the VM.
2. Open VirtualBox → VM Settings → Network → Adapter 1 → Advanced → Port Forwarding.
3. Add a TCP rule: Host IP `127.0.0.1`, Host Port `8080`, Guest IP blank, Guest Port `80`.
4. Save and start the VM.
5. In a Windows browser, open `http://127.0.0.1:8080`.

If host port 8080 is already in use, choose a free host port and use it in the browser URL. Keep this service bound to localhost for the local exercise.

## 5. Verify Nginx after reboot

~~~bash
sudo systemctl status nginx
ss -tuln
curl -I http://127.0.0.1
~~~

## Lab record

- Ubuntu release:
- VM memory / CPU / disk:
- Network mode:
- OpenSSH installed and running:
- Nginx installation result:
- Nginx service status:
- Local curl HTTP response:
- Windows host browser test result:
- Screenshots:
