# Vehicle-Cloud
V2V Mesh Implementation demonstration using B.A.T.M.A.N with NDN, ndn-pyhton-repo and PSync.

Project code can be found in the companion repository: [brewski/v2v-cloud](https://github.com/Brewski7/v2v-cloud).

# Vehicle-Cloud Demonstration Gallery

This repository contains visual demonstrations of the **Vehicle-to-Vehicle (V2V) communication prototype** developed as part of the *Vehicle-Cloud* project.  
The demonstrations illustrate both the **Named Data Networking (NDN) dissemination process** within a wireless mesh and the **functional proof-of-concept (PoC)** implementation operating on real Raspberry Pi nodes.

---

## 🧩 1. NDN Data Dissemination — A Visual Demo

### 🎬 Demo Video

<p align="center">
  <a href="https://github.com/Brewski7/Vehicle-Cloud/raw/main/demos/v2v-visual-demo-2x.mp4">
    <img src="demos/visual_thumbnail.png" alt="NDN Data Dissemination Demo" width="70%">
  </a>
  <br>
  <a href="https://github.com/Brewski7/Vehicle-Cloud/raw/main/demos/v2v-visual-demo-2x.mp4">
    <img src="https://img.shields.io/badge/▶️%20Click%20to%20View-Video-blue">
  </a>
</p>

### 🧠 Description
This visualization demonstrates how **Named Data Networking (NDN)** disseminates information across a multi-hop V2V mesh.  
Each node represents a vehicle equipped with the NDN Forwarding Daemon (NFD), exchanging **Interest** and **Data** packets via **B.A.T.M.A.N.** at the link layer.

**What the viewer observes:**
- Nodes issue Interests for named data (e.g., `/factory/config/v3`).  
- Interests propagate hop-by-hop through the wireless mesh.  
- Returned Data packets follow the reverse path, caching content at intermediate nodes.  
- Caching reduces redundant traffic and lowers latency for repeated requests.  

This demo visually contrasts NDN’s *content-centric* forwarding model with traditional *address-centric* networking.

---

### 🗣️ Narration Script
> I start an NDN instance on **bmw-x4**, hosting a 25 MB dummy data file.  
> Next, node **legion** requests this data — you can observe the Interest packets being sent and the Data being received.  
>  
> I then clear **legion**’s cache to remove any stored Data. Afterward, I request the same file from **m3**, but to demonstrate routing behavior, I synthetically disconnect **m3** from **x3**.  
> The Data now traverses from **x4 → legion → m3**, confirming that it’s not being served from legion’s cache.  
>  
> When **g3** requests the same data, it’s delivered directly from **legion’s cached storage**, showing in-network caching in action.  
>  
> Finally, I clear the Data previously received by **m3**. This time, something interesting happens — for a brief moment, **m3 receives Data simultaneously via both legion and x3**, demonstrating the **adaptive routing and redundancy** of **B.A.T.M.A.N.** and **NDN** working together.

---

## ⚙️ 2. Implemented PoC — A Functional Demo

### 🖼️ Abstracted View (CLI Representation)
![Functional Demo — Abstracted View](demos/Waldo%20GIF2.gif)

### 🎥 Full Video

<p align="center">
  <a href="https://raw.githubusercontent.com/Brewski7/Vehicle-Cloud/main/demos/v2v-functional-demo1p5.mp4">
    <img src="demos/functional_thumbnail.png" alt="Functional PoC Demo" width="70%">
  </a>
  <br>
  <a href="https://raw.githubusercontent.com/Brewski7/Vehicle-Cloud/main/demos/v2v-functional-demo1p5.mp4">
    <img src="https://img.shields.io/badge/▶️%20Click%20to%20View-Video-green">
  </a>
</p>


### 🧩 Description
This demonstration shows the **operational Proof-of-Concept (PoC)** running on multiple Raspberry Pi 4 nodes acting as vehicles in an ad-hoc Wi-Fi mesh.  
Each node executes the full V2V software stack — **B.A.T.M.A.N.-adv**, **NFD**, **PSync**, and **ndn-python-repo** — to exchange data autonomously without infrastructure.

**What the viewer observes:**
- Command-line output showing nodes booting, joining the mesh, and establishing NFD faces over `bat0`.  
- PSync synchronization events as updates are published and sequence numbers increment.  
- Repository operations where `ndn-python-repo` inserts and retrieves content dynamically.  
- All nodes converge to an identical dataset, confirming synchronized multi-hop operation.

The accompanying GIF abstracts the CLI interface for a quick overview, while the video provides a full operational walkthrough of the system.

---

### 🗣️ Narration Script
> The demo begins by showing the **2.4 GHz frequency** configuration — this detail becomes important later.  
>  
> I then start the **Vehicle-Cloud** services on several nodes. You can observe the **NDN prefixes** each node subscribes to, representing their active data namespaces.  
>  
> Next, I inject data files into the cloud through node **x3**.  
> The first file is a **common ECU configuration**, shared across all nodes — you can see synchronization updates propagate to every participant.  
>  
> Then, I insert **ADAS source files** intended only for nodes **i7** and **xm**. Notice how the other nodes ignore this update, even though they continue maintaining a consistent global state of the shared dataset.  
>  
> I confirm this by displaying each node’s **local storage directories**, which contain only the files relevant to that node’s assigned role.  
>  
> When nodes **i7** and **x1** join the network, **i7** immediately retrieves its previously published ADAS file along with the common ECU file, while **x1** receives only the ECU file. This demonstrates automatic synchronization upon joining.  
>  
> I then issue a small **command to bmw-x4** to display its **battery voltage**, showing remote command execution through the mesh.  
>  
> Finally, I disseminate a **frequency-switching script** to transition all nodes from **2.4 GHz** to **5 GHz** operation.  
> After the script is distributed, a follow-up command instructs all nodes to execute it simultaneously — demonstrating **coordinated distributed execution** within the V2V mesh.

---

> <sub>© 2025 Waldo Jordaan. All rights reserved.  
> Provided for academic demonstration under NDA.  
> Redistribution or modification prohibited.  
> See the [LICENSE](./LICENSE) file for details.</sub>


