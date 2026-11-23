# Initialization Order

The initialization order of the various parts on a Page are key to ensuring data is retrieved and displayed properly. The Order tab of a Visual Page Definition helps simplify the initialization ordering process by providing a simple user interface.

## Orders

The Order page displays the various Content Parts on the Page as small tiles organized by their Initialization Order (e.g. - Order 5 : 1). A Content Part's initialization order is made up of an Initialization Order, then within that the Initialization Order there is an Initialization Order Sub for further granularity. To edit a Part's Initialization Order either double-click the tile representing the Part or click the tile once and click the "Change Order" button. This can also be done from the Part's properties under the Advanced tab (on the Parts Page).

## Colors

The default color of the tile representing a Content Part is blue. However, if there is a problem with the initialization order of the Part, its color may reflect the issue.

### Orange

If the tile representing a Content Part is orange, the Target or Source Data Key for that part is blank. If this occurs, ensure that all parts have a Target and Source Data Key configured.

### Red

If the tile representing a Content Part is red, the Source Data Key does not exist at the time (in the current execution order of the page). In this case, edit either this Part to ensure that it loads after its Source Data Key is available (later Initialization Order, such as 10), or edit its Data Source to an earlier Initialization Order (such as 1).
