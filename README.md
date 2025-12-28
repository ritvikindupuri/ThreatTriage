# Cloud-Native AI Security Triage Agent: SOC Automation & Response

## Project Overview

This project implements a cloud-native security triage application that models real-world SOC (Security Operations Center) and SOAR (Security Orchestration, Automation, and Response) workflows. It is designed to ingest manually entered JSON threat alerts—formatted as AWS GuardDuty and CloudTrail logs—and orchestrate a team of specialized AI agents to automate the analysis, classification, and response recommendation process.

The system transforms low-level JSON alerts into explainable, analyst-ready incident reports, bridging the critical gap between raw telemetry and actionable incident response.

## Try the Workflow

If you want to try the workflow I created, use this link:
[Launch Cloud-Native AI Security Triage Agent](https://opal.google/?flow=drive:/1Lv4hLhh5ni14v7Kf9osOJPMzybdcZm_o&shared&mode=app)

---

## Technical Architecture

The application orchestrates a pipeline of specialized agents powered by Gemini 2.5 Flash (for high-speed normalization and mapping) and Gemini 2.5 Pro (for complex reasoning and credibility analysis).

<p align="center">
  <img src=".assets/Screenshot 2025-12-28 134726.png" alt="AI Agent Workflow Architecture" width="800"/>
  <br>
  <em>Figure 1: Multi-Agent Orchestration Workflow for Automated Triage</em>
</p>

### Agent Pipeline
1.  **Normalize & Summarize Agent (Gemini 2.5 Flash):**
    * Ingests raw, nested JSON alerts provided by the user.
    * Parses and normalizes critical fields (Source IP, IAM Role, ARN, Event Time).
    * Generates a concise, human-readable summary of the security event.

2.  **MITRE ATT&CK Mapping Agent (Gemini 2.5 Flash):**
    * Analyzes behavioral patterns (e.g., AssumeRole, CreateAccessKey).
    * Maps observed actions to specific MITRE ATT&CK Cloud Matrix techniques (e.g., Account Manipulation, Cloud Infrastructure Discovery).

3.  **Credibility Analysis Agent (Gemini 2.5 Pro):**
    * Performs deep contextual reasoning on risk factors.
    * Evaluates indicators such as Tor exit node usage, MFA status, geographical anomalies, and API call velocity to assign a "Credibility Score."

4.  **Classification & Response Agent (Gemini 2.5 Flash):**
    * Categorizes the alert (False Positive, Benign Suspicious, Confirmed Threat).
    * Selects the appropriate response playbook (Ignore, Monitor, Isolate, Escalate to Tier-2).

5.  **Reporting Agent:**
    * Synthesizes all agent outputs into a structured SOC report.
    * Generates both a UI-friendly Executive Summary and a machine-parsable JSON artifact for SIEM integration.

---

## Capabilities & Output

The system produces a comprehensive Security Triage Report that mimics a Tier-1 Analyst's output but is generated in seconds.

### 1. Executive Summary & Indicators
The dashboard provides an immediate "at-a-glance" assessment, highlighting the Alert Classification, Credibility Score, and Recommended Response. Key Indicators of Compromise (IoCs) like malicious IPs and compromised Access Keys are extracted for rapid blocking.

<p align="center">
  <img src=".assets/Screenshot 2025-12-28 142443.png" alt="Executive Summary Dashboard" width="800"/>
  <br>
  <em>Figure 2: Executive Summary displaying Threat Classification and Key Indicators</em>
</p>

### 2. Transparent Decision Flow & Telemetry
Unlike "black box" AI tools, this system provides a Transparent Decision Flow. It outlines exactly why the AI flagged the event, mapping the logic from the initial Normalization step through to the MITRE mapping. It also visualizes the raw event timeline to allow human analysts to verify the AI's findings.

<p align="center">
  <img src=".assets/Screenshot 2025-12-28 142512.png" alt="Detailed Event Timeline and Recommendations" width="800"/>
  <br>
  <em>Figure 3: CloudTrail Event Timeline and Step-by-Step Response Playbook</em>
</p>

---

## Technology Stack

* **Platform:** Google Opal (Workflow Orchestration & App Builder)
* **AI Models:** Google Gemini 2.5 Flash (Latency-sensitive tasks), Gemini 2.5 Pro (Complex Reasoning)
* **Data Sources:** Manual JSON Input (GuardDuty & CloudTrail Schemas)
* **Security Standards:** MITRE ATT&CK Framework (Cloud Matrix)

---

## Conclusion

This project demonstrates the potential of GenAI to modernize Security Operations. By effectively modeling the cognitive workflow of a human analyst—normalization, contextualization, classification, and response—the system reduces alert fatigue and standardizes the triage process. It proves that AI agents can reliably handle the "heavy lifting" of Tier-1 analysis, allowing human security engineers to focus on complex threat hunting and incident containment.
