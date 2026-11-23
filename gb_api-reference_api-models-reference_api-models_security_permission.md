# Permission

This object is used when checking for more granular permissions when users access pages within the TrakSYS Web. The model is commonly used with Permission Sets.

## Properties

`string Action`

Gets or sets the Permission Action for a specific Permission. The Permission Actions refer to a user’s ability to do something to an entity (e.g. create, modify, and delete data). The Action can come from built-in Permissions specified for Roles or from custom Permission Sets.

{% hint style="info" %}
If Custom Permission Sets are being used, Permission Actions are only available for Grid Permission Sets. Flat Permission Sets only contain Permission Items.
{% endhint %}

`string Item`

Gets or sets the Permission Item for a specific Permission. A Permission Item refers to the specific entity that the action will affect (e.g. Areas, Products, Tags, etc).

`string Set`

Gets or sets a Permission Set Key. This is commonly used with Custom Permission Sets.
