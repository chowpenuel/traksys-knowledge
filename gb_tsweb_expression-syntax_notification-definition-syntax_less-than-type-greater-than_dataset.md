# dataset

This is used to retrieve data from a table data source defined within `<ets_dataset>` tags. Multiple dataset data sources (`<ets_dataset>` tags) can be declared within a single Notification Definition.

## Examples

```html
{dataset[systems.0]|SystemName}
```

Returns the value of the column called SystemName from the first row in the `<ets_dataset>` source data table named systems.

### Querying data in a Notification Definition Body Content

The following example queries the ID and Name of a specific System and can be placed within the Body Content of the Notification Definition configuration.

```html
<div>
   <p> {dataset[dataQuery].html|ID}, {dataset[dataQuery].html|NAME} </p>
</div>
<ets_dataset name="dataQuery">
   SELECT 
   ID,
   NAME
   From tSystem where ID = 79
</ets_dataset>
```

This will generate an email notification displaying the ID and Name in `SystemID, SystemName` format. Example output is shown below:

```
79, Packaging
```
