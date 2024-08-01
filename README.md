# HUBWTT

 (HUBWTT.exe) is an app to display Workspace ONE Hub for Windows configuration settings managed application deployment settings, baseline information, profiles, sensors, scripts, and workflows and associated details.
Using the --item option, the tool can display more detail about an individual item including the install command and detection criteria for an application deployed with SfD, or the actual script deployed with Workspace ONE Scripts as examples.
The tool will also test network connctivity from this device to required network endpoints as documented at
https://ports.esp.vmware.com/home/Workspace-ONE-UEM and https://learn.microsoft.com/en-us/windows/privacy/manage-windows-11-endpoints. This is useful for both enrolled and yet to be enrolled devices.
Additional features include the ability to export the HUBW LiteDB to then be shared with VMware Global Support if required, and a LAPS 'like' functionality to rotate a local 'Admin' password on a schedule, escrow with a sensor and decrypt.

## Requirements
- .NET 6.0 (requirement for HUBW already)
- Windows 10+
- Workspace ONE HUB for Windows 2109+ (requires LiteDB)
- Administrator: Command Prompt

## Note: The following limitations exist today:
- Windows 11 ARM64 not supported
- Many Profiles do not display

        Phil Helmling, helmlingp@vmware.com, @philhelmling

# Disclaimer
**THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL
VMWARE,INC. BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.**

# Usage
HUBWTT provides options to list information within relative groups:
- Applications
- Baselines
- General (HUBW info)
- Profiles
- Scripts
- Sensors
- Workflows

![HUBWTT.exe --help](Images/Screenshot%202024-02-23%20at%207.52.22 am.png)

HUBWTT also provides detailed information on individual items specified with the --item option. Use the **--item _NameOfAttribute_** to return only the value of that item. This is great for returning a value to a sensor. This option is available with many of the provided functions. For example:

`HUBWTT.exe g --item ServerVersion`

![HUBWTT.exe g --item ServerVersion](Images/Screenshot%202024-02-22%20at%208.37.02 pm.png)


## Future Plans
Future features include:
- Capture logs
- Redirect logs to central log server for analysis
- Enrolment User SID Mismatch check
- Enrol device with pre-installed Workspace ONE Intelligent Hub (AirwatchAgent.msi) similar to command line enrolment. Good for imaging and VDI use cases.
- Unenrol device without uninstalling Workspace ONE Intelligent Hub (AirwatchAgent.msi). Good for VDI and troubleshooting.
- Display App deployment log details
- Display all profiles
- Initiate HUBW sync with strict thresholds
- Improve exportHUBW to zip with password provided
- Improve importHUBW to unzip with password provided

# Apps Information

`HUBWTT.exe apps` or `HUBWTT.exe a` or `HUBWTT.exe A`

List Applications deployed to the device, including the name, architecture, assignment, install status, last error reported and last install date/time.

![HUBWTT.exe apps](Images/Screenshot%202024-02-22%20at%208.37.39 pm.png)

The name of the application can be provided to the **--item** option to return details about the specific application. This is useful for troubleshooting application deployments without having to view SfD logs stored in the registry in XML data format.

`HUBWTT.exe a --item "Horizon View Broker Change`

![HUBWTT.exe a --item "Horizon View Broker Change"](Images/Screenshot%202024-02-22%20at%208.38.18 pm.png)

# Baselines Information

`HUBWTT.exe baselines` or `HUBWTT.exe b` or `HUBWTT.exe B`

List Baselines deployed to the device, including the status on the device, the status on the server, when the baseline was last applied to the device and the overall compliance status according to the baseline.

![HUBWTT.exe baselines](Images/Screenshot%202024-02-22%20at%208.38.49 pm.png)

# Export HUBW LiteDB

`HUBWTT.exe exportHUBW`

![HUBWTT.exe exportHUBW](Images/Screenshot%202024-01-04%20at%203.37.22 pm.png)

Exports the HUBW LiteDB into a ZIP and placed on the Desktop of the current user. A password will be asked for and used to secure the file.
This function should only be used under the direction of GSS and Engineering. Please provide the ZIP file and password to GSS.

# General HUBW Information

`HUBWTT.exe general` or `HUBWTT.exe g` or `HUBWTT.exe G`

List Hub for Windows configuration settings and sample.

This command will output general HUB configuration settings and then output into separate tables, HUB Samples Last Sent Time followed by HUB Custom Lookup values:

![HUB General Configuration Settings](Images/Screenshot%202024-02-22%20at%208.35.18 pm.png)

This table is useful for determining when information is sent back to the platform.
![HUB Sample Info](Images/Screenshot%202024-02-22%20at%208.35.57 pm.png)

![HUB Lookup Info](Images/Screenshot%202024-02-22%20at%208.36.13 pm.png)

The name of the attribute can be provided to the **--item** option to return details about a specific attribute and can be used with a sensor.

`HUBWTT.exe g --item ServerVersion`

![HUBWTT.exe g --item ServerVersion](Images/Screenshot%202024-02-22%20at%208.37.02 pm.png)

# LAPS

`HUBWTT.exe laps`

Enable LAPS 'like' functionality to rotate a local 'Admin' password on a schedule. The encrypted and hashed passcode is stored in the HKLM\SOFTWARE\AirWatchMDM registry key which is only accessible by users with local Administrator permissions. The hashed passcode can then be retrieved by a sensor using the --get option.
![](Images/Screenshot%202024-02-21%20at%202.32.30%20pm.png)

