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
