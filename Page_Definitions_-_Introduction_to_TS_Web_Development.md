<!-- Slide number: 1 -->
# Introduction to TS Web Development

### Notes:
This module will introduce you to working with the Front-End of a TrakSYS implementation.

<!-- Slide number: 2 -->
# Developer Section

![](Picture5.jpg)

![A screenshot of a phone Description automatically generated](Picture6.jpg)
Page Definitions
Build and maintain the Navigation Hierarchy of the Implementation.
Content
Re-useable user-defined Pages and Parts.
Library
Implementation specific web resources such as images, JavaScript, and CSS files.
Scripts
Definitions for all .NET script classes used in Logic Service and the Web.
Modules
Modules that can be executed by the Data Management Service.
Operations
Advanced entities that allow the extension and customization of the TrakSYS menus.

### Notes:
Page development occurs in the Developer section of an implementation. In the Page Definitions Hub 1, you are able to build and maintain the pages of the Implementation's front-end.
There are a number of different Hubs in the Developer Section that support the development of the front-end as well. Each section is briefly described above. This module will focus only upon the Page Definitions Hub, but many of the other hubs will be covered in other modules.

MURF ai: Maverick, P: 0, S: 0

<!-- Slide number: 3 -->

![](Pagedevelopmentocc.jpg)
# Developer Section

![](Picture5.jpg)

![A screenshot of a phone Description automatically generated](Picture6.jpg)

Page Definitions
Build and maintain the Navigation Hierarchy of the Implementation.
Content
Re-useable user-defined Pages and Parts.
Library
Implementation specific web resources such as images, JavaScript, and CSS files.
Scripts
Definitions for all .NET script classes used in Logic Service and the Web.
Modules
Modules that can be executed by the Data Management Service.
Operations
Advanced entities that allow the extension and customization of the TrakSYS menus.

![](Thereareanumbero.jpg)

### Notes:
Page development occurs in the Developer section of an implementation. In the Page Definitions Hub 1, you are able to build and maintain the pages of the Implementation's front-end.
There are a number of different Hubs in the Developer Section that support the development of the front-end as well. Each section is briefly described above. This module will focus only upon the Page Definitions Hub, but many of the other hubs will be covered in other modules.

<!-- Slide number: 4 -->
# Page Definitions Hub

![](Picture7.jpg)
Used to create, configure and organize the Page hierarchy that makes up a TrakSYS Solution

Manage Content Pages, Visual and Open type Page Definitions

Contains both user-defined and built-in Sections / Hubs

Note that Sites, Sections and Hubs (1 and 2) also contain Spokes

### Notes:
In the Page Definitions hub, you are able to create, configure, and organize the Pages and Hierarchy within your solution. This includes the ability to manage the built-in and user-defined sections and hubs.
You won't be able to delete or change the standard sections, which are denoted by the "default" tag below their name, but you can even add your own user-defined pages to the standard sections.

<!-- Slide number: 5 -->
# Page Definitions Hub

![](InthePageDefiniti.jpg)

![](Picture7.jpg)

![](Youwontbeableto.jpg)

Used to create, configure and organize the Page hierarchy that makes up a TrakSYS Solution

Manage Content Pages, Visual and Open type Page Definitions

Contains both user-defined and built-in Sections / Hubs

Note that Sites, Sections and Hubs (1 and 2) also contain Spokes

### Notes:
In the Page Definitions hub, you are able to create, configure, and organize the Pages and Hierarchy within your solution. This includes the ability to manage the built-in and user-defined sections and hubs.
You won't be able to delete or change the standard sections, which are denoted by the "default" tag below their name, but you can even add your own user-defined pages to the standard sections.

<!-- Slide number: 6 -->
# Page Hierarchy Review

![](Picture2.jpg)

### Notes:
When creating new Page Definitions, you are able to add user-defined pages at any level of the implementation. This example shows a possible user-defined set of Pages. Each page will be linked together through the standard navigation by default and are otherwise independent of each other.

Each Page will be one of three types, which determines how it is implemented. Let's look at those three types.

<!-- Slide number: 7 -->
# Page Hierarchy Review

![](WhencreatingnewPa.jpg)

![](Picture2.jpg)

![](EachPagewillbeon.jpg)

### Notes:
When creating new Page Definitions, you are able to add user-defined pages at any level of the implementation. This example shows a possible user-defined set of Pages. Each page will be linked together through the standard navigation by default and are otherwise independent of each other.

