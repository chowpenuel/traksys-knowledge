# isObjectButNotArray

```javascript
Boolean isObjectButNotArray(Any o)
```

Returns `true` if the `o` parameter is an object but not an array. In JavaScript, it is difficult to distinguish an object from and array, since all arrays are objects. This function aids in doing reflection-like operations on variables.

## Parameters

```javascript
Any o
```

## Examples

### Basic Examples

```javascript
// the following returns true
ets.util.isObjectButNotArray( new Date() );
ets.util.isObjectButNotArray( { } );
ets.util.isObjectButNotArray( ets );

// the following returns false
ets.util.isObjectButNotArray( [] );
ets.util.isObjectButNotArray( null );
ets.util.isObjectButNotArray( 1 );
ets.util.isObjectButNotArray( 'bac' );
ets.util.isObjectButNotArray( true );
```
