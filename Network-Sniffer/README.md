# Network Traffic Analyzer v1.0

A high‑performance, real‑time network packet sniffer and analyzer built in Python with Scapy, Rich, asyncio and threading. Designed to give you deep visibility into your network traffic protocol breakdown, geographic distribution, live packet stream and post‑capture exports - all in a sleek, console-based dashboard.

---

## Key Features

* **Multi‑Protocol Decoding**

  * IPv4, IPv6, TCP, UDP, ICMP, ARP
  * Automatic service detection (HTTP, HTTPS, DNS, SSH, FTP, SMTP, DHCP, NTP, etc.)

* **Live Interactive Dashboard**

  * Header panel with status, packet counts, data volume, runtime, interface & filter
  * Live packet table (time, direction, src/dst IP & location, protocol, size)
  * Protocol distribution chart
  * Geographic distribution chart (GeoIP lookup with caching)

* **Concurrent Capture & Analysis**

  * Non‑blocking capture thread writing to PCAP
  * Async packet queue processed by ThreadPoolExecutor workers
  * Smooth UI updates via Rich’s Live rendering

* **GeoIP Integration**

  * Uses MaxMind GeoLite2‑City database
  * Automatic country/region lookup with LRU cache (configurable size)
  * Graceful handling of private, unknown or lookup‑error addresses

* **Exports & Reporting**

  * **network\_capture.pcap** for full packet dump (Wireshark/tcpdump)
  * **network\_stats.json** with total packets, bytes, protocol & geo stats
  * Final summary panel on Ctrl+C with output file paths

* **Flexible Filtering**

  * BPF filters (`-f "tcp port 80"`, `-f "not port 22"`, etc.)
  * Source/destination IP or port filters via BPF expression
  * Built‑in validation of filter syntax

* **Robust Error Handling**

  * Missing GeoIP DB, write errors, invalid interface or filter
  * Network interface enumeration via netifaces
  * Fallbacks for IP detection and directory creation

---

## Prerequisites

* **Python 3.7+**
* **pip** package manager
* **MaxMind GeoLite2‑City.mmdb** (place under `GeoIP/GeoLite2‑City.mmdb`)
* **Root** privileges(sudo)

---

## Installation on Linux

1. **Clone the Repository**

   ```bash
   git clone https://github.com/jidne24/CodeAlpha-Task.git
   cd CodeAlpha-Task/Network-Sniffer
   ```

2. **MaxMind GeoLite2 Database**

   * If you already have `GeoLite2-City.mmdb` in `network-sniffer/GeoIP/`, skip this step.
   * Otherwise, download it from [Google Drive](https://drive.google.com/file/d/1QIzOCBCYsc2mAnJSbZI--MWcXZ-YGfG9/view?usp=sharing) and place it at:

     ```
     CodeAlpha-Task/Network-Sniffer/GeoIP/GeoLite2-City.mmdb
     ```

3. **Create & Activate a Virtual Environment** (recommended)

   ```bash
   # Linux/macOS
   python3 -m venv venv
   source venv/bin/activate
   ```

4. **Install Dependencies**

   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

   **requirements.txt** includes:

   ```
   scapy
   rich
   geoip2
   netifaces
   ```

---

## Usage

### Basic Capture (all traffic)

```bash
sudo python sniffer.py -i eth0
```

### Apply a BPF Filter

```bash
sudo python3 sniffer.py -i wlan0 -f "tcp port 443"
```

### Exclude SSH Traffic

```bash
sudo python3 sniffer.py -i any -f "not port 22"
```

Press **Ctrl+C** to stop capture and view export summary.

---

## Troubleshooting

````
| **Invalid BPF filter**             | Verify syntax or remove special characters<br>Use simple tests first     |
| **Missing GeoIP database error**   | Ensure `GeoIP/GeoLite2-City.mmdb` exists and is readable                |
| **Dependencies installation fails** | Update pip and retry:<br>`pip install --upgrade pip`<br>`pip install -r requirements.txt` |
````
---

## Output

- **Output/network_capture.pcap**  
Raw packet capture (open in Wireshark/tcpdump)

- **Output/network_stats.json**  
```json
{
  "total_packets": 1234,
  "total_bytes": 567890,
  "protocol_counts": { "TCP": 800, "UDP": 300 },
  "country_counts": { "United States": 400, "Local/Private": 834 },
  "timestamp": "2025-07-04T15:23:10.123456"
}
````

---


## License

This project is released under the **MIT License**.
Feel free to use, modify and distribute!

---

*Developed by Gidne Huda for CodeAlpha Cybersecurity Internship.*
