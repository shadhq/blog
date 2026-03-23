---
title: "Docker Automation in Local Networks"
description: "Setting up a self-healing homelab with Docker Compose, Watchtower, and Portainer. Automating the updates of 20+ containers without breaking production."
pubDate: 2026-03-20
tags: ["homelab", "automation"]
---

# Docker Automation

Homelab management shouldn't be a full-time job. 

## The Stack

I use a simple stack to keep everything in sync:

1. **Watchtower**: For automated updates.
2. **Portainer**: For visual management.
3. **Uptime Kuma**: For health checks.

## The Config

```yaml
version: '3.8'
services:
  watchtower:
    image: containrrr/watchtower
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    command: --interval 3600 --cleanup
```

Everything stays updated, and I can sleep peacefully.
