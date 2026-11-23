# Step Outputs

As Steps complete their execution and exit, an opportunity is presented to map Step Output values into Process Parameters.

{% hint style="info" %}
This type of configuration is useful when attempting to save the Output values from one Step to the Process Parameters for use with a later Step in the Process. It is **not** necessary when an Output value is required in the **next** Step, as all Outputs are automatically passed to the next Step as part of the **Process Values** mechanism.
{% endhint %}

## Outputs Tab

The Outputs Tab within the Step's Property page lists all of the configured Process Parameters. The entry field provided allows the assignment of an outgoing **Process Values** entry (by Key).

## Direct Assignment

If the outgoing **Process Values** Key is known, it can be typed directly into the entry field. Note that if the specified Key does not exist in the **Process Values** at runtime, an error will be thrown and the Process could stop executing.

## Outputs Picker

Selecting the "picker" icon displays a list of known Step Outputs. Selecting an entry will assign its Key into the text entry field.

### Step Outputs

Known StepType specific Outputs are listed under the **Step** section of the picker tree.

### Common Outputs

Standard Outputs that are available for every Step Type are listed under the **Common** section of the picker tree.

### Dynamic Outputs

Some Step Types may generate dynamic Outputs at runtime. These will **not** be listed in the picker tree and must directly typed into the entry field.
