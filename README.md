# Private DNS + WireGuard VPN

Self-hosted **WireGuard VPN** combined with **Technitium DNS Server** to provide secure remote access, private DNS resolution, and optional ad-blocking for VPN clients.

---

## ✨ Features

* Secure WireGuard VPN
* Private DNS using Technitium DNS Server
* Optional DNS-level ad blocking
* VPN clients automatically use the private DNS
* Web UI to monitor and manage DNS queries
* Easy QR code configuration for mobile devices

---

## 🧰 Requirements

* Ubuntu 22.04 or later
* Docker & Docker Compose
* Public IP address or domain name
* UDP port **51820** open on the firewall

---

## 📁 Project Structure

```
private-dns-wireguard/
├── docker-compose.yaml
├── README.md
└── .gitignore
```

---

## 🚀 Deployment

### 1️⃣ Clone the repository

```bash
git clone https://github.com/YOUR_GITHUB_USERNAME/private-dns-wireguard.git
cd private-dns-wireguard
```

---

### 2️⃣ Start the services

```bash
docker compose up -d
```

---

### 3️⃣ Verify containers

```bash
docker ps
```

You should see:

* `wireguard`
* `technitium-dns`

---

## 📱 VPN Client Setup

* QR codes are generated automatically inside the WireGuard container
* Example path:

```
/config/peer_phone/peer_phone.png
```

* Scan the QR code using the WireGuard mobile app
* DNS will be automatically set to the private VPN DNS IP (example: `10.8.0.1`)

---

## 🌐 Access Technitium DNS Web UI

From a connected VPN client, open:

```
http://10.8.0.1:5380
```

(Default credentials can be configured inside Technitium if required)

---

## 🌍 Enable Internet Access for VPN Clients

Run the following commands on the **host machine**:

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

```bash
sudo iptables -t nat -A POSTROUTING -s 10.8.0.0/24 ! -d 10.8.0.0/24 -j MASQUERADE
```

---

## 🛠 Troubleshooting

**Web UI not reachable**

* Ensure VPN is connected
* Check container logs:

```bash
docker logs technitium-dns
```

**DNS not resolving**

* Confirm `PEERDNS` is set to the VPN DNS IP
* Verify Technitium container is running

## 🤝 Contributions

Pull requests and improvements are welcome.
Feel free to fork and customize for your own environment.
