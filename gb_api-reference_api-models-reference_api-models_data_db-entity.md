# Db\[ENTITY]

This is a representation of all the objects in the `Api.Model.Data` namespace. Each instance represents a one to one mapping of a table, with a `Db` prefix and the removal of the `t` database prefix.

Each object will contain a list of all the fields in the table, as well a few standard Dictionaries (see below).

## Properties

`Dictionary<string, CustomPropertyValue> CustomProperties`

This contains a `Dictionary` of `CustomPropertyValues`. By default, the behavior of the keys represent the `CustomPropertyValue.FullKey` and are case insensitive.

`IDictionary<string, object> X`

This contains a case insensitive `IDictionary` object. This is populated by the various `LoadSqlX` methods.
