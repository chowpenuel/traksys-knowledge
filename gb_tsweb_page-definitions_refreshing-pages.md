# Refreshing Pages

The refresh architecture uses a modern push model. A Refresh Key is broadcast out and all clients (typically Page Definitions) listening for that Key will be refreshed. This is an efficient model as it reduces the amount of unnecessary refreshes and heavy taxing done when a Page reloads and executes a data intensive query. Now, refreshes only occur when certain criteria are met.

## Broadcasting

### Entities

Certain Entities such as Systems and Tags whose changes are felt in real-time can be configured to broadcast a Refresh Key. Tags will broadcast their configured Refresh Key (see the [Tag](../../entity-reference/configuration-entities/tag) Entity Reference Topic) when their value changes. Systems will broadcast their configured Refresh Key (see the [System](../../entity-reference/configuration-entities/system) Entity Reference Topic) when any of the following Entities related to the System change:

* KPI Calculations (including counts, etc.)
* Events (start and end)
* Samples
* Tasks

### ASP .NET Script

Refresh Keys can also be broadcast using ASP.NET Script. The first method can be used in the code behind of a Page Definition while the second method can be used in Scripts and even Data Management Modules since it is part of the TrakSYS API.

* `this.Ets.Pages.BroadcastChangeNotificationForKey("RefreshKey");`
* `this.Ets.Api.Util.Web.RefreshWebForKey("RefreshKey");`

Note that the WebServerPaths setting in Installation Manager TrakSYS Settings should be configured in order for Refresh Key broadcasts to function properly.

## Receiving

### Page Definitions

Refresh Keys can be used on all Page Definition Types (Content, Visual, and Open). The Refresh Key property on the Page Definition should be configured with the Refresh Key of the desired Entity. For example, if the Page Definition should refresh when a System change occurs (e.g. - a System Overview Dashboard), the Refresh Key property on the Page Definition should match the Refresh Key of a System, typically `SYSTEM.{SystemID}` (e.g. - SYSTEM.112).

### Instanced Pages

Instanced Page Definitions require a bit more attention. Depending on what the Page Definition is Instanced over (e.g. - Pages Instanced per System), will determine what the Refresh Key property on the Page Definition should be. For example, when a Page is instanced over Systems, since the Refresh Key is a Script type property, Values Keys are accepted. Therefore, the Refresh Key on the Page may be `SYSTEM.{SystemID}` or `SYSTEM.{SystemKey}`, but a Value must be provided in the Values Dictionary for the SystemID or SystemKey.

### Fixed Page Refresh

For cases when a fixed Page Refresh interval is necessary, Pages Definitions have a **Refresh Minutes** property. This property can be used to force a refresh of the Page every X minutes, independent of whether a Refresh Key for the Page was broadcast.
