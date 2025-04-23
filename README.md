<img width="600" src="https://github.com/user-attachments/assets/3139ed02-bf2c-4d30-973e-12dc1063fcba" alt="Incident Response Lifecycle"/>

# Incident Response Report: Virtual Machine Brute Force Detection

## Platforms and Languages Leveraged
- Windows 10 Virtual Machines (Microsoft Azure)
- EDR Platform: Microsoft Defender for Endpoint
- Kusto Query Language (KQL)
- Microsoft Sentinel

##  Scenario

Management has raised concerns about a potential brute force attack on devices within our network. Multiple virtual machines have begun showing a high volume of failed logon attempts within a short timeframe. Microsoft Defender for Endpoint flagged repeated access attempts from unfamiliar external IP addresses, some of which targeted the same devices multiple times. At this stage, it is unclear whether any of the attempts have been successful, prompting immediate investigation. The goal is to detect brute force login attempts across virtual machines and analyze the source of failed logins to mitigate potential unauthorized access risks.

