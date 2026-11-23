# General

#### Name

Identifies the page throughout the application. If either Navigation Title or Page Title are provided, the Page Title will be used in their respective place.

#### Key

Used to reference the page programmatically and within the URL. Each Page Key must be unique within each hierarchy.

#### Icon

Displays an icon in the title of the page.

#### Navigation Icon

Displays an icon in the navigation to the page.

#### Navigation Title

This Title is used on links to this page from the Tree View and elsewhere. If no value is provided, the Page Name is used in its place.

#### Page Title

This Title is displayed at the top of the very top of the page. If no value is provided, the Page Name is used in its place.

#### Refresh Keys

Used to refresh the page remotely either by Logic Service or any time the Keys are called, typically by a System or Tag configured with Refresh Keys (see the Configuration Section for more information). Multiple Keys can be used in this field by separating with a comma.

#### Refresh (Minutes)

Sets a fixed page refresh every X minutes, independent of the Refresh Keys configured. The default is 0 minutes, meaning that no scheduled refresh will occur.

#### Preview URL

Specifies the URL that will be used when the page is Previewed. If no value is specified, then the default page URL will be used.

#### Instance Type

Specifies the type of Instancing that will be used for the page. This property can be defined directly on page creation, but will display as ready only after the page has been created. At this point, the Instance Type can be changed for the individual page within the Developer Section.

#### Page Level Type

This read-only field displays whether the page is a Section, Hub 1, Hub 2, Hub 3, or Spoke.

#### Content Key

This read-only field displays the Content Key which can be referenced when linking to this type of page directly. For example, using `C={ContentKey}` in the URL will link directly to the desired Content Page without having to instance the page.
