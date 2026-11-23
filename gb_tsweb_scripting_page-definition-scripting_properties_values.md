# Values

## Dictionary Methods

The Values Dictionary implements the `IDictionary` which has its own set of shared extensions. See [Dictionaries](dictionaries) for more.

### Setting Values (with Trace)

Sets values while also outputting Trace messages.

```csharp
public override void Add(string key, object value)
public void Add(string key, object value, string traceCategory)
public void Set(string key, object value, string traceCategory)
```

### DataTable Helpers

Loads or copies DataTables into the dictionary and writes common metadata keys (ex: `HasData`, `RowCount`, `SelectedIndex`, and `Selected.*`).

```csharp
public DataTable GetDataTableAndCopy(string sql, string dataTableKey, bool autoSelectedFirstRow, string traceCategory = null, int cacheSeconds = 0, params string[] dependencies)
public DataTable GetDataTableAndCopyWithSelected(string sql, string dataTableKey, bool autoSelectedFirstRow, string whenField, string equalsValue, List<DataRow> selectedRows, string traceCategory = null, int cacheSeconds = 0, params string[] dependencies)
public List<DataRow> AddDataTableInformation(DataTable dt, string dataTableKey, bool autoSelectFirstRow, string traceCategory = null)
public List<DataRow> AddDataTableInformationWithSelected(DataTable dt, string dataTableKey, bool autoSelectFirstRow, string whenField, string equalsValue, List<DataRow> selectedRows, string traceCategory = null)
```

### Paging Helpers

Writes and reads paging keys under a consistent prefix (ex: `{key}.Paging.*`).

```csharp
public void AddPagedDataInformation(IPagedDataInfo info, string targetKey, string traceCategory = null)
public IPagedDataInfo GetPagedDataInformation(string targetKey)
```

### Bulk Population Helpers

Populates keys from models, DataTables, or other dictionaries using key prefixes.

```csharp
public bool CopyFromModel(object model, string keyPrefix, string traceCategory = null, bool ignoreMudt = true)
public bool OverwriteFromDictionary<T>(IEnumerable<KeyValuePair<string, T>> dict, string keyPrefix = null, string traceCategory = null)
public bool ExplodeByIndex(string keyPrefix, DataTable dt, string traceCategory = null)
public bool ExplodeByFieldName(string keyPrefix, string fieldName, DataTable dt, string traceCategory = null)
```
