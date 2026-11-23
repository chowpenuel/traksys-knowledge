# Devices

Devices configured under TrakSYS Administrator can be used to identify specific clients that access the TrakSYS Web. Identifying a Device allows for a customizable experience, such as displaying a dashboard differently, directing to a specific URL, as well as a wide variety of other customizations.

## Configuration

See the [Device](../entity-reference/configuration-entities/device) topic under Configuration Entities.

## Accessing the Current Device

### Scripts

The current Device information can be retrieved in both the Values Script as well as a Page Definition Script. For example, in Values Script, the following can be used to access Device information:

* `this.Device`

Similarly, in a Page Definition Script, the following can be used to access Device information:

* `this.Ets.Device`

### Utilizing Values

On each Page load, the following values are available by default in the Values Dictionary:

`{ETS.Device.ID}` `{ETS.Device.Name}` `{ETS.Device.Identifier}` `{ETS.Device.SystemID}`

When a client is identified, TrakSYS automatically populates these values with the Device information. For example:

`[ETS.Device.ID] = '4'`

`[ETS.Device.Name] = 'User's PC'`

`[ETS.Device.Identifier] = 'USERNAME-PC'`

`[ETS.Device.SystemID] = '12'`

{% hint style="info" %}
If after configuring a Device, these values are still not being populated, use the **Refresh Device** button under **Settings** for the currently logged in User.
{% endhint %}

### Custom Properties

If Custom Properties are configured on the Device Entity, these Custom Property values will automatically appear in the Values Dictionary when the Device is detected. The Custom Properties will be added with a Values Key following a standard nomenclature: `SCHEME_KEY.CUSTOM_PROPERTY_KEY`.
