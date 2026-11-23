# License

The License section of the TrakSYS Installation Manager displays current License information and provides actions to import, activate, or delete licenses.

## Status

### Status

Displays whether or not a valid TrakSYS License has been found in the TrakSYS Database.

## License

### Company

Displays the Company to which this TrakSYS installation is licensed to.

### Notes

Displays any notes that may be on License.

### Serial Number

Displays the Serial Number of this TrakSYS installation's License.

### Version

Displays the Version of TrakSYS which the License can run.

### Expiration

Displays the Expiration Date of the current License.

## Features

Provides a table of Features which can be enabled when activating the imported License.

### Feature

Name of the feature.

### Value

Typically represents the quantity available for a particular feature (e.g. TrakSYS Event Definitions - 500 or TrakSYS Users - 25). Some features display an asterisk (\*) in the value field denoting that this is just a feature line item that is enable throughout the application (e.g. TrakSYS Journal or TrakSYS Advanced Scripting).

### Host

Name of the machine which will host the selected feature. Typically this is the name of the application server. Host names must be properly configured before attempting to activate a License. Some features are independent of a Host and therefore display "N/A" for this field.

## Actions

### Import License

Provides a prompt to specify the location of the license file to be imported. This Action is only available when there is no valid License already activated.

### Delete License

Action to delete the current license. This Action is only available when there is a valid License already activated.

### Activate License (Online)

Once a license is imported, it must be activated. The Activate License (Online) Action is the fastest way to activate a TrakSYS License (requires the application server to be connected to the internet). This Action is only available when there is no valid License currently activated.

{% hint style="info" %}
This option will only be enabled for Perpetual and Offline Subscription Licenses
{% endhint %}

### Create Activation Data

In cases where the application server does not have access to the internet, License activation will have to be done via a two-step process. First, Create Activation Data, by specifying the desired location of the output file. This output file must be sent to Parsec. Note, this Action is only available when there is no valid License already activated. Parsec will provide an Activation file to complete the second step of this offline activation process. Host names must be properly configured before generating Activation Data.

{% hint style="info" %}
This option will only be enabled for Perpetual and Offline Subscription Licenses
{% endhint %}

### Import Activation Data

The second step of the offline activation process requires importing the provided Activation file by specifying its location in the prompt. Upon Import of a valid Activation file, the TrakSYS License should be successfully activated. This Action is only available when there is no valid License already activated.

{% hint style="info" %}
This option will only be enabled for Perpetual and Offline Subscription Licenses
{% endhint %}

### Validate Subscription

When an installation has access to the internet and is using an Online Subscription License, the Validate Subscription button must be clicked after installing the license. This process makes the initial contact with the license validation servers and binds the current server instance to the license. Once the license is active, this button can be clicked at any time to manually perform a license validation check. This is in addition to the normal license validation check that is performed automatically once per day.

{% hint style="info" %}
This option will only be available for Online Subscription Licenses.
{% endhint %}
