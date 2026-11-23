<!-- Slide number: 1 -->
# Content Page Definitions

### Notes:

<!-- Slide number: 2 -->
# Adding a Content Page

![A screenshot of a computer Description automatically generated](Picture3.jpg)

Locate the parent Page in the Hierarchy and select the appropriate child Page Definition List

Select the New menu option at the top of the Page Definition List in Slice 2

Once a Page Definition is added to the Hierarchy, it is available in the TrakSYS User Interface

### Notes:
In this module, we'll take a look at one of the three types of Page Definitions, the Content Page type. Before going into the specifics of how a content page functions, let's first look at how to implement any Page Definition type.

In the Developer Section, under the Page Definitions Hub 1, you are able to access and view the entire navigation hierarchy. The first Slice 1 will show an item slice for the Site level page. From there, you will be able to use the pattern just like the configuration section to work your way through the levels of navigation. For example, at the Site level, there are Related Menu options for the site's two children, the Sections, and Spokes.

At each level, except for the Site level, you will have the option to create and modify Page Definitions. To create a new one, simply select the New menu option and build the page from there. As you add new Page Definitions, you'll see them immediately added this developer navigation area, and the rest of the live implementation.

<!-- Slide number: 3 -->
# Content Page Catalog

![](Picture10.jpg)
Select the first tab in the New Page to choose a pre-built Content Page from the Catalog

Content Pages are grouped by Application Function

Both Standard TrakSYS Content Pages, and user-defined Content Pages are listed in the Catalog

Selecting a Content Page reveals a description and details in the Slice 3.

### Notes:
When you select to create a new page, you'll be presented with a number of different options, including a Tab for each of the three different Page Definition Types.
The Content Page tab will show you the Content Page Catalogue, which contains all of the Content Page options. These options are presented in a tree view, grouped together based upon their intended functionality. Selecting one will display a short description of it in Slice 3. When you have found one that you want to use, select the "New" button to continue.

<!-- Slide number: 4 -->
# Page Definition | General Properties

![A screenshot of a computer Description automatically generated](Picture3.jpg)
NamePrimary name of the Page
KeyUnique identifier for the page within its parent navigational element.  Use to build the URL address for accessing the Page.  The Key will also be used for the .NET class name for the Page, so it is recommended to use PascalCase conventions.
Navigation TitleOptional name to be displayed in the navigation links.
Page TitleOptional name to be displayed at the top of the Page.
Refresh MinutesTimer interval for auto-refreshing the Page contents.
Refresh KeysIdentifier(s) for enabling push page refreshes.

### Notes:
Depending on the Content Page you select, you will be presented with different sets of properties, but all Page Definitions share at few general properties. The General, Visibility, and Notes tabs for all Page Definitions will be the same, with any specific properties being added on additional tabs. Before we cover any specific properties, let's take a look at the general ones.

Each Page Definition requires a Name and a Key.
The Name becomes the primary display name for the Page and is used in the Developer Section, the standard navigation, and on the page itself by default. The Navigation Title and Page Title properties can override the default name if desired, but are optional.
The Key becomes the primary identifier for the Page from a navigational and database perspective. Because of this, it must be unique within the parent element to ensure there are no conflicts. Keep in mind that most Page Definition types have their normal direct child, like how a Section has Hub 1's as a child, but they also have Spokes as children. That means that all Spokes and Hub 1's that share the same parent Section should have unique keys, even though you may not see them side-by-side in the developer menus.

Outside of the Name and Key, the rest are optional. The last two properties are the Refresh (Minutes) and the Refresh Keys properties. Using these will cause a page to automatically refresh on a specified basis. For Refresh Minutes, this identifies a flat interval for the page to refresh on. For Refresh Keys, you are able to identify strings that can be matched to configuration elements or called through script to trigger a refresh instead. The Refresh Keys property is more complex and will be revisited in the Demonstration.

<!-- Slide number: 5 -->
# Page URLS by Key

![A screenshot of a computer Description automatically generated](Picture3.jpg)
Base Pages URLhttp://servername/ts/pages/

http://servername/ts/pages/sitehttp://servername/ts/pages/ocv

http://servername/ts/pages/site/sectionhttp://servername/ts/pages/ocv/packaging