A scheduled task is created and runs at the interval specified.
![](Images/Screenshot%202024-02-21%20at%202.31.19%20pm.png)

![HUBWTT.exe laps --help](Images/Screenshot%202024-02-21%20at%201.25.54 pm.png)

`HUBWTT.exe laps --set --rotate 90 --account AccountName --cert certificate_subjectName`
Create a randomly generated password, encrypted with the provided certificate public key and hashed for storage in the registry and setup Schedule Task to rerun the same command at the specified interval (days).
![HUBWTT.exe laps --set --rotate 60 --account philtest --cert certificate_subjectName](Images/Screenshot%202024-02-22%20at%208.47.13 pm.png)

`HUBWTT.exe laps --get`
Run --get within a WS1 Sensor to escrow the encrypted version of the password.
![HUBWTT.exe laps --get](Images/Screenshot%202024-02-22%20at%208.44.04 pm)

`HUBWTT.exe laps --decode --passcode passcode_string --cert certificate_subjectName`
From a device enrolled into the same WS1 tenant, and with a certificate holding the private key, decrypt the passcode back to the password using the provided certificate.
![HUBWTT.exe laps --decode --passcode passcode_string --cert certificate_subjectName](Images/Screenshot%202024-02-22%20at%208.46.16 pm.png)

**Note:** For Proof of Concept purposes, the **AwDeviceRoot** certificate deployed to an enrolled device will be used to encrypt the password. Bear in mind that this capability is not as secure as using a public/private key pair to encrypt/decrypt the password.
![HUBWTT.exe laps --set --rotate 60 --account philtest](Images/Screenshot%202024-02-21%20at%202.29.57 pm.png)
![HUBWTT.exe laps --get](Images/Screenshot%202024-02-21%20at%202.30.23 pm.png)
![HUBWTT.exe laps --decode --passcode passcode_string](Images/Screenshot%202024-02-21%20at%202.31.02 pm.png)

# Profiles Information

`HUBWTT.exe profiles` or `HUBWTT.exe p` or `HUBWTT.exe P`

List Profiles deployed to the device including the install status, version and context deployed to. 
**Note:** Only some profiles are displayed at present. Future development on this to come!

![HUBWTT.exe profiles](Images/Screenshot%202024-02-22%20at%208.39.10 pm.png)

Use the **--item _NameOfProfile_** parameter to return detailed info on that profile. For example:

`HUBWTT.exe p --item "Win10 - BitLocker TPM Only Profile Settings"`

![HUBWTT.exe p --item "Win10 - BitLocker TPM Only Profile Settings](Images/Screenshot%202024-02-22%20at%208.40.15 pm.png)

# Scripts Information

`HUBWTT.exe scripts` or `HUBWTT.exe s` or `HUBWTT.exe S`

List Scripts deployed to the device including the last execution date/time, the deployment status, result code and error.

![HUBWTT.exe scripts](Images/Screenshot%202024-02-22%20at%208.41.49 pm.png)

_**Note:**_ _Scripts are also deployed with Workflows and are also listed here._

Use the **--item _NameOfScript_** to return detailed info on that script, including the actual script code, last sample send and last return value. This is very useful when troubleshooting deployments, script formatting issues and determining actual return values. For example:

`HUBWTT.exe s --item "GPP-AmazonUK"`

![HUBWTT.exe s --item "GPP-AmazonUK"](Images/Screenshot%202024-02-22%20at%208.42.21 pm.png)

# Sensors Information

`HUBWTT.exe sensors` or `HUBWTT.exe e` or `HUBWTT.exe E`

List Sensors deployed to the device including the name of the sensor, the returned value and last execution date/time.

![HUBWTT.exe Sensors](Images/Screenshot%202024-02-22%20at%208.40.55 pm.png)

Use the **--item _NameOfSensor_** to return detailed info on that sensor, including the actual sensor code, last sample send and last return value. For example:

`HUBWTT.exe e --item get_device_serialnumber`

![HUBWTT.exe e --item get_device_serialnumber](Images/Screenshot%202024-02-22%20at%208.41.23 pm.png)

# Test Network

`HUBWTT.exe testnet`

Tests documented HUBW network endpoints.
HUBW required ports are listed at [Workspace ONE UEM Network Endpoints]https://ports.esp.vmware.com/home/Workspace-ONE-UEM
Microsoft also requires numerous networks whitelisted for functions such as WNS here
[Windows 11 Network Endpoints]https://learn.microsoft.com/en-us/windows/privacy/manage-windows-11-endpoints

The function will run the following tests on each endpoint:
- ping
- tcpsocket
- httpget
                
Some endpoints can reside on multiple ports and therefore each port and protocol will be tested for each endpoint.
As long as one of the tests pass, the endpoint should be accessible. **If unsure, please test manually!**

![HUBWTT.exe testnet](Images/Screenshot%202024-02-23%20at%2011.36.45 am.png)

# Workflows Information

`HUBWTT.exe workflows` or `HUBWTT.exe w` or `HUBWTT.exe W`

List Workflows deployed to the device the name, status and last executed date/time.

![HUBWTT.exe workflows](Images/Screenshot%202024-02-22%20at%208.42.51 pm.png)

Use the **--item _NameOfWorkflow_** to return detailed info on that workflow, including the status, workflow steps and details including last executed date/time of the individual step, next step, resource type, and status of each individual step. For example:

`HUBWTT.exe w --item "Slack Updater Workflow"`

![HUBWTT.exe w --item "Slack Updater Workflow](Images/Screenshot%202024-02-22%20at%208.43.22 pm.png)
