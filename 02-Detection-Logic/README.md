

# 🔍 Pillar 2: Detection Logic (GLS 500-User Baseline)

## Executive Summary
For the initial GLS rollout, the detection strategy focused on securing the primary attack vectors: Identity and Email. The goal was to establish high-fidelity alerts for "Low-Hanging Fruit" threats common in the logistics industry.

## Integrated Data Sources
To power these detections, I enabled the following native connectors:
* **Microsoft Entra ID:** To monitor authentication patterns and administrative changes.

To power the high-fidelity detections for the 500-user baseline, I orchestrated the integration of Microsoft Entra ID. By streaming Sign-in and Audit logs into the central workspace, we established visibility into the identity perimeter—specifically allowing for the detection of MFA-bypass techniques used against regional shipping staff.

* **Microsoft Defender XDR:** To ingest endpoint and email telemetry for cross-domain correlation.

## Baseline Analytics Rules
The following rules were configured to identify account takeover attempts and phishing activity:

### 1. MFA Fatigue (Multiple Rejected MFA Challenges)
* **Goal:** Detect attackers attempting to bypass Multi-Factor Authentication by spamming the user with push notifications.
* **Logic:** Alert triggers when a single user rejects multiple MFA prompts within a 10-minute window followed by a successful login.

### 2. Impossible Travel
* **Goal:** Identify potential credential harvesting where a user account is accessed from two geographically distant locations faster than a human can travel.
* **Logic:** Correlation of Entra ID sign-in logs with geographic IP data.

### 3. Mass Cloud File Deletion
* **Goal:** Protect GLS shipping manifests and proprietary logistics data from "wiper" attacks or disgruntled employee activity.
* **Logic:** Triggers on a high volume of file deletions in SharePoint or OneDrive within a short burst.

## Logic Validation
Each rule was manually tuned during the first 30 days to establish a baseline for "normal" logistics operations, reducing false positives from regional shipping staff accessing the portal via various VPN exit nodes.
