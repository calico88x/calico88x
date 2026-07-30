# ✨ Hi, I'm Nova

**Manufacturing systems leader turned DevOps, networking, and local-AI builder.**

19 years in manufacturing 🏭 → building infrastructure, networks, and self-hosted AI systems 💻  
Ontario, Canada 🍁

---

## 🌱 About Me

- Former manufacturing generalist turned self-taught technologist — nearly two decades of making complex systems work under real-world pressure before I ever touched a compiler
- Running **two distinct homelabs**: a local-AI inference stack on an **HP ZGX Nano G1n (NVIDIA DGX Spark)** with 128 GB unified memory and a GB10 Grace Blackwell SoC, plus a hardened KVM, networking, and security lab on **Proxmox VE 9**
- Daily-driving **Arch Linux** with **Hyprland on Wayland**, Rofi, LUKS encryption, LVM, and a personalized dotfiles setup
- Running an Ubuntu-based Kubernetes environment with Rancher Desktop, nested virtualization, and K9s
- Studying CCNA networking with [NetworkChuck Academy](https://academy.networkchuck.com/start)
- Studying DevOps and Kubernetes with [KubeCraft](https://www.skool.com/kubecraft)
- Learning backend development through [boot.dev](https://boot.dev), with a focus on Python, Go, Linux, and systems fundamentals

> **Philosophy:** I feel more comfortable driving my car when I understand how the brakes work.

---

## 🔧 What I'm Working On

| Project | What It Does |
|---|---|
| **VM Homelab** 🖥️ | Proxmox VE 9 on bare metal with a virtualized OPNsense router, multi-VLAN segmentation, Pi-hole + Unbound + DNSSEC, Prometheus/Grafana/Loki observability, Suricata IDS/IPS, and Twingate zero-trust access |
| **ZGX Homelab** ⚡ | Fully self-hosted AI inference stack built around vLLM, LiteLLM, Hermes-Agent, SearXNG, and ComfyUI |
| **Yuki** 🐾 | On-device AI agent running through Hermes-Agent and Telegram, powered by Qwen3.6-35B-A3B NVFP4 on the DGX Spark |
| **Luna** 🌙 | Cloud-resident AI agent running with OpenClaw on a VPS — Yuki's counterpart and predecessor |
| **YKG** 🧠 | Yuki Knowledge Graph: a Kuzu embedded graph database with automated extraction, a 28-pattern query interface, and Obsidian synchronization |
| **Ant-Farm** 🐜 | Cyberpunk-themed agentic sandbox inspired by [*Generative Agents: Interactive Simulacra of Human Behavior*](https://arxiv.org/abs/2304.03442) by Park et al. ([source code](https://github.com/joonspk-research/generative_agents)) |
| **Dashboards** 📊 | Custom monitoring and information displays for the homelab ecosystem |
| **Learning** 📚 | Backend development with Python, Go, Git, and SQL; CCNA networking; and practical DevOps/Kubernetes engineering |

---

## 🖥️ Network & Security Homelab

A learning-first infrastructure project built around a single Proxmox VE 9 host. The goal is to understand every layer — no black boxes.

**Hardware:** Intel i5-12600K · 32 GB RAM · 931 GB NVMe · Intel i350-T4 quad-port NIC

### Core Services

| Guest | Role | Notes |
|---|---|---|
| **OPNsense** | Router / Firewall | FreeBSD · WAN IPS with Hyperscan · multi-VLAN routing · pf firewall |
| **Pi-hole** | DNS | Pi-hole v6 · Unbound · DNSSEC · DNS enforcement across VLANs through NAT redirect |
| **Docker LXC** | Observability hub | Prometheus · Grafana · Alertmanager · Loki · Promtail · cAdvisor |
| **Ubuntu (VM 105)** | Virtual desktop / Kubernetes | Ubuntu 24.04 · Rancher Desktop · Kubernetes · K9s · Docker |
| **MotorTown (VM 108)** | Game server | Ubuntu 24.04 · XFCE · Steam + Proton · automated startup chain · Telegram alerts |

### Security Posture

- 🛡️ Suricata IDS on the management bridge and IPS on the OPNsense WAN interface using ET Open and abuse.ch rulesets
- 🔒 Inter-VLAN isolation prevents IoT and LAN segments from reaching management infrastructure
- 🔑 Proxmox VE firewall restricts management access to trusted IPs with a default DROP policy
- 🔍 CVE tracking and remediation notes are maintained for every patched vulnerability
- 📡 Twingate provides zero-trust remote administration without exposing VPN or management ports

### Observability

Prometheus scrapes every 60 seconds with 30-day retention. Grafana provides dashboards across the environment, Alertmanager sends Telegram notifications for availability and resource alerts, and Loki aggregates logs from four hosts across seven streams.

---

## 🛠️ Tech Stack

### Languages & Web

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat-square&logo=gnu-bash&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white)
![HTML](https://img.shields.io/badge/HTML-E34F26?style=flat-square&logo=html5&logoColor=white)

### Infrastructure & Containers

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![Proxmox VE](https://img.shields.io/badge/Proxmox_VE_9-E57000?style=flat-square&logo=proxmox&logoColor=white)
![Rancher Desktop](https://img.shields.io/badge/Rancher_Desktop-0075A8?style=flat-square&logo=rancher&logoColor=white)
![K9s](https://img.shields.io/badge/K9s-4361EE?style=flat-square)

### Operating Systems & Desktop

![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![Arch Linux](https://img.shields.io/badge/Arch_Linux-1793D1?style=flat-square&logo=archlinux&logoColor=white)
![Wayland](https://img.shields.io/badge/Wayland-FFBC00?style=flat-square&logo=wayland&logoColor=black)
![Hyprland](https://img.shields.io/badge/Hyprland-58E1FF?style=flat-square)
![Ubuntu Server](https://img.shields.io/badge/Ubuntu_Server-E95420?style=flat-square&logo=ubuntu&logoColor=white)
![Ubuntu 26.04](https://img.shields.io/badge/Ubuntu_26.04-E95420?style=flat-square&logo=ubuntu&logoColor=white)
![Debian](https://img.shields.io/badge/Debian_13_Trixie-A81D33?style=flat-square&logo=debian&logoColor=white)

### Systems & Platform Engineering

![NVIDIA](https://img.shields.io/badge/NVIDIA_GB10-76B900?style=flat-square&logo=nvidia&logoColor=white)
![systemd](https://img.shields.io/badge/systemd-000000?style=flat-square&logo=linux&logoColor=white)
![SSH](https://img.shields.io/badge/SSH-4D4D4D?style=flat-square&logo=openssh&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)
![Vim](https://img.shields.io/badge/Vim-019733?style=flat-square&logo=vim&logoColor=white)
![tmux](https://img.shields.io/badge/tmux-1BB91F?style=flat-square&logo=tmux&logoColor=white)

### AI & Inference

![vLLM](https://img.shields.io/badge/vLLM-FF6B6B?style=flat-square)
![LiteLLM](https://img.shields.io/badge/LiteLLM-5C7CFA?style=flat-square)
![Hermes Agent](https://img.shields.io/badge/Hermes--Agent-8B5CF6?style=flat-square)
![OpenClaw](https://img.shields.io/badge/OpenClaw-F97316?style=flat-square)
![SGLang](https://img.shields.io/badge/SGLang-9B59B6?style=flat-square)
![ComfyUI](https://img.shields.io/badge/ComfyUI-222222?style=flat-square)
![Ollama](https://img.shields.io/badge/Ollama-404040?style=flat-square)
![Open WebUI](https://img.shields.io/badge/Open_WebUI-000000?style=flat-square)
![Hugging Face](https://img.shields.io/badge/Hugging_Face-FFD21E?style=flat-square&logo=huggingface&logoColor=black)

### Data, Backend & Knowledge Systems

![KuzuDB](https://img.shields.io/badge/KuzuDB-005F8F?style=flat-square)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Obsidian](https://img.shields.io/badge/Obsidian-7C3AED?style=flat-square&logo=obsidian&logoColor=white)

### Networking & Security

![OPNsense](https://img.shields.io/badge/OPNsense-D94F00?style=flat-square&logo=opnsense&logoColor=white)
![Suricata](https://img.shields.io/badge/Suricata_IDS%2FIPS-EF3B2D?style=flat-square)
![Pi-hole](https://img.shields.io/badge/Pi--hole_v6-96060C?style=flat-square&logo=pi-hole&logoColor=white)
![Twingate](https://img.shields.io/badge/Twingate-1E40AF?style=flat-square)

### Observability

![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![Alertmanager](https://img.shields.io/badge/Alertmanager-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![Loki](https://img.shields.io/badge/Loki-F5A623?style=flat-square&logo=grafana&logoColor=white)

### CCNA Networking Knowledge

![Cisco IOS](https://img.shields.io/badge/Cisco_IOS-1BA0D7?style=flat-square&logo=cisco&logoColor=white)
![VLANs](https://img.shields.io/badge/VLANs-1BA0D7?style=flat-square&logo=cisco&logoColor=white)
![Spanning Tree](https://img.shields.io/badge/Spanning_Tree-1BA0D7?style=flat-square&logo=cisco&logoColor=white)
![IPv4 Subnetting](https://img.shields.io/badge/IPv4_Subnetting-1BA0D7?style=flat-square&logo=cisco&logoColor=white)

### Tools & Platforms

![Telegram](https://img.shields.io/badge/Telegram-26A5E4?style=flat-square&logo=telegram&logoColor=white)

---

## 🐾 Quick Facts

- 🤖 I run **Yuki**, an on-device AI cat-girl with hybrid BM25 + vector memory, a knowledge graph, background memory consolidation, and TTS
- 🎨 ComfyUI handles local image and video generation with FLUX, Z-Image Turbo, and SageAttention patched for SM121A on GB10
- 🧠 I document everything: living documentation, versioned architecture diagrams, CVE research summaries, phased restore scripts, and lessons-learned logs
- 🔒 My infrastructure follows zero-trust access, multi-VLAN segmentation, supply-chain-aware upgrades, and CVE review before deployment
- 🐧 I upgraded a production Proxmox host from PVE 8 to PVE 9 and Debian 12 to Debian 13 Trixie in place, then documented what broke and why
- 🎮 I run a dedicated MotorTown server because debugging Steam, Proton, and `SteamAPI_Init()` failure chains absolutely counts as Linux administration
- 🎮 I also run a dedicated modded Minecraft server deployed via Kubernetes with persistent volume storage and Playitt.gg for external domain hosting
- ⚡ I can probably troubleshoot your network setup

---

## 💡 How I Work

Coming from a trade background means I think in systems: what fails, why it fails, and what it takes to keep it running at 3 a.m. I apply the same mindset to software and infrastructure — document before you forget, test before you ship, and understand what every layer is doing.

I run reconnaissance before I change anything. I read the configuration before I edit it. I document what I learned even when nothing broke — and when something does break, I document that too.

> *“Learn to manage AI, or AI will learn to manage you.”*

---

## 📬 Reach Me

- **GitHub:** [calico88x](https://github.com/calico88x)
- **Telegram:** [@nova88x](https://t.me/nova88x)
- **LinkedIn:** [Nova Peck](https://www.linkedin.com/in/nova-peck/)
- **X:** [@xCalico88x](https://x.com/xCalico88x)
- **Portfolio:** [NovaLabs](https://novalabs88.tech)

---

*Thanks for stopping by. If something on this profile looks interesting, ask — I'm always happy to explain how it works.*
