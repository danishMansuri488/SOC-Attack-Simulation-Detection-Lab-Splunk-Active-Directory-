# Incident Report

## SOC Attack Simulation & Detection Lab using Splunk Enterprise, Active Directory & Sysmon

---

# 1. Incident Overview

| Field | Details |
|--------|---------|
| Incident ID | IR-001 |
| Incident Title | Brute Force Login Attempt Detection |
| Incident Category | Authentication Attack |
| Severity | Medium |
| Status | Resolved |
| Detection Platform | Splunk Enterprise |
| Log Source | Windows Security Event Logs |
| Windows Event ID | 4625 |
| MITRE ATT&CK Technique | T1110 – Brute Force |
| Analyst | Danish Mansuri |
| Investigation Date | July 2026 |

---

# 2. Executive Summary

During the implementation of the **SOC Attack Simulation & Detection Lab**, a brute-force authentication attack was simulated against a Windows domain user account to validate the effectiveness of the monitoring and detection environment.

Multiple failed login attempts generated Windows Security Event ID **4625**, which was collected through Splunk Universal Forwarder and forwarded to Splunk Enterprise. The configured detection rule identified repeated failed authentication attempts and automatically triggered a security alert.

The incident was investigated using Search Processing Language (SPL) queries, Windows Security Event Logs, and dashboard visualizations. The investigation confirmed that the activity was intentionally generated within the laboratory environment for educational purposes and did not impact any production systems.

---

# 3. Detection Details

The incident was detected using an automated Splunk alert configured to monitor repeated failed authentication attempts.

### Detection Query

```spl
index=main EventCode=4625
| stats count by Account_Name
| where count > 5
```

### Detection Logic

The alert continuously monitors Windows Security Event ID **4625**.

When the number of failed authentication attempts exceeds the configured threshold, Splunk Enterprise automatically generates an alert for SOC analyst review.

---

# 4. Investigation Process

The following investigation methodology was performed after the alert was triggered.

### Step 1 – Alert Review

The generated alert was reviewed within Splunk Enterprise to verify the detection time, affected user account, and event count.

### Step 2 – Event Verification

Windows Security Event Logs were examined to confirm that Event ID **4625** represented failed authentication attempts.

### Step 3 – Log Analysis

Additional SPL searches were executed to determine:

- Number of failed login attempts
- Target user account
- Source host
- Event timestamps
- Related authentication events

### Step 4 – Root Cause Analysis

The investigation confirmed that the activity originated from a manually simulated brute-force attack performed within the laboratory environment.

### Step 5 – Incident Validation

No successful compromise occurred.

No unauthorized access was obtained.

The detection rule functioned exactly as expected.

---

# 5. Evidence Collected

The following evidence was used during the investigation.

- Windows Security Event Logs
- Splunk Search Results
- Failed Login Dashboard
- Failed Login Trend Dashboard
- Brute Force Detection Alert
- Latest Security Events Panel

These artifacts confirmed that the generated attack was successfully detected and recorded.

---

# 6. Impact Assessment

Since the activity occurred inside an isolated virtual laboratory, there was no operational impact.

If this attack occurred within a production environment, potential risks could include:

- Password guessing attacks
- Unauthorized account access
- Account lockout
- Credential compromise
- Privilege escalation after successful authentication

---

# 7. MITRE ATT&CK Mapping

| Tactic | Technique | Technique ID |
|---------|-----------|--------------|
| Credential Access | Brute Force | T1110 |
| Initial Access | Valid Accounts (Potential Follow-up) | T1078 |

This mapping aligns the simulated attack with the MITRE ATT&CK Framework, demonstrating how enterprise SOC teams classify adversary behavior.

---

# 8. Recommendations

Based on the investigation, the following security recommendations are suggested:

- Enforce strong password policies.
- Configure account lockout thresholds.
- Enable Multi-Factor Authentication (MFA).
- Continuously monitor failed authentication attempts.
- Review privileged account activities regularly.
- Configure automated SIEM alerts for authentication anomalies.
- Conduct periodic security log reviews.

---

# 9. Lessons Learned

This investigation reinforced several important SOC practices.

- Windows Security Event Logs provide valuable authentication visibility.
- Automated SIEM alerts significantly reduce detection time.
- SPL queries simplify log analysis and investigation.
- Dashboards improve situational awareness during security monitoring.
- Combining Active Directory, Sysmon, and Splunk provides comprehensive visibility into Windows environments.

---

# 10. Conclusion

The simulated brute-force attack was successfully detected, investigated, and validated using Splunk Enterprise. The configured dashboards, SPL queries, and automated alerts accurately identified suspicious authentication activity and demonstrated a complete SOC monitoring workflow.

This incident report highlights practical experience with Windows security monitoring, SIEM implementation, threat detection, and incident investigation. The project closely reflects real-world responsibilities performed by Security Operations Center (SOC) analysts and demonstrates hands-on experience with enterprise security technologies.

---

## Prepared By

**Danish Mansuri**

Master of Computer Applications (Cyber Security & Digital Forensics)

SOC Attack Simulation & Detection Lab

July 2026
