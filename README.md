# ✨ Hi, I'm Nova

**Systems-minded builder working across infrastructure, Kubernetes, observability, networking, security, local AI, and automation.**

19 years in manufacturing systems 🏭 → building and operating **NovaLabs**, my self-hosted infrastructure and engineering lab.
Ontario, Canada 🍁

> **Philosophy:** I feel more comfortable driving my car when I understand how the brakes work.

---

## 🧪 NovaLabs

**NovaLabs is my living systems lab.**

It spans traditional infrastructure, networking, Kubernetes, observability, data engineering, local AI inference, automation, developer environments, security research, and experimental AI systems.

I use it to learn technologies by actually operating them: deploying workloads, breaking things, recovering them, instrumenting them, documenting them, and turning what worked into repeatable infrastructure.

| Domain                           | Current Environment                                                           |
| -------------------------------- | ----------------------------------------------------------------------------- |
| 🖥️ **Compute & Virtualization** | Proxmox VE 9 · NVIDIA DGX Spark · Raspberry Pi 5 · Debian · Ubuntu            |
| ☸️ **Container Platform**        | k3s · Kubernetes · Flux GitOps · Docker · containerd                          |
| 🧠 **Local AI**                  | NVIDIA GB10 · vLLM · LiteLLM · Hermes Agent · Ollama · Hugging Face · ComfyUI |
| 🎧 **Audio & Multimodal AI**     | Whisper · diarization · TTS · screen vision · persistent AI memory            |
| 📊 **Observability**             | Prometheus · Grafana · Loki · Alertmanager · Alloy · Telegraf · TimescaleDB   |
| 🌐 **Networking**                | OPNsense · VLANs · Pi-hole · Unbound · Traefik · Cloudflare Tunnel            |
| 🛡️ **Security**                 | Suricata · Twingate · SOPS + age · CVE tracking · network segmentation        |
| 🔧 **Platform Engineering**      | Forgejo · GitHub · Renovate · ChezMoi · Mise · systemd                        |
| 💾 **Data**                      | PostgreSQL · TimescaleDB · pgAdmin · persistent Kubernetes storage            |

---

# 🚀 What I'm Building

## ☸️ [Lovelace Cluster](https://github.com/calico88x/lovelace-cluster)

A heterogeneous **k3s cluster operated declaratively with Flux**.

```mermaid
flowchart TD
    forgejo["Forgejo<br/>Source of Truth"]
    github["GitHub<br/>Public Mirror"]
    flux["Flux<br/>GitOps Reconciliation"]

    control["lovelace<br/>Raspberry Pi 5<br/>ARM64 Control Plane"]
    worker["k8s-worker-01<br/>Debian x86_64<br/>Workload Node"]

    forgejo -->|mirror| github
    forgejo -->|desired state| flux

    flux --> control
    flux --> worker
```

Current platform features include:

* Raspberry Pi 5 ARM64 control plane
* Debian x86_64 workload node
* Forgejo as the primary Git service
* GitHub as an external public mirror
* Flux reconciliation from `main`
* Kustomize base + environment overlays
* SOPS + age encrypted Kubernetes secrets
* Traefik ingress
* persistent local storage
* node-bound workloads where appropriate
* Renovate dependency automation
* Prometheus-based observability
* Grafana dashboards
* centralized log collection with Alloy and Loki
* externally exposed applications through purpose-specific tunnels

The rule is simple:

> **Git is desired state. Kubernetes is current state.**

---

## ⚙️ Minecraft — All of Create

One of the largest stateful workloads running on Lovelace is a dedicated **modded Minecraft Create server**.

Rather than treating it like a manually managed game server, I built it as an actual Kubernetes application.

### Platform

* **Minecraft 1.21.1**
* **NeoForge**
* **All of Create**
* dedicated Kubernetes namespace
* StatefulSet deployment
* dedicated x86_64 worker scheduling
* 8-vCPU worker capacity for faster JVM and modpack startup
* separate lifecycle from my Paper Minecraft environment

### GitOps Delivery

```mermaid
flowchart LR
    change["Configuration Change"]
    branch["Forgejo<br/>Branch / Pull Request"]
    main["main"]
    flux["Flux"]
    kustomize["Kustomize"]
    sts["Minecraft<br/>StatefulSet"]

    change --> branch
    branch --> main
    main --> flux
    flux --> kustomize
    kustomize --> sts
```

