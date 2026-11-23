# Querystring

```javascript
Class ets.objects.Querystring([String baseQs])
```

An object that can be instantiated and assist in managing HTML Query String parameters, allowing more structured access to the Query String and control of adding or updating specific values. On each page request, the global object ets.querystring is automatically instantiated and contains all of the Query String values for the current page.

## Parameters

```javascript
String baseQs = undefined
```

If the baseQs is not passed in then the current URL will be used.

## Examples

### Basic Example

```javascript
var currentQueryString = new ets.objects.Querystring(); // returns current page Querystring
 
var customQuerystring = new ets.objects.Querystring('/ts/pages/home/demo?systemID=5&title=Line+A'); // returns the custom URL's Querystring
```
