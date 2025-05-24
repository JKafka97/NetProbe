# 🔍 NetProbe

**NetProbe** is a lightweight, CLI-based local network scanner and monitoring tool built with **Go**, **gRPC**, and **Bash**. It helps you discover active devices, open ports, basic services, and track changes on your LAN over time.

---

## ✨ Features

- 🔎 Fast IP & port scanning on your local network
- 📡 Device discovery (IP, MAC, hostname)
- 🔐 Service detection (HTTP, SSH, etc.)
- 📁 Store historical scan data (JSON or BoltDB)
- 🛠️ gRPC API for remote querying and integrations
- 🧪 Bash scripts for cron-based automation
- 🛡️ Optional security via tokens or TLS

---

## 📷 Example

```bash
$ netprobe scan
Scanning 192.168.1.0/24...
Found 5 devices.

$ netprobe list
IP              MAC               Hostname        Open Ports
192.168.1.2     aa:bb:cc:dd:ee:ff raspberrypi     22, 80
192.168.1.10    11:22:33:44:55:66 android-device  443

$ netprobe get 192.168.1.2
{
  "ip": "192.168.1.2",
  "mac": "aa:bb:cc:dd:ee:ff",
  "hostname": "raspberrypi",
  "ports": [22, 80],
  "services": {
    "22": "SSH",
    "80": "HTTP"
  }
}
```
## ⚙️ Architecture Overview

┌────────────┐         ┌────────────────┐
│ CLI/Bash   │───────▶│   gRPC Server   │
└────────────┘         └────────────────┘
     ▲                        ▲               
     │                        │               
┌────┴─────┐     ┌────────────┴────────────┐
│ Cron Job │     │     Scanner Engine      │
└──────────┘     └────────────┬────────────┘
                              ▼                
                      ┌───────────────┐       
                      │  Storage DB   │       
                      └───────────────┘

