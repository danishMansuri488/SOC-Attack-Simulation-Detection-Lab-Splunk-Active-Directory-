# SPL Queries

This document contains the Search Processing Language (SPL) queries used in the **SOC Attack Simulation & Detection Lab using Splunk Enterprise, Active Directory & Sysmon**.

---

# 1. Successful Logins

### Objective
Monitor successful user authentication.

```spl
index=main EventCode=4624
```

---

# 2. Failed Logins

### Objective
Detect failed authentication attempts.

```spl
index=main EventCode=4625
```

---

# 3. Failed Login Trend

### Objective
Visualize failed login attempts over time.

```spl
index=main EventCode=4625
| timechart count
```

---

# 4. New User Created

### Objective
Monitor newly created user accounts.

```spl
index=main EventCode=4720
```

---

# 5. User Account Enabled

### Objective
Detect user account activation.

```spl
index=main EventCode=4722
```

---

# 6. Password Reset

### Objective
Monitor password reset activities.

```spl
index=main EventCode=4724
```

---

# 7. Privileged Group Changes

### Objective
Detect users added to privileged groups.

```spl
index=main EventCode=4728
```

---

# 8. Latest Security Events

### Objective
Display the latest security events.

```spl
index=main
| table _time host EventCode Account_Name
| sort - _time
```

---

# 9. Top Event Codes

### Objective
Display the most frequently occurring Event IDs.

```spl
index=main
| top EventCode
```

---

# 10. Brute Force Detection Alert

### Objective
Detect multiple failed login attempts.

```spl
index=main EventCode=4625
| stats count by Account_Name
| where count > 5
```

---

# 11. New User Creation Alert

### Objective
Generate an alert when a new user account is created.

```spl
index=main EventCode=4720
```

---

# 12. Privileged Group Change Alert

### Objective
Generate an alert when a user is added to a privileged group.

```spl
index=main EventCode=4728
```
