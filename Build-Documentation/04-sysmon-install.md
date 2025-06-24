# Sysmon Installation

## Objective

Install Microsoft Sysinternals Sysmon on the Windows 10 endpoint to enable granular event logging. This forms a critical component of the endpoint visibility stack in the SOC lab.

---

## Sysmon Purpose

Sysmon provides detailed event logging for process creation, network connections, file writes, and more. It works in tandem with tools like Wazuh and Windows Event Forwarding (WEF) to supply deep endpoint telemetry for detection engineering.

---

## Files Used

The following files were downloaded from Microsoft and placed in a shared folder named `SysmonShare`:

- `Sysmon.exe`
- `Sysmon64.exe`
- `Eula.txt`
- `sysmonconfig.xml` – SwiftOnSecurity’s public config file  
  [Source](https://github.com/SwiftOnSecurity/sysmon-config)

---

## Host Setup

### 1. Create Shared Folder (from Kali host)

Directory created:

--  
/home/eoin/VM-Shares/Sysmon  
--

Contents copied into that directory (unzipped from Microsoft Sysinternals zip).

![Sysmon Download Screenshot](../images/downloadsysmon.png)

### 2. Configure VM Shared Folder

In VirtualBox Manager:
- Go to **Settings → Shared Folders**
  - Folder Path: `/home/eoin/VM-Shares/Sysmon`
  - Folder Name: `SysmonShare`
  - Options enabled:  
    Auto-mount  
    Make Permanent

> Guest Additions were installed prior to this step to enable shared folder access.

---

## In-VM Installation

### 1. Map the Shared Folder in Windows 10 VM

```
net use Z: \\VBOXSVR\SysmonShare  
```

### 2. Run Sysmon with Configuration

``` 
Z:\Sysmon64.exe -accepteula -i Z:\sysmonconfig.xml  
```

Output should confirm successful installation.

---

## Verification

To confirm Sysmon is running:

```
 sc query sysmon64
```
-Sysmon is running 

![Sysmon Running](../images/sysmonrunning.png)

---

## Snapshot Taken

Snapshot Name: **Post-Sysmon-Install**

This snapshot serves as a rollback point prior to any agent deployments or attack simulations.