Each Page will be one of three types, which determines how it is implemented. Let's look at those three types.

<!-- Slide number: 8 -->
# Page Definition Types | Content Page

![A screenshot of a computer Description automatically generated](Picture2.jpg)
Content Page (out-of-the-box)
Content built into the TrakSYS product.  These Pages cannot be altered (other than what is exposed via Parameters and configuration settings).

Visual
Pages that are constructed by assembling Content Parts using a grid based visual editor.  The behavior of the Visual Page is primarily manipulated by setting properties through user friendly form based interfaces.  For more advanced needs, the server side behavior of the page can be controlled using ASP.NET script.

Open
Pages built by hand-coding the user interface portion (HTML, CSS and JavaScript), and the server side code (ASP.NET).  While these types of pages are more complex to create, there are no limitations or restrictions as to the functionality and layout that can be created.

![A screenshot of a computer screen Description automatically generated](Picture3.jpg)

### Notes:
The first type is the Content Page.

This type is the "out of the box" style, which features a single set of properties to control the entire page. While they are limited in option, they are extremely quick to deploy. There are a number of content pages based around common TrakSYS interfaces to assist with quick deployments of common solutions. Even with their limited nature, they can often provide an easy starting point for many implementation with the option to build upon or improve the pages later.

<!-- Slide number: 9 -->
# Page Definition Types | Content Page

![](Thefirsttypeisth.jpg)

![A screenshot of a computer Description automatically generated](Picture2.jpg)
Content Page (out-of-the-box)
Content built into the TrakSYS product.  These Pages cannot be altered (other than what is exposed via Parameters and configuration settings).

Visual
Pages that are constructed by assembling Content Parts using a grid based visual editor.  The behavior of the Visual Page is primarily manipulated by setting properties through user friendly form based interfaces.  For more advanced needs, the server side behavior of the page can be controlled using ASP.NET script.

Open
Pages built by hand-coding the user interface portion (HTML, CSS and JavaScript), and the server side code (ASP.NET).  While these types of pages are more complex to create, there are no limitations or restrictions as to the functionality and layout that can be created.

![](Thistypeistheou.jpg)
Content Page (out-of-the-box)
Content built into the TrakSYS product.  These Pages cannot be altered (other than what is exposed via Parameters and configuration settings)..

![A screenshot of a computer screen Description automatically generated](Picture3.jpg)

### Notes:
The first type is the Content Page.

This type is the "out of the box" style, which features a single set of properties to control the entire page. While they are limited in option, they are extremely quick to deploy. There are a number of content pages based around common TrakSYS interfaces to assist with quick deployments of common solutions. Even with their limited nature, they can often provide an easy starting point for many implementation with the option to build upon or improve the pages later.

<!-- Slide number: 10 -->
# Page Definition Types | Visual

Content Page (out-of-the-box)
Content built into the TrakSYS product.  These Pages cannot be altered (other than what is exposed via Parameters and configuration settings).

Visual
Pages that are constructed by assembling Content Parts using a grid based visual editor.  The behavior of the Visual Page is primarily manipulated by setting properties through user friendly form based interfaces.  For more advanced needs, the server side behavior of the page can be controlled using ASP.NET script.

Open
Pages built by hand-coding the user interface portion (HTML, CSS and JavaScript), and the server side code (ASP.NET).  While these types of pages are more complex to create, there are no limitations or restrictions as to the functionality and layout that can be created.

### Notes:
The second type of page definition is the Visual Page.

These pages are built using a combination of multiple editors. They utilize a Grid Editor to setup the blueprint of page, a Parts Editor with a library of configurable parts to put components, known as Content Parts, on the page, and a few script editors for extensibility. Each content part will have its own set of properties, leading to a massive amount of combinations through user friendly configuration settings.

<!-- Slide number: 11 -->
# Page Definition Types | Visual

![](Thesecondtypeofp.jpg)

Content Page (out-of-the-box)
Content built into the TrakSYS product.  These Pages cannot be altered (other than what is exposed via Parameters and configuration settings).

Visual
Pages that are constructed by assembling Content Parts using a grid based visual editor.  The behavior of the Visual Page is primarily manipulated by setting properties through user friendly form based interfaces.  For more advanced needs, the server side behavior of the page can be controlled using ASP.NET script.

Open
Pages built by hand-coding the user interface portion (HTML, CSS and JavaScript), and the server side code (ASP.NET).  While these types of pages are more complex to create, there are no limitations or restrictions as to the functionality and layout that can be created.

