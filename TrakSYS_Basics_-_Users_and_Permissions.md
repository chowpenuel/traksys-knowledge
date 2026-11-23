<!-- Slide number: 1 -->
# Users

<!-- Slide number: 2 -->
# Users
Represents a Single or Group of identifiable Individuals

User Types
Windows User/GroupReference to a Windows User/Group login(DOMAIN\login) or (DOMAIN\group)
TrakSYS User/GroupTrakSYS managed Logins and Groupings
OIDC User/GroupTies the User to an existing User/Group from an external Identity Provider that supports OpenID Connect
API UserTies the User to a Web Api Request through HTTP Authorization headers.
EveryoneA special type that includes all users, allowing blanket permissions to be granted

![](Picture2.jpg)

### Notes:
Let's first begin with Users.

There are multiple types of Users within TrakSYS, some that represent individuals, and some that represent groups. For example, you can have a User that is of the TrakSYS User type that represents a specific operator, but you can also have a User that is of the TrakSYS Group type that represents all operators on a certain asset.

For each User Type, there is a different way to log in. For this module, we will be focusing upon the most common ones, the Windows and TrakSYS User/Group types and the Everyone user. Please reference the Support Site for use of the OIDC and API Users.

<!-- Slide number: 3 -->
# Authentication

![A screenshot of a login box Description automatically generated](Picture4.jpg)
TrakSYS allows for the use of all TrakSYS User Types simultaneously

TrakSYS first attempts to use Windows Authentication, asking for a TrakSYS Login as a backup

Integrated Windows Authentication is based upon Browser Support
Internet Explorer
Edge
Chrome
Firefox
Etc.

### Notes:
All User Types can be used at the same time within TrakSYS. You are able to log-in using any combination of the User Types based upon your implementation needs. For example, you may use Window User type logins for Manager or Supervisor logins, but utilize TrakSYS Group User type logins for line operators to simply your user maintenance.

When attempting to access implementation content, TrakSYS will default to using Windows Authentication as the first method of user verification. If that fails, the user will be redirected to the standard TrakSYS User Login page. This flow is supported with any browser that supports Windows Authentication, and other versions of this login process can be implemented as needed. Let's take a look at the process in more detail.

<!-- Slide number: 4 -->
# Authentication
Request
User accesses the TrakSYS user Interface from a specific browser/device combination.

Credentials passed to Server
If supported by the browser,
Windows credentials are passed to the server.

Authentication
Login and password are checked against the Active Directory.

User not Found or no Permissions
If the current User is not found in Active Directory or has no Permissions then prompt.
No Windows Authentication Support
If the browser does not support Windows Authentication then prompt.

Access Granted
The requested content/page is retrieved and presented.

Authentication
Login and password are checked against the TrakSYS User list.
Login Prompt
User is prompted for a login and password.

![A screenshot of a login box Description automatically generated](Picture50.jpg)

### Notes:
Starting with the top left, someone tries to access the implementation. When this request is made, a combination of device and browser information is passed to TrakSYS.

Next, TrakSYS uses that information and attempts to validate the User. If Windows Credentials are available, they will then be checked against Windows Active Directory and checked to see if they match a configured TrakSYS User. If successful, the Windows User is granted their matching permissions.

If the browser does not support Windows Authentication, or if no matching User with the required Permissions is found, the user will instead be prompted to provide a set of TrakSYS User credentials. If they are able to provide credentials with the proper permissions, they will be granted access to the page.

This check is done on every page. If the user has already been validated, the User's credentials will be checked before prompting for new login information.

<!-- Slide number: 5 -->
# Roles

<!-- Slide number: 6 -->
# Roles

![](Picture14.jpg)
Joe

![](Picture12.jpg)
Bob

![](Picture10.jpg)
Dan
Users
Represent a named collection of one or more Permissions defined within TrakSYS

Permissions can include the following:
Built-in Permissions for Configuration and Data Activities
Page Access Rights
User-Definable Permissions

Users are associated with one or more Roles to establish their Page Access and functional Rights
Line 2 Operators

Events (View/Modify)
KPI (View)
L2 Reports (Yes to All)
L2 Reports – MTBF (No)
Supervisors

Events (Create/Delete)
L1 Reports – MTBF (Yes)
L2 Reports – MTBF (Yes)
Task Review (Yes)
Line 1 Operators

