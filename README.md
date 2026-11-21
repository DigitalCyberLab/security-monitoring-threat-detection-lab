# Security Monitoring and Threat Detection Lab

## Project Overview

This project focuses on building a cybersecurity monitoring environment using Ubuntu Linux and Wazuh, an open-source security monitoring platform.

The goal was to gain practical experience monitoring Linux systems, collecting security events, analyzing logs, detecting suspicious activity, and investigating potential security threats.

## Project Objectives

- **Security Monitoring:** Monitor Linux systems for security-related activity.
- **Log Analysis:** Collect and examine system logs.
- **Threat Detection:** Identify suspicious activity, including repeated failed SSH login attempts.
- **Security Alerts:** Generate and investigate security alerts.
- **Incident Investigation:** Analyze security events and determine what happened.
- **Documentation:** Record configurations, testing procedures, screenshots, and findings.

## Technologies

- Ubuntu Linux Server
- Wazuh 4.14.10
- Linux system logs
- SSH
- VirtualBox
- GitHub

## Lab Environment

The lab consists of three virtual machines operating in a controlled virtual network.

| System | Operating System | Role |
|---|---|---|
| Wazuh Server | Amazon Linux 2023 | Central security monitoring and alert management |
| Jump Server | Ubuntu 26.04.1 LTS | SSH access and monitored Linux system |
| Internal Server | Ubuntu 26.04.1 LTS | Internal system and monitored Linux server |

Both the Jump Server and Internal Server have Wazuh agents installed and connected to the central Wazuh Manager.

## Security Testing

The following controlled security tests were performed:

- Reviewing Linux authentication logs.
- Generating failed SSH login attempts.
- Verifying SSH authentication failure detection.
- Simulating repeated SSH login failures to test brute-force detection.
- Executing controlled sudo commands to verify privileged activity monitoring.
- Verifying that Wazuh collected events and generated security alerts.

## Security Detection and Testing Results

The Wazuh security monitoring lab successfully detected and recorded the following controlled security tests:

| Security Test | Wazuh Rule | Alert Level | Result |
|---|---:|---:|---|
| SSH Failed Login Detection | 5710 | 5 | Successful |
| SSH Brute-Force Detection | 5712 | 10 | Successful |
| Sudo Privilege Monitoring | 5402 | 3 | Successful |

### Verified Capabilities

- Centralized collection of Linux authentication logs.
- Detection of failed SSH login attempts.
- Correlation of repeated SSH failures to identify brute-force activity.
- Monitoring of sudo commands and root privilege usage.
- Security alert generation and investigation through the Wazuh Dashboard.
- MITRE ATT&CK technique mapping.
- Monitoring of multiple Linux systems through a centralized security platform.

## Project Outcomes and Learning Experience

Successfully configured and tested a multi-machine Linux security monitoring lab using Wazuh.

This project provided practical experience with:

- Security Information and Event Management (SIEM).
- Linux security monitoring.
- Log collection and analysis.
- SSH authentication monitoring.
- Brute-force detection.
- Privileged command monitoring.
- Security alert investigation.
- Basic incident detection and response procedures.

These skills are relevant to entry-level SOC Analyst and Junior Security Analyst positions.

## Evidence and Documentation

Screenshots of the security detection results are available in the `Screenshots/` directory.

Detailed testing procedures and results are documented in:

`Documentation/SSH_Failed_Login_Test.md`

## Project Goal

Build a functional security monitoring lab that demonstrates foundational Security Operations Center (SOC) skills and complements the Linux Secure Jump Server Lab.

## Project Status

**Completed**
