# Resource Translation

TrakSYS allows for the translation of user interfaces via Resource Strings. Resources containing translations can either be compiled into files or added directly into the TrakSYS database. Resource Strings can be referenced and used on all Page and Part types.

## Configuration

### Locales

The Locale determines what language Resource Items will be translated to. A single Resource Item may have translations in each Locale. The Locale is represented by the standard Microsoft culture abbreviations (e.g. - Spanish is abbreviated `es`).

Typically, Locales are looked up based on the current culture of the browser. However, User configuration also includes a Locale property to allow Users to always view TrakSYS in the specified Locale.

### Resource Groups

Organizational group for Resource Items. Typically a Resource Group represents a Page, where all the Resource Items may be translatable strings on the Page. The Group Key must be unique.

### Resource Items

Resource Items are the actual Resource String that will be translated. The Item Key must be unique within the Resource Group. An Item's content can be dynamic. For example, if the Item is to display `"Area 3 - Operator View for Line 5"`, where the area name and line number varies, the Resource Item text can be configured as `"Area {0} - Operator View for Line {1}"`. The parameters can be sent in when translating the Item, see below.

### Translations

Translating Items can be done on a per Resource Item basis, or an entire Locale can be exported which provides an Excel (xlsx) file comprised of all the translatable Resource Items within a given Locale. Once the translations are complete in the Excel sheet, they can be imported into TrakSYS.

{% hint style="info" %}
For Multi-Site installations, Translations are configured on the Root Site.
{% endhint %}

## Implementation

### Syntax

The typical syntax of a Resource String is **`resx:Group_Key.Item_Key`**,Assembly\_Key and is comprised of the following:

#### Prefix

The prefix **`resx:`** denotes that the string is a translatable Resource String Item.

#### Group Key

The **`Group_Key`** determines which Resource Group too look up the Resource Item.

#### Item Key

The **`Item_Key`** specifies the Resource Item which will be replaced with either its Default Value or its Translated Value depending on the end user's locale.

#### Suffix

The **`Assembly_Key`** suffix determines where to look up the Resource. Possible values include:

* Core
* Ts.Core
* Db

For built-in Items, found most in standard Content Parts, the **`Core`** or **`Ts.Core`** suffixes are used, while configured Translation Items typically use the **`Db`** suffix to denote that the lookup be done from the TrakSYS database.

If a Resource Item is referenced that hasn't been created yet, the Item Key is displayed as a placeholder. For example, if the Resource String `"resx:OP.Page_Title,Db"` is used on a Page but does not exist in the configuration, "Page\_Title" will be displayed as a placeholder until the Resource Item is created.

### Page & Part Properties

Many Page and Part properties support Resource Strings, including many Caption and Text fields. Some properties fields include a blue lookup icon, which allow for searching for a Resource Item instead of having to type it out manually.

### ASP.NET Script

In some cases, like setting a Page Title or other more custom solutions, Resource Strings may have to be accessed and translated from a Page's Script. TrakSYS includes an extension method on resource strings to return translated strings, called **`Translate()`**. This method accepts parameters which coincide with the arguments in the Resource Item or its translation. For example: `"Operator View for Line {0}"` might be translated with: `"resx:OP.Page_Title,Db".Translate(5);`

{% hint style="info" %}
When writing .NET Script where Resource Strings are desired but not created yet, the prefix `todo:` can be used in place of `resx:`. For example, using `"todo:Group_Key.Item_Key,Db"` will render as `"Group_Key.Item_Key,Db"` to make the process of creating the Resource Groups and Items quicker when the time comes.
{% endhint %}
