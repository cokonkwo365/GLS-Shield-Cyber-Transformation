
# 🏛️ Pillar 1: Architecture Decisions (GLS 500-User Baseline)

## Executive Summary
For the initial deployment of the Guardian Shield initiative at the regional hub (500 staff), I architected a lean, centralized security ecosystem designed for rapid visibility and operational control.

## The Architecture Decision: Single-Workspace Design
**Problem:** GLS required immediate log visibility across identity and endpoints without the high cost of enterprise-scale data ingestion.
**Decision:** I manually deployed a single **Log Analytics Workspace** to act as the centralized data store for Microsoft Sentinel.

# 🏛️ Pillar 1: Architecture Decisions (GLS 500-User Baseline)

## Executive Summary
For the initial deployment of the Guardian Shield initiative at the regional hub (500 staff), I architected a lean, centralized security ecosystem designed for rapid visibility and operational control.

## The Architecture Decision: Single-Workspace Design
**Problem:** GLS required immediate log visibility across identity and endpoints without the high cost of enterprise-scale data ingestion.
**Decision:** I manually deployed a single **Log Analytics Workspace** to act as the centralized data store for Microsoft Sentinel.

### Why this Architecture?
1. **[span_1](start_span)Minimized Complexity:** A single-workspace model simplifies cross-source log correlation for a small hub[span_1](end_span).
2. **Cost Governance:** Utilizing a "Pay-as-you-go" model ensured GLS only paid for ingested data during the initial tuning phase.
3. **[span_2](start_span)Operational Speed:** A manual setup allowed for immediate connection of high-value data sources (Entra ID and Defender for Office 365) to protect against active phishing threats[span_2](end_span).

## Infrastructure Components
- **[span_3](start_span)[span_4](start_span)SIEM/SOAR:** Microsoft Sentinel (Enabled on LAW)[span_3](end_span)[span_4](end_span).
- **Data Storage:** Log Analytics Workspace (LAW) with 90-day retention.
- **Identity Security:** Microsoft Entra ID integration for centralized sign-in telemetry.
