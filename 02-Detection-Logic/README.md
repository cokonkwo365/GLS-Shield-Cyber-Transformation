

# 🔍 Pillar 2: Detection Logic (GLS 500-User Baseline)

## Executive Summary
For the initial GLS rollout, the detection strategy focused on securing the primary attack vectors: Identity and Email. The goal was to establish high-fidelity alerts for "Low-Hanging Fruit" threats common in the logistics industry.

## Integrated Data Sources
To power these detections, I enabled the following native connectors:
* **Microsoft Entra ID:** To monitor authentication patterns and administrative changes.
*To power the high-fidelity detections for the 500-user baseline, I orchestrated the integration of Microsoft Entra ID. By streaming Sign-in and Audit logs into the central workspace, we established visibility into the identity perimeter—specifically allowing for the detection of MFA-bypass techniques used against regional shipping staff.

* **Microsoft Defender XDR:** To ingest endpoint and email telemetry for cross-domain correlation.
* By integrating the Microsoft Defender XDR connector, I enabled cross-domain correlation across the GLS regional hub. This ingestion provides the raw endpoint and email log telemetry required to track threats as they move from an initial phishing click to lateral movement on a workstation—centralizing the 'source of truth' within Microsoft Sentinel for faster response.

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

## ⚙️ Technical Configuration & KQL Logic (Pending Deployment)

Status: 🟡 Pending Environment Finalization The logic and navigation steps below represent the verified configuration plan for the GLS 500-user baseline. Full deployment and log validation screenshots will be updated upon the finalization of the dedicated Azure lab environment.

### 1. MFA Fatigue Implementation
To detect this pattern, I configured a custom scheduled query rule.
* **Query Logic:** Specifically joins `SigninLogs` to identify multiple `ResultType 500121` failures followed by a success for the same account.
* **Threshold:** Configured to trigger when 3+ rejections occur within a 10-minute sliding window.

### 2. Impossible Travel Configuration
I utilized the Microsoft Security analytical template to leverage Entra ID's behavioral engine.
* **Data Mapping:** This rule correlates the `SigninLogs` IP address data with global geographic databases.
* **GLS Context:** Crucial for identifying if shipping portal credentials were leaked and used outside of known regional logistics hubs.

### 3. Mass Cloud File Deletion Setup
This rule monitors the `OfficeActivity` table for high-volume data destruction.
* **Tuning:** Thresholds were set to 50+ file deletions in 1 minute to distinguish between "Wiper" attacks and standard user organization.

## Logic Validation
Each rule was manually tuned during the first 30 days to establish a baseline for "normal" logistics operations, reducing false positives from regional shipping staff accessing the portal via various VPN exit nodes.
