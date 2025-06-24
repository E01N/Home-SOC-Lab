# Network Configuration

## Objective

Configure isolated, host-only networking between the Kali Linux host and the Windows 10 SOC endpoint virtual machine to simulate a real-world internal network environment and enable secure log forwarding.

---

## Virtual Network Design

| System     | Role              | IP Address       | Network Type     | Adapter Name |
|------------|-------------------|------------------|------------------|---------------|
| Kali Host  | Attacker / SIEM   | 192.168.56.1     | Host-Only        | vboxnet0      |
| Windows VM | SOC Endpoint      | 192.168.56.20    | Host-Only        | Intel PRO/1000 MT |

---

## Configuration Steps

### 1. Created Host-Only Network (vboxnet0)

- Used VirtualBox Host Network Manager:
  - IP: `192.168.56.1`
  - Subnet: `255.255.255.0`
  - DHCP: Disabled
- Interface created on host: `vboxnet0`

---

### 2. Configured Windows VM Network Adapter

- Adapter 1:
  - Attached to: `Host-Only Adapter`
  - Name: `vboxnet0`
- Set static IP manually:
  - IP: `192.168.56.20`
  - Subnet: `255.255.255.0`
  - Gateway: *(none)*
  - DNS: *(none)*

![VM Network Screenshot](../networkconfig.png)
---

### 3. Verified Host IP (Kali)

On Kali (host):

```
ip a | grep vbox
```

Confirmed IP: 192.168.56.1 on vboxnet0.

---

### 4. Connectivity Test

- From **Kali (host)**:

```
ping 192.168.56.20
```

- From **Windows VM (CMD)**:

```
ping 192.168.56.1
```

✅ Both systems successfully responded to pings.

---

## Snapshot

Took VirtualBox snapshot after setup:

- Snapshot name: Clean-Install-Network-Configured
- Description: Windows fully installed, network configured for host-only lab.

---
