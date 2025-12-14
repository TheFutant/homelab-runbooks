# Home Lab Runbooks

A small, practical collection of homelab runbooks focused on reliability, repeatability, and quick recovery.

This repo is intentionally **sanitized**: it documents the *how* without publishing the *where* (no real hostnames, IPs, internal domains, tokens, or secrets).

## What this covers

Core goals:
- Reliable home services: DNS/ad-blocking, Home Assistant, NAS/media, dashboards
- Experimentation: Docker containers, ESP32/OLED dashboards, Meshtastic/LoRa
- Documentation and repeatability: runbooks, backups, configs

Typical stack patterns you’ll see here:
- Pi-hole for DNS and local records
- BookStack wiki for documentation
- OpenMediaVault for storage + Docker workloads
- Home Assistant for automation

## Repo structure

```text
runbooks/
  homelab-at-a-glance.md
  bookstack.md
  pihole.md
  nas-omv.md
templates/
  docker-compose.yml        # optional, generic templates only
  env.example               # placeholders only, never real secrets
diagrams/
  (optional) network diagrams and sketches

