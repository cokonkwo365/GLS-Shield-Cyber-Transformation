# GLS-Shield-Cyber-Transformation
Enterprise security transformation for GLS. Showcasing detection &amp; SOAR automation via Microsoft Sentinel, Defender XDR, and KQL hunting strategies.

# 🛡️ GLS Shield: Enterprise Cyber Transformation

## Project Overview
This repository documents the end-to-end security transformation for **Guardian Logistics & Supply (GLS)**. The project follows a strategic progression from a 500-user manual baseline to a fully automated, 8,000-user global enterprise defense posture.

## 📈 Technical Progression
This portfolio is organized into four distinct pillars:

### [01. Architecture Decisions](./01-Phase-1-Foundations)
[cite_start]Establishing the centralized security "brain" (Log Analytics & Sentinel) to provide visibility across 45 global hubs[cite: 1, 2].

### [02. Detection Logic](./02-Detection-Logic)
[cite_start]Engineering high-fidelity KQL rules to identify lateral movement, credential harvesting, and "Living-off-the-Land" techniques[cite: 3, 4, 5].

### [03. Operational Handling](./03-Operational-Handling)
[cite_start]Standardizing the incident lifecycle: Triage, Containment, and Eradication within the Microsoft Defender portal[cite: 6, 7, 8].

### [04. Automation for Scale](./04-Automation-for-Scale)
[cite_start]Deploying Infrastructure as Code (ARM Templates) and SOAR Playbooks (Logic Apps) to manage enterprise-scale threat volume[cite: 9, 10, 11].

---
## 🛠️ Technology Stack
* **SIEM/SOAR:** Microsoft Sentinel
* **XDR:** Microsoft Defender for Endpoint, Identity, and Office 365
* **Identity:** Microsoft Entra ID
* **IaC:** Azure Resource Manager (ARM) Templates
