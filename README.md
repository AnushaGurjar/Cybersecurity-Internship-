Task 1: Scan Your Local Network for Open Ports

1. Objective

The objective of this task was to perform basic network reconnaissance by identifying active devices on a local network and checking for open TCP ports. This helps in understanding network exposure, identifying commonly running services, and recognizing potential security risks associated with unnecessary or improperly secured network services.

2. Tools Used

- Nmap 7.99
- Termux on Android
- Git and GitHub for storing and documenting the scan results
- Wireshark: Not used because it was listed as optional in the task instructions

3. Network Information

The local device IP address identified during the task was:

"192.168.0.105"

Based on this address, the local network range was identified as:

"192.168.0.0/24"

This range contains 256 possible addresses, from "192.168.0.0" through "192.168.0.255".

4. Network Discovery

The first scan was performed using:

nmap -sn 192.168.0.0/24

This is a host discovery scan used to identify active devices without performing a port scan.

Results

Two active hosts were identified:

IP Address| Status| Observation
"192.168.0.1"| Up| Likely the local network router/gateway
"192.168.0.105"| Up| Android device used for the task

The scan reported:

256 IP addresses scanned, 2 hosts up.

5. Port Scanning

The task guide suggested a TCP SYN scan using:

nmap -sS 192.168.0.0/24

However, on the non-rooted Android/Termux environment, Nmap reported that the SYN scan required root privileges.

Therefore, a TCP connect scan was used instead:

nmap -sT 192.168.0.0/24

The "-sT" scan performs TCP connections to determine whether ports are open and does not require root privileges in this environment.

6. Scan Results

Host: "192.168.0.1"

The following TCP ports were identified as open:

Port| Service| General Purpose
22/tcp| SSH| Secure remote administration
53/tcp| DNS| Domain name resolution
80/tcp| HTTP| Web-based services/interfaces
1900/tcp| UPnP| Network device/service discovery

Nmap reported 996 other scanned TCP ports as closed.

Host: "192.168.0.105"

No open TCP ports were detected among Nmap's default 1,000 scanned TCP ports.

Nmap reported:

1,000 closed TCP ports.

7. Security Analysis

Port 22 - SSH

SSH is commonly used for secure remote administration. An exposed SSH service can increase the attack surface of a device if it is unnecessarily accessible or poorly configured.

Security measures can include strong authentication, disabling unnecessary remote access, restricting access to trusted devices, and keeping the service updated.

Port 53 - DNS

DNS is used to resolve domain names into IP addresses. A DNS service on a router can be completely normal because routers may provide DNS-related services to devices on the local network.

However, DNS services should be appropriately configured and should not provide unnecessary external access.

Port 80 - HTTP

HTTP is commonly used for web-based interfaces and services. Unlike HTTPS, ordinary HTTP does not provide encryption for the HTTP connection itself.

If an administrative interface is exposed through HTTP, it should be properly protected and, where appropriate, HTTPS should be preferred.

Port 1900 - UPnP

UPnP allows devices on a network to discover and communicate with compatible services automatically. It can be useful in home networks, but unnecessary UPnP exposure can increase the overall attack surface.

If UPnP is not required, disabling it can reduce unnecessary network exposure.

Important Observation

An open port does not automatically mean that a device is vulnerable. An open port simply indicates that a network service is accepting connections. Determining whether a vulnerability exists would require additional authorized security testing and configuration analysis.

8. Results File

The Nmap scan results were saved as:

"task1_scan.txt"

The file was committed to Git and uploaded to a GitHub repository for documentation and future reference.

9. Limitations

- The original task recommended a TCP SYN scan ("-sS"), but this required root privileges in the Android/Termux environment.
- A TCP connect scan ("-sT") was therefore used.
- The scan covered Nmap's default 1,000 most common TCP ports rather than all 65,535 TCP ports.
- Device identification was based primarily on IP addresses and scan behavior, so the identity of "192.168.0.1" as the router is an observation rather than a confirmed hardware identification.
- Wireshark packet analysis was not performed because it was optional.

10. Conclusion

This task provided practical experience with basic network reconnaissance using Nmap. The scan identified two active devices on the local network and found four open TCP services on "192.168.0.1", while no open ports were detected among the default 1,000 TCP ports scanned on "192.168.0.105".

The task demonstrated how open ports can reveal network services and contribute to a device's attack surface. It also highlighted the importance of understanding the limitations of scanning tools and adapting techniques to the permissions and environment available.

11. Evidence

The original Nmap output is stored in:

"task1_scan.txt"

The scan results were also uploaded to the associated GitHub repository as part of the project documentation.
