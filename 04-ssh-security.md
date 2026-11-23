# SSH and secure remote access

## Goal

Enable secure remote administration of the Ubuntu Server VM and understand SSH key authentication.

## 1. Check the SSH server

If OpenSSH Server was selected during Ubuntu installation:

~~~bash
sudo systemctl status ssh
~~~

If it is not installed, install and start it:

~~~bash
sudo apt update
sudo apt install openssh-server
sudo systemctl enable --now ssh
sudo systemctl status ssh
~~~

## 2. Generate an SSH key on Windows

Open PowerShell on the Windows host, not inside the VM:

~~~powershell
ssh-keygen -t ed25519 -C "ayush-module-02"
~~~

Accept the default file location. Set a passphrase when prompted. This creates a private key and a matching public key in your Windows user profile's `.ssh` folder.

- `id_ed25519` is the private key. Never upload or share it.
- `id_ed25519.pub` is the public key. This is the key that can be installed on the VM.

## 3. Connect to a VirtualBox NAT VM

With a NAT adapter, the guest is not normally directly reachable from the host by its guest IP. Add a port-forwarding rule in VirtualBox:

1. Shut down the VM.
2. Open VM Settings → Network → Adapter 1 → Advanced → Port Forwarding.
3. Add a TCP rule: Host IP `127.0.0.1`, Host Port `2222`, Guest IP blank, Guest Port `22`.
4. Save and start the VM.

If host port 2222 is already in use, choose another unused host port and use it consistently below.

## 4. Install the public key on the VM

Replace `VM_USER` with your actual Ubuntu username. Run in Windows PowerShell:

~~~powershell
Get-Content "$env:USERPROFILE\.ssh\id_ed25519.pub" | ssh -p 2222 VM_USER@127.0.0.1 "umask 077; mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys; chmod 700 ~/.ssh; chmod 600 ~/.ssh/authorized_keys"
~~~

The first connection may ask you to trust the VM's host key. Confirm only when you are sure you are connecting to your own VM. Enter your VM password if asked.

## 5. Test key-based login

~~~powershell
ssh -i "$env:USERPROFILE\.ssh\id_ed25519" -p 2222 VM_USER@127.0.0.1
~~~

Replace `VM_USER`. Confirm you can log in using the key before changing any password-authentication settings.

## 6. Security reminders

- Never copy `id_ed25519` into GitHub.
- Never paste private key contents into a README, issue, chat, or screenshot.
- Keep the SSH passphrase private.
- Keep password authentication enabled until key login has been tested in a separate session.
- For this beginner VM, do not expose SSH to the public internet.

## Lab record

- SSH server status:
- Key algorithm:
- Public key installed (yes/no):
- Host port used:
- Successful key login tested (yes/no):
- Error encountered and resolution:
- Evidence filenames (do not include private key contents):
