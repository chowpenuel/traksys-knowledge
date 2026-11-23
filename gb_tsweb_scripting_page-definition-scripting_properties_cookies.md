# Cookies

## IEtsCookieDictionary Cookies

Allows access to the `Cookies` dictionary, providing an interface for interacting with a user's browsing session state using Cookies.

### Interfaces

```csharp
public interface IEtsCookieDictionary : 
IDictionary<string, object>,
ICollection<KeyValuePair<string, object>>,
IEnumerable<KeyValuePair<string, object>>,
IEnumerable
```

## Examples

The following code demonstrates the most simple and straightforward way to set and then examine a cookie value.

{% tabs %}
{% tab title="Setting a Cookie" %}
This example uses the dictionary's indexer syntax as a simple way to add the cookie:

```csharp
protected void SetCookieValue_Click(object sender, EventArgs e)
</strong>{
  const string cookieKey = "MY_TEST_COOKIE";
  
  // Generate a random number for the value
  var value = new Random().Next(100);
  
  this.Ets.Cookies[cookieKey] = value;
  return;
}
```
{% endtab %}

{% tab title="Reading a Cookie" %}
This example uses the standard TrakSYS extension method `GetAsInt()` to retrieve a cookie value and then parse it as an integer:

```csharp
protected override bool ContentPage_Init()
{
  const string cookieKey = "MY_TEST_COOKIE";
  
  // read the value from the key
  var value = this.Ets.Cookies.GetAsInt(cookieKey);
  
  // stick the value into the values dictionary for display somewhere on the page.
  this.Ets.Values["SomeKey"] = value;
}
```
{% endtab %}
{% endtabs %}

## Methods

The Cookies Dictionary implements the `IDictionary` which has its own set of shared extensions. See [Dictionaries](dictionaries) for more.

### Cookies Dictionary Methods

`IEtsCookieDictionary` separately defines the following methods:

```csharp
void Add(string key, object value, TimeSpan timeSpan)
void Add(KeyValuePair<string, object> item, TimeSpan timeSpan)
void SetCookieValue(string key, object value, TimeSpan span)
```

Each sets a cookie named `ETS.CCC.{key}` to the provided `value`. The cookie's expiration is set to the current time + the provided `span`.

It is recommended to provide a span, but for certain overloads `span` is optional. If not provided, it will default to one year.

### Remarks

#### Cookie Duration

You can control the amount of time that a cookie persists in the user's browsing session. Two options exist:

1. Using **indexer syntax**, the cookie's duration will be set to the special value `Session`. This means that the cookie will last only as long as the user's browsing session is active. If they close their browser, log out, or restart their computer, the cookie will be discarded.
2. Using the **`SetCookieValue` method**, you specify an amount of time with the `span` parameter. This will set the cookie's expiration date to a value calculated as the current time + `span`.

#### Removing Cookies

You can remove a cookie immediately by removing the entry from the dictionary. The recommended way to achieve this is to use `RemoveByKeyIfExists(string key)` . Removing an entry from the dictionary will cause TrakSYS to _invalidate_ the cookie by setting its value to empty, and its expiration time to the current time; which in turn causes the user's browser to remove the cookie.

You should _not_ attempt to invalidate a cookie by just changing its value to a "null" or empty value.

```csharp
protected void DeleteMyCookie_Click(object sender, EventArgs e)
{
  const string cookieKey = "MY_TEST_COOKIE";
  
  // ❌ Don't do this:
  this.Ets.Cookies[cookieKey] = null;
  
  // ✅ The safe way to empty or remove a cookie.
  this.Ets.Cookies.RemoveByKeyIfExists(cookieKey);

  // ✅ Alternatively, remove all cookies.
  this.Ets.Cookies.Clear();
  
  return;
}
```
