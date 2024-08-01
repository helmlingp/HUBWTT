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

**General | general | -G | -g**

List Hub for Windows configuration settings and sample.

`HUBWTT.exe -g`

![HUBWTT.exe General](Images/Screenshot%202023-10-26%20at%208.21.20%20pm.png)

This command will output general HUB configuration settings and then output into separate tables, HUB Samples Last Sent Time followed by HUB Custom Lookup values:

![HUB General Configuration Settings](Images/Screenshot%202023-10-26%20at%208.21.10%20pm.png)

This table is useful for determining when information is sent back to the platform.
![HUB Sample Info](Images/Screenshot%202023-10-26%20at%208.20.52%20pm.png)

![HUB Lookup Info](Images/Screenshot%202023-10-26%20at%208.20.40%20pm.png)

***Detailed information for an item***

Use the **--item _NameOfAttribute_** with the General command to return only the value of that item. This is great for returning a value to a sensor. For example:

`HUBWTT.exe -g --item vIDMServer`

![HUBWTT.exe -g --item vIDMServer](Images/Screenshot%202023-10-27%20at%2011.18.35%20am.png)


**Baselines | baselines | -B | -b**

`HUBWTT.exe -b`

List Baselines deployed to the device, including the status on the device, the status on the server, when the baseline was last applied to the device and the overall compliance status according to the baseline.

![HUBWTT.exe Baselines](Images/Screenshot%202023-10-26%20at%208.22.19%20pm.png)


**Apps | apps | -A | -a**

`HUBWTT.exe -a`

List Applications deployed to the device, including the name, architecture, assignment, install status, last error reported and last install date/time.

![HUBWTT.exe Apps](Images/Screenshot%202023-10-26%20at%208.20.26%20pm.png)

The name of the application can be provided to the **--item** option to provide details about the application. This is useful for troubleshooting application deployments without having to view SfD logs stored in the registry in XML data format.

`HUBWTT.exe -a --item "Horizon View Broker Change`

![HUBWTT.exe -a --item "Horizon View Broker Change](Images/Screenshot%202023-10-28%20at%209.31.40%20am.png)


**Profiles | profiles | -P | -p**

`HUBWTT.exe -p`

List Profiles deployed to the device including the install status, version and context deployed to.

![HUBWTT.exe Profiles](Images/Screenshot%202023-10-26%20at%208.19.35%20pm.png)

Use the **--item _NameOfProfile_** parameter to return detailed info on that profile. For example:

`HUBWTT.exe -p --item "Win10 - BitLocker TPM Only Profile Settings"`

![HUBWTT.exe -p --item "Win10 - BitLocker TPM Only Profile Settings](Images/Screenshot%202023-10-26%20at%208.17.46%20pm.png)

**Scripts | scripts | -S | -s**

`HUBWTT.exe -s`

List Scripts deployed to the device including the last execution date/time, the deployment status, result code and error.

![HUBWTT.exe Scripts](Images/Screenshot%202023-10-26%20at%208.19.56%20pm.png)

_**Note:**_ _Scripts are also deployed with Workflows and are also listed here._

Use the **--item _NameOfScript_** to return detailed info on that script, including the actual script code, last sample send and last return value. This is very useful when troubleshooting deployments, script formatting issues and determining actual return values. For example:

`HUBWTT.exe -s --item "GPP Communications"`

![HUBWTT.exe -s --item "GPP Communications"](Images/Screenshot%202023-10-26%20at%208.17.23%20pm.png)


**Sensors | sensors | -E | -e**

`HUBWTT.exe -e`

List Sensors deployed to the device including the name of the sensor, the returned value and last execution date/time.

![HUBWTT.exe Sensors](Images/Screenshot%202023-10-26%20at%208.19.24%20pm.png)

Use the **--item _NameOfSensor_** to return detailed info on that sensor, including the actual sensor code, last sample send and last return value. For example:

`HUBWTT.exe -e --item "oracle_virtualbox"`

![HUBWTT.exe -e --item "oracle_virtualbox"](Images/Screenshot%202023-10-26%20at%208.18.33%20pm.png)

**Workflows | workflows | -W | -w**

`HUBWTT.exe -w`

List Workflows deployed to the device the name, status and last executed date/time.

![HUBWTT.exe Workflows](Images/Screenshot%202023-10-26%20at%208.19.02%20pm.png)

Use the **--item _NameOfWorkflow_** to return detailed info on that workflow, including the status, workflow steps and details including last executed date/time of the individual step, next step, resource type, and status of each individual step. For example:

`HUBWTT.exe -w --item "Slack Updater Workflow"`

![HUBWTT.exe -w --item "Slack Updater Workflow](Images/Screenshot%202023-10-26%20at%208.18.46%20pm.png)

**logs | --logs | -l**

`HUBWTT.exe -l`

Configure HUBW to stream logs to a serilog compatible server such as [Datalust Seq Server](https://datalust.co/). The tool provides the option to install Seq Server to the local device, configure filters to make the review of logs simpler, as well as ingest all existing logs from the device, or the tool can simply configure the device to stream logs to an existing server, configure filters and ingest existing logs using a provided APIKEY.

_**Note:**_ _Seq is a licensed product with a free single user license. Please check https://datalust.co/pricing for further information in order to abide by licensing requirements._

The following logs are ingested:
- VMware Telemetry Service
  - C:\ProgramData\VMWOSQEXT\logger\*.txt
  - C:\ProgramData\VMware\vmwetlm\logs\*.txt
- VMware Tunnel for Windows
  - C:\ProgramData\VMware\VMware Tunnel\TunnelService\*.log
  - C:\ProgramData\VMware\VMware Tunnel\TunnelUI\*.*
- Workspace ONE Intelligent HUB for Windows
  - C:\ProgramData\AirWatch\UnifiedAgent\Logs\*.log
  - C:\ProgramData\AirWatch\UnifiedAgent\Logs\BaselineLogs\*.log

  **Note: some logs can't be ingested as they are not in a consistent format.**
- Workspace ONE SfD
  - C:\ProgramData\AirWatchMDM\Support\*.log

Watch the [Seq Server demo](https://datalust.co/seq#:~:text=Seq%20is%20a%20centralized%20log,using%20techniques%20you%20already%20know.) to learn how to use Signals (filters). 

![HUBWTT.exe logs viewed in Seq Server Console with HUBW Updater Signal](Images/Screenshot%202023-10-28%20at%2010.15.21%20am.png)

Feedback on this tool is always welcome, including addition Signals or modification to existing provided Signals.

**testnet | -testnet | -t**

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


![HUBWTT.exe testnet](Images/Screenshot%202023-10-28%20at%2010.30.42%20am.png)
