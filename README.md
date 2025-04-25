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

![image](https://github.com/user-attachments/assets/3c38992a-5d8f-4300-babc-af394935bfd1)

<p>
<img src="https://github.com/user-attachments/assets/a1f27344-c7bd-43a7-870a-48db901d135c"  alt="KQL Query"/> &emsp; &emsp;
<img src="https://github.com/user-attachments/assets/3ecd848f-b646-418a-a505-6153216bc3da"   alt="KQL Query Results"/>
</p>

---

### 2. Searched the `DeviceLogonEvents` Table a Second Time

Searched for events within the last 5 hours to see if the malicious IP addresses discovered in Step 1 successfully logged into any devices. No successful logins were detected from these IP addresses.

**Query used to locate events:**

![image](https://github.com/user-attachments/assets/49941831-9220-4af4-8cea-7b20498a80c0)

![image](https://github.com/user-attachments/assets/c7602fa3-db3e-4ef1-aa10-5e8f5e7f79a6)

---

### 3. Isolated the affected devices in Microsoft Defender

All 8 impacted devices were isolated in Microsoft Defender for Endpoint, and an antimalware scan was run to ensure no malware was present.

**Ex. 1: Device: win-vm-grand:**
![image](https://github.com/user-attachments/assets/759080c1-42e8-4875-bae7-c6fef186d571)

---

### 4. Updated NSG(network security group) attached to the virtual machine

The network security group (NSG) rules were updated to block RDP access from the public internet. RDP is now only accessible from authorized home IP addresses to maintain secure remote access. As a result, any RDP attempt from unauthorized IP addresses will be denied by a default deny rule at the bottom of the NSG rule list.

![image](https://github.com/user-attachments/assets/aaef6360-8393-48cd-bd03-2b5deb64321d)

A corporate policy proposal was also submitted to enforce this configuration for all virtual machines moving forward.

---

### 5. Restored impacted virtual machines

Reviewed and completed write-up for incident resolution. Finalized reporting and closed out the incident in Microsoft Sentinel as a true positive.

![image](https://github.com/user-attachments/assets/5e6c7a40-2dba-4bae-b12c-8a943c56c7b7)













