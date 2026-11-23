# SimpleView

```javascript
Class ets.bb.dataBinding.SimpleView(Backbone.Model dataSource, jQuery $template, jQuery $output, [Boolean initialRender], [String isVisibleProperty])
```

One way data binding for Backbone models. The template binding format includes:

`{{ if()... }}` - JS evaluate `{{: propertyName }}` - HTML encode `{{= propertyName }}` - Render string without HTML encoding

## Parameters

```javascript
Backbone.Model dataSource
```

Can be a Backbone model or collection.

```javascript
jQuery $template
```

jQuery object that contains the HTML template.

```javascript
jQuery $output
```

```javascript
Boolean initialRender = true
```

If `true`, `$template` will be render on object creation. If `false`, `$template` will be rendered when a property on the `dataSource` changes or `render` method is called.

```javascript
String isVisibleProperty = ""
```

This is the property name on the `dataSource` that determines if the `$output` is visible or not during render. This property is ignored for Backbone collections.

## Examples

### Simple ReadOnly View

JavaScript code:

```javascript
// create backbone object
var meal = new Backbone.Model({
  "appetizer": "tomato soup",
  "entree": "mac & cheese",
  "dessert": "<strong>apple pie</strong>", // contains HTML tags and should not be rendered with encoding
  "isOrdered": true // will be used for simple JavaScript statement
});
```

```javascript
ets.bb.page.listenTo(ets.bb.page, "ready", function(page) {
  // it is okay to have the template and output be the same jQuery node.
  var view = new ets.bb.dataBinding.SimpleView(meal, $('#food-template'), $('#food'), /* initialRender */ true);
});
```

View Fragment part

```html
<div class="col-sm-12 tscontentpart-dynamic">
  <div id="food"></div>
  <div id="food-template" style="display:none">
    <h1>Lunch Order:</h1>
    {{ if (isOrdered) { }}<p>Order Placed!</p>{{ } else { }}<p>Order NOT Placed!</p>{{ } }}
    <ul>
      <li>Appetizer: {{:appetizer}}</li>
      <li>Main Course: {{:entree}}</li>
      <li>Dessert: {{=dessert}}</li>
    </ul>
  </div>
</div>
```

HTML output

```html
<div class="col-sm-12 tscontentpart-dynamic">
  <div id="food">
    <h1>Lunch Order:</h1>
    <p>Order Placed!</p>
    <ul>
      <li>Appetizer: tomato soup</li>
      <li>Main Course: mac &amp; cheese</li>
      <li>Dessert: <strong>apple pie</strong></li>
    </ul>
  </div>
  <div id="food-template" style="display:none">
    <h1>Lunch Order:</h1>
    {{ if (isOrdered) { }}<p>Order Placed!</p>{{ } else { }}<p>Order NOT Placed!</p>{{ } }}
    <ul>
      <li>Appetizer: {{:appetizer}}</li>
      <li>Main Course: {{:entree}}</li>
      <li>Dessert: {{=dessert}}</li>
    </ul>
  </div>
</div>
```

Try Data Binding

```javascript
meal.set("entree", "hamburger"); // the "Main Course" HTML will automatically change
meal.set("isOrdered", false); // the text '<p>Order NOT Placed!</p>' will be rendered
```
