\# Home Lab



A self-hosted infrastructure project built to learn and demonstrate practical

networking, virtualization, and security concepts — clustered virtualization,

zero-trust-adjacent mesh networking, and network segmentation for media/traffic

isolation.



\## Overview



This lab runs on a clustered Proxmox VE environment, with workloads spanning

media services, AI inference, and network infrastructure. The focus throughout

has been correct security boundaries — scoping VPN protection to only the

traffic that needs it, segmenting untrusted workloads, and using cert-based

authentication for remote access rather than exposing services directly.



\## Architecture



\### Virtualization — Proxmox Cluster

A 3-node Proxmox VE cluster (mixed hardware: a Cisco UCS C220 M3 and two HP

EliteDesk 705 G4 Minis) hosts all VMs and containers. Clustering provides

quorum and centralized management across otherwise heterogeneous hardware.



\### Remote Access — Self-Hosted Mesh VPN (Headscale)

Rather than relying on a third-party control plane, remote access to lab

devices is handled by a self-hosted Headscale instance (an open-source

implementation of the Tailscale control server), running behind a

reverse-proxied, cert-secured connection. Devices enroll individually and

authenticate via signed certificates — no service is exposed to the open

internet without going through the mesh first.



\### Network Segmentation — VPN-Scoped Traffic (Gluetun)

Rather than routing all lab traffic through a VPN indiscriminately, only the

services that specifically require it are routed through a dedicated

VPN-gateway container (Gluetun). Everything else communicates over normal

LAN/HTTPS — avoiding a single point of failure and avoiding unnecessary

latency on traffic that gains no privacy benefit from tunneling.



\### Media Server — Jellyfin

A self-hosted media server, running as an isolated service with its own

library and transcoding pipeline (GPU-accelerated via NVENC).



\## Skills Demonstrated



\- Clustered virtualization and quorum management (Proxmox VE)

\- Self-hosted VPN mesh with certificate-based authentication (Headscale)

\- Network segmentation and scoped VPN routing (Gluetun)

\- Container orchestration and service isolation (Docker/LXC)

\- Infrastructure documentation and version control practices



\## Status



Actively maintained and expanding — current work includes Kubernetes (K3s)

deployment across the Proxmox cluster and Ansible-based configuration

management for reproducible builds.

