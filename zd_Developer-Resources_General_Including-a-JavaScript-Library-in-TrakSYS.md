# Including a JavaScript Library in TrakSYS

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004358527-Including-a-JavaScript-Library-in-TrakSYS*
*Last updated: 2025-05-21T22:49:59Z*

---

Applies To | TrakSYS 10.0.4+

### **Summary**

This article addresses the best way to include JavaScript libraries in TrakSYS. It is **_not_** recommended to globally include JavaScript libraries for the entire web application. The main reason is that typically a special library is only required for a few pages. Global inclusion will incur a negative performance overhead on every page, as well as potentially introducing JavaScript memory leaks.

### **Overview**

The recommended approach to loading JavaScript libraries is to use the TrakSYS implementation of the module loading pattern. On pages that need the particular library, as part of the TrakSYS JavaScript page loading, the library is requested by key, which will return a `Promise` object. The key is provided so that if other parts on the page want to use the same library, it is only downloaded once. The `Promise` object provides a standard mechanism to start writing code only once the library has successfully downloaded.

By leveraging this pattern, you can include JavaScript libraries using TrakSYS Library Items. This code can be incorporated into Content Parts, letting them use JavaScript libraries without having to include a library file on every page.

#### **Example**

The following example downloads the [d3js v4](https://d3js.org/) library from the Internet and uses it to display a simple "Hello World" example.

First add a Div Part (`TsDiv)` to the Page with an ID of "D3Chart".

In the page's code behind (the Script editor), add the following code to the `ContentPage_Final()` method:
    
    
    this.Ets.Js.AddScriptSrc("https://d3js.org/d3.v4.min.js");
    

Finally, enter the following code in the JavaScript editor (NOT the Shared JS).
    
    
    ets.readyAll(function(page) {
        var w = 500;
        var h = 100;
        var svg = d3.select('#D3Chart').append('svg')
          .attr('width', w)
          .attr('height', h)
          .style('background-color', '#63b1dc'); // tscolor-blue-light
        svg.append('text')
          .text('hello d3 world')
          .attr('x', 100)
          .attr('y', 50);
    });
    

#### **See Also**

  * [Creating a link for a Library Item](https://portal.parsec-corp.com/hc/en-us/articles/115004358707)
  * [D3.js : d3js.org](https://d3js.org/)


