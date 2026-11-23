# Tab Strip

A form input part that renders a dynamic number of tab selectors. Parts can be assigned to a tab using CSS classes. Clicking on a tab shows the assigned parts and hides the others.

{% hint style="warning" %}
This part is incompatible with the built-in PDF Export functionality. Attempting to use this part with that functionality will only allow the page to render content shown for the first tab. It is not possible to render content generated for other tabs.
{% endhint %}

## General

### Tabs | Caption

An expression or constant that specifies the caption displayed for the user interface element.

### Tabs | Anchor Key

Specifies the anchor name (HTML `<a name="">`) that will be rendered for the tab. This is useful when navigating to a page, and initializing the page to a specific tab. Each tab is required to have a unique Anchor Key value configured.

### Tabs | Tab Selector

Specifies a CSS class name that will be associated with the tab. This is used to assign specific parts to a tab. To assign a part to a tab, set the part's CSS Class property value to the CSS class name configured for the tab.

### Tabs | Visible

An expression or constant that evaluates to the string "0" or "1". If the value is "0", this element will NOT be rendered to the user interface.

### Tabs | Icon

Specifies the glyphicon CSS class for a built-in icon.\
\
Through the user interface, the icon can be selected by using a search tool and visual selector. When setting this property through code, it is recommended that the visual interface is used to locate the desired icon and the text value be retrieved and copy/pasted into code.

### Appearance | Layout Mode

Specifies the layout and alignment of the rendered tabs.

## Responsive

### Visible | Visible in LG Screen

When false, this part will be hidden (via client-side bootstrap CSS) when the browser screen size in in the bootstrap LG range. See the [bootstrap responsive utility reference](https://getbootstrap.com/css/#responsive-utilities) for details.

### Visible | Visible in MD Screen

When false, this part will be hidden (via client-side bootstrap CSS) when the browser screen size in in the bootstrap MD range. See the [bootstrap responsive utility reference](https://getbootstrap.com/css/#responsive-utilities) for details.

### Visible | Visible in SM Screen

When false, this part will be hidden (via client-side bootstrap CSS) when the browser screen size in in the bootstrap SM range. See the [bootstrap responsive utility reference](https://getbootstrap.com/css/#responsive-utilities) for details.

### Visible | Visible in XS Screen

When false, this part will be hidden (via client-side bootstrap CSS) when the browser screen size in in the bootstrap XS range. See the [bootstrap responsive utility reference](https://getbootstrap.com/css/#responsive-utilities) for details.

## Advanced

### CSS Class

Any CSS class values added to this property will be rendered to the part's HTML. While the CSS is typically rendered to an outer DIV element, the exact HTML element that this CSS is added to is part specific.

### Visible

When false, this part will NOT be rendered to the browser. For most visual parts, this means that any processing (Values Dictionary manipulation, data retrieval, etc...) will not be executed. For Data Table parts, setting the Visible to false will still allow the part to execute its query and place its resultant dataset in the Values dictionary, however any visual debugging elements will not be rendered.

### Initialization Order

Indicates the order that this part will be loaded and executed on the containing page. This value also indicates which script method (ContentPage\_PartPreInitXX) should be used to initialize properties just before the part is loaded. If this property is left blank, each part will load using its own default Initialization Order.

### Initialization Order Sub

Indicates the order that this part will be loaded and executed on the containing page. This property value is used in conjunction with the Initialization Order value to create the final load sequence (the Initialization Order Sub value is used as a decimal value added to the Initialization Order). For example if the Initialization Order is 3 and the Order Sub is 2, the actual load order would be 3.2.

If this property is left blank, each part will load using its own default Initialization Order Sub (typically 1).
