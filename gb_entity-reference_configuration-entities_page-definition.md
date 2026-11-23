# Page Definition

## Summary

### Entity Name

Page Definition

### Database Table Name

`tPageDefinition`

### API Object Name

`DbPageDefinition`

### Entity Description

Each row in this table represents a Page Definition.

## Properties

`Parent GUID [ ParentGuid ]`

Specifies the GUID value of the parent page when the current page is a Shadow Copy. Additionally, this field shows the GUID of the parent page if the current page is included in the TrakSYS Template Transfer functionality.

`Navigation Icon CSS [ NavigationIconCss ]`

CSS that specifies the navigation icon displayed.

`Page Title [ PageTitle ]`

The title text of the Page Definition.

`Site Page Definition ID [ SitePageDefinitionID ]`

The unique identifier of the Site Page Definition under which the Page Definition is configured.

`Section Page Definition ID [ SectionPageDefinitionID ]`

The unique identifier of the Section Page Definition under which the Page Definition is configured.

`Hub1 Page Definition ID [ Hub1PageDefinitionID ]`

The unique identifier of the Hub1 Page Definition under which the Page Definition is configured.

`Hub2 Page Definition ID [ Hub2PageDefinitionID ]`

The unique identifier of the Hub2 Page Definition under which the Page Definition is configured.

`Hub3 Page Definition ID [ Hub3PageDefinitionID ]`

The unique identifier of the Hub3 Page Definition under which the Page Definition is configured.

`Page Level Type [ PageLevelType ]`

The Page Definition's level type with respect to the page hierarchy.

`Is Visible In Navigation [ IsVisibleInNavigation ]`

This field determines whether or not the Page Definition is visible in the TrakSYS Web navigation.

`Is Header Visible [ IsHeaderVisible ]`

This field determines whether or not the Page Definition's header is visible.

`Is Footer Visible [ IsFooterVisible ]`

This field determines whether or not the Page Definition's footer is visible.

`Is Title Visible [ IsTitleVisible ]`

This field determines whether or not the Page Definition's title is visible.

`Is Bread Crumbs Visible [ IsBreadCrumbsVisible ]`

This field determines whether or not the Page Definition is visible in breadcrumbs navigation.

`Is Spokes Visible [ IsSpokeVisible ]`

This field determines whether or not the spokes under the Page Definition are visible.

`Is Tree Visible [ IsTreeVisible ]`

This field determines whether or not the navigation tree is visible when viewing the Page Definition.

`Instance Type [ InstanceType ]`

The Page Definition's configured instance type.

`Instance Script [ InstanceScript ]`

The script used for instancing of the Page Definition.

`Value Script [ ValueScript ]`

The script used for adding entries to the Values Dictionary when the Page loads.

`CSS [ Css ]`

Custom CSS shared by the Page Definition and Page Definitions under it.

`JavaScript [ Js ]`

Custom JavaScript shared by the Page Definition and Page Definitions under it.

`Content Mode [ ContentMode ] : ETS.Core.Enums.ContentPageMode`

Enum for the Page Definition's content mode.

* **Visual** = 0
* **Open** = 1
* **Key** = 2

`Content View [ ContentView ]`

The gridview content of the Page Definition.

`Content Code [ ContentCode ]`

The C# page script content of the Page Definition.

`Content Key [ ContentKey ]`

Read-only field for the Page Definition's key, which can be referenced to link directly to the page using `c={ContentKey}` format. Content Mode = 2 only.

`Content Page Parameters [ ContentPageParameters ]`

JSON string of the Page Definition's Content Properties. Content Mode = 2 only.

`Content JavaScript [ ContentJs ]`

Custom JavaScript of the Page Definition.

`Content Css [ ContentCss ]`

Custom CSS of the Page Definition.

`Preview Url [ PreviewUrl ]`

The preview URL of the page defintion. Used to preview the page during development.

`Refresh Seconds [ RefreshSeconds ]`

The Page Definition's refresh period in seconds.

`RefreshKeys Ex [ RefreshKeysEx ]`

The expressionable key that will refresh the page when broadcast.

`Return URLs Excluded [ ReturnUrlsExcluded ]`

This property affects how `ETS.ReturnUrl` is determined.

It represents a list of URLs (separated by carriage return) that are excluded from consideration for navigation when the Back Button is clicked. The asterisk (`*`) may be used as a wildcard, and it is not necessary to specify querystring elements. For example, the entry `*/LineOverview` excludes any URL that ends with `LineOverview` from consideration.

This list is evaluated on the page where the Back button is shown. For example, if you have a Section page with a Spoke page and you want the Back button to ignore the Spoke, add the Spoke URL pattern to the Section page properties.

Entries are matched against full page URLs using the normal `/TS/pages/<site_externalID>/...` pattern, with wildcard support. For example, `/TS/pages/root/config*` excludes all pages under root config. Equivalent patterns such as `*root/config*` or `*/config*` will also match.

{% hint style="info" %}
Example Scenario

You have three pages: **Line Overview** (section), **Event Overview** (hub), and **Event Edit** (spoke). You want the Back button on **Event Overview** to return to **Line Overview**, and you want to avoid treating **Event Edit** as the “previous page” when you come back from editing.

* You start on **Line Overview**.
* You click into **Event Overview**. **Event Overview** stores its Return URL as **Line Overview**.
* From **Event Overview**, you open **Event Edit**. **Event Edit** stores its Return URL as **Event Overview**.
* You save and return to **Event Overview**. TrakSYS would normally update **Event Overview**’s Return URL to **Event Edit**, but **Event Overview** excludes **Event Edit**.
* Because it’s excluded, **Event Overview** keeps the prior Return URL, so the Back button still takes you to **Line Overview**.
{% endhint %}

`Back Visible [ IsBackVisible ] : ETS.Core.Enums.InheritableBoolean`

Determines whether the Back button will be visible for a page.

`Back Button Caption [ BackCaption ]`

Specifies the caption of the Back button. If no value is provided, the button will display "Back."

`Back Icon [ BackIconCss ]`

Contains the CSS Class used to reference an Icon for the button.

`Template Bypass [ TemplateBypass ]`

Contains a Boolean value that determines whether the entity will be excluded from the TrakSYS Template Transfer functionality. This also determines whether this page will stop receiving change updates from a parent page if the current page is a Shadow Copy.
