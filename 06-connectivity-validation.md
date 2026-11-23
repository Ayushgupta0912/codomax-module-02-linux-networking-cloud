# Linux server connectivity validation

## Goal

Use repeatable checks to confirm the VM's network configuration and the deployed web service.

## Validation checklist

### A. Host and interface details

~~~bash
hostnamectl
ip -br address
ip route
~~~

Record the hostname, active interface, IP address, and default route.

### B. DNS resolution

~~~bash
resolvectl status
getent hosts ubuntu.com
~~~

Record which resolver is configured and whether the hostname resolves to one or more IP addresses.

### C. Outbound network connectivity

~~~bash
ping -c 4 1.1.1.1
curl -I https://ubuntu.com
~~~

Ping can be filtered. A successful HTTPS request is another useful test of outbound connectivity.

### D. Listening ports

~~~bash
sudo ss -tulpn
~~~

Check whether SSH and the intended web service are listening. Record the actual ports from your VM output.

### E. Firewall

~~~bash
sudo ufw status verbose
~~~

Confirm that only the required rules for the lab are present. If UFW is inactive, record that fact rather than reporting that firewall rules were tested.

### F. Nginx service

~~~bash
systemctl is-active nginx
curl -I http://127.0.0.1
~~~

If Nginx is not active, inspect its logs:

~~~bash
sudo journalctl -u nginx -n 50 --no-pager
~~~

### G. Windows host test

If VirtualBox NAT port forwarding is configured for guest TCP 80 to host TCP 8080, open `http://127.0.0.1:8080` from the Windows host. Record whether the default Nginx page loads.

## Results table

Fill this table with your actual observations:

| Check | Expected observation | Actual result |
|---|---|---|
| VM IP address | A valid address on the VM interface | Pending |
| Default route | A default route is shown | Pending |
| DNS lookup | Hostname resolves | Pending |
| SSH service | Active when installed and started | Pending |
| Nginx service | Active after installation | Pending |
| Local HTTP test | HTTP response from 127.0.0.1 | Pending |
| Host browser test | Nginx page via forwarded port | Pending |
| UFW rules | Required rules only | Pending |

## Troubleshooting hints

- No IP address: inspect the VirtualBox adapter setting and DHCP status.
- DNS lookup fails but an IP test works: inspect DNS configuration.
- Nginx is inactive: check `systemctl status nginx` and its journal.
- Local curl works but host browser fails: check VirtualBox port forwarding, host port availability, guest port, and UFW.
- SSH connection fails: verify the SSH service, NAT port-forwarding rule, username, host port, and key permissions.

Do not write "passed" until the test has actually been performed.
