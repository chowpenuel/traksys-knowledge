# MQTT Tag

## Summary

### Entity Name

MQTT Tag

### Database Table Name

`tTag`, `tTagMqtt`

### API Object Name

`DbTagMqttComposite`

### Entity Description

MQTT Tags provide a way to retrieve data from an MQTT Broker by referencing a specific Topic. Along with this, they support different Quality of Service options for different use cases. For those that use the Sparkplug B protocol, these tags can accept these payloads when the Use Sparkplug option is checked within the MQTT Access Name.

`Topic [ Topic ]`

Contains the Topic that is assigned to the configured MQTT Tag. This determines how the MQTT Tag will recieve values from the MQTT Broker.

`Quality of Service [ QualityOfService ]`

Specifies the Quality of Service used when values are broadcasted to the MQTT Broker. The possible values are:

* **At Most Once (0)**
* **At Least Once (1)**
* **Exactly Once (2)**

`Sparkplug Metric [ SparkplugMetric ]`

Specifies the alias of the Metric value that will be assigned to the tag when receiving a Sparkplug payload. If an alias is not used, the Metric Name can be used for this field instead.