http://servername/ts/pages/site/section/hub1http://servername/ts/pages/ocv/packaging/line1

http://servername/ts/pages/site/section/spokehttp://servername/ts/pages/ocv/packaging/overview

### Notes:
The Key in particular is extremely important as it is used to also build the Page URL to access the Page Definition. This is also why it must have a unique value within the parent, to ensure the URLs are all unique.

You can see an example of how this URL building works on the right. The base URL for an implementation is:http:// servername/ ts/ pages/

From here, you simply add each Key for the next layer, one at a time. The first layer is a Site, so you would use the Site's Key. In this example, that is OCV.
To access the first section, you would then add the section key, such as "Packaging"
Then a Hub1, then a Hub2, then a Hub3 all as needed

At any point, you can also choose to go to one of the spokes by providing the Spoke's key. Of course, Spokes have no children, so that would be the farthest that URL chain could go.

<!-- Slide number: 6 -->
# Page Definition | Visibility Properties

![A screenshot of a computer Description automatically generated](Picture3.jpg)
Settings to control the Visibility of Navigational elements displayed on the Page

Options include…
TrueAlways show the element.
FalseNever show the element.
InheritShow the element based on the parent’s setting.

Visible in Navigation shows/hides the Page from being displayed in the Navigation

### Notes:
In addition to the general properties, each Page Definition also has a few properties that control the visibility of the built-in aspects of the Page. While you cannot directly edit out Headers, Footers, and Navigation Tree, you can choose to hide them if you do not wish to see them.  This action will shift the contents of the page appropriately to fill in the hidden space.

These properties affect how you navigate between the pages using the standard TrakSYS navigation UI. If you choose to hide certain navigational elements, you may need to create your own versions of them on your pages to allow users to navigate between the pages.

As a quick description of each, here are what the first 6 properties cover.

Header: The top blue bar that contains the Site in the top left, Sections in the middle, and Login on the right.
Footer: The bottom blue bar that contains the developer tools in the bottom left, and TrakSYS information in the bottom right.
Title: The Name of the page in the top left of each page.
Breadcrumbs: The navigation chain above the Title, spanning across the top of each page.
Tree: The navigation Tree View on the Left while on a Section or a Section's child that has at least one Hub1
Spokes: The navigational links to a page's spokes in the top right of a page.

By default, these values are set to Inherit so they can be easily set for entire portions of the navigation. If all pages are set to Inherit, the default is true.

Lastly, there is a "Visible in Navigation" property. This property controls if this page is visible through the standard TrakSYS navigational UI elements, like the Header and the Tree. If set to false, the page will not show up in the standard UI.  You'll be able to see the other respective pages set to true in the Header for sections, the tree for Hub 1's, but the page ticked false will disappear from the list. However, the Page can still be accessed through it's direct link, so it can be navigated to using custom links on a page, or through someone who knows the URL. It is expected that all pages will have proper permission checks enforced, as hiding a page does not prevent it from being used or accessed.

<!-- Slide number: 7 -->
# Content Page Properties

![A screenshot of a computer Description automatically generated](Picture2.jpg)
Specify property values at Design Time

Fixed values configured by the Page Developer

Default values if Dynamic values are not Present

Dynamic values will be covered in a later section.

### Notes:
Lastly, all Content Pages will have some unique properties that govern how it behaves. Since each of the Content Pages serve a different purpose, we won't be covering any specific properties right now. Generally, these properties drive how the page will look and function.  You will find that the majority of the properties will have two columns. The left hand column is the static value, which is normally manually entered, and the right hand column is the dynamic value. The use of the Dynamic values will be covered in more detail in later Modules.

Most pages will require at least one of the properties to be set in order to function. You will find these under the "Properties" tab. Most of the properties in this tab will require valid inputs to be able to render the page. For ease of use, each page does include error handling messages if it is improperly configured, so you will know which properties are missing.

<!-- Slide number: 8 -->
# Content Page Definitions:System Discrete Real-Time Overview

### Notes:
To give this more grounding, we're going to take a look at a specific Content Page example, the System Discrete Real-Time Overview. We'll examine some of the simple properties, how they can be used, and how a typical Content Page functions.

<!-- Slide number: 9 -->
# System Discrete Real-Time Overview

