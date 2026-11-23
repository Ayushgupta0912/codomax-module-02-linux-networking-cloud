# Networking, DNS, ports, firewalls, and security groups

## Goal

Understand the basic information needed to connect to a Linux server and control which network traffic is allowed.

## 1. Core concepts

- **IP address:** identifies a network interface on an IP network.
- **Subnet and CIDR prefix:** describe the network range, for example `/24`.
- **Default gateway:** the next-hop router used to reach destinations outside the local subnet.
- **DNS:** translates names such as `example.com` into IP addresses.
- **Port:** identifies a service endpoint on a host. TCP and UDP are separate transport protocols.
- **Firewall:** allows or blocks traffic according to rules.

Common ports:

| Port | Typical use | Transport |
|---|---|---|
| 22 | SSH remote administration | TCP |
| 53 | DNS | UDP and TCP |
| 80 | HTTP | TCP |
| 443 | HTTPS | TCP |

A service does not automatically become reachable just because its port is open. The service must also be running and listening on the correct interface.

## 2. Inspect network configuration

~~~bash
ip -br address
ip route
hostname -I
resolvectl status
~~~

Record the VM interface name, assigned IP address, default route, and DNS servers. Do not guess these values; record the output from your own VM.

## 3. Test DNS and basic connectivity

~~~bash
getent hosts ubuntu.com
ping -c 4 1.1.1.1
curl -I https://ubuntu.com
~~~

A ping may be blocked by a network even when web access works. Treat ping as one diagnostic check, not the only proof of connectivity.

## 4. Inspect listening ports

~~~bash
ss -tuln
sudo ss -tulpn
~~~

The second command may need `sudo` to show process details for all sockets. Do not expose services you do not intend to use.

## 5. Configure UFW carefully

Check the current status:

~~~bash
sudo ufw status verbose
~~~

For a local Ubuntu Server lab, allow SSH before enabling the firewall:

~~~bash
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw enable
sudo ufw status numbered
~~~

Only allow port 80 after you intend to run the web server. If the OpenSSH application profile is unavailable, inspect available profiles with `sudo ufw app list`. You can use `sudo ufw allow 22/tcp` as an alternative after confirming that SSH uses port 22.

To remove a rule, first inspect its number with `sudo ufw status numbered`. Then delete the correct rule by number, checking the prompt carefully:

~~~bash
sudo ufw delete RULE_NUMBER
~~~

Do not blindly copy `RULE_NUMBER`.

## 6. Cloud security groups — concept

A cloud security group is a virtual network access control attached to cloud resources such as virtual machine network interfaces. In common cloud platforms, security groups are stateful: return traffic for an allowed connection is automatically permitted.

Good beginner practice:
- Keep inbound access closed by default.
- Allow only required ports.
- Restrict administrative SSH access to a trusted source IP or approved VPN where possible.
- Avoid opening SSH (22) to `0.0.0.0/0`.
- Review outbound rules according to the application's needs.
- Remove temporary rules after testing.

The UFW commands above configure the Ubuntu VM's host firewall. They do not create or configure an AWS, Azure, or other cloud security group. Complete a cloud security-group exercise only in an approved sandbox and confirm its cost settings first.

## Lab record

- VM IP address:
- Default gateway:
- DNS resolver:
- DNS lookup result:
- Ports found listening:
- UFW status before:
- Rules added:
- UFW status after:
- Cloud security group exercise (if assigned):
- Evidence filenames:
