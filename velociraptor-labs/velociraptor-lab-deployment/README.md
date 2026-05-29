# Deploying Velociraptor in a Small DFIR Lab Environment Using UTM

## Overview

This project documents the deployment of a small DFIR lab environment using Velociraptor within UTM virtual machines. The goal of the lab is to develop hands-on experience with enterprise-style DFIR tooling, endpoint visibility, artifact collection and investigative workflows within a controlled environment.

The lab currently consists of:

* A Linux-based Velociraptor Server
* Windows endpoint clients with the Velociraptor agent installed
* Isolated virtual networking using UTM
* Centralised artifact collection and endpoint visibility

---

## Objectives

* Deploy and configure a functional Velociraptor server
* Deploy endpoint agents to Windows clients
* Explore artifact collection and remote triage capabilities
* Develop familiarity with enterprise DFIR workflows
* Document deployment methodology and investigative findings

---

## Environment

| Component    | Purpose                               |
| ------------ | ------------------------------------- |
| UTM          | Virtualisation platform               |
| Linux VM     | Velociraptor Server                   |
| Windows VM   | Endpoint client                       |
| Velociraptor | DFIR and endpoint visibility platform |

---

## Planned Areas of Exploration

* Windows Event Log analysis
* Persistence mechanisms
* User activity artifacts
* Browser forensics
* PowerShell activity
* Threat hunting workflows
* Artifact collection and triage

---

## Repository Structure

```text
velociraptor-lab-deployment/
│
├── README.md
├── screenshots/
├── configs/
├── artifacts/
└── notes/
```

## Status

Lab deployment currently in progress.
