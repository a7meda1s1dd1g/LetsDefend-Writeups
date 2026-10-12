# SOC141 – Phishing URL Detected

## Alert Information

| Field | Details |
|---|---|
| Platform | LetsDefend |
| Event ID | 86 |
| Alert | SOC141 – Phishing URL Detected |
| Severity | High |
| Event Time | 2021-03-22 21:23:12 (+03:00) |
| Source Host | EmilyComp |
| Source IP | `172.16.17.49` |
| Destination Domain | `mogagrocol.ru` |
| Destination IP | `91.189.114.8` |
| Device Action | Allowed |
| Verdict | True Positive |

## 1. Investigation

The alert was triggered after a user accessed a suspicious URL hosted on `mogagrocol.ru`. The proxy logs showed that the request was allowed, indicating that the URL was not blocked at the time of access.

**Requested URL:**

`http://mogagrocol.ru/wp-content/plugins/akismet/fv/index.php?email=ellie@letsdefend.io`

The URL was analyzed using VirusTotal, where 10 out of 90 security vendors flagged it as malicious or phishing-related. This supported the assessment that the URL was malicious.

The investigation confirmed that the user had accessed the URL on March 22, 2021, at 20:23:54 (+03:00).

### Evidence 1 – Alert Details

![Alert Details](screenshots/01-alert-details.png)

*The alert details identify the source endpoint, destination, requested URL, and allowed device action.*

### Evidence 2 – URL Reputation

![URL Analysis](screenshots/02-url-analysis.png)

*VirusTotal detection results supported the classification of the URL as malicious.*

## 2. Incident Response

The following response actions were recorded during the investigation:

- **Endpoint isolation:** Host `172.16.17.49` was contained to reduce the risk of further malicious activity.
- **URL and IP blocking:** The URL and associated IP address were added to the proxy and firewall blocklists.
- **Escalation:** The incident was escalated to Level 2 / Incident Response for further forensic investigation.

### Evidence 3 – Response Actions

![Incident Response](screenshots/03-incident-response.png)

*The response notes document the containment, blocking, and escalation actions.*

## 3. Conclusion

The investigation determined that the user accessed a malicious phishing URL that was allowed through existing filtering controls. The endpoint was isolated, blocking measures were applied, and the incident was escalated for further forensic review.

The alert was correctly classified as a **True Positive**. However, the available evidence does not independently confirm malware execution, credential theft, or successful endpoint compromise.

**Final Verdict:** True Positive – Malicious URL Accessed  
**Response Status:** Endpoint contained; URL/IP blocked; escalated to L2/IR.

---

*Lab Environment: LetsDefend | Role: Security Analyst*