Events (View/Modify)
KPI (View)
L1 Reports (Yes to All)
L1 Reports – MTBF (No)

Line 1 Operators

![](Picture121.jpg)

![](Picture120.jpg)

![](Picture123.jpg)

![](Picture122.jpg)
Line 2 Operators

![](Picture112.jpg)

![](Picture111.jpg)

![](Picture114.jpg)

![](Picture113.jpg)
Supervisors

![](Picture108.jpg)

![](Picture107.jpg)

### Notes:
Of course, for this Authentication Process to matter, the User Permissions must be identified. In TrakSYS, this is done through Roles.

A Role represents a collection of Permissions. Each Role can be given any desired combination of these three. Users can then be assigned to these Roles to receive the combination of the associated permissions. Before we go more indepth with the example on the right, let's see what these permissions look like.

<!-- Slide number: 7 -->
# Permissions
Each Role is associated with a set of…
…Implementation-Specific Permissions
…Data and Configuration Action Permissions
…Page Access Permissions

![A screenshot of a survey Description automatically generated](Picture3.jpg)

![A screenshot of a chat Description automatically generated](Picture2.jpg)

![A screenshot of a computer Description automatically generated](Picture4.jpg)

![A screenshot of a computer Description automatically generated](Picture5.jpg)

### Notes:
Each role is able to identify access to these 3 types of permissions. All three types are fully configurable through the web

First, Page Permissions
Page permissions allow you to identify a page or set of pages that the Role should or should not have access to. This is covered more in the next slides.

Second, Built-in Configuration and Data Actions.
For the Configuration and Data entities allow you to identify access through the use of a simple Matrix. For the Configuration elements, you are able to identify View/Create/Modify and Delete permissions for every single configurable entity in the software. For data, you can identify Create/Modify and Delete. There is no View option Data since that is controlled through implementation specific page definitions. We'll look at this in more detail during the demonstration

Third, User-Definable Permission Sets
The User-Definable Permissions allow you to create additional Matrixes of permissions. These permissions can be referenced easily through API to allow for more specific permissions than what are available in the standard configuration. This will be covered in more detail in a later module.

Between the three options, you are able to fully control access to all aspects of the implementation.

<!-- Slide number: 8 -->
# Page Permissions

<!-- Slide number: 9 -->
# Page Permissions

Hub 3s
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
Roles can provide access rights to pages in an implementation.

Access Modes:
Yes (single Page)
Yes to All (Parent and all Child Pages)
No Access

The standard navigation elements in the TrakSYS Web will automatically hide any pages that the user does not have access to.

While Page Permissions give access to the page, the page may have additional permission requirements to use the page’s functionality.

### Notes:
Let's take the deeper look at Page Permissions.

These are assigned to a role to identify the Role's access rights to a page.

There are 3 different options:
Yes, which affects a single page
Yes to All, which affects a page and all of its children

And

No Access, which affects a Single page

Based upon the combination of Page Permissions that a User has, they will either be granted or be denied access to a Page. To simply this for the end-user, TrakSYS will also automatically hide any pages that a User does not have access to from the standard Navigation elements.

Let's look at these different access modes using the example page hierarchy on the right.

<!-- Slide number: 10 -->
# Page Permissions

Hub 3s
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
Yes (single Page)

This provides access to a single page. Page can be accessed directly through its URL but will otherwise require access to the Parent Page to access it through the standard navigation.

### Notes:
First is the "Yes (Single Page)" Access type.

This will provide the use with access to that page specifically. Keep in mind, this does not affect any parent or children pages.

For Example: If you were to provide a role with "Yes" access to the "Reports" Hub 1, Users with that Role would be able to navigate to the Reports page while in the Packaging Section. However, if they did not have access to the Packaging Section, they would never see that navigation option in the first place. In that scenario, you would want to also provide them with Access to the Packaging section OR another method of accessing the Reports URL, such as a direct link or bookmark. In addition, even though you've given them access to the "Reports" Hub 1, that role does not have access to any of the children pages and would not be able to see or access any of the Hub 2's without additional permissions.

<!-- Slide number: 11 -->
# Page Permissions

Hub 3s
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
Yes to All (Parent and all Child Pages)

This provides access to a page, as well as every child page related to it.

e.g. If given Yes to All on Hub1, the role would have access to any Hub2’s, Hub3’s, and Spokes that have the associated Hub1 as a parent.

