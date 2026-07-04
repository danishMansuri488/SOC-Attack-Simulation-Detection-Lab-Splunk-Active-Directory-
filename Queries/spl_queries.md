# SPL Queries

## Project
**SOC Attack Simulation & Detection Lab using Splunk Enterprise, Active Directory & Sysmon**

This document contains the Search Processing Language (SPL) queries used to monitor Windows Security Events, build dashboards, and configure alerts in Splunk Enterprise.

---

## Dashboard Queries

### 1. Successful Logins (Event ID 4624)

**Purpose:** Monitor successful user authentication.

```spl
index=main EventCode=4624
```

---

### 2. Failed Logins (Event ID 4625)

**Purpose:** Detect failed authentication attempts.

```spl
index=main EventCode=4625
```

---

### 3. Failed Login Trend

**Purpose:** Visualize failed login attempts over time.

```spl
index=main EventCode=4625
| timechart count
```

---

### 4. New User Created (Event ID 4720)

**Purpose:** Detect newly created user accounts.

```spl
index=main EventCode=4720
```

---

### 5. User Enabled (Event ID 4722)

**Purpose:** Monitor enabled user accounts.

```spl
index=main EventCode=4722
```

---

### 6. Password Reset (Event ID 4724)

**Purpose:** Detect password reset operations.

```spl
index=main EventCode=4724
```

---

### 7. Privileged Group Changes (Event ID 4728)

**Purpose:** Detect users added to privileged groups.

```spl
index=main EventCode=4728
```

---

### 8. Latest Security Events

**Purpose:** Display the latest collected security events.

```spl
index=main
| table _time host EventCode Account_Name
| sort - _time
```

---

### 9. Top Event Codes

**Purpose:** Display the most frequent Windows Event IDs.

```spl
index=main
| top EventCode
```

---

## Alert Queries

### 10. Brute Force Detection Alert

**Purpose:** Trigger an alert when failed login attempts exceed the defined threshold.

```spl
index=main EventCode=4625
| stats count by Account_Name
| where count > 5
```

---

### 11. New User Creation Alert

**Purpose:** Trigger an alert when a new user account is created.

```spl
index=main EventCode=4720
```

---

### 12. Privileged Group Change Alert

**Purpose:** Trigger an alert when a user is added to a privileged group.

```spl
index=main EventCode=4728
```

---

## Summary

These SPL queries were developed to support real-time monitoring, dashboard visualization, and automated threat detection within the SOC Attack Simulation & Detection Lab. They enable SOC analysts to identify authentication events, account management activities, and suspicious behavior efficiently using Splunk Enterprise.
