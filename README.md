# 🛡️ Home SOC Lab

A two-laptop, LAN-only security monitoring lab built to practice **SOC fundamentals, endpoint telemetry, SIEM investigation, and evidence-based documentation**.

A Windows endpoint sends events to a Wazuh single-node stack running on Linux. The dashboard makes those events searchable for investigation.

> This is an educational SOC lab and an evidence-backed MVP. It is not a production SOC and does not claim attack detection that has not been verified.

**Stack:** Wazuh 4.14.8 | Docker Compose | Windows 11 agent | EndeavourOS host

![Home SOC Lab architecture](screenshots/01-lab-architecture.png)

## 🎯 Portfolio Goals

This lab is being developed to demonstrate practical junior SOC skills:

- SIEM deployment and endpoint onboarding
- Windows event collection
- Security-event search and triage
- Evidence collection and documentation
- Incident-investigation workflow
- MITRE ATT&CK mapping as new cases are added
- Safe handling of screenshots, identifiers, and credentials

## 🎬 Demo

The animation below is a slideshow of three real, redacted Wazuh screenshots, **not** a recording of live interaction.

![Wazuh overview, active endpoint and Windows events](demo.gif)

| Overview | Windows endpoint |
| :---: | :---: |
| ![Overview showing one active agent and alert counts](screenshots/02-wazuh-overview.png) | ![Windows endpoint active in Wazuh](screenshots/03-active-endpoint.png) |

**Windows events:** Threat Hunting was filtered to the Windows agent and the last 24 hours. The captured results include a successful Windows logon and process creation events. These are routine telemetry, not proof of an attack.

![Recent Windows events in Threat Hunting](screenshots/04-windows-events.png)

## 🧱 Architecture

![Flow from endpoint activity to dashboard](diagrams/event-flow.png)

| Component | Role |
| --- | --- |
| Windows Wazuh Agent | Collects endpoint telemetry and connects to the manager over the local network. |
| Wazuh Server | Enrolls agents, receives events, decodes them, and evaluates rules. Filebeat forwards alerts. |
| Wazuh Indexer | Stores searchable Wazuh data. |
| Wazuh Dashboard | Provides agent status, event search, and Threat Hunting views. |

The three central components run as separate containers on the same Linux laptop using the official Wazuh Docker single-node deployment. Agent enrollment uses TCP 1515, agent events use TCP 1514, and the dashboard uses HTTPS 443. The indexer (9200) and manager API (55000) are bound to localhost on the host; no router port forwarding or public Internet exposure was configured.

## ✅ What Was Verified

- Wazuh Server, Indexer, and Dashboard containers were running.
- The indexer cluster reported GREEN status.
- The Windows agent registered and displayed as **Active**.
- The dashboard displayed recent events from the Windows endpoint.
- Observed events included successful Windows logon and process-creation telemetry.
- Filebeat connected to the indexer.
- A direct authenticated request to the manager API succeeded.

These checks were made locally on the Linux server. The Windows service startup mode (`Automatic`) and a direct browser connection **from Windows** are not evidenced by this repository. No screenshot of PowerShell has been fabricated.

## 🔎 Investigation Workflow

Future investigation cases in this repository will follow a consistent SOC-style structure:

```text
Alert / event
    ↓
Validate timestamp and affected host
    ↓
Identify user, process, IP, port, or other indicators
    ↓
Correlate related events
    ↓
Determine benign / suspicious / malicious context
    ↓
Map to MITRE ATT&CK when appropriate
    ↓
Document findings and recommended response
```

A reusable template is available in [investigations/INVESTIGATION_TEMPLATE.md](investigations/INVESTIGATION_TEMPLATE.md).

## 🧪 Planned Investigation Cases

These are **roadmap items**, not completed detections:

- Multiple failed logons / brute-force-style activity
- Suspicious PowerShell execution
- Network scanning inside the isolated lab
- Sysmon-enriched process investigation
- MITRE ATT&CK mapping for verified behaviors

Completed cases will be added only after evidence is captured and reviewed.

## 🚀 Reproduce Safely

1. Prepare two laptops on the same LAN: one Linux Docker host and one Windows endpoint.
2. Follow the official Wazuh Docker single-node deployment instructions for Wazuh 4.14.8.
3. Change default/demo credentials before making the dashboard accessible on the LAN.
4. Install the official Wazuh Agent on Windows and configure the Linux host as the manager.
5. Allow only the required local-network connections; do not expose the lab to the public Internet.
6. Confirm the endpoint is **Active**, then inspect real events in Threat Hunting.

This repository documents the lab and redacted evidence; it is not a one-command installer.

## 🔐 Evidence and Privacy

Screenshots were captured from the running Wazuh UI. The endpoint hostname and private IP were replaced with `WINDOWS-ENDPOINT` and `192.168.0.x` **in the images only**.

Do not publish:

- credentials or session URLs
- TLS private keys
- Wazuh agent keys
- raw event exports containing personal data
- local Docker configuration containing passwords

## 📌 Current Scope

The current MVP demonstrates:

- endpoint enrollment
- event transport
- searchable Windows telemetry
- SIEM visibility
- architecture documentation
- evidence handling

It does **not yet** include custom detection rules, Sysmon, Suricata, notifications, cloud infrastructure, a VPN, or public exposure.

## 🔭 Roadmap

- [ ] Add first documented SOC investigation
- [ ] Add Sysmon telemetry
- [ ] Map verified activity to MITRE ATT&CK
- [ ] Add an incident-report example
- [ ] Add additional detection and triage exercises
