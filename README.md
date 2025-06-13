# Splunk SIEM: Failed LogIn IP Analysis

This project demonstrates how to use Splunk Cloud as a SIEM tool to identify brute-force attacks by analyzing Linux `auth.log` data.

---

## Tools Used
- Splunk Cloud (14-day trial)
- Sample SSH `auth.log`
- Search Processing Language (SPL)

---

## Objectives
- Ingest raw Linux SSH logs into Splunk
- Extract attacker IPs using `rex` field extractions
- Build a dashboard to monitor failed login attempts

---

## Key SPL Query

```spl
index=main sourcetype=linux_secure "Failed password"
| rex "from (?<ip>\d{1,3}(?:\.\d{1,3}){3})"
| stats count by ip
| sort -count