![A screenshot of a computer Description automatically generated](Picture2.jpg)

### Notes:
To begin with, this is an example of the standard System Discrete Real-Time Overview (which will be shorted to SDRO going forward) with minimal adjustments made. It is a fairly complex page, with a lot of data, but it is a standard page that can be deployed very quickly. Let's take a look at the properties of the page.

<!-- Slide number: 10 -->
# SDRO Properties

![A screenshot of a computer Description automatically generated](Picture9.jpg)

### Notes:
This page has three key properties, a System, a KPI Calculation, and a System Data Mode.
The first two in this example are being set using the dynamic value. The specifics of how this works is not important at this time, and will be covered later. The important information is that this page needs to be told what System and KPI Calculation it is intended to display, and what Data Mode (of which the options are "Job" and "Shift") should it use.
You can see that, whatever value is provided for the System value is going to determine what System's name is displayed at the top of the left-most column in the page.

Similarly, there are properties to control more specific aspects of the page. For example, under "Column Widths" are values for Left, Center, Right, Tile, and Chart. These control how wide certain sections of the page are, and can be adjusted based upon the implementation's needs.

<!-- Slide number: 11 -->
# SDRO Properties

![A screenshot of a computer Description automatically generated](Picture3.jpg)

![A screenshot of a phone Description automatically generated](Picture4.jpg)

### Notes:
Other properties for the SDRO include...

General Content Options – to hide and show entire sections of page content
Override Links – to change where the links on the page navigate to, such as the "Overview" and "End" buttons under my Job header
Charts – to hide or show certain charts on the page

And

Advanced – to control various formatting needs

As a reminder, each Content Page will have different options to use. There may be similarities in the groups of properties that help with understanding patterns, but the specifics will differ.

<!-- Slide number: 12 -->
# Adjusted SDRO

![A screenshot of a computer Description automatically generated](Picture2.jpg)

### Notes:
Using the properties for the SDRO, you can adjust the standard page that was shown earlier to instead look like this. If you were not using certain content, like Manual Events, Tasks, and Journals, this layout for the page may be more appealing.

These can be easily updated as you go, to allow the page to be deployed quickly, and then updated easily. However, keep in mind that the limitation for the page is based upon what properties are available. You will not be able to adjust every single aspect of the page, and that is the tradeoff for the standardized content. If you need more flexibility, then you would transition into using a Visual Page and continue from there.

<!-- Slide number: 13 -->
# Performance Related Pages
Event Attention List
Lists Events requiring Attention
Event Attention
Detailed Event Information and Options
Event Categorization
Category Assignment
Real-Time Overview
Current Job/ShiftEvent OverviewKPI Overview
Planned Jobs
Lists upcoming Jobs
Create New Job
Manually create Job
Completed Jobs
Lists finished Jobs
End Job
End Job Production
Start Job
Begin Job Production
Job Overview
Job SummaryKPIs for JobEvents for Job

### Notes:
Taking a step back, let's look at Content Pages against as a whole.

When you implement a content page, it's intended to help with a  common solution need. Most content pages will include links to additional pages. All of the linked pages are also content pages, intended to help round out the solution. You can see the SDRO listed on the left side of this diagram. When you implement that Content Page, it will automatically link to copies of each of the other Content Pages shown in this diagram.

<!-- Slide number: 14 -->
# Replacement Pages

![](Picture2.jpg)

### Notes:
Of course, you do not have to use all of those pages. A few slides ago, we mentioned that there are properties that allow you to override the standard links on a Content Page. Using those properties, you're able to mix in your own pages into the Content Page trees, using the pages that are useful, and replacing the ones that aren't. This helps to ensure that Content Pages can be mixed into any implementation, allowing the implementor to more quickly deploy common solutions and to focus upon the client-specific aspects.  In addition, any pages that you build can also link back to a content page and it's standard workflow.

<!-- Slide number: 15 -->
# Adding a Content Page

### Notes:
Let’s look at an example of using Content Pages in a demonstration, starting with the SDRO.

<!-- Slide number: 16 -->
# Refresh Keys

### Notes:
As a final demonstration, we'll also revisit the topic of Refresh Keys by setting one up for a Content Page.
