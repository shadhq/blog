---
title: "Homelab V2: Moving to Proxmox and K3s"
description: "Why I decided to migrate away from Docker Compose into a proper K3s Kubernetes cluster on Proxmox, and how it improved my uptime."
pubDate: 2026-03-22
tags: ["homelab", "infrastructure", "proxmox", "kubernetes"]
---

Welcome to the new blog. Today, we're talking about the transition from a simple Docker Compose setup to a full-fledged Kubernetes cluster using K3s on Proxmox VE.

> "A homelab is never finished, only abandoned."

## The Old Setup

Before this, I was running everything on a single Intel NUC with 32GB of RAM. The services were robust, but:
1. Updates meant downtime for the entire stack.
2. Managing secrets and backups was a manual, error-prone shell script.
3. It wasn't "enterprisey" enough for my taste.

```yaml
version: '3.8'
services:
  nginx:
    image: nginx:latest
    ports:
      - "80:80"
```

## Enter Proxmox

By installing Proxmox VE on the bare metal, I instantly gained the ability to spin up LXC containers and VMs. 

<div class="callout-info">
**Tip:** Always use ZFS for your Proxmox boot drive if you have enough RAM. The snapshot capabilities will save your weekend!
</div>

## The K3s Cluster

I deployed 3 VMs directly into Proxmox:
- 1 Control Plane node
- 2 Worker nodes

Bootstrapping K3s is incredibly simple. For the master node:

```bash
curl -sfL https://get.k3s.io | sh -
```

And for the workers:

```bash
curl -sfL https://get.k3s.io | K3S_URL=https://<master_ip>:6443 K3S_TOKEN=<node_token> sh -
```

<div class="callout-warning">
**Warning:** Ensure ports 6443 (apiserver) and 8472 (flannel) are open between your VMs! Otherwise your nodes will show as `NotReady`.
</div>

## Conclusion

Migrating to K3s took a weekend (and a lot of coffee), but the deployment pipelines and metrics (hello Prometheus/Grafana) are totally worth it. Now, if something crashes, Kubernetes just restarts it. Magic.
