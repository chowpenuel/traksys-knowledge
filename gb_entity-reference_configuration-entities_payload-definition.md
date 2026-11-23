# Payload Definition

## Summary

### Entity Name

Payload Definition

### Database Table Name

`tPayloadDefinition`

### API Object Name

`DbPayloadDefinition`

### Entity Description

A Payload Definition specifies the data and format that is being transported with TrakSYS Connect.

## Properties

`Payload Definition Type ID [ PayloadDefinitionTypeID ]`

The unique identifier (primary key) of the Payload Definition Type.

`Payload Definition Group ID [ PayloadDefinitionGroupID ]`

The ID of the Payload Definition Group.

`Payload Type [ PayloadType ] : ETS.Core.Enums.PayloadType`

The payload type for the definition. Possible types are:

* **Custom** = 0
* **Xml** = 1
* **Json** = 2
* **Csv** = 3
* **StringOnly** = 4
* **QueryString** = 6

`Content Parameters [ ContentParameters ]`

A JSON configuration object that stores settings specific to the selected `Payload Type [ PayloadType ]`.

This value is maintained by the Payload Definition editor as the Payload is created/updated. The JSON schema is not shared across all payload types; each type has its own set of keys.

### Content Parameters

`Content Parameters [ ContentParameters ]` is a JSON object whose keys and values depend on `Payload Type [ PayloadType ] : ETS.Core.Enums.PayloadType`.

The sections below list the supported JSON keys by payload type and show an example of the stored JSON.

#### Payload Type = Xml (1)

`Root Content [ RootContent ]`

The full root content for the XML payload, including the XML declaration and the outermost (root) element.

{% hint style="info" %}
Example Json: `json { "RootContent": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\r\n<Po/>" }`
{% endhint %}

#### Payload Type = Json (2)

`Root List [ IsRootList ]`

Controls whether the JSON document root is a single object or a list/array of objects.

{% hint style="info" %}
Example Json: `json { "IsRootList": false }`
{% endhint %}

#### Payload Type = Csv (3)

`Line Separator [ LineSeparator ] : ETS.Core.Enums.PayloadCsvImportRowSeparatorMode`

Controls the row separator used when importing/parsing CSV.

* **CrLf** = 0 (carriage return + line feed: `\r\n`)
* **NewLine** = 1 (line feed: `\n`)

`Column Separator [ ColSeparator ]`

The character used to separate columns (default is `,`).

`Header Line [ HeaderLine ]`

The header row content used when the CSV document provides column headers as the first row. The value is the literal first line of the CSV document (column names separated by `ColSeparator`).

`First Row Contains Header [ IsFirstRowHeader ]`

When true, the first row is treated as the header row.

`Quote Option [ QuoteOption ] : ETS.Core.Enums.QuoteOption`

Controls what quote character (if any) is used to wrap CSV field values.

* **None** = 0
* **Single** = 1 (`'`)
* **Double** = 2 (`"`)

{% hint style="info" %}
Example Json: `json { "LineSeparator": 0, "ColSeparator": ",", "HeaderLine": "Timestamp,Line,ProductCode,GoodCount,ScrapCount", "IsFirstRowHeader": true, "QuoteOption": 2 }`
{% endhint %}

#### Payload Type = QueryString (6)

No additional configuration values are stored. JSON is intentionally empty and cannot be changed through the standard editor.

{% hint style="info" %}
Example Json: `json {}`
{% endhint %}

#### Payload Type = Custom (0)

`Content Parameters [ ContentParameters ]`

For Custom payloads, the JSON is entered and stored verbatim. No additional keys are generated or validated by the Payload Definition editor.

{% hint style="info" %}
Example Json: `json { "CustomParameter": "CustomValue" }`
{% endhint %}
