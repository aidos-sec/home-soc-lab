# SOC Investigation Template

Use this template for evidence-backed investigation cases added to the Home SOC Lab.

## Case Title

Short descriptive name, for example: `Multiple Failed Logons on WINDOWS-ENDPOINT`.

## Objective

What behavior is being investigated, and what question should the investigation answer?

## Lab Context

- **Endpoint:**
- **Data source:**
- **SIEM view / query:**
- **Time window:**

## Trigger / Initial Observation

Describe the alert or event that started the investigation.

## Evidence

Record only evidence that was actually observed.

| Field | Value |
| --- | --- |
| Timestamp | |
| Host | |
| User | |
| Source IP | |
| Destination IP | |
| Event / Rule ID | |
| Process | |
| Command line | |

Add redacted screenshots when useful.

## Analysis

Explain how the evidence was interpreted and which related events were checked.

Questions to consider:

- Is the activity expected for this host or user?
- Are there related events before or after it?
- Is there a successful action following repeated failures?
- Are the source and destination systems known?
- Does the process or command line fit normal activity?

## MITRE ATT&CK Mapping

Only add a technique when the observed behavior supports it.

- **Technique:**
- **Technique ID:**
- **Reason for mapping:**

## Assessment

Choose one and explain why:

- Benign / expected
- Benign test activity
- Suspicious
- Malicious
- Inconclusive

## Recommended Response

Document what a SOC analyst should verify, contain, or escalate next.

## Lessons Learned

What did this case teach about logging, detection, investigation, or response?

## Evidence Handling Notes

Confirm that screenshots and exported data were reviewed for credentials, private IPs, hostnames, usernames, session tokens, or other sensitive information before publication.