![](Thesepagesarebuil.jpg)
Visual
Pages that are constructed by assembling Content Parts using a grid based visual editor.  The behavior of the Visual Page is primarily manipulated by setting properties through user friendly form based interfaces.  For more advanced needs, the server side behavior of the page can be controlled using ASP.NET script.

### Notes:
The second type of page definition is the Visual Page.

These pages are built using a combination of multiple editors. They utilize a Grid Editor to setup the blueprint of page, a Parts Editor with a library of configurable parts to put components, known as Content Parts, on the page, and a few script editors for extensibility. Each content part will have its own set of properties, leading to a massive amount of combinations through user friendly configuration settings.

<!-- Slide number: 12 -->
# Page Definition Types | Open

![](Picture7.jpg)
Content Page (out-of-the-box)
Content built into the TrakSYS product.  These Pages cannot be altered (other than what is exposed via Parameters and configuration settings).

Visual
Pages that are constructed by assembling Content Parts using a grid based visual editor.  The behavior of the Visual Page is primarily manipulated by setting properties through user friendly form based interfaces.  For more advanced needs, the server side behavior of the page can be controlled using ASP.NET script.

Open
Pages built by hand-coding the user interface portion (HTML, CSS and JavaScript), and the server side code (ASP.NET).  While these types of pages are more complex to create, there are no limitations or restrictions as to the functionality and layout that can be created.

![A screenshot of a computer Description automatically generated](Picture4.jpg)

### Notes:
The last type of page is the Open page. This is a developer-style page that involves script-based editors.  Both the front end and back end are designed by script. There are ways to utilize pre-built TrakSYS parts and the TrakSYS API, but it is intended as a layer without limits to ensure any implementation needs can be met.

<!-- Slide number: 13 -->

![](Thelasttypeofpag.jpg)
# Page Definition Types | Open

![](Picture7.jpg)
Content Page (out-of-the-box)
Content built into the TrakSYS product.  These Pages cannot be altered (other than what is exposed via Parameters and configuration settings).

Visual
Pages that are constructed by assembling Content Parts using a grid based visual editor.  The behavior of the Visual Page is primarily manipulated by setting properties through user friendly form based interfaces.  For more advanced needs, the server side behavior of the page can be controlled using ASP.NET script.

Open
Pages built by hand-coding the user interface portion (HTML, CSS and JavaScript), and the server side code (ASP.NET).  While these types of pages are more complex to create, there are no limitations or restrictions as to the functionality and layout that can be created.
Open
Pages built by hand-coding the user interface portion (HTML, CSS and JavaScript), and the server side code (ASP.NET).  While these types of pages are more complex to create, there are no limitations or restrictions as to the functionality and layout that can be created.

![A screenshot of a computer Description automatically generated](Picture4.jpg)

### Notes:
The last type of page is the Open page. This is a developer-style page that involves script-based editors.  Both the front end and back end are designed by script. There are ways to utilize pre-built TrakSYS parts and the TrakSYS API, but it is intended as a layer without limits to ensure any implementation needs can be met.

<!-- Slide number: 14 -->
# Page Definitions Hub

![A screenshot of a computer Description automatically generated](Picture3.jpg)
Each layer has different levels of extensibility

To add a page, find the parent in the navigation and select to create a New Child

Each Type will be covered in more details in their own Modules

### Notes:
The different layers all have their own level of extensibility based upon the implementation need. A Content Page is fastest, but has the least options, the Open Page is the most flexible but requires a largest skillset to implement. You are able to add any of these page types at any level of the navigation as necessary, allowing you to mix and match the pages types as needed.

This module was intended only to introduce you to the types of pages and the basic patterns. You will learn more about each type of Page in the upcoming modules.

<!-- Slide number: 15 -->
# Page Definitions Hub

![](Thedifferentlayers.jpg)

![](Thismodulewasinte.jpg)

![A screenshot of a computer Description automatically generated](Picture3.jpg)
Each layer has different levels of extensibility

To add a page, find the parent in the navigation and select to create a New Child

Each Type will be covered in more details in their own Modules

### Notes:
The different layers all have their own level of extensibility based upon the implementation need. A Content Page is fastest, but has the least options, the Open Page is the most flexible but requires a largest skillset to implement. You are able to add any of these page types at any level of the navigation as necessary, allowing you to mix and match the pages types as needed.

This module was intended only to introduce you to the types of pages and the basic patterns. You will learn more about each type of Page in the upcoming modules.
