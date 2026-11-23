# Visual Page Life-Cycle

The following describes the sequence of key activities in the life-cycle of a Visual Content Page. ???

* **Page Code :** Indicates a section of the code that the page author would be creating.
* **TrakSYS** : Indicates some actions that are executed behind the scenes, automatically by the TrakSYS infrastructure.

## Page Code : Page\_Init

This is a standard ASP .NET page level event. There is typically no need to utilize this.

## Page Code : ContentPage\_Init

This is a TrakSYS override method. It is typically the earliest opportunity to add code to a page. At this stage, any Page level properties will have been set from the Values collection.

From within this method, code may read from the Values collection (typically parameters passed into the page), read from the Page level properties, load data/entities from the database to be used later in the page, and finally insert values into the Values collection for Content Parts to consume later in the page life-cycle. It is important to note that Content Part properties that have not yet been loaded, should not be directly manipulated, as they can be overwritten later when the Part is loaded.

This is an ideal place to check page permissions, set resource strings, and set non-data driven properties to any non-Content Part elements of the page.

## Page Code : ContentPage\_PartPreInit01

This is a TrakSYS override method. It is called just before Content Parts with ContentPropertiesInitOrder = 1 are initialized.

From within this method, code may read from the Values collection (typically parameters passed into the page or inserted there from earlier executed Parts and code), read from the Page level properties, load data/entities from the database to be used later in the page, and finally insert values into the Values collection for Content Parts to consume later in the page life-cycle. It is important to note that Content Part properties that have not yet been loaded, should not be directly manipulated, as they can be overwritten later when the Part is loaded.

{% hint style="info" %}
Most filter type Parts default to ContentPropertiesInitOrder = 1. This is so that they may get inputs from the user interface, and place them back into the Values collection for consuming Parts to utilize later.
{% endhint %}

### TrakSYS : Load Properties for Parts 1

All Content Parts with ContentPropertiesInitOrder = 1 will load their properties with values set through the Part's configuration user interface, or with mapped values from the Values collection (again depending on the Part's configured behavior).

### TrakSYS : Initialize Parts 1

The Initialize() method is called on all Content Parts with ContentPropertiesInitOrder = 1. This fires off the ContentPart\_Init method inside the part. During this initialization, the part will typically obtain values from its properties, execute code (retrieve data, populate itself, etc…), and then finally, place new values back into the Values collection for other parts to consume.

## Page Code : ContentPage\_PartPreInit05

See explanation above for ContentPage\_PartPreInit01.

{% hint style="info" %}
Most data retrieval type Parts (Data Tables) default to ContentPropertiesInitOrder = 5. This is so that they may utilize values from the Values collection placed there earlier by filters (order = 1), retrieve data from the sources, and place the data back into the Values collection for pure data consumer Parts (order = 10) to utilize later.
{% endhint %}

### TrakSYS : Load Properties for Parts 5

See explanation above for Load Properties for Parts 1.

### TrakSYS : Initialize Parts 5

See explanation above for Initialize Parts 1.

## Page Code : ContentPage\_PartPreInit10

See explanation above for ContentPage\_PartPreInit01.

{% hint style="info" %}
Most data consuming user interface Parts (tables, charts, etc…) default to ContentPropertiesInitOrder = 10. This is so that they may utilize data placed in the Values collection from data producing Parts.
{% endhint %}

### TrakSYS : Load Properties for Parts 10

See explanation above for Load Properties for Parts 1.

### TrakSYS : Initialize Parts 10

See explanation above for Initialize Parts 1.

## Page Code : ContentPage\_Final

This is a TrakSYS override method. At this stage, all Content Parts have been initialized. It is now completely safe to directly manipulate part properties. Although there may be little use in doing so for properties that control how a Part loads, there may be some properties that do not get utilized until render time.

## Page Code : Page\_Load

This is a standard ASP .NET page level event. There is typically no need to utilize this.

## Page Code : Page\_PreRender

This is a standard ASP .NET page level event. There is typically no need to utilize this. It is noteworthy that during the base page PreRender code (before the event is raised to the Content Page author), the DataBind() method is called on all parts.
