# Library

Library Items can be used to upload and store assets and resources for reoccurring use throughout the application. Library Items are most typically used for images such as logos, or SOP's (Standard Operating Procedures) that can be displayed on Task Forms or other User Interfaces. The Library Items are stored in the database yet still accessed via a URL.

## Uploading

### Group

Library Items are organized into Library Item Groups. Note the Key of the Library Item Group as it is used in the link when accessing / linking to a Library Item.

### Name

Name of the particular Library Item. This Name will be used in the link when accessing / linking to a Library Item and therefore should include underscores or dashes instead of spaces. It is not necessary to include the file extension in the Library Item Name. If left blank, the Library Item Name will be populated from the uploaded file name.

### Alternate Name

The optional Alternate Name of the Library Item can be a translated name, or some other external name for the Library Item.

### MIME Type

The MIME Type allows the browser to determine what extension to append to the file name when the Library Item is eventually downloaded. In cases when the Library Item will only be displayed and not downloaded (such as image), the MIME Type may be left blank.

{% hint style="info" %}
Each Site can have its own Library Item Groups and therefore Library Items. This is important when accessing/linking to a Library Item as the Site Key is part of the link. See the Accessing section below.
{% endhint %}

## Accessing

### Link

A Library Item is typically accessed via link using a unique route. The template for a Library Item link looks like:

`/ts/library/{SiteKey}/{LibraryItemGroupKey}/{LibraryItemName}`

#### SiteKey

The Site Key is simply the Page Definition Key of the Site to which the Library Group / Library Item belongs.

#### LibraryItemGroupKey

The Library Item Group Key is the Key of the Library Item Group to which the Library Item belongs.

#### LibraryItemName

The Library Item Name is the Name given to the Library Item when it was uploaded. If the Name field was left blank when uploading, then the Library Item Name is the name of the file that was originally uploaded.
