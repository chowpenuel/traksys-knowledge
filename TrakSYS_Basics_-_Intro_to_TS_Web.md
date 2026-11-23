<!-- Slide number: 1 -->
# Accessing the Web

<!-- Slide number: 2 -->
# Accessing the Web

![](Picture61.jpg)
Installation
The TS Web must first be setup through the TrakSYS Installation Manager. TrakSYS requires specific IIS features to be installed on the server in order to support its deployment and use.

Advanced Settings
Additional implementation-wide Web settings can be assigned through the Overview tab of the Installation Manager.

### Notes:
To access the TrakSYS web, you will need to navigate to it through your implementation's URL. This can be found in the Installation Manager, under the "Webs" tab. If your implementation is setup properly
The default url is "http:// <your server name> /ts".

These are ways to change this URL, as well as some additional Web-related settings that can be assigned through the "Overview" tab of the installation manager. These settings and processes are beyond the scope for this module, but are documented on the Support Site if you wish to further explore those capabilities.

<!-- Slide number: 3 -->
# Accessing the Web
Upon successful setup and installation configuration, the TrakSYS application user interface will be accessible by navigating a browser to…

http:// servername / ts

![A screenshot of a computer Description automatically generated](Picture4.jpg)

### Notes:
Once you have navigated to the implementation's URL, you will be able to see the front-end to the implementation.

Depending on what database, credentials, and interfaces you have available, the first screen you are directed to may vary, but you will see the blue TrakSYS navigation bar across the top, with "TrakSYS" and the company name in the top left.

<!-- Slide number: 4 -->
# Hierarchy

<!-- Slide number: 5 -->
# Navigation Basics: Hierarchy

Hub 3s
Spokes
Sections
Hub 2s
Site
Hub 1s
OCV
Batching
Tableting
Packaging
Overview
Reports
Events
MTBF
OEE
OEE
Avail
Perf
Qual
System Check
Multi-Line
Job Editor
Alternate View
New/Edit

### Notes:
Before we begin looking at pages in the Web, let's go through the general page hierarchy.  This will help you understand how pages are layered.

TrakSYS has 5 distinct page layers and one additional general-use layer, as shown in this diagram. For the 5 distinct page layers, they follow a strict parent-child relationship. The first layer is a site. The second layer is a Section, and every Section Page will always have a Site Page for a parent. The same applies to each of the next 3 page layers, called Hub 1, Hub 2, and Hub 3 pages.

For a simple comparison, you can compare this to how you navigate through Files and Folders on a computer. The first 5 page layers are like Folders. Each folder can have a parent, and these folders are nested. In TrakSYS, the Site, Section, and Hubs are like these folders.

If the first 5 layers are folders, you can think of the Spokes as Files. These Spokes cannot have any children and they can be a child to any of the other page Layers. You can have a Spoke as a child to a Site. You can have a Spoke as a child to a Hub 2. This is similar to how you can have a File in any folder, but you do not have a File within a File.

In TrakSYS, each of these Sites, Sections, Hubs, and Spokes are a Page Definition.  Page Definitions are web pages that can have different functionality based upon your needs and can vary significantly, but generally have some key similarities and patterns.

<!-- Slide number: 6 -->
# Navigation Basics: Hierarchy
Section

Site

![A screenshot of a computer Description automatically generated](Picture9.jpg)

![A screenshot of a computer Description automatically generated](Picture8.jpg)

Spoke

Hub 1

Hub 2

Hub 3

### Notes:
To begin with, all pages have a standard navigation pattern that can be used to navigate between the pages. In the displayed example, we are looking at a Hub 1.
You can see the Site in the top left. Next to it are all the sections. These are both always visible while in the Site. You can see that we are currently in the "Packaging" section based upon the darker color around the section's navigation element.

Once a Section is selected, the gray navigation area on the left becomes visible. Normally, you are only able to see the currently selected layer and its children. This image has been slightly altered to give a better view and perspective. You can see that we are currently looking at the "Line 1" hub 1 based upon the darker color around the hub 1's navigation element.

As the Hub 1 is selected, the children Hub 2 would be displayed on the left hand tree view. If a Hub 2 were selected, the children Hub 3's would be displayed.

In the top right, you can see the Spokes. Since each page can have their own spokes, the displayed options are the spokes for the currently selected page. You can only navigate to the Spokes of the current page using this standard navigation. In this example, the "Line 1" page has 3 spokes that can be accessed.

For any page, the general pattern will be the same.

<!-- Slide number: 7 -->
# Navigation Basics: Breadcrumbs

![A screenshot of a computer Description automatically generated](Picture3.jpg)

### Notes:
As you navigate through the pages, you will also be able to see the "Breadcrumbs" being built along the top of the page. These breadcrumbs will let you know where you are in the page hierarchy. In this example, you can see that We are in the OCV site, in the Configuration Section, and in the Tags Hub 1 based upon the highlighted navigational elements. This is also reflected in the breadcrumbs.

<!-- Slide number: 8 -->
# Navigation Terminology

<!-- Slide number: 9 -->
# Slices

<!-- Slide number: 10 -->
# Navigation Basics: Slices

![A screenshot of a computer Description automatically generated](Picture3.jpg)
Slice 3
Slice 1
Slice 2

### Notes:
Outside of the Standard sections, the interface and design is entirely up to the developer. However, within the standard sections, there are standard navigation patterns built into many of the pages. Throughout the modules, there will be references to these patterns and the standard terminology.

The most prominent pattern can be seen in the built in Configuration section. This section utilizes the pattern of dividing pages into three equal size areas to present the information. Each area is referred to as a Slice. Each slice is numbered from the left to the right to help identify which one is being referenced, starting with Slice 1 on the left.

In the Configuration Section, you will also see how this pattern is used to create an intuitive UI. When a page is selected, the matching information will be displayed in Slice 1. Slices 2 and 3 may be empty. As something is selected in Slice 1, the related information is displayed in the next Slice. For example, In the Tags screen that is shown, Slice 1 is shown first. Once a group is selected from Slice 1, Slice 2 will show the Tags within the Group, and Slice 3 shows more information about the selected Tag Group.

When a Tag is selected in Slice 2, Slice 3 is updated to show more information about the selected tag. This helps by having a consistent flow of information going from the left to the right based upon the user selections. If something is selected in Slice 3, everything shifts to continue the pattern. The original Slice 3 will slide to the left, becoming the new Slice 1. The related information is shown in a new Slice 2, and the pattern can continue. This navigation happens on the same page, although it may feel like you are navigating through a number of options. As this happens, you'll see the breadcrumbs expand to show the full trail of entities you pass through during this configuration process.

The format shown in Slice 3 is also a common format known as an Item Slice. Let's look at it in more detail.

<!-- Slide number: 11 -->
# Navigation Basics: Item Slice

![A screenshot of a computer Description automatically generated](Picture3.jpg)
Entity Name
Common Actions
Key Properties
Related (typically Child) Entities
Actions

### Notes:
The Item Slice is intended to provide all of the relevant options for a specific Entity or Item in TrakSYS. In this example, the Item Slice is showing all of the information for one of the Tags in the implementation. Regardless of which Entity it is showing, the pattern will be similar.
The name is identified at the top. Directly below it will be any common actions, which is typically the "Edit" option. Below it are any Key Properties, such as the ID, Types, and other Foreign-Key related entities. Below that are the Related Entities, which are typically children entities. And lastly any other actions are available at the bottom.

<!-- Slide number: 12 -->
# Slices