The deployment includes:

* reusable Kustomize base
* cluster-specific staging overlay
* Flux-controlled reconciliation
* Forgejo as source of truth
* GitHub mirror
* encrypted configuration using SOPS + age
* Git-controlled server configuration
* declarative workload scheduling

### Persistent World Storage

Minecraft world data lives on dedicated persistent storage attached to the Kubernetes worker.

```mermaid
flowchart LR
    sts["Minecraft StatefulSet"]
    pvc["PersistentVolumeClaim"]
    pv["Retained PersistentVolume"]
    disk["Dedicated Worker Storage"]

    sts --> pvc
    pvc --> pv
    pv --> disk
```

The design includes:

* dedicated host storage
* static persistent volume
* persistent volume claim
* retained world data across pod recreation
* node affinity to keep storage and workload together
* Kubernetes-safe handling of stateful data

The server can be destroyed and recreated without treating the Minecraft world itself as ephemeral container state.

### External Access

Player traffic is exposed through a dedicated **Playit tunnel** rather than directly opening the game server to the Internet.

```mermaid
flowchart LR
    players["Players"]
    playit["Playit Tunnel"]
    service["Kubernetes Service"]
    server["Minecraft Create Server"]

    players --> playit
    playit --> service
    service --> server
```

Tunnel credentials remain encrypted in Git.

### Observability

The server is integrated into the wider NovaLabs monitoring stack.

I can observe:

* Minecraft service availability
* JVM / server metrics
* worker CPU and memory
* filesystem capacity
* storage utilization
* network activity
* node health
* public tunnel reachability

Logs are collected through **Grafana Alloy → Loki** and explored alongside infrastructure metrics in Grafana.

Minecraft telemetry is also included in the durable NovaLabs telemetry pipeline for historical analysis.

```mermaid
flowchart LR
    mc["Minecraft Create"]
    metrics["Metrics Exporters"]
    alloy["Grafana Alloy"]
    prom["Prometheus"]
    loki["Loki"]
    grafana["Grafana"]
    timescale["TimescaleDB"]

    mc --> metrics
    mc --> alloy

    metrics --> prom
    alloy --> loki

    prom --> grafana
    loki --> grafana

    prom -->|remote write| timescale
    timescale --> grafana
```

It is, perhaps unnecessarily, a **GitOps-operated, observable, stateful distributed-systems exercise disguised as Minecraft**.

And that is precisely why I built it.

---

## ⚡ [DGX Model Manager](https://github.com/calico88x/DGX-Model-Manager)

A **Compose-first model operations control plane for NVIDIA DGX Spark**.

Built to manage the operational side of local AI infrastructure:

* Hugging Face model inventory
* local model metadata inspection
* Ollama model discovery and management
* Hugging Face model search and downloads
* DGX-aware deployment planning
* vLLM deployment workflows
* SGLang deployment workflows
* llama.cpp support
* Docker Compose lifecycle management
* serving-engine discovery
* LiteLLM routing
* host and service diagnostics
* authentication
* role-based access
* API tokens
* audit logging
* multi-node DGX Spark architecture

The primary development target is an:

**NVIDIA DGX Spark · GB10 Grace Blackwell · 128 GB unified memory**

The goal is to treat local models like actual infrastructure rather than a collection of shell scripts.

---

## 🧰 [NovaLabs Dotfiles](https://github.com/calico88x/novalabs-dotfiles)

A centralized configuration and userland management system for the NovaLabs fleet using **ChezMoi + Mise**.

The architecture deliberately separates ownership:

| Layer                | Owner                |
| -------------------- | -------------------- |
| User configuration   | ChezMoi              |
| Portable CLI tooling | Mise                 |
| System components    | OS / platform vendor |

Current profiles cover:

`Proxmox` · `Docker` · `Pi-hole` · `UbuntuLab` · `Lovelace` · `k8s-worker-01` · `DGX Spark` · `OPNsense`

The repository manages:

* Bash environment
* Neovim + LazyVim
* pinned plugin state
* Tree-sitter tooling
* Rust toolchain
* Starship
* Fastfetch
* btop
* LazyGit
* LazyDocker
* tmux
* Vim
* Git configuration
* portable CLI utilities

