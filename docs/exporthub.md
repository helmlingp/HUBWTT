# Export HUBW LiteDB

<div style="text-align: right"

[Go to Table of Contents](../README.md#toc)
</div>

This function backs up or exports the HUBW LiteDB and logs to allow Engineering and Global Support Services to analyse a device for support purposes. The log capture is similar to the capture logs function within the HUBW > Troubleshooting menu in the System Tray.

**Note: This function should only be used under the direction of GSS and Engineering.**

The function:

- requests a password from the user, which will be used to encrypt the LiteDB and password protect the log bundle (ZIP)
- copies the current HUBW LiteDB file
- encrypts the backup copy with the password and a salt
- performs an integrity check of the backup copy and closes gracefully
- moves the backup copy to the desktop of the current user
- captures all HUBW logs
- captures relevant Windows Event Log files
- captures running Processes
- captures status of Services
- creates a password protected and encrypted ZIP file that includes the HUBW LiteDB backup copy and log bundle with the naming convention *HUBWExport_devicename_yyyymmddhhmmss.zip*

**Note: Please provide the ZIP file AND password to GSS!**

## Usage

`HUBWTT.exe exportHUBW`

![HUBWTT.exe exportHUBW](../Images/HUBWTT-exportHUBW.png)

The ***devicename-export-hubagent.litedb*** file is encrypted and password protected and can only be opened by Global Support Services. 

The log bundle includes logs from the following folders:
- C:\ProgramData\VMware\vmwetlm\logs
- C:\ProgramData\VMWOSQEXT\logger
- C:\ProgramData\AirWatch\UnifiedAgent\Logs
- C:\ProgramData\AirWatch\UnifiedAgent\Logs\BaselineLogs
- C:\Users\Phil\AppData\Local\VMware\IntelligentHub\Logs
- C:\ProgramData\AirWatchMDM\Support
- C:\ProgramData\VMware\VMware Tunnel\TunnelService
- C:\ProgramData\VMware\VMware Tunnel\TunnelUI
- C:\Temp\PpkgInstaller 

An example Export may contain the following and follow this structure:

```
HUBWExport_DESKTOP-43SFVK2_20241010110446/
├── DESKTOP-43SFVK2-export-hubagent.litedb
├── Device
│   ├── Agents
│   │   ├── Application Deployment Agent
│   │   │   ├── AirWatchMDM-InstallCA-x64-23.10.3.528-20240919.log
│   │   │   ├── AirWatchMDM-x64-23.10.3.528-20240919.log
│   │   │   ├── VMware.Hub.SfdAgent.DeployCmd-20240919.log
│   │   │   ├── VMware.Hub.SfdAgent.DeployCmd-20241003.log
│   │   │   ├── VMware.Hub.SfdAgent.DeployCmd-20241010.log
│   │   │   ├── VMware.Hub.SfdAgent.DeployCmd.nondeploy-20240919.log
│   │   │   ├── VMware.Hub.SfdAgent.DeployCmd.nondeploy-20241003.log
│   │   │   └── VMware.Hub.SfdAgent.DeployCmd.nondeploy-20241010.log
│   │   ├── DEEM Telemetry Agent
│   │   ├── DEEM Telemetry Service
│   │   ├── Factory Provisioning Package
│   │   ├── VMware Tunnel Service
│   │   ├── VMware Tunnel UI
│   │   └── Workspace ONE Intelligent Hub
│   │       ├── AW.ProtectionAgent.PowershellExecutor64-20240919.log
│   │       ├── AW.ProtectionAgent.PowershellExecutor64-20241010.log
│   │       ├── AW.WinPC.Updater-20241010.log
│   │       ├── AWACMClient-20240919.log
│   │       ├── AWACMClient-20241003.log
│   │       ├── AWACMClient-20241010.log
│   │       ├── AWProcessCommands-20240919.log
│   │       ├── AWProcessCommands-20241010.log
│   │       ├── Baseline-20240919.log
│   │       ├── Baseline-20241010.log
│   │       ├── BaselineLogs
│   │       ├── DSM-20240919.log
│   │       ├── DSM-20241003.log
│   │       ├── DSM-20241010.log
│   │       ├── DeemInstall_10102024_103334.log
│   │       ├── DeemInstall_10102024_103334_001_vmwetlm_hub.msi.log
│   │       ├── DeemInstall_10102024_103829.log
│   │       ├── DeemInstall_10102024_104328.log
│   │       ├── DeemInstall_10102024_104828.log
│   │       ├── DeemInstall_10102024_105328.log
│   │       ├── DeemRebootCheck_10102024_103331.log
│   │       ├── DeemRebootCheck_10102024_103331_000_vmwetlm_hub.msi.log
│   │       ├── DeviceEnrollment-20240919.log
│   │       ├── DeviceEnrollment-20241010.log
│   │       ├── HubMSIUpdate.log
│   │       ├── InstallerLog_10102024_103230.log
│   │       ├── InstallerLog_19092024_232151.log
│   │       ├── StorageUpgrade-20241010.log
│   │       ├── TaskScheduler-20240919.log
│   │       ├── TaskScheduler-20241003.log
│   │       ├── TaskScheduler-20241010.log
│   │       ├── VMware.Hub.Win32Agent.AppXInstaller-20240919.log
│   │       ├── VMware.Hub.Win32Agent.AppXInstaller-20241010.log
│   │       ├── VMwareHubHealthMonitoring-20240919.log
│   │       ├── VMwareHubHealthMonitoring-20241003.log
│   │       ├── VMwareHubHealthMonitoring-20241010.log
│   │       ├── Workflow-20240919.log
│   │       ├── Workflow-20241003.log
│   │       └── Workflow-20241010.log
│   └── Windows
│       ├── Application_EventLogs.evtx
│       ├── HKLM-SOFTWARE-AirWatchMDM_RegistryExport.txt
│       ├── HKLM-SOFTWARE-AirWatch_RegistryExport.txt
│       ├── HKLM-SOFTWARE-Microsoft-EnterpriseDesktopAppManagement_RegistryExport.txt
│       ├── HKLM-SOFTWARE-Microsoft-EnterpriseResourceManager_RegistryExport.txt
│       ├── HKLM-SOFTWARE-Microsoft-Provisioning-OMADM-Accounts_RegistryExport.txt
│       ├── HKLM-SOFTWARE-Microsoft-Provisioning-OMADM-MDMDeviceID_RegistryExport.txt
│       ├── LocaleMetaData
│       │   ├── Application_EventLogs_0.MTA
│       │   ├── Microsoft-Windows-BitLocker-BitLocker Management_EventLogs_0.MTA
│       │   ├── Microsoft-Windows-BitLocker-DrivePreparationTool-Operational_EventLogs_0.MTA
│       │   ├── Microsoft-Windows-Bits-Client-Operational_EventLogs_0.MTA
│       │   ├── Microsoft-Windows-DeviceManagement-Enterprise-Diagnostics-Provider-Admin_EventLogs_0.MTA
│       │   └── System_EventLogs_0.MTA
│       ├── Microsoft-Windows-BitLocker-BitLocker Management_EventLogs.evtx
│       ├── Microsoft-Windows-BitLocker-DrivePreparationTool-Operational_EventLogs.evtx
│       ├── Microsoft-Windows-Bits-Client-Operational_EventLogs.evtx
│       ├── Microsoft-Windows-DeviceManagement-Enterprise-Diagnostics-Provider-Admin_EventLogs.evtx
│       ├── Processes.txt
│       ├── Services.txt
│       └── System_EventLogs.evtx
└── User
    └── Agents
        └── Workspace ONE Intelligent Hub
            ├── AW.ProtectionAgent.PowershellExecutor64-20240919.log
            ├── AwWindowsIpc-20240919.log
            ├── AwWindowsIpc-20241003.log
            ├── AwWindowsIpc-20241010.log
            ├── VMware.Hub.Win32Agent.AppXInstaller-20240919.log
            └── VMware.Hub.Win32Agent.AppXInstaller-20241010.log
```
