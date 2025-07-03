# Home-Network-Reconnaissance-Project

This project simulates a real-world internal reconnaissance and vulnerability assessment, conducted on a personal home network using **Nmap**. The goal was to discover active hosts, enumerate open ports and services, and analyze each device's exposure from a security perspective — similar to what a junior SOC analyst or penetration tester might do in a corporate network environment.


## Tools Used:

- **Kali Linux** (running in UTM on 2020 MacBook Pro)
- **Nmap 7.94**
- **Wi-Fi Subnet Range**: '192.168.X.X/24'


## Project Goals:

- Discover all active running hosts on my local network.
- Identify ports, status, services, and OS fingerprints on each device.
- Assess potential risks, exposure, or weak points.
- Document results in a report format.


## Devices Scanned 

| Device         | IP Address      | Open Ports    | Key Services   | OS Detected
|----------------|-----------------|-----------------|----------------|-----------
| MacBook Pro    | 192.168.X.X     |22, 53, 5000, 7000  | SSH, DNS, Airplay               |macOS (no exact match)
| iPhone 15 Plus | 192.168.X.X     |62078            | tcpwrapped sync               |IOS (not fingerprinted)                | Xbox One       | 192.168.X.X     |2869             |UPnP (IIS httpd)                |Windows 11 / Server 2008 (guess)
| HP Printer     | 192.168.X.X     |80, 443, 631, 8080, 9100|IPP, nginx, JetDirect | Embedded Linux (likely)             |
| AT&T DSL Router| 192.168.X.X     | 53, 80, 443       |DNSMasq, lighttpd                |Embedded linux (Arris)
----------------------------------------------------------------------------------


## Security Insights Per Device

### MacBook Pro
- SSH (22) exposed — secure login enabled.
- Ports 5000/7000 reveal AirPlay (RTSP service) — expected for macOS.
- DNS port 53 might indicate mDNS or Bonjour services.

### iPhone 15 Plus
- Only one port (62078) open — sync service for iTunes/Finder.
- tcpwrapped shows limited fingerprinting — secure.
- Very limited surface area — well-secured.

### Xbox One
- Port 2869 open — UPnP over Microsoft IIS httpd.
- OS guesses include Windows 11 and Server 2008.
- No critical services exposed — mostly passive media sharing.

### HP ENVY Photo 7158
- Exposes ports 80, 443, 631, 8080, and 9100.
- JetDirect (9100) can be abused in open networks.
- Admin panel accessible via HTTP and HTTPS — likely no default password enabled.
- TLS certificate is valid but self-signed.

### AT&T DSL Router
- DNSMasq 2.89 running on port 53.
- Admin interface open on 80 (HTTP) and 443 (HTTPS).
- Self-signed certificate from Arris — not safe for remote management.
- Port 111 filtered — a good sign of firewall enforcement.

---

## Summary of Risks

| Risk | Device | Description |
|------|--------|-------------|
| Default admin UI exposed | Router, Printer | Web login pages with no rate limiting or CAPTCHA |
| Streaming services exposed | MacBook | AirPlay (RTSP) ports open |
| JetDirect open | Printer | Allows raw print jobs without authentication |
| UPnP running | Xbox One | Common service but can be abused in some setups |

---

## Recommendations

- Disable unnecessary services (AirPlay, JetDirect, UPnP)
- Enforce strong passwords on printer/router interfaces
- Keep firmware updated (Router, Printer)
- Segment IoT devices on a separate VLAN
- Disable remote admin on your router unless absolutely needed

---