Each server retains its own visual identity through generated:

* host-colored Starship prompts
* Fastfetch configurations
* btop themes

The repository is maintained primarily in **Forgejo**, with GitHub serving as the public mirror.

---

# 📊 Observation & Intelligence

A significant part of NovaLabs is not simply running services.

It is building the instrumentation required to **understand what those systems are actually doing**.

---

## 🤖 AI Inference Operations Dashboard

My DGX Spark is shared by several different inference consumers:

* my own interactive AI workloads
* Yuki / Hermes
* applications
* background services
* friends using private inference access

I built a Grafana dashboard specifically to see that shared inference pipeline as an operational system.

### Serving Layer

The dashboard observes:

* vLLM availability
* LiteLLM availability
* running requests
* waiting requests
* completed requests
* request success rate
* scheduler concurrency

### GPU & Memory

Because the GB10 uses a unified-memory architecture, memory behavior is particularly important.

I monitor:

* GPU utilization
* GPU temperature
* unified memory usage
* model-serving memory pressure
* KV-cache utilization

### Inference Performance

The dashboard exposes:

* token throughput
* prompt activity
* generation activity
* latency
* request volume
* model activity

### Multi-user Visibility

LiteLLM gives me visibility above the raw inference-engine layer.

That means I can distinguish traffic generated by different consumers rather than merely seeing:

> GPU busy.

I can observe inference usage associated with individual users and services, including separate Hermes activity.

```mermaid
flowchart LR
    nova["Nova"]
    yuki["Yuki / Hermes"]
    apps["Applications"]
    friends["Friends"]
    services["Background Services"]

    litellm["LiteLLM<br/>Routing + Attribution"]
    vllm["vLLM<br/>Inference Engine"]
    gb10["NVIDIA GB10<br/>Unified Memory"]

    prom["Prometheus"]
    grafana["Grafana<br/>Inference Operations"]

    nova --> litellm
    yuki --> litellm
    apps --> litellm
    friends --> litellm
    services --> litellm

    litellm --> vllm
    vllm --> gb10

    litellm -->|usage metrics| prom
    vllm -->|serving metrics| prom
    gb10 -->|hardware metrics| prom

    prom --> grafana
```

The result is an operational view of **who is using the inference platform, what the serving engine is doing, and what that workload is doing to the hardware**.

---

## 📺 TV Tuner & Streaming Observation

I built a dedicated observation layer around my **over-the-air TV streaming environment** while troubleshooting live-TV reliability problems with Plex and later migrating the workload to Jellyfin.

The tuner itself is an **HDHomeRun**, but the interesting part of the project became understanding the entire path a television stream takes through the lab.

```mermaid
flowchart LR
    antenna["OTA Antenna"]
    tuner["HDHomeRun<br/>Network TV Tuner"]
    network["NovaLabs Network"]

    plex["Plex"]
    jellyfin["Jellyfin"]

    clients["TV / Streaming Clients"]

    metrics["Prometheus<br/>System + Storage Metrics"]
    logs["Loki<br/>Application Logs"]
    grafana["Grafana<br/>TV Streaming Observation"]

    antenna --> tuner
    tuner --> network

    network --> plex
    network --> jellyfin

    plex --> clients
    jellyfin --> clients

    network --> metrics
    plex --> metrics
    jellyfin --> metrics

    plex --> logs
    jellyfin --> logs

    metrics --> grafana
    logs --> grafana
```

The project started because intermittent TV-streaming problems are difficult to diagnose from the player alone.

A stalled or degraded live stream could originate from several different layers:

* tuner reception
* network transport
* media-server behavior
* transcoding
* storage
* CPU or memory pressure
* client playback
* application instability

The observation environment lets me correlate streaming problems with the rest of the system instead of treating every playback failure as a generic Plex or Jellyfin problem.

I can examine things such as:

* media-server availability
* host CPU and memory
* filesystem capacity
* storage utilization
* network activity
* container health
* application logs
* tuner-related infrastructure
* transcoding behavior
* events occurring at the same time as a playback problem

This became particularly useful during my migration from **Plex to Jellyfin**, where I could compare behavior while changing the media-serving layer without changing the tuner or underlying network.

The result is less:

> *“The TV froze again.”*

and more:

