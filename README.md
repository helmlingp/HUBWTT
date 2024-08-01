# HUBWTT
Workspace ONE HUB for Windows Troubleshooter Tool (HUBWTT.exe) is an app to display Workspace ONE Hub for Windows configuration settings managed application deployment settings, baseline information, profiles, sensors, scripts, and workflows and associated details.
Using the --item option, the tool can display more detail about an individual item including the install command and detection criteria for an application deployed with SfD, or the actual script deployed with Workspace ONE Scripts.
The tool will also test network connctivity from this device to required network endpoints as documented at
https://ports.esp.vmware.com/home/Workspace-ONE-UEM. Microsoft also requires numerous networks whitelisted for
functions such as WNS here https://learn.microsoft.com/en-us/windows/privacy/manage-windows-11-endpoints. This is useful for both enrolled and yet to be enrolled devices.

# Requirements
- .NET 6.0 (requirement for HUBW already)
- Windows 10+
- Workspace ONE HUB for Windows 2109+ (requires LiteDB)
- Administrator: Command Prompt

**Note: The following limitations exist:**
- Windows 11 ARM64 not supported
- CSP Profiles do not display
![Download HUBWTT.exe here](https://ent.box.com/s/mba3kus5zgg2sv5yp1a7jb7t7jzikv2s)

# Requirements
- .NET 6.0 (requirement for HUBW already)
- Windows 10+
- Workspace ONE HUB for Windows 2109+ (requires LiteDB)
- Administrator: Command Prompt

**Note: The following limitations exist:**
- Windows 11 ARM64 not supported
- CSP Profiles do not display

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
- General HUBW info
- Baselines
- Applications
- Profiles
- Scripts
- Sensors
- Workflows

HUBWTT also provides detailed information on individual items specified with the --item option. Examples of usage below.

HUBWTT also provides functions to test network connectivity from the endpoint device to required services, as well as securely export the HUBW LiteDB if required and under direction of VMware GSS or Engineering.

**general | g | G**

List Hub for Windows configuration settings and sample.

![HUBWTT.exe General](Images/Screenshot%202023-10-26%20at%208.21.20%20pm.png)

![HUBWTT.exe General](Images/Screenshot%202023-10-26%20at%208.21.20%20pm.png)

This command will output general HUB configuration settings and then output into separate tables, HUB Samples Last Sent Time followed by HUB Custom Lookup values:

![HUB General Configuration Settings](Images/Screenshot%202023-10-26%20at%208.21.10%20pm.png)

This table is useful for determining when information is sent back to the platform.
![HUB Sample Info](Images/Screenshot%202023-10-26%20at%208.20.52%20pm.png)

![HUB Lookup Info](Images/Screenshot%202023-10-26%20at%208.20.40%20pm.png)

***Detailed information for an item***

Use the **--item _NameOfAttribute_** with the General command to return only the value of that item. This is great for returning a value to a sensor. For example:

`HUBWTT.exe g --item vIDMServer`

![HUBWTT.exe g --item vIDMServer](Images/Screenshot%202023-10-27%20at%2011.18.35%20am.png)


**baselines | b | B**

`HUBWTT.exe b`

List Baselines deployed to the device, including the status on the device, the status on the server, when the baseline was last applied to the device and the overall compliance status according to the baseline.

![HUBWTT.exe baselines](Images/Screenshot%202023-10-26%20at%208.22.19%20pm.png)


**apps | a | A**

`HUBWTT.exe a`

List Applications deployed to the device, including the name, architecture, assignment, install status, last error reported and last install date/time.

![HUBWTT.exe apps](Images/Screenshot%202023-10-26%20at%208.20.26%20pm.png)

The name of the application can be provided to the **--item** option to provide details about the application. This is useful for troubleshooting application deployments without having to view SfD logs stored in the registry in XML data format.

`HUBWTT.exe a --item "Horizon View Broker Change`

![HUBWTT.exe a --item "Horizon View Broker Change](Images/Screenshot%202023-10-28%20at%209.31.40%20am.png)


**profiles | p | P**

`HUBWTT.exe p`

List Profiles deployed to the device including the install status, version and context deployed to.

![HUBWTT.exe profiles](Images/Screenshot%202023-10-26%20at%208.19.35%20pm.png)

Use the **--item _NameOfProfile_** parameter to return detailed info on that profile. For example:

`HUBWTT.exe p --item "Win10 - BitLocker TPM Only Profile Settings"`

![HUBWTT.exe p --item "Win10 - BitLocker TPM Only Profile Settings](Images/Screenshot%202023-10-26%20at%208.17.46%20pm.png)

**scripts | s | S**

`HUBWTT.exe s`

List Scripts deployed to the device including the last execution date/time, the deployment status, result code and error.

![HUBWTT.exe scripts](Images/Screenshot%202023-10-26%20at%208.19.56%20pm.png)

_**Note:**_ _Scripts are also deployed with Workflows and are also listed here._

Use the **--item _NameOfScript_** to return detailed info on that script, including the actual script code, last sample send and last return value. This is very useful when troubleshooting deployments, script formatting issues and determining actual return values. For example:

`HUBWTT.exe s --item "GPP Communications"`

![HUBWTT.exe s --item "GPP Communications"](Images/Screenshot%202023-10-26%20at%208.17.23%20pm.png)


**sensors | e | e**

`HUBWTT.exe e`

List Sensors deployed to the device including the name of the sensor, the returned value and last execution date/time.

![HUBWTT.exe Sensors](Images/Screenshot%202023-10-26%20at%208.19.24%20pm.png)
![HUBWTT.exe Sensors](Images/Screenshot%202023-10-26%20at%208.19.24%20pm.png)

Use the **--item _NameOfSensor_** to return detailed info on that sensor, including the actual sensor code, last sample send and last return value. For example:

`HUBWTT.exe e --item "oracle_virtualbox"`

![HUBWTT.exe e --item "oracle_virtualbox"](Images/Screenshot%202023-10-26%20at%208.18.33%20pm.png)

**workflows | w | W**

`HUBWTT.exe w`

List Workflows deployed to the device the name, status and last executed date/time.

![HUBWTT.exe workflows](Images/Screenshot%202023-10-26%20at%208.19.02%20pm.png)

Use the **--item _NameOfWorkflow_** to return detailed info on that workflow, including the status, workflow steps and details including last executed date/time of the individual step, next step, resource type, and status of each individual step. For example:

`HUBWTT.exe w --item "Slack Updater Workflow"`

![HUBWTT.exe w --item "Slack Updater Workflow](Images/Screenshot%202023-10-26%20at%208.18.46%20pm.png)

**testnet**
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

`HUBWTT.exe testnet`

![HUBWTT.exe testnet](Images/Screenshot%202023-10-28%20at%2010.30.42%20am.png)

exportHUBW
`HUBWTT.exe exportHUBW`

![HUBWTT.exe exportHUBW](Images/Screenshot%202024-01-04%20at%203.37.22 pm.png)

Exports the HUBW LiteDB into a ZIP and placed on the Desktop of the current user. A password will be asked for and used to secure the file.
This function should only be used under the direction of GSS and Engineering. Please provide the ZIP file and password to GSS.
