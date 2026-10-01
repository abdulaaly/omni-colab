# 🌐 OmniColab: Distributed Multi-Account GPU Swarm

**OmniColab** is an open-source orchestration layer that pools multiple free Google Colab accounts, volunteer community notebooks, and local hardware into a unified, high-availability GPU compute cluster with zero cloud costs.

---

## ⚡ Key Features

- **Multi-Account Pooling**: Connect 2 to 5+ Google account Colab sessions.
- **Sub-Second Auto-Failover**: When Account 1 hits daily GPU limits or idle sleep, traffic automatically shifts to Account 2 without breaking your running task.
- **Anti-Idle KeepAlive Heartbeat**: Prevents Colab from disconnecting during idle periods.
- **Community Swarm Training**: 1-click link allows open-source volunteers to contribute their GPU to train models collectively (Petals/Hivemind pattern).
- **Local Fallback Engine**: If all cloud Colabs sleep simultaneously, requests seamlessly route to your local CPU/heuristic engine so your workflow never halts.

---

## 🚀 Quickstart

### 1. Launch Worker Notebook on Your Google Accounts
Open `OmniColab_Worker.ipynb` in your Google Colab accounts (or click "Open in Colab") and click **Run All**.
Each account will output a Cloudflare or ngrok tunnel URL (e.g., `https://worker-1.trycloudflare.com`).

### 2. Start the OmniColab Coordinator
```bash
python coordinator.py
```
Register your worker tunnels:
```python
from coordinator import OmniColabCoordinator

coordinator = OmniColabCoordinator()
coordinator.add_worker("https://account1.trycloudflare.com", account_tag="Google Account #1")
coordinator.add_worker("https://account2.trycloudflare.com", account_tag="Google Account #2")

# Send inference or training batches
result = coordinator.dispatch("/act", {"goal": "Click Login", "elements": [...]})
```

---

## 📄 License
Apache-2.0 © abdulaaly