> **“What changed in the system at the exact moment the stream failed?”**

That distinction is a recurring theme throughout NovaLabs: if a problem is intermittent, make it observable.

---

## 🕐 NovaLabs Time Service

Accurate time is one of those infrastructure dependencies that is almost invisible until it goes wrong.

I built a dedicated **time synchronization service and Grafana observation dashboard** to understand how clocks across NovaLabs behave rather than relying solely on a binary `synchronized: yes` status.

The system tracks time synchronization as measurable infrastructure.

```mermaid
flowchart TD
    upstream["Upstream NTP Sources"]

    timesvc["NovaLabs<br/>Time Service"]

    proxmox["Proxmox"]
    docker["Docker / Monitoring"]
    lovelace["Lovelace"]
    worker["k3s Worker"]
    hosts["Other NovaLabs Hosts"]

    exporter["NTP / Clock Metrics"]
    prom["Prometheus"]
    grafana["Grafana<br/>Time Observation"]

    upstream --> timesvc

    timesvc --> proxmox
    timesvc --> docker
    timesvc --> lovelace
    timesvc --> worker
    timesvc --> hosts

    timesvc --> exporter
    proxmox --> exporter
    docker --> exporter
    lovelace --> exporter
    worker --> exporter

    exporter --> prom
    prom --> grafana
```

The dashboard focuses on questions that ordinary system status commands do not answer very well:

* **Are the hosts synchronized?**
* **Which time source is currently being selected?**
* **What stratum am I operating at?**
* **How far is the local clock from its reference?**
* **How much correction is being applied?**
* **Is clock offset stable over time?**
* **Did synchronization behavior change after moving to another source?**

One of the most interesting measurements is the **observed clock offset**.

Rather than simply seeing that synchronization is active, I can watch the clock continuously move around its reference at microsecond-scale resolution and see how that behavior changes when the selected time source changes.

```mermaid
flowchart LR
    source["NTP Reference"]
    clock["Host Clock"]
    correction["Clock Discipline"]
    offset["Observed Offset"]
    history["Prometheus / TimescaleDB"]
    grafana["Grafana"]

    source --> correction
    clock --> correction

    correction --> clock
    correction --> offset

    offset --> history
    history --> grafana
```

This turns NTP from a background daemon into another observable distributed system.

The goal is not extreme precision for its own sake. It is to ensure that every system generating:

* metrics
* logs
* alerts
* database records
* Kubernetes events
* security events

has a trustworthy concept of **when something actually happened**.

That becomes increasingly important as NovaLabs grows into a distributed environment where events from many independent machines need to line up on the same timeline.


---

## 🛡️ CVE Tracker

Security work in NovaLabs includes a dedicated **CVE tracking dashboard**.

I use it to maintain visibility into vulnerabilities relevant to systems I actually operate rather than relying solely on generic vulnerability news.

The broader workflow includes:

* vulnerability tracking
* affected-system investigation
* CVE research
* remediation status
* patch documentation
* historical notes on vulnerabilities that were actually addressed

This is evolving into a broader **cyber intelligence pipeline** built around authoritative structured sources.

Current source work includes:

* CISA KEV
* FIRST EPSS
* ENISA EUVD
* ThreatFox
* privacy and regulatory intelligence sources

```mermaid
flowchart LR
    kev["CISA KEV"]
    epss["FIRST EPSS"]
    euvd["ENISA EUVD"]
    threatfox["ThreatFox"]
    privacy["Privacy / Regulatory Sources"]

    ingest["NovaLabs<br/>Intelligence Ingestion"]
    normalize["Normalize + Enrich"]
    datastore["Historical Data Store"]
    dashboard["CVE Tracker<br/>Dashboard"]

    kev --> ingest
    epss --> ingest
    euvd --> ingest
    threatfox --> ingest
    privacy --> ingest

    ingest --> normalize
    normalize --> datastore
    datastore --> dashboard
```

The long-term architecture separates vulnerability intelligence, exploitation likelihood, known-active exploitation, and privacy / sovereignty events while retaining historical state for analysis.

---

## 📈 NovaLabs Telemetry Warehouse

Live monitoring and historical telemetry serve different purposes.

So NovaLabs uses both.

