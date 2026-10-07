# SOC114 - Malicious Attachment Detected (Phishing)

| Field | Value |
|---|---|
| Date / Time | [FILL IN] |
| Platform | LetsDefend (Exchange alert, Beginner) |
| Severity | High |
| Verdict | **True Positive** |
| MITRE ATT&CK | T1566.002 Phishing: Spearphishing Link, T1204.002 User Execution: Malicious File (platform tag: T1598.001) |
| Related controls | PCI DSS 5.4.1 (anti-phishing), 12.10 (incident response); ISO 27001:2022 A.5.24-A.5.26 (incident management), A.8.7 (malware protection); SWIFT CSCF 6.1 (malware protection), 7.1 (incident response planning) |
| Affected assets | User: richard@letsdefend.io, Endpoint: [FILL IN hostname/IP] |

## 1. Executive summary

A phishing email with the subject "Invoice" was delivered to one user and the security gateway allowed it. The email contained a link to a malicious ZIP file, and the user opened it. The affected endpoint was identified and contained, and the email was removed. No command-and-control (C2) communication or further impact was found.

## 2. Alert details

| Item | Value |
|---|---|
| Subject | Invoice |
| Sender | accounting@cmail.carleton.ca |
| Recipient | richard@letsdefend.io |
| SMTP server IP | 49.234.43.39 |
| Device action | Allowed (delivered) |
| Playbook | Phishing Playbook - Security Analyst |

## 3. Investigation

| # | What I checked | Why | Finding |
|---|---|---|---|
| 1 | Email body and attachments/URLs | To find the delivery mechanism | Contains a URL pointing to a downloadable ZIP |
| 2 | Reputation of URL and IP | To confirm malicious intent | Classified malicious / network trojan. [FILL IN: tool used and detection ratio] |
| 3 | Sender and SMTP source | To check for spoofing or a compromised account | [FILL IN: SPF/DKIM/DMARC result; does 49.234.43.39 belong to the sender's domain?] |
| 4 | Mail delivery status | To determine exposure | Delivered to the user's mailbox |
| 5 | Whether the link was opened | To determine if the user was compromised | Opened. Endpoint identified. [FILL IN: evidence, e.g. proxy/endpoint log] |
| 6 | Post-click activity on the endpoint | To check for C2 or further compromise | No confirmed C2 communication or additional impact. [FILL IN: what you searched] |

## 4. Timeline

| Time | Event |
|---|---|
| [FILL IN] | Email received and allowed by the gateway |
| [FILL IN] | User opened the malicious link/file |
| [FILL IN] | Alert triggered |
| [FILL IN] | Endpoint contained |
| [FILL IN] | Email deleted from mailbox |

## 5. Root cause analysis

The user received and opened a convincing invoice-themed email. Contributing factors:
- The gateway allowed the email despite a malicious link.
- The link used a download-redirect pattern, which can hide the real payload location.
- User awareness: an unexpected "Invoice" email from an unknown sender was opened.

## 6. Impact and risk assessment

- **Confirmed:** one user opened the malicious content.
- **Not found:** C2 traffic or further activity.
- **Risk rating:** Likelihood High x Impact Medium = **High** before containment. Residual risk is **Low** after containment, provided the endpoint is clean. [ADJUST if you disagree]

## 7. Containment, eradication, recovery

- Isolated the affected endpoint.
- Deleted the phishing email from the mailbox.
- [FILL IN if done: checked for the same email in other mailboxes, blocked indicators, reset user credentials]

## 8. Indicators of compromise

| Type | Value | Context |
|---|---|---|
| URL | `https://download.cyberlearn.academy/download/download?url=https://files-ld.s3.us-east-2.amazonaws.com/c9ad9506bcccfaa987ff9fc11b91698d.zip` | Malicious download (network trojan) |
| IP | 172.67.166.172 | Flagged malicious |
| Sender | accounting@cmail.carleton.ca | Phishing sender |
| SMTP IP | 49.234.43.39 | Mail source |

Note: 172.67.166.172 appears to belong to Cloudflare's range (verify). If so, blocking by IP could affect unrelated sites, so block at the URL or domain level.

## 9. Recommendations

**Prevention**
- Enable URL rewriting and sandbox detonation of links in the email gateway (PCI DSS 5.4.1).
- Block downloads of ZIP/archive files from uncategorized or newly seen domains at the proxy.
- Enforce SPF, DKIM, and DMARC checks and quarantine failures.

**Detection**
- SIEM rule: alert when a user visits a URL containing a nested `url=` redirect to a file-hosting domain and then downloads an archive.
- SIEM rule: alert when a file downloaded from an email link is executed or extracted on the endpoint.

**Process**
- Add a step to the phishing playbook: search all mailboxes for the same sender, subject, and URL.
- Run targeted awareness training on invoice-themed phishing.

**Change request (example)**
- *Change:* block archive downloads from uncategorized domains at the web proxy. *Benefit:* stops a common malware delivery path. *Risk:* some legitimate downloads blocked, so provide an exception process.

## 10. Lessons learned

- A "True Positive" needs evidence at every step: reputation check, delivery, user click, and post-click activity.
- The alert was caught after the user clicked, so prevention at the gateway and proxy would reduce reliance on detection.
- IOC blocking must consider shared infrastructure such as CDNs.
