# require

```javascript
jQueryPromise require(String libraryKey, [String libraryUrl])
```

Require allows including of a JS file in a page only when needed. Once a file is added, additional calls with the same `libraryUrl` or `libraryKey` will not be added to the page again. This method should not be confused with node.js's require.

## Parameters

```javascript
String libraryKey
```

```javascript
String libraryUrl = ""
```

## Examples

### Using External Library Chart.js

* Create a Visual Content Page
* Add a View Fragment

```html
<div class="col-sm-12 tscontentpart-dynamic">
  <canvas id="MyChart" width="400" height="400"></canvas>
</div>
```

* Add code to page's JS

```javascript
ets.bb.page.listenTo(ets.bb.page, 'ready', function (page) {
  var promise = page.require('chartjs', 'https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.4.0/Chart.js');
  promise.done(function () {
    createMyChart();
  });
});

function createMyChart() {
  var data = {
    labels : ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"],
    datasets : [{
        label : "My dataset",
        borderWidth : 1,
        data : [75, 29, 81, 70, 89],
      }
    ]
  };

  new Chart($('#MyChart'), {
    type : 'bar',
    data : data,
    options : {
      responsive : false
    }
  });
}
```