```mermaid
flowchart TD
    hosts["Hosts + Services"]
    node["node_exporter"]
    apps["Application Exporters"]
    kube["Kubernetes Metrics"]

    prom["Prometheus<br/>Operational Monitoring"]
    grafana["Grafana<br/>Live Dashboards"]

    telegraf["Telegraf<br/>Remote Write Receiver"]
    timescale["TimescaleDB<br/>Durable Telemetry"]

    hosts --> node
    hosts --> apps
    hosts --> kube

    node --> prom
    apps --> prom
    kube --> prom

    prom --> grafana
    prom -->|remote write| telegraf

    telegraf --> timescale
    timescale -->|historical queries| grafana
```

Prometheus remains the live operational monitoring system.

TimescaleDB provides durable historical telemetry for:

* host health
* virtualization
* storage
* network behavior
* containers
* Minecraft
* infrastructure availability
* telemetry warehouse health

This allows Grafana to move beyond short retention windows and answer longer-term questions about how the lab behaves.

---

# 🧠 AI Systems

## 🐾 Yuki

Yuki is my locally hosted AI agent environment.

She runs through a private stack built around:

* Hermes Agent
* LiteLLM
* vLLM
* local speech services
* tools
* persistent memory
* local inference on DGX Spark

The larger goal is not simply to run an LLM locally.

It is to understand how to operate an **AI system**.

```mermaid
flowchart LR
    user["User"]
    speech["Speech"]
    tools["Tools"]
    memory["Persistent Memory"]

    agent["Hermes Agent"]
    routing["LiteLLM"]
    inference["vLLM"]
    gpu["DGX Spark / GB10"]

    observability["Prometheus + Grafana"]

    user --> agent
    speech --> agent
    tools <--> agent
    memory <--> agent

    agent --> routing
    routing --> inference
    inference --> gpu

    agent --> observability
    routing --> observability
    inference --> observability
    gpu --> observability
```

---

## 🎧 Many Ears

**Many Ears** extends Yuki beyond conversational text and gives her a pipeline for listening to and processing audio.

The project grew from a simple idea:

> What would an AI system need in order to actually listen?

The pipeline handles audio as something that can be processed, analyzed, and understood rather than simply played back.

Current work includes:

* audio ingestion
* music listening
* audio processing
* speech transcription
* speaker diarization
* processing longer recordings
* producing structured information that downstream AI systems can use

The architecture separates listening from reasoning.

```mermaid
flowchart LR
    audio["Audio / Music"]
    capture["Audio Capture"]
    processing["Audio Processing"]

    transcription["Transcription"]
    diarization["Speaker Diarization"]
    analysis["Audio Analysis"]

    context["Structured Context"]
    yuki["Yuki"]

    audio --> capture
    capture --> processing

    processing --> transcription
    processing --> diarization
    processing --> analysis

    transcription --> context
    diarization --> context
    analysis --> context

    context --> yuki
```

The important distinction is that Yuki does not need to perform every expensive audio operation inside the conversational model itself.

**Many Ears acts as the perception layer.**

---

## 👁️ [DGX Eyes and Ears](https://github.com/calico88x/DGX-Eyes-and-Ears)

A separate multimodal experiment exploring an AI that can share the user's visual and auditory environment.

```mermaid
flowchart LR
    subgraph pc["Windows Client"]
        mic["Microphone"]
        screen["Screen Capture"]
        client["Conversation Client"]
        memory["Persistent Memory"]
    end

    subgraph dgx["DGX Spark"]
        stt["Whisper STT"]
        vision["Vision-Language Model"]
        litellm["LiteLLM"]
        vllm["vLLM"]
        tts["Local TTS"]
    end

    mic --> stt
    screen --> vision

    stt --> client
    vision --> client
    memory <--> client

    client --> litellm
    litellm --> vllm

    vllm --> tts
    tts --> client
```

The client combines:

* microphone input
* screen capture
* speech recognition
* visual context
* conversational inference
* persistent memory
* local text-to-speech

The project explores what locally hosted conversational AI looks like when it can perceive the same environment as the person using it.

---

# 🛠️ Technology Domains

