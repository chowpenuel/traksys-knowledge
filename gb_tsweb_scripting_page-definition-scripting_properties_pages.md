# Pages

## IPageLocationInfo Pages

Allows access to the `Pages` class which contains properties such as ApplicationPath, SuccessUrl, and methods such as `RedirectToSelf` and `RedirectToSuccessUrl`.

### Properties

```csharp
string ApplicationPath
```

Gets the absolute path to the TrakSYS application, typically "/TS".

```csharp
string BaseRoutePath
```

Gets the absolute path on which all URLs within the application are based.

```csharp
List<LinkItemViewModel> BreadcrumbItems
```

Gets a list of Breadcrumbs that appear on this Page (if `IsBreadcrumbsVisible` set to true).

```csharp
int ContentPageDefinitionID
```

Gets the Page Definition ID of this instanced Page.

```csharp
string ContentPageIconCss
```

Gets the Page Icon Css (e.g. - "tsicon-blank") of this instanced Page.

```csharp
ContentPageMode ContentPageMode
```

Gets the ContentPageMode of this Page (i.e. - Visual, Open, Key).

```csharp
string ContentPageRefreshKeysEx
```

Gets the Refresh Keys configured on this Page.

```csharp
int ContentPageRefreshSeconds
```

Gets the Refresh Seconds configured on this Page.

```csharp
string DocumentTile
```

Gets the name of this Page Definition (this is the Name property in the configuration for this Page Definition).

```csharp
string FolderUrl
```

Gets this Page's URL up until the last enclosing folder. Typically, this is the entire URL excluding the Spoke (if applicable).

```csharp
string FullUrlPath
```

Gets the full URL path to this Page including the query string.

```csharp
IPageContext Hub1
```

Contains this Hub1 if the current Page is a Hub1 or the parent Hub1 if this is a Spoke or Hub 2 beneath a Hub1 in this Section's hierarchy. Otherwise, this is null.

```csharp
List<PageMenuItem> Hub1s
```

Contains a list of all the level-one Hubs in this Section's hierarchy.

```csharp
List<PageMenuItem> Hub1Spokes
```

Contains a list of all the Spokes belonging to this Hub1 (if the current Page is a Hub1) or the parent Hub1 in this hierarchy.

```csharp
IPageContext Hub2
```

Contains this Hub2 if the current Page is a Hub2 or the parent Hub2 if this is a Spoke beneath a Hub2 in this Section's hierarchy. Otherwise, this is null.

```csharp
List<PageMenuItem> Hub2s
```

Contains a list of all the level-two Hubs in this Section's hierarchy.

```csharp
List<PageMenuItem>Hub2Spokes
```

Contains a list of all the Spokes belonging to this Hub2 (if the current Page is a Hub2) or the parent Hub2 in this hierarchy.

```csharp
bool IsBreadcrumbsVisible
```

Gets or sets whether the Breadcrumbs on this Page are visible.

```csharp
bool IsCEquals
```

Gets whether or not this Page is a "c equals" Page, that is, a Content Page that is not instanced, but rather referenced using the "c=" parameter on the query string (e.g. - c=ETS.Application.Event.EventAttention).

```csharp
bool IsClientDirtyCheckEnabled
```

When set to true, this property will add an asterisk (\*) to the Page Title at the top of the Page any time a change is made and will prompt an alert if the user tries to navigate away before submitted an edited form. The default value of this property is false.

```csharp
bool IsFooterVisible
```

Gets or sets whether the Footer on this Page is visible.

```csharp
bool IsHeaderVisible
```

Gets or sets whether the Header on this Page is visible.

```csharp
bool IsSpokesVisible
```

Gets or sets whether the Spokes on this Page are visible.

```csharp
bool IsTitleVisible
```

Gets or sets whether the Title on this Page is visible.

```csharp
bool IsTreeVisible
```

Gets or sets whether the Tree on this Page is visible.

```csharp
string PageUrl
```

Gets this Page's current URL.

```csharp
string QueryString
```

Gets the `QueryString` of this Page as a string.

```csharp
string ReturnUrl
```

Contains the Return URL of this page. This is typically the URL of the referring Page, however this can be overwritten.

```csharp
IPageContext Section
```

