# Web API

The TrakSYS Web API allows for interaction with TrakSYS entities and data from a JavaScript environment. The Web API is comprised of many of the same methods available in the traditional TrakSYS API.

## Constructing URL

A typical URL to call the Web API consists of a Root Path, a Route, and encoded Parameters.

### Root Path

The beginning of the URL should be the TrakSYS Root Path, this can be retrieved from `ets.rootPath`.

### Routing

The route defines what part of the Web API with which to interface. The route begins with `/api/{SiteKey}` followed by the area of the API (e.g. `/util/db`). The most common Web API areas are:

`/data`

Includes the same methods as the TrakSYS API Data namespace (e.g. `/DbSystem/Load/ByID?ID={ID}` or `/DbArea/Save/UpdateExisting`). While most `Save` methods of the API return `Result` objects, and can be called using the `ets.helper.asyncCallWebApi` method, most of the `Get` methods do not return `Result` objects. Therefore, in cases when a `Result` object is not returned, failures should be checked for when the request is returned.

`/util/db`

Includes routes similar to those in the TrakSYS API `Data.Util` namespace.

* `/GetDataTable` - returns a `Result<DataTable>`.
* `/GetCachedDataTable` - returns a `Result<DataTable>`.
* `/ExecuteSql` - returns a `Result<bool>` after executing the given SQL statement.
* `/CheckConnection` - returns a `Result<bool>` to give the status of the TrakSYS Database connection.
* `/DatabaseDisplayName` - returns a string with the name of the current TrakSYS Database. Note: this method does not return a `Result` object, failures should be checked for after the request is returned.

### Parameters & Encoding

Typically, `GET` requests require parameters to be passed along the URL. The TrakSYS Web API includes helper functions to encode these parameter values. For example, numerical values or SQL strings should be encoded in order to be passed along the `GET URL` correctly. See the [JavaScript Reference](../tsweb/javascript-reference/ets/util/encodeurlvalue) for further information.

* `ets.util.encodeUrlValue("SELECT TOP 1 * FROM tSystem");`

Parameters in the TrakSYS Web API are named after their TrakSYS API base counterpart. For example, in the TrakSYS API, the `GetDataTable` method is declared as:

* `Result<DataTable> DbUtilityService.GetDataTable(string sql, [string connectionString], [int commandTimeout])`

Thus, when this route is called in JavaScript (i.e. `ets.rootPath + '/api/{SiteKey}/Util/Db/GetDataTable?...'`), QueryString parameters should include SQL and optional values for `ConnectionString` and `CommandTimeout`. See the [API Reference]() for the specific Model or Service being called to determine which Parameters to use.

### Full URL

A typical `GET` request URL is comprised of the `ets.rootPath`, the route, and possibly encoded parameters. For example:

* `var getUrl = ets.rootPath + '/api/{SiteKey}/Util/Db/GetDataTable?Sql=' + ets.util.encodeurlValue(sql);`

A typical `POST` request URL is comprised of the `ets.rootPath` and the route. For example,

* `var postUrl = ets.rootPath + '/api/{SiteKey}/data/DbSystem/Save/UpdateExisting';`

## Calling

### GET Requests

Depending on whether or not a call returns a result object determines how to make the `GET` request. If a `Result` object is returned, the `ets.helper.asyncCallWebApi` method can be used. If a `Result` object is not returned, the jQuery `$.get` function can be used.

**ets.helper.asyncCallWebApi**

```javascript
var getUrl = ets.rootPath + '/api/Home/Util/Db/GetDataTable?Sql=' + ets.util.encodeUrlValue(sql);
ets.helper.asyncCallWebApi({ url: getUrl })
  .done(function(dt) {
    for(row in dt.Return) {
      // some code ... dt.Return[row]['ColumnName']
    }
  })
  .fail(function(r) {
    ets.debug.logArray(r.Messages);
  });
```

{% hint style="warning" %}
Replace `Home` in `getURL` with a valid Site Key.
{% endhint %}

**$.get**

```javascript
var getUrl = ets.rootPath + '/api/Home/Data/DbArea/Load/ByID?ID=' + 1;
$.get(function(getUrl).done(function(a) {
  // update UI

  // save object for later
  area = a;
})
.fail(function() {
  ets.debug.log('Area load failed!');
});
```

{% hint style="warning" %}
Replace `Home` in `getURL` with a valid Site Key.
{% endhint %}

{% hint style="warning" %}
If these requests are to be done when the page loads, run in `ets.bb.page.on('ready', function() { // request code });`
{% endhint %}

### POST Requests

Depending on whether or not a call returns a `Result` object determines how to make the `POST` request. If a `Result` object is returned, the `ets.helper.asyncCallWebApi` method can be used. If a result object is not returned, the jQuery `$.post` function can be used.

**ets.helper.asyncCallWebApi**

```javascript
var postUrl = ets.rootPath + '/api/Home/Data/DbArea/Save/UpdateExisting';
ets.helper.asyncCallWebApi({ url: postUrl, type: 'POST', data: JSON.stringify(area), contentType: 'application/json' })
  .done(function(r) {
    alert(r.Success);
  })
  .fail(function(r) {
    ets.debug.logArray(r.Messages);
  });
```

{% hint style="warning" %}
Replace `Home` in `getURL` with a valid Site Key.
{% endhint %}

**$.post**

```javascript
var postUrl = ets.rootPath + '/api/Home/Data/DbArea/Save/UpdateExisting';
$.post(postUrl, area)
  .done(function(r) {
    alert(r.Success);
  })
  .fail(function(r) {
    ets.debug.logArray(r.Messages);
  });
```

{% hint style="warning" %}
Replace `Home` in `getURL` with a valid Site Key.
{% endhint %}
