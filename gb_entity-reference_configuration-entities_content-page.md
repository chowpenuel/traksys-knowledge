# Content Page

## Summary

### Entity Name

Content Page

### Database Table Name

`tContentPage`

### API Object Name

`DbContentPage`

### Entity Description

Custom Content Pages allow the creation of pages with editable View and Script. Custom Content Pages support HTML5, ASP.NET controls, and TrakSYS parts. Intended for extensibility purposes where standard Content Pages cannot fulfill specific requirements, Custom Content Pages can be reused throughout the TrakSYS application the same way as standard Content Pages.

{% hint style="info" %}
Any modifications made to a Custom Content Page will affect all instances of that page currently in use.
{% endhint %}

## Properties

`Content Page Group ID [ ContentPageGroupID ]`

Specifies the parent Content Page Group.

`Content View [ ContentView ]`

Contains the Front-End HTML/ASP.NET User Controls for this Content Page.

`Content Code [ ContentCode ]`

Contains the script for this Content Page.

`Content JS [ ContentJS ]`

Contains the JavaScript for this Content Page.

`Content Css [ ContentCss ]`

Contains the CSS for this Content Page.

`Return URLs Excluded [ ReturnUrlsExcluded ]`

Contains the URLs that will be excluded when the user clicks the Back button on a Content Page.

`Back Visible [ IsBackVisible ]`

Determines whether the Back button will be visible for a Content Page

`Back Button Caption [ BackCaption ]`

Specifies the caption of the Back button. If no value is provided, the button will display "Back."

`Back Icon [ BackIconCss ]`

Contains the CSS Class used to reference an Icon for the button.
