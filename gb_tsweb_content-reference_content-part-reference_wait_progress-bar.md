# Progress Bar

A linear bar to show the progress of an action.

## General

### Height

Specifies a fixed height (in pixels) for the Progress Bar part.

### Appearance | Gutter Color

Specifies the background color for the Progress Bar.

### Appearance | Striped

When enabled, a striped pattern will appear on the Progress Bar.

### Appearance | Animated

When enabled, the striped pattern will be animated across the Progress Bar. The Striped setting must be enabled to view the effect.

### Data | Minimum Value

Specifies the minimum value to be displayed on the Progress Bar.

### Data | Maximum Value

Specifies the maximum value to be displayed on the Progress Bar.

### Data | Value

Specifies the current value to be displayed on the Progress Bar.

## Point

### Label | Text

An expression or constant that specifies the text that will be rendered on the Progress Bar.

### Label | Font Size

Specifies the font size for the text that will be rendered on the Progress Bar.

### Label | Color

Specifies the font color for the text that will be rendered on the Progress Bar.

### Tip

An expression or constant that specifies the tool-tip text that will be rendered when hovering over the Progress Bar.

### Color

Specifies the color to be displayed on the Progress Bar.

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
