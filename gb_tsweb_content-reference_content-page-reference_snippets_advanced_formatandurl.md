# Advanced\_FormatAndUrl

Format | Product

Determines how Product information, if any, will be formatted on the page. The "Name Only" or "Code Only" will show either the Product Name or the Product Code, respectively. The "Name and Code" option will show the Product Name with the Product Code in brackets (e.g. ProductName \[ ProductCode ] ). Conversely, the "Code and Name" option will display the Product Code with the Product Name in brackets. This format can be set using the Values Key `Theme.FormatProduct` and passing in a valid enum value.

#### Format | Date/Time

Determines how Date/Time information, if any, will be formatted on the page. See the [Number and Date Format](../../../expression-syntax/format/number-and-date-format) topic. This format can be set using the Values Key "Theme.FormatDateTime" and passing in a valid Date/Time format.

#### Format | Date

Determines how Dates, if any, will be formatted on the page. See the [Number and Date Format](../../../expression-syntax/format/number-and-date-format) topic. This format can be set using the Values Key "Theme.FormatDate" and passing in a valid Date format.

#### Format | Quantity

Determines how quantities, if any, will be formatted on the page. See the [Number and Date Format](../../../expression-syntax/format/number-and-date-format) topic. This format can be set using the Values Key "Theme.FormatQuantity" and passing in a valid Number format.

#### Format | Tile

Determines how a Tile, if any, will be displayed on the page. This format can be set using the Values Key "Theme.FormatTile" and passing in a valid enum value.

#### URL | Success URL

This field determines where the Page will redirect upon successful execution. If no value is provided, the Return URL is used.

#### URL | Return URL

This field determines where the Page will redirect if the User decides to cancel execution and go back to a previous Page. If no value is provided, the user will be returned to the Page from which they came.
