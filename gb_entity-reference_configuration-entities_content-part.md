# Content Part

## Summary

### Entity Name

Content Part

### Database Table Name

`tContentPart`

### API Object Name

`DbContentPart`

### Entity Description

Custom Content Parts allow the creation of parts with editable View and Script. Custom Content Parts support HTML5, ASP.NET controls, and TrakSYS parts. Intended for for extensibility purposes where standard Content Parts cannot fufill specific requirements, Custom Content Parts can be reused on Visual Pages throughout the TrakSYS application the same way as standard Content Parts.

{% hint style="info" %}
Any modifications made to a Custom Content Part will affect all instances of that part currently in use.
{% endhint %}

## Properties

`Content Part Group ID [ ContentPartGroupID ]`

Specifics the parent Content Part Group.

`Content View [ ContentView ]`

Contains the Front-End HTML/ASP.NET User for this Content Part.

`Content Code [ ContentCode ]`

Contains the script for this Content Part.
