# SSH Failed Login Detection Test

## 1. Objective

Verify that the Ubuntu Jump Server records unsuccessful SSH authentication attempts in its system authentication logs.

## 2. Test Environment

- Operating System: Ubuntu Linux 26.04.1 LTS
- Server: Ubuntu Jump Server
- Username: josh
- Service: OpenSSH
- Log File: `/var/log/auth.log`

## 3. Test Procedure

Three intentional failed SSH login attempts were performed against the Jump Server using an incorrect password.

The authentication logs were examined using:

```bash
sudo grep -a "Failed password" /var/log/auth.log | tail -n 10
```

## 4. Test Results

**Status: Successful**

The authentication logs recorded all three unsuccessful SSH login attempts.

| Detail | Result |
|---|---|
| Failed attempts | 3 |
| Target account | josh |
| Source IP | 127.0.0.1 |
| Authentication method | SSH password |
| Date | November 19, 2026 |

### Recorded Events

- 17:11:31 UTC — Failed password
- 17:11:37 UTC — Failed password
- 17:11:42 UTC — Failed password

## 5. Security Analysis

The three failed authentication events were intentionally generated during controlled testing.

The source address was `127.0.0.1`, indicating that the SSH connection originated locally on the Jump Server.

These events demonstrate that Ubuntu successfully recorded unsuccessful SSH authentication attempts.

## 6. Conclusion

The test successfully demonstrated the ability to generate and identify failed SSH authentication events through Linux system logs.

This provides a foundation for centralized security monitoring and automated threat detection using Wazuh.

## 7. Next Steps

- Configure Wazuh monitoring.
- Collect authentication events centrally.
- Generate security alerts.
- Investigate suspicious login activity.

- ## 2. Internal Server SSH Failed Login Detection

**Result: Successful**

A controlled SSH authentication test was performed on the Internal Server.

Test details:
- Server: Internal Server
- Operating System: Ubuntu 26.04.1 LTS
- IP Address: 192.168.50.20
- Test username: invalidtest
- Source IP: 127.0.0.1
- Wazuh Rule ID: 5710
- Alert Level: 5
- Detection: SSH login attempt using a non-existent user

Wazuh successfully collected the authentication events from
/var/log/auth.log and generated Rule 5710 alerts.

The events were received and recorded by the Wazuh Manager.

The Wazuh Dashboard authentication failure count increased
from 53 to 59 during testing.

**Conclusion:** Internal Server SSH authentication monitoring
and failed-login detection were successfully verified.

## 3. SSH Brute-Force Detection

**Result: Successful**

A controlled SSH brute-force simulation was performed against the Internal Server to verify Wazuh's correlation and threat detection capabilities.

**Test environment:**
- Target: Internal Server
- Operating System: Ubuntu 26.04.1 LTS
- Target IP: 192.168.50.20
- Test username: invalidtest
- Source IP: 127.0.0.1
- Wazuh Manager: 192.168.50.30

**Detection configuration:**
- Wazuh Rule ID: 5712
- Alert Level: 10
- Detection frequency: 8 matching events
- Time window: 120 seconds
- Source IP correlation: Enabled

Multiple failed SSH authentication attempts were generated using separate SSH connections within the configured detection window.

Wazuh successfully correlated the authentication failures and generated Rule 5712 brute-force alerts.

The Wazuh Dashboard subsequently displayed three Rule 5712 alerts at severity level 10.

Additional authentication-related detections were also observed:

- Rule 2502: Repeated password failures
- Rule 5551: Multiple failed logins within a short period
- Rule 5758: Maximum authentication attempts exceeded

**Conclusion:** SSH brute-force detection and authentication event correlation were successfully verified using the default Wazuh ruleset.

No default Wazuh detection rules or SSH security limits were modified during testing.
