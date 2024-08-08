# General HUBW Information

<div style="text-align: right"

[Go to Table of Contents](../README.md#toc)
</div>

`HUBWTT.exe general` or `HUBWTT.exe g` or `HUBWTT.exe G`

Lists Hub for Windows configuration settings, HUBW sample info such as when the sample was taken and sent, and other custom lookup info such as Custom Attributes, and enrolled user email address.

This command will output general HUB configuration settings, HUB Samples Last Sent Time followed by HUB Custom Lookup values into separate tables as displayed below:

![HUB General Configuration Settings](../Images/HUB-General-Info.png)

This table is useful for determining when information is sent back to the platform.

![HUB Sample Info](../Images/HUB-Sample-Info.png)

This table is useful for determining other values.

![HUB Lookup Info](../Images/HUB-Lookup-Info.png)

The name of the attribute can be provided to the **--item** option to return details about a specific attribute.

This is useful for returning this value with a sensor, for example:

`HUBWTT.exe g --item ServerVersion`

![HUBWTT.exe g --item ServerVersion](../Images/HUBWTT-g-item-ServerVersion.png)
