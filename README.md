# HUBWTroubleshooter

Workspace ONE HUB for Windows Troubleshooter Tool

An app to display Workspace ONE Hub for Windows configuration settings.

### General | general | --G | --g 

List Hub for Windows configuration settings and sample. For example:

`HUBWTroubleshooter.exe General` 

Use the `--item` with the General command to return only the value of that item. This is great for returning a value to a sensor. For example:

`HUBWTroubleshooter.exe --g --item <vIDMServer>`

### Baselines | baselines | --B | --B 

List Baselines

`HUBWTroubleshooter.exe General`

### Apps | apps | -A | -a 

List Applications

`HUBWTroubleshooter.exe Apps`

### Profiles | profiles | -P | -A 

List Profiles

`HUBWTroubleshooter.exe Profiles`

Use the `--item` to return detailed info on that profile. For example:

`HUBWTroubleshooter.exe --p --item "Windows BitLocker Profile"` 

### Scripts | scripts | -S | -s 

List Scripts

`HUBWTroubleshooter.exe Scripts`

Use the `--item` to return detailed info on that script, including the actual script code, last sample send and last return value. For example:

`HUBWTroubleshooter.exe --s --item "set_baseline_reapply"`

### Sensors | sensors | -E | -e 

List Sensors

`HUBWTroubleshooter.exe Sensors`

Use the `--item` to return detailed info on that sensor, including the actual sensor code, last sample send and last return value. For example:

`HUBWTroubleshooter.exe --e --item "dell_warranty"`

### Workflows | workflows | -W | -w 

List Workflows

`HUBWTroubleshooter.exe Workflows`

Use the `--item` to return detailed info on that workflow, including the status, last executed date/time and workflow steps. For example:

`HUBWTroubleshooter.exe --w --item "dell_bios_upg" `

### logs | --logs | -l 

Configure HUBW log streaming. Can also install Seq Server to local device and configure filters. Seq Server demo

`HUBWTroubleshooter.exe Logs`

### testnet | --testnet | -t 

Tests documented HUBW network endpoints. HUBW required ports are listed at [Workspace ONE UEM Network Endpoints](https://ports.esp.vmware.com/home/Workspace-ONE-UEM). Microsoft also requires numerous networks whitelisted for functions such as WNS here [Windows 11 Network Endpoints](https://learn.microsoft.com/en-us/windows/privacy/manage-windows-11-endpoints)

The function will run the following tests on each endpoint:

- ping
- tcpsocket
- httpget

Some endpoints can reside on multiple ports and therefore each port and protocol will be tested for each endpoint. As long as one of the tests pass, the endpoint should be accessible. **If unsure, please test manually!**

`HUBWTroubleshooter.exe testnet`
