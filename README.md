# Private DNS + WireGuard VPN

Self-hosted WireGuard VPN with Technitium DNS for private DNS, ad-blocking, and secure browsing.

## Features

- WireGuard VPN for secure connection
- Technitium DNS for private DNS & ad-blocking
- VPN clients use `10.x.x.x` as DNS
- Web UI for monitoring DNS queries
- Easy QR code setup for mobile clients

## Requirements

- Ubuntu 22.04+ server
- Docker & Docker Compose
- Public IP or domain
- Open UDP port 51820

## Deployment

1. Clone the repo:

```bash
git clone https://github.com/<your-username>/private-dns-vpn.git
cd private-dns-vpn


Start Docker Compose:

docker compose up -d


Verify containers:

docker ps


Connect VPN client using QR code /config/peer_phone/peer_phone.png
DNS will automatically be 10.x.x.x

Access Technitium Web UI:
http://IP:5380 (from VPN client)


Enable Internet Access for VPN clients
sudo sysctl -w net.ipv4.ip_forward=1
sudo iptables -t nat -A POSTROUTING -s 10.x.x.x/24 ! -d 10.x.x.x/24 -j MASQUERADE

Troubleshooting

Web UI not reachable: check VPN connection and container logs

DNS not resolving: ensure PEERDNS=10.x.x.x and Technitium is running
=======
# private-dns-wireguard
