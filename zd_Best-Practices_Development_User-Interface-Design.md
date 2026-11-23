# User Interface Design

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360009094974-User-Interface-Design*
*Last updated: 2025-08-07T21:52:32Z*

---

### Summary

This section will cover best practices for laying out TrakSYS pages to conform with standard look and feel, as well as to ease maintenance as changes are made.

### 3-Column Layout

TrakSYS pages can be laid out using a series of rows and columns. One of the most common layouts used within the standard TrakSYS Content Pages, is the 3-column layout. The typical column sizes are 2/8/2, however the exact sizes may vary depending on the specific page needs.

Column 1 (left) typically contains page header details (using Header and Detail Parts), or filters for interactive pages.

Column 2 (center) typically contains the main page content like tables, tile lists, charts, etc.

Column 3 (right) is reserved for details for selected rows or points from the center page content. For example, clicking a table row may reveal additional details in the right column. When no data is selected, the right column contents should be hidden.

Consistently using the 3-column layout presents a functional expectations to users, as well as provides a familiar look and feel alongside standard TrakSYS pages.

### Data Part Location

When arranging content on a TrakSYS Visual Page Definition, some standard parts contain functionality, but no visible user interface. Data Table/Source parts are the most common example of this scenario. In some cases, complex pages can contain a large number of UI and data-provider parts arranged in many different rows and columns. In these arrangements, it can be difficult to relocate a specific part during development.

Implementation teams should agree on a consistent placement for non-visible parts such as data sources. Two recommended options are:

  1. Place all data table parts in a dedicated row at the bottom of the page, or
  2. Place data table parts directly above or below the UI part that consumes its data. Whatever the technique, consistency across the team will ease maintaining complex layouts.



### Understanding Initialization Order

Initialization Order is one of the fundamental concepts of Page design and Content Part interoperability. Simply put, Parts that retrieve or calculate information must execute before Parts that consume, display, or operate on it. The following are key concepts to understand and master.

#### Basic Concepts

  * Initialization Order for each Part is displayed in the lower-right corner of the Part tile in the Parts designer page. The number after the colon is the Sub-Order.
  * Parts are loaded and executed in Initialization Order sequence (lowest to highest). Parts with the same Order number are further sorted by their Sub-Order value. The execution order of Parts with the same Initialization Order (and Sub-Order) cannot be guaranteed.
  * Initialization Order (and Sub-Order) values can be any integer. The actual values are irrelevant, only their relative value to other Parts on the page.



#### Default Initialization Order for Commonly Used Parts

  * Filter and Form Parts (Order 1 or 2)
  * Data Source Parts (Order 5)
  * User Interface Parts (Order 10)



The "Order" designer page displays all Parts in Initialization and Sub-Order sequence. This is useful in diagnosing Order issues on complex Pages with many Parts.

### Refresh Keys

The concept of Refresh Keys provides for an optimized page-refresh mechanism. As an alternative to simply setting a page with live data to refresh every N seconds, Refresh Keys allow pages to be updated intelligently, only when new data is actually available.

TrakSYS can automatically broadcast a specified "Refresh Key" to any page listening whenever standard information is updated (Job Start, Event End, Task Due, etc.). Pages are configured to listen for specific keys, and will initiate a page refresh when the key is received. As typical real-time data updates do not occur every few seconds, this can significantly reduce the number of page reloads that occur.