### Notes:
The "Yes to All" option provides that cascading permission. A role with "Yes to All" access for a page will be able to access the identified page as well as all of the Page's children.

In the example shown, "Yes to All" is being given to the "Reports" Hub 1. Similar to the "Yes (Single Page)" permission, this role grants access to that page, but since it is a "Yes to All", it is also granting access to every Hub 2 and Hub 3 underneath that parent.

<!-- Slide number: 12 -->
# Page Permissions

Hub 3s
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
No Access

This denies access to a specific page, within that Role. Commonly used alongside the Yes to All permission.

e.g. If given Yes to All on Hub1, but given No Access to a child Hub2, access to that specific Hub2 would be revoked.

### Notes:
Lastly, there is the "No Access" option. This is meant to be used in conjunction with a "Yes to All" permission. A role with a "No Access" permission is being explicitly denied access to an individual page.

In the previous example, a "Yes to All" permission granted access to every Report that was built. However, it is possible that you may not want to grant access to a specific report. For example, let's say there is an MTBF report that is suitable for a supervisor, but not for the general operators. If you wanted to grant access to every Report except the MTBF report using just the "Yes" and "Yes to All" permissions, you normally would have to give explicit "Yes" permissions to "Reports", "Yes to All" to "Events", and "Yes to All" to OEE. Alternatively, you can use the "No Access" option to simplify this. Provide "Yes to All" to the "Reports" hub, and then simply deny access to the "MTBF" Hub 2 with a "No Access" override.

<!-- Slide number: 13 -->
# Having Multiple Roles

![](Picture14.jpg)
Joe

![](Picture12.jpg)
Bob

![](Picture10.jpg)
Dan
Users
A user with more than one role will gain the permissions of each role. That user will be able to access pages and activities that any of their roles can access.

Example Scenario:
If a user has two roles, A and B. Role A says users cannot view a report. Role B Says users can view that same report. Since one of the roles says the user can view the report, they can view the MTBF report.
Line 2 Operators

Events (View/Modify)
KPI (View)
L2 Reports (Yes to All)
L2 Reports – MTBF (No)
Supervisors

Events (Create/Delete)
L1 Reports – MTBF (Yes)
L2 Reports – MTBF (Yes)
Packaging Scheduler (Yes)
Task Review (Yes)
Line 1 Operators

Events (View/Modify)
KPI (View)
L1 Reports (Yes to All)
L1 Reports – MTBF (No)

Line 1 Operators

![](Picture40.jpg)

![](Picture39.jpg)

![](Picture42.jpg)

![](Picture41.jpg)
Line 2 Operators

![](Picture31.jpg)

![](Picture30.jpg)

![](Picture33.jpg)

![](Picture32.jpg)
Supervisors

![](Picture27.jpg)

![](Picture26.jpg)

### Notes:
Now that the general permissions are covered, there's one final topic, cross-role interactions.
When a User has more than 1 role associated with it, they can end up with a mix of permissions

Let's look at the example on the right we displayed earlier.

We have 3 roles identified. Line 1 Operators, Line 2 Operators, and Supervisors.
Line 1 and Line 2 Operators have very similar permissions. Both have the ability to View and Modify Event information and can View KPI data. In addition, each role also has been configured to view their respective Reports but are denied access to the MTFB report.
Supervisors on the other hand have permissions to Create and Delete Event data and to Modify KPI Data. They also can view two additional pages, the Packaging Scheduler and the Task Review page as well as the MTBF reports.

We also have 3 users that have been identified and associated with these roles.
Bob has both Operator roles and will be able to View/Modify Events and see both sets of Reports, but is denied viewing permissions for both MTBF reports.
Joe has the Line 1 Operators role and the Supervisors role. He will be able to see all of the Line 1 Reports, including the MTBF report because of the Supervisor role. He will also be able to see the Line 2 MTBF report if he navigates to it, but since he was not given the Line 2 Operator role, he will not have access to the parent and will not see it show up in his standard navigation.

When using multiple roles that have potential overlaps, be sure to test your results. When used properly, this segregation of permissions can allow for very versitile and powerful user control.

<!-- Slide number: 14 -->
# Configuring a New User

### Notes:
Let’s look at a simple example of configuring a brand new user for a TrakSYS implementation