## ☸️ Platform, Containers & GitOps

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square\&logo=kubernetes\&logoColor=white)
![k3s](https://img.shields.io/badge/k3s-FFC61C?style=flat-square\&logo=k3s\&logoColor=black)
![Flux](https://img.shields.io/badge/Flux-5468FF?style=flat-square\&logo=flux\&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square\&logo=docker\&logoColor=white)
![containerd](https://img.shields.io/badge/containerd-575757?style=flat-square\&logo=containerd\&logoColor=white)
![Proxmox VE](https://img.shields.io/badge/Proxmox_VE_9-E57000?style=flat-square\&logo=proxmox\&logoColor=white)
![Traefik](https://img.shields.io/badge/Traefik-24A1C1?style=flat-square\&logo=traefikproxy\&logoColor=white)
![SOPS](https://img.shields.io/badge/SOPS-5C4EE5?style=flat-square)

## 🧠 AI & Inference

![NVIDIA](https://img.shields.io/badge/NVIDIA_DGX_Spark-76B900?style=flat-square\&logo=nvidia\&logoColor=white)
![GB10](https://img.shields.io/badge/Grace_Blackwell_GB10-76B900?style=flat-square\&logo=nvidia\&logoColor=white)
![vLLM](https://img.shields.io/badge/vLLM-FF6B6B?style=flat-square)
![LiteLLM](https://img.shields.io/badge/LiteLLM-5C7CFA?style=flat-square)
![Hermes Agent](https://img.shields.io/badge/Hermes_Agent-8B5CF6?style=flat-square)
![Ollama](https://img.shields.io/badge/Ollama-000000?style=flat-square\&logo=ollama\&logoColor=white)
![Hugging Face](https://img.shields.io/badge/Hugging_Face-FFD21E?style=flat-square\&logo=huggingface\&logoColor=black)
![ComfyUI](https://img.shields.io/badge/ComfyUI-222222?style=flat-square)

## 🎧 Audio & Multimodal AI

![Whisper](https://img.shields.io/badge/Whisper-412991?style=flat-square\&logo=openai\&logoColor=white)
![Diarization](https://img.shields.io/badge/Speaker_Diarization-7950F2?style=flat-square)
![TTS](https://img.shields.io/badge/Local_TTS-BD5FFF?style=flat-square)
![Vision](https://img.shields.io/badge/Vision_Language_Models-5C7CFA?style=flat-square)

## 📊 Observability & Telemetry

![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square\&logo=grafana\&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat-square\&logo=prometheus\&logoColor=white)
![Loki](https://img.shields.io/badge/Loki-F5A623?style=flat-square\&logo=grafana\&logoColor=white)
![Alertmanager](https://img.shields.io/badge/Alertmanager-E6522C?style=flat-square\&logo=prometheus\&logoColor=white)
![Grafana Alloy](https://img.shields.io/badge/Grafana_Alloy-F46800?style=flat-square\&logo=grafana\&logoColor=white)
![Telegraf](https://img.shields.io/badge/Telegraf-22ADF6?style=flat-square\&logo=influxdb\&logoColor=white)
![TimescaleDB](https://img.shields.io/badge/TimescaleDB-FDB515?style=flat-square\&logo=postgresql\&logoColor=black)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square\&logo=postgresql\&logoColor=white)

## 🌐 Networking & Security

![OPNsense](https://img.shields.io/badge/OPNsense-D94F00?style=flat-square\&logo=opnsense\&logoColor=white)
![Pi-hole](https://img.shields.io/badge/Pi--hole-96060C?style=flat-square\&logo=pi-hole\&logoColor=white)
![Unbound](https://img.shields.io/badge/Unbound-2F4F4F?style=flat-square)
![Suricata](https://img.shields.io/badge/Suricata_IDS%2FIPS-EF3B2D?style=flat-square)
![Twingate](https://img.shields.io/badge/Twingate-1E40AF?style=flat-square)
![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=flat-square\&logo=cloudflare\&logoColor=white)
![VLANs](https://img.shields.io/badge/VLANs-1BA0D7?style=flat-square\&logo=cisco\&logoColor=white)
![DNSSEC](https://img.shields.io/badge/DNSSEC-005A9C?style=flat-square)
![CVE Research](https://img.shields.io/badge/CVE_Research-B91C1C?style=flat-square)
![EPSS](https://img.shields.io/badge/EPSS-DC2626?style=flat-square)
![CISA KEV](https://img.shields.io/badge/CISA_KEV-991B1B?style=flat-square)

## 🔧 DevOps & Source Control

![Forgejo](https://img.shields.io/badge/Forgejo-FB923C?style=flat-square\&logo=forgejo\&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square\&logo=git\&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square\&logo=github\&logoColor=white)
![Renovate](https://img.shields.io/badge/Renovate-1A1F6C?style=flat-square\&logo=renovatebot\&logoColor=white)
![ChezMoi](https://img.shields.io/badge/ChezMoi-00AEEF?style=flat-square)
![Mise](https://img.shields.io/badge/Mise-6C5CE7?style=flat-square)
![systemd](https://img.shields.io/badge/systemd-000000?style=flat-square\&logo=linux\&logoColor=white)
![SSH](https://img.shields.io/badge/OpenSSH-4D4D4D?style=flat-square\&logo=openssh\&logoColor=white)

## 💻 Systems & Development

![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square\&logo=linux\&logoColor=black)
![Debian](https://img.shields.io/badge/Debian-A81D33?style=flat-square\&logo=debian\&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=flat-square\&logo=ubuntu\&logoColor=white)
![FreeBSD](https://img.shields.io/badge/FreeBSD-AB2B28?style=flat-square\&logo=freebsd\&logoColor=white)
![Arch Linux](https://img.shields.io/badge/Arch_Linux-1793D1?style=flat-square\&logo=archlinux\&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square\&logo=python\&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat-square\&logo=gnu-bash\&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat-square\&logo=go\&logoColor=white)
![Neovim](https://img.shields.io/badge/Neovim-57A143?style=flat-square\&logo=neovim\&logoColor=white)
![LazyVim](https://img.shields.io/badge/LazyVim-2E7DE9?style=flat-square\&logo=neovim\&logoColor=white)
![tmux](https://img.shields.io/badge/tmux-1BB91F?style=flat-square\&logo=tmux\&logoColor=white)

---

# 🔬 Current Focus

Right now I'm particularly interested in:

* **GitOps and Kubernetes platform engineering**
* **durable observability and telemetry architecture**
* **Grafana as an investigative interface rather than just a status screen**
* **local AI inference infrastructure**
* **multi-user AI serving**
* **AI observability and inference economics**
* **audio and multimodal AI perception**
* **cyber vulnerability intelligence**
* **Linux systems engineering**
* **networking and CCNA fundamentals**
* **security, segmentation, and infrastructure hardening**
* **self-hosted developer platforms**
* **reproducible workstation and server environments**
* **stateful workloads on Kubernetes**
* **turning manual operations into documented, version-controlled systems**

---

# 💡 How I Work

My background is in manufacturing systems, where reliability is not theoretical: equipment has to run, problems need root causes, and fixes need to survive the next shift.

I bring the same mindset to infrastructure.

**Inspect before changing.
Understand ownership boundaries.
Make the desired state explicit.
Automate the repeatable parts.
Instrument the system.
Observe what actually happened.
Document what you learned.**

Most of my projects start with:

> *“I want to understand how this works.”*

Eventually that tends to become a:

`repository` · `dashboard` · `runbook` · `service` · `pipeline` · `automation`

I don't want the lab to hide complexity from me.

I want it to make complexity **observable, explainable, and manageable**.

---

# 📚 Learning in Public

NovaLabs is intentionally a learning environment.

I use real infrastructure to explore:

* Kubernetes architecture and operations
* GitOps workflows
* routing and switching
* VLANs
* OSPF
* Linux administration
* PostgreSQL and time-series systems
* monitoring and telemetry
* infrastructure security
* vulnerability intelligence
* backend development
* containerization
* local AI systems
* inference serving
* multimodal AI
* audio processing

The repositories here aren't meant to present a magically finished environment.

They're a record of systems being:

**designed → deployed → observed → broken → understood → improved**

---

# 📬 Reach Me

* **GitHub:** [calico88x](https://github.com/calico88x)
* **Portfolio:** [NovaLabs](https://novalabs88.tech)
* **LinkedIn:** [Nova Peck](https://www.linkedin.com/in/nova-peck/)
* **Telegram:** [@nova88x](https://t.me/nova88x)
* **X:** [@xCalico88x](https://x.com/xCalico88x)

---

> *“Learn to manage AI, or AI will learn to manage you.”*
