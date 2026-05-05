# ✨ Hi, I'm Nova ✨

19 years in manufacturing 🏭 → pivoting into software & AI 💻  
Ontario, Canada 📍  
Will trade code for good food 🍕

---

## 🌱 About Me

- Former manufacturing generalist turned self-taught developer - I spent nearly two decades learning how to make things work under real-world pressure before I ever touched a compiler
- Running **two distinct homelabs**: an AI inference stack on an **HP ZGX Nano G1n (NVIDIA DGX Spark)** - 128 GB unified memory, GB10 Grace-Blackwell SoC - and a fully hardened network/security lab on **Proxmox VE 9**
- Learning backend development on [boot.dev](https://boot.dev) - working toward Python and Linux certifications
- Philosophy: I feel more comfortable driving my car when I understand how the brakes work

<p align="center">
  <img src="https://api.boot.dev/v1/users/public/073a4846-c225-4087-b67a-750322f884e9/thumbnail" width="400" />
</p>

---

## 🔧 What I'm Working On

| Project | What It Does |
|---------|-------------|
| **VM Homelab** 🖥️ | Proxmox VE 9 on bare metal - virtualized OPNsense router, multi-VLAN segmentation, Pi-hole + Unbound + DNSSEC, full Prometheus/Grafana/Loki monitoring stack, Suricata IDS/IPS, Twingate zero-trust remote access |
| **ZGX Homelab** | Fully self-hosted AI inference stack - vLLM · LiteLLM · OpenClaw · SearXNG · ComfyUI |
| **Yuki** 🐾 | On-device AI agent (Telegram bot) powered by Qwen3.6-35B-A3B NVFP4, running fully on the DGX Spark |
| **Luna** 🌙 | Cloud-resident AI agent running on a VPS - Yuki's counterpart and predecessor |
| **YKG** | Yuki Knowledge Graph - Kuzu embedded graph DB with automated extraction, 28-pattern query interface, and Obsidian sync |
| **NA-RT-VC** | Network-attached realtime voice changer - RVC inference over VBAN routed from the DGX Spark to my gaming PC (~30–40ms latency) |
| **Ant-Farm** | Cyberpunk-themed agentic sandbox world 🐜 inspired by [Generative Agents: Interactive Simulacra of Human Behavior](https://arxiv.org/abs/2304.03442) · Park et al., 2023 · [[source code]](https://github.com/joonspk-research/generative_agents) |
| **Dashboards** | Custom monitoring & info displays for the homelab ecosystem |
| **Learning** | Backend Development: Python, Go, Git, SQL, and more via boot.dev + CCNA via NetworkChuck Academy |

---

## 🖥️ Network & Security Homelab

A learning-first infrastructure project built around a single Proxmox VE 9 host. The goal is understanding every layer - no black boxes.

**Hardware:** Intel i5-12600K · 32 GB RAM · 931 GB NVMe · Intel i350-T4 quad-port NIC

**What's running:**

| Guest | Role | Notes |
|-------|------|-------|
| OPNsense | Router / Firewall | FreeBSD · IPS (Hyperscan) on WAN · multi-VLAN · pf |
| pihole | DNS | Pi-hole v6 · Unbound · DNSSEC · forced for all VLANs via NAT redirect |
| Docker LX | Monitoring hub | Prometheus · Grafana · Alertmanager · Loki · Promtail · cAdvisor |
| MotorTown (VM 108) | Game server | Ubuntu 24.04 + XFCE · Steam + Proton · auto-start chain · Telegram alerts |

**Security posture:**
- 🛡️ Suricata IDS on MGMT bridge (Proxmox host) + IPS on WAN (OPNsense) - ET Open + abuse.ch rulesets
- 🔒 Inter-VLAN isolation: IoT/LAN segments cannot reach management infrastructure
- 🔑 PVE firewall restricts to trusted IPs only - default DROP
- 🔍 CVE tracking and remediation documentation maintained for every patched vulnerability
- 📡 Zero-trust remote access via Twingate - no VPN, no open ports for admin

**Monitoring stack:** Prometheus (60s scrape · 30-day retention) → Grafana dashboards for every host · Alertmanager → Telegram bot "Max" for InstanceDown, HighCPU, HighMemory, LowDisk alerts · Loki log aggregation from 4 hosts, 7 streams · 30-day retention

---

## 🛠️ Tech Stack

**Languages & Scripting**  
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat-square&logo=gnu-bash&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white)

**Infrastructure & Containers**  
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Proxmox VE](https://img.shields.io/badge/Proxmox_VE_9-E57000?style=flat-square&logo=proxmox&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![Ubuntu](https://img.shields.io/badge/Ubuntu_24.04-E95420?style=flat-square&logo=ubuntu&logoColor=white)
![Debian](https://img.shields.io/badge/Debian_13_Trixie-A81D33?style=flat-square&logo=debian&logoColor=white)
![NVIDIA](https://img.shields.io/badge/NVIDIA_GB10-76B900?style=flat-square&logo=nvidia&logoColor=white)
![systemd](https://img.shields.io/badge/systemd-000000?style=flat-square&logo=linux&logoColor=white)
![SSH](https://img.shields.io/badge/SSH-4D4D4D?style=flat-square&logo=openssh&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)

**AI / Inference Stack**  
![vLLM](https://img.shields.io/badge/vLLM-ff6b6b?style=flat-square)
![LiteLLM](https://img.shields.io/badge/LiteLLM-5C7CFA?style=flat-square)
![OpenClaw](https://img.shields.io/badge/OpenClaw-orange?style=flat-square)
![SGLang](https://img.shields.io/badge/SGLang-9B59B6?style=flat-square)
![ComfyUI](https://img.shields.io/badge/ComfyUI-222222?style=flat-square)
![Ollama](https://img.shields.io/badge/Ollama-404040?style=flat-square)
![Open WebUI](https://img.shields.io/badge/Open_WebUI-000000?style=flat-square)
![Hugging Face](https://img.shields.io/badge/Hugging_Face-FFD21E?style=flat-square&logo=huggingface&logoColor=black)

**Databases & Memory**  
![KuzuDB](https://img.shields.io/badge/KuzuDB-005F8F?style=flat-square)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Obsidian](https://img.shields.io/badge/Obsidian-7C3AED?style=flat-square&logo=obsidian&logoColor=white)

**Networking & Security**  
![OPNsense](https://img.shields.io/badge/OPNsense-D94F00?style=flat-square&logo=opnsense&logoColor=white)
![pfSense](https://img.shields.io/badge/Suricata_IDS/IPS-EF3B2D?style=flat-square)
![Pi-hole](https://img.shields.io/badge/Pi--hole_v6-96060C?style=flat-square&logo=pi-hole&logoColor=white)
![Twingate](https://img.shields.io/badge/Twingate-1E40AF?style=flat-square)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![Loki](https://img.shields.io/badge/Loki-F5A623?style=flat-square&logo=grafana&logoColor=white)

**Tools & Platforms**  
![Telegram](https://img.shields.io/badge/Telegram-26A5E4?style=flat-square&logo=telegram&logoColor=white)

---

## 🐾 Quick Facts

- 🤖 Runs **Yuki** - an on-device AI cat-girl with cross-session memory (BM25 + vector hybrid), a knowledge graph, background memory consolidation ("dreaming"), and TTS
- 🎨 ComfyUI handles image & video gen locally (FLUX, Z-Image Turbo, SageAttention-patched for SM121A)
- 🧠 Documenting everything - living docs, versioned architecture diagrams, CVE research summaries, phased restore scripts, and lessons-learned logs
- 🔒 Zero-trust remote access (Twingate), multi-VLAN OPNsense, supply-chain-aware upgrade discipline, and a habit of reading CVE advisories before they hit the news cycle
- 🐧 Upgraded a production Proxmox host from PVE 8 → PVE 9 (Debian 12 → 13 Trixie) in-place - then wrote up everything that broke and why
- 🎮 Running a dedicated MotorTown game server - because debugging a Steam + Proton + SteamAPI_Init() failure chain counts as Linux sysadmin experience
- ⚡ Can probably troubleshoot your network setup

---

## 💡 How I Work

Coming from a trade background means I think in systems - what fails, why it fails, what it takes to keep it running at 3am. I apply the same mindset to software: document before you forget, test before you ship, and know what every layer is actually doing. I don't trust a system I can't explain.

I run recon before I touch anything. I read the config file before I edit it. I write down what I learned even when nothing broke. And when something does break, I write down that too.

> *"Learn to manage AI, or AI will learn to manage you."*

---

## 📬 Reach Me

- **GitHub:** [calico88x](https://github.com/calico88x)
- **Telegram:** [@nova88x](https://t.me/nova88x)
- **LinkedIn:** [@Nova Peck](https://www.linkedin.com/in/nova-peck-34626a211/)
- **X:** [@xCalico88x](https://x.com/xCalico88x)
- **YouTube:** [@pinkcalico88](https://www.youtube.com/@pinkcalico88)
- **Suno:** [@xjustnova88](https://suno.com/@xjustnova88)

---

*Thanks for stopping by! If you see something cool on this profile, just ask - I'm always happy to explain how it works.*
