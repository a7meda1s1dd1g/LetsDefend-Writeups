# LetsDefend Write-ups

Incident reports for SOC alerts I investigated on [LetsDefend](https://letsdefend.io). Each report follows a consistent structure: investigation steps, root cause analysis, risk assessment, MITRE ATT&CK mapping, links to compliance controls, and recommendations for prevention and detection.

The goal is to practice the full incident response workflow, not only reach a verdict, and to connect each alert to the security controls that would prevent or detect it.

## About me

["Communication System Engineering student in University of Science and Technology, building hands-on experience in security monitoring, incident response, and compliance (PCI DSS, ISO 27001, SWIFT CSP). Looking for a junior cybersecurity engineer or analyst role."]

- LinkedIn: [FILL IN]
- Email: [ahmedalsiddig2003@gmail.com]

## Alert index

| Alert | Type | Severity | Verdict | MITRE ATT&CK | Report |
|-------|------|----------|---------|--------------|--------|
| SOC114 | Phishing (malicious link/attachment) | High | True Positive | T1566.002, T1204.002 | [Read](alerts/SOC114-Malicious-Attachment-Phishing.md) |

*More reports are added as I complete them.*

## How each report is structured

1. **Executive summary** - a non-technical overview a manager can read in 30 seconds
2. **Alert details** - what triggered, source, destination, raw data
3. **Investigation** - each step with what I checked, why, and what I found
4. **Timeline** - sequence of events
5. **Root cause analysis** - how it happened and why existing controls missed it
6. **Impact and risk assessment** - likelihood x impact, residual risk
7. **Containment, eradication, recovery** - actions taken
8. **Indicators of compromise** - IPs, URLs, hashes, senders
9. **Recommendations** - prevention, detection (SIEM rule ideas), process, and change requests
10. **Lessons learned**

## Frameworks referenced

- **MITRE ATT&CK** - technique mapping for each alert
- **PCI DSS v4.0** - relevant requirements (e.g. 5.4.1 anti-phishing, 10 logging and monitoring, 12.10 incident response)
- **ISO/IEC 27001:2022** - relevant Annex A controls
- **SWIFT CSP / CSCF** - relevant controls for financial messaging environments

Control references are my own mapping for learning purposes and are checked against the published framework documents. They are not audit advice.

## Skills practiced

- Email and phishing analysis (headers, URLs, attachments, sender reputation)
- Threat intelligence lookups and IOC extraction
- Incident response: containment, eradication, recovery
- Root cause analysis and risk assessment
- Mapping incidents to MITRE ATT&CK and compliance controls
- Writing clear technical and executive-level reports
- Proposing detection logic and change requests

## Repository layout

```
.
├── README.md
├── alerts/      # one report per alert
└── images/      # sanitized screenshots used in reports
```

## Notes

- Reports describe my **methodology and reasoning**, not answer keys for the platform's challenges.
- Screenshots are cropped to remove personal information.
- I used AI tools to help with structure and formatting. The investigations and analysis are my own, and I verify the technical references.
- The IOCs listed come from a training platform and are not live threats.
