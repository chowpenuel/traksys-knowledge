# log

```javascript
void log(Any info, [String objectCaption], [Number maxArray])
```

This function outputs debug information to the browser's console window, as well as to the debug pop-up near the bottom of the page.

## Parameters

```javascript
Any info
```

```javascript
String objectCaption = ""
```

The caption will be displayed directly above the log in the debug window.

```javascript
Number maxArray = 10
```

If `info` is an array and has a length larger than the maxArray, individual items in the array will not be rendered.

## Examples

### Simple Log Entry

Code:

```javascript
ets.debug.log('test');
```

Output:

```javascript
17:11.162 test
```

### Object data display with Caption

Code:

```javascript
var obj = { name: 'My Object', number: 5 };
ets.debug.log(obj, 'My Caption');
```

Output:

```javascript
17:11.597 My Caption
          name = My Object
        number = 5
```

### Nested Object Data

Code:

```javascript
var obj = {
    name: 'Nested Data',
    number: 42,
    owner: {
        fname: 'Arthur',
        lname: 'Dent'
    },
    dolphins: []
};
ets.debug.log(obj);
```

Output:

```javascript
17:12.006 name: 'Nested Data',
        number: 42,
        owner: object
        dolphins: array[0]
```
