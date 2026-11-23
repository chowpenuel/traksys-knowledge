# Navigation Tiles

An array of dynamic Tiles that can be used as menu navigation. Each Tile can be configured with display text, an icon, background color and navigation URL, client (JS) action, or server side call-back to execute script.

## General

### Default Button Key

Specifies which Button will be rendered as the "default" Button. The default button will be activated when the "Enter" key is pressed on the page. This property is not required. The value specified here must match the Key value of a Button defined below.

### Tiles | Text 1

An expression or constant that specifies the main text caption for the item.

### Tiles | Text 2

An expression or constant that specifies the sub-text caption for the item.

### Tiles | Enabled

An expression or constant that evaluates to the string "0" or "1". If the value is "0", this element will be rendered as "disabled" (typically grayed out and not active).

### Tiles | Visible

An expression or constant that evaluates to the string "0" or "1". If the value is "0", this element will NOT be rendered to the user interface.

### Tiles | Width

Specifies the width (in bootstrap 1-12) for the item.

### Tiles | Icon

Specifies the glyphicon CSS class for a built-in icon.\
\
Through the user interface, the icon can be selected by using a search tool and visual selector. When setting this property through code, it is recommended that the visual interface is used to locate the desired icon and the text value be retrieved and copy/pasted into code.

### Tiles | Color

Specifies a color for the item.

### Advanced | Height

Specifies the relative height for the Tiles.

### Advanced | Text 1 Size

Specifies the relative font size for the Text 1 caption in the Tiles.

### Advanced | Text 2 Size

Specifies the relative font size for the Text 2 caption in the Tiles.

### Advanced | Icon Size

Specifies the relative icon size for the Tiles.

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

Any CSS class values added to this property will be rendered to the part's HMTL. While the CSS is typically rendered to an outer DIV element, the exact HTML element that this CSS is added to is part specific.

### Visible

When false, this part will NOT be rendered to the browser. This means that any processing (Values Dictionary manipulation, data retrieval, etc...) will not be executed.

### Initialization Order

Indicates the order that this part will be loaded and executed on the containing page. This value also indicates which script method (`ContentPage_PartPreInitXX`) should be used to initialize properties just before the part is loaded. If this property is left blank, each part will load using its own default Initialization Order.

### Initialization Order Sub

Indicates the order that this part will be loaded and executed on the containing page. This property value is used in conjunction with the Initialization Order value to create the final load sequence (the Initialization Order Sub value is used as a decimal value added to the Initialization Order). For example if the Initialization Order is 3 and the Order Sub is 2, the actual load order would be 3.2.

If this property is left blank, each part will load using its own default Initialization Order Sub (typically 1).