Contains this Section if the current Page is a Section or the parent Section if this is a Hub or Spoke beneath a Section in the hierarchy.

```csharp
List<PageMenuItem> Sections
```

Contains a list of all the Sections belonging to this Page's Site.

```csharp
List<PageMenuItem> SectionSpokes
```

Contains a list of all the Spokes belonging to this Section (if the current Page is a Section) or the parent Section in this hierarchy.

```csharp
IPageContext Site
```

Gets the current Site (Page Definition) of this Page.

```csharp
int SiteID
```

Gets the `SiteID` of this Page.

```csharp
List<PageMenuItem> Sites
```

Gets all the PageMenuItems of the different Site Pages for this application.

```csharp
List<PageMenuItem> SiteSpokes
```

Contains a list of all the Spokes belonging to this Site (if the current Page is a Site Page) or the parent Site in this hierarchy.

```csharp
IPageContext Spoke
```

Contains this Spoke if the current Page is a Spoke, otherwise, this is null.

```csharp
List<LinkItemViewModel> SpokeItems
```

Gets a list of the Spoke links visible in the top right corner of the Page (if `IsSpokesVisible` set to true).

```csharp
string SuccessUrl
```

Contains the Success URL of this Page. This is typically the URL of the referring page (i.e. - the same as the Return URL), but may be overwritten. This is typically the Page which will be redirected to upon successful execution.

```csharp
string Title
```

Gets the Page Title of this Page Definition (this is the Page Title property in the configuration for this Page Definition).

```csharp
string UrlPath
```

The URL path of this Page (without query string parameters).

### Methods

```csharp
void BroadcastChangeNotificationForKey(string key)
```

Broadcasts a refresh throughout the application for the provided Refresh Key.

```csharp
string BuildSelfUrlIfNecessary(string url)
```

Returns a URL; if the URL parameter provided begins with `self:`, this Page's URL is returned with the query string of the provided URL parameter. Otherwise, this Page's URL is returned.

```csharp
string BuildUrlPathForLevel(PageDefinitionLevel level)
```

Returns a URL path built up until the PageDefinitionLevel provided.

```csharp
bool CurrentUrlEquals(this IPageLocationInfo pages, string compareToUrl, params KeyValuePair<string, string>[] keys)
```

Determines whether the provided parameters (URL and query string parameters in the form of a KeyValuePair) are the same as the this Page's current URL. This is an extension method defined in ETS.Core.Extensions.ControlExtensions.

```csharp
bool IsSameUrl(string compareUrl, [bool ignoreTrace])
```

Determines whether this Page's current URL is the same as the `compareURL` parameter provided.

```csharp
bool RedirectToAccessDenied(this IPageLocationInfo page, [string set], [string item], [string action])
```

Redirects to the standard Access Denied page. Optional parameters may be included for a more verbose error when the user is redirected. This is an extension method defined in ETS.Core.Extensions.ControlExtensions.

```csharp
bool RedirectToErrorPageWithCode(this IPageLocationInfo page, int code)
```

Redirects to the standard Error Page displaying the parsed error of the provided HTTP error code (e.g. 404). This is an extension method defined in ETS.Core.Extensions.ControlExtensions.

```csharp
bool RedirectToLicenseErrorPage(this IPageLocationInfo page)
```

Redirects to the standard License Error Page. This is an extension method defined in ETS.Core.Extensions.ControlExtensions.

```csharp
bool RedirectToPageUrl()
```

Redirects to this Page's URL (without query string parameters).

```csharp
bool RedirectToReturnUrl()
```

Redirects to this Page's Return URL. This is typically the URL of the referring page, but may be overwritten.

```csharp
bool RedirectToSelf()
```

Redirects to this Page's URL (including query string parameters).

```csharp
bool RedirectToSelfAddReturnUrl()
```

Redirects to this Page's URL (including query string parameters) and adds the Return URL as a query string parameter.

```csharp
bool RedirectToSuccessUrl()
```

Redirects to this Page's Success URL. This is typically the URL of the referring page (i.e. - the same as the Return URL), but may be overwritten.

```csharp
bool RedirectToUrl(string url, [bool endResponse])
```

Redirects to the provided `url` parameter.