Aside from becoming familiar with [how Refresh Keys work](https://portal.parsec-corp.com/hc/en-us/articles/115010453508), the recommendation is that this technique should be used instead of fixed page refreshes, considerably lowering the load on the web and database server back ends.

### Navigation and Page Icons

Any TrakSYS Page Definition can be configured with a Navigational Icon that will show up in the Section, Hub or Spoke menu render. In addition, a separate Page Icon can be configured that will render next to the Page's title.

TrakSYS contains a large library of standard icons that can be used to decorate UI elements. Icons are a simple, low-cost, high-value technique to improve user understanding of options, as well as boost the aesthetics of a solution.

### Visible in Navigation

While creating a TrakSYS solution user interface, many pages act as "dialogs", or pages that can only be navigated to by clicking and passing information into them. Data entry/edit forms, and drilldown popup reporting are common examples. As these pages do not function properly without the expected parameters being passed in, they have no value showing up as Hubs or Spokes in the navigation. As a general rule, pages with required parameter input would qualify as dialogs.

It is recommended that for these types of dialog pages, the Visible in Navigation be set to false. This prevents a link from being rendered in the user interface.

### Icons, Icons, Icons

Most standard TrakSYS UI elements (Headers, Tiles, Buttons, Menu Links, etc.) support the optional setting of an icon. When using icons throughout an application, strive to make consistent choices, as there are usually several alternatives for the same graphic concept.

TrakSYS contains a large library of standard icons that can be used to decorate UI elements. Icons are a simple, low-cost, high-value technique to improve user understanding of options, as well as boost the aesthetics of a solution.

### Tile Text Arrangement

The TrakSYS Tile Part is a versatile UI component that can be used to display a number of data points and information in the same element. Tiles can contain up to 6 different textual elements, 3 in the upper-left corner, and 3 in the lower right. The following are some tips for the most effective and attractive use of Tile text:

#### Separate Lines for Labels

It is recommended that data values and textual labels be separated onto different lines of Tile text. This makes it easier for users to focus in on the data values.

#### Smaller Font for Labels

In conjunction with the previous recommendation, use a smaller font size for the label text. Labels are usually helpful when a user is learning the system, but after regular use, they are typically blocked out as users understand what the data value represents.

#### Less is More

Just because there are 6 text positions on a Tile does not mean they all have to be used. When possible, stick to 1 main piece of data to be represented (probably the largest-font-size line). The other positions can be used for labels or minor supporting data.

### Client-Side Confirm Dialogs

TrakSYS provides an excellent client-side mechanism for eliciting user confirmation of a click, before navigating off page or submitting. The [**ets.ui.confirm**](https://support.parsec-corp.com/refdocs/11/traksys/tsweb/javascript-reference/ets/ui/confirm.html) and [**ets.ui.confirmButton**](https://support.parsec-corp.com/refdocs/11/traksys/tsweb/javascript-reference/ets/ui/confirmbutton.html) JavaScript methods can be called to display an attractive TrakSYS confirmation dialog. Note the different techniques for confirming before a client-side navigation and a server-side post-back.

### Splash on Submit

In many user interface scenarios, a button or link is clicked which initiates a time consuming server-side request. The standard web browser behavior in this case is to continue to display the originating page, while a small status indicator spins somewhere in the browser UI. This often times confuses end-users, as they do not see any noticeable change in the page they just clicked.

TrakSYS exposes a useful and simple JavaScript for this scenario. The [**ets.ui.showSplashScreen**](https://support.parsec-corp.com/refdocs/11/traksys/tsweb/javascript-reference/ets/ui/showsplashscreen.html) method covers the originating screen with a shadowed effect, clearly indicating to end-users that the page is disabled and waiting for a server response.

### Separate Data Entry and Filtering

When building interactive pages and forms, an important design pattern to follow is to avoid combining data entry form fields, and selection/filtering elements on the same page. Combining these concepts creates situations where data entry may be partially completed, and filtering interaction causes a page refresh which clears un-saved entries. While there are advanced techniques that can be employed to mitigate the issues, this is generally a confusing situation for end-users and should be avoided.

### Learn the Form Pattern

Nearly every TrakSYS project requires data entry/editing forms to be created. Form building is complex, and a large percentage of effort is typically devoted to non-value add work like retrieving data, populating controls, validating, and writing back.

The TrakSYS infrastructure and API provide many functions and patterns that significantly reduce the non-value add aspects of form building. Learning and leveraging the available tools and patterns, allows implementers to focus on enhancing the business process and improving the user experience.

### Post-Redirect-Get

When creating user experiences that receive input and refresh the display, a common pattern is to "post" back to the application, process on the server and allow the screen to be refresh. This is called a POST request in web application terminology. Once a screen is refreshed after a POST, if a user "refreshes" the page using one of the browser mechanisms (refresh button or menu option), the POST operations execute again on the server. In cases where the server-side operations creates or modifies data, this can create unexpected results.

In addition, the ContentPage_Init script of a page is run before the Server_Click script. Modifying data in the Server_Click script may change states that were initially set in ContentPage_Init. Recalling the same page with a GET (self: link in TrakSYS) will allow the page to be refreshed with ContentPage_Init script.

It is strongly recommended that at the conclusion of server-side activity due to a POST, the browser be redirected to its own URL with a "Redirect" call. This method refreshes the page with a GET call, which prevents unexpected re-execution of server-side on user page refreshes. This is an established web development best practice.
