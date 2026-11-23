# Environment

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360007427973-Environment*
*Last updated: 2023-10-27T09:48:39Z*

---

### Summary

This article lists tips and best practices for setting up a TrakSYS development environment as well as time-saving tips for using the browser to maximize implementation efficiency.

### Change Web Theme Color for Development Instance

For implementations where a production and development environment are both accessible to developers and users, it is common for "mistakes" to be made while modifying configuration and user interfaces, specifically, accidentally changing something in the wrong environment.

To minimize confusion and mistakes when working in both environments, it is recommended that the TrakSYS Web "band colors" (the header and footer of every page) be modified in the development environment. 

To modify the band colors for a TrakSYS Web, alter the **CustomNavBarBackColor** property in **Installation Manager | TrakSYS Settings | Web**.

After changing this setting, the TrakSYS Web must be "reloaded" by using the Reload Application button on the **Administration | Settings** page in the Web.

### IsTransferTarget for Production/Development Situations

For implementations where a production and development environment are both accessible to developers and users, accidentally modifying configuration in the production environment can introduce significant problems.

To minimize or eliminate this possibility, TrakSYS exposes a setting called **IsTransferTarget** that can be activated in the production database that will lock out the property pages for entities that are being written to by the Database Transfer.

After changing this setting, the TrakSYS Web must be "reloaded" by using the Reload Application button on the **Administration | Settings** page in the Web.

More information on these two settings can be found in the [Database Transfer Guide](https://portal.parsec-corp.com/hc/en-us/articles/115004492907).

### Partner License vs. Customer License Features

Parsec partners are granted access to a TrakSYS Development license for internal and project implementation use. It is very common during the initial phases of project development, that the TrakSYS installation is activated in the partner's environment using the partner Development license. The partner Development license has rights to all TrakSYS features, as well as very high limits for "metered" features like Users and Definitions.

When this scenario is present, it is extremely important the developers ensure that they are not using features or quantities that are not supported in the customer's purchased license.

### Script Windows Require Silverlight

TrakSYS includes a rich in-product script editing toolset including IntelliSense and syntax highlighting. However, the editor is made possible by a special browser technology called Silverlight. As Silverlight is only available in Internet Explorer, this is the recommended browser for scripting developers. There is a simple text version of the editor that is rendered in other browser types for small or emergency editing of script.

### Keyboard Shortcuts

When using the in-product script editor windows, there are several keyboard shortcuts that can save time and increase efficiency while scripting (these are also available in the tooltips for the related command buttons on the toolbar).

Save | Control-Shift-S

Preview | Control-Shift-R (Preview is only available in Page script editors)

### Testing for Screen Sizes

With the introduction of responsive design elements in TrakSYS, it is more common to be designing user interfaces for multiple target devices and screen sizes. The following are some tips and considerations for testing.

Leverage the built-in browser features for testing different screen sizes. All of the major browsers now expose built-in Developer Tools that allow the browser window to be automatically re-sized to standard device sizes and resolutions. This can be very useful as a first-pass testing technique.

As there are so many variations in devices, screen sizes, resolution and DPI, it is highly recommended that testing with the actual devices be included as early in development as possible.

### Multiple Monitors

While it may seem obvious, configuration and development with TrakSYS is significantly more productive and efficient when using multiple monitors (2 or more). Several of the other tips in this article are even more effective when used in conjunction with multiple monitors.

### Multiple Browser Windows and Tabs

As a side-effect of the configuration and development interface now being 100% web based, it is possible to open multiple different views into the application simultaneously. This includes separate browser windows and multiple tabs within each window. Used strategically, this can significantly improve development efficiency.

These techniques are even more effective when combined with multiple monitors.

### Preview Page

When developing Pages (within the Grid, Part or Script editors), there is a **Preview** (Control-Shift-R) action in the menu above the editor. Clicking the **Preview** action opens the current Page (in the end-user view mode) in a new browser window or tab (depending on the browser configuration). Successive clicks of **Preview** refreshes the Page in the already opened window/tab. Used properly, a developer can achieve rapid cycles of Page changes and view refreshes.

This technique is even more effective when combined with multiple monitors (the Preview window/tab on the 2nd display).

### Browser Favorites

Throughout the configuration and development of a project, specific areas and Pages of the TrakSYS web will be utilized frequently. Take advantage of saving links to commonly used Pages in the browser's Favorites, bookmarks, or link bars. Using this technique, commonly used areas to Pages in multiple development servers can be managed using familiar and simple browser functionality.

### Custom Navigation Menu Pages

As an alternative to using the browser Favorites/bookmarks for cataloging commonly visited Pages, TrakSYS makes it is very simple to construct simple menu navigation Pages. With zero script, Pages can be set up using standard Header, Menu and Tile Parts (linking to the desired targets) to create custom high-level navigational menus within the natural flow of the application.

A thorough example of this can be found in the TrakSYS Demonstration database in the OCV site. The root Page in the Configuration Section is a custom navigation menu allowing quick access to the most commonly used items deep within the hierarchy.

### Multiple Browser Types

In most implementations, there are groups of Users that are assigned different access and permissions via Roles. Testing the access behaviors simultaneously with developing the Pages and permissions configurations can be tedious as the developer must constantly alternate between an administrative User and the User type being tested.

In the TrakSYS Web, the user security context is per browser type. Once logged in with a specific browser type (say Chrome), all successive Chrome windows opened will assume the same User context. However, opening the TrakSYS Web in another browser type (say Edge) will allow an independent login to occur. In this way a developer can be logged into Chrome as the administrator (to make adjustments to configuration), and Edge as the end-user to test the access behavior.
