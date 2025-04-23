<img width="600" src="https://github.com/user-attachments/assets/3139ed02-bf2c-4d30-973e-12dc1063fcba" alt="Incident Response Lifecycle"/>

# Incident Response Report: Virtual Machine Brute Force Detection

## Platforms and Languages Leveraged
- Windows 10 Virtual Machines (Microsoft Azure)
- EDR Platform: Microsoft Defender for Endpoint
- Kusto Query Language (KQL)
- Microsoft Sentinel

##  Scenario

Management has raised concerns about a potential brute force attack on devices within our network. Multiple virtual machines have begun showing a high volume of failed logon attempts within a short timeframe. Microsoft Defender for Endpoint flagged repeated access attempts from unfamiliar external IP addresses, some of which targeted the same devices multiple times. At this stage, it is unclear whether any of the attempts have been successful, prompting immediate investigation. The goal is to detect brute force login attempts across virtual machines and analyze the source of failed logins to mitigate potential unauthorized access risks.

### High-Level Incident Response Plan

- **Check `DeviceLogonEvents`** for any abnormal login patterns and investigate repeated failed logins from external IP addresses in order to assess potential compromise. 
- **Check `DeviceLogonEvents`** for any successful login attempts made by the malicious IP addresses.
- **If applicable, `isolate affected devices`, `block malicious IP addresses`, `run an antimalware scan`, and `update NSG security rules`** to prevent future brute-force attempts

## Steps Taken

### 1. Searched the `DeviceLogonEvents` Table

Searched for events within the last 5 hours where a remote IP address failed to log in to the same host more than 10 times. Identified 16 such incidents, including one where two different hosts were targeted by the same IP address: 89.248.160.144.

**Query used to locate events:**

