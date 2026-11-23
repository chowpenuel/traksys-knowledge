<!-- Slide number: 1 -->
# Content Page Navigation

### Notes:

<!-- Slide number: 2 -->
# Related Content Pages

![](Picture11.jpg)
How does this work?

Where is the Planned Job Page?

### Notes:
Content Pages within TrakSYS automatically link together. For example, if you implement a System Discrete Real-Time Overview Content Page, it will automatically link to a Planned Jobs Content Page without any additional development needed. That relation may be a little confusing. Even though you only implemented one page, somehow the reset of the pages exist and can be navigated to, even though they have not been configured as part of your Page Definitions and Page Hierarchy. So how does that work?

<!-- Slide number: 3 -->
# “C Equals”

![A screenshot of a computer Description automatically generated](Picture3.jpg)
…/ocv/packaging/linehub/

![](Picture12.jpg)
…/ocv/packaging/linehub/?c=ETS.Application.Job.JobDiscreteListForSystemPlanned
( programmatic identified for Content Page )

### Notes:
This is done through a syntax and capability that is referred to as “C Equals”.

When clicking a link on a Content Page, there will always be a default link to go with it. If you do not override this link through the Page’s Configuration, you will be direct to a “C Equals” url. It is the same URL that you are currently on, but with an added Key Value Pair in the QueryString. This Key Value Pair uses the Key of “C”, and a value of a long string, typically beginning with ETS. This Key of “C” is a special key that has some unique applications.

In this example, the string is “ETS.Application.Job.JobDiscreteListForSystemPlanned”. When a TrakSYS page loads, it will check to see if this “C” key is being set. If it is being set, then the Page will actually decide to ignore the rest of the standard page execution, opting instead to load the default version of a Content Page. Which Content Page it loads is based upon the Value provided. In this example, the Key provided matches the Key for the Discrete Job List for System Planned, so that is the page that would be loaded.

For these “C Equal” pages, you can pass in values on the QueryString to set some of the parameters for the page, but you are limited to using only the standard properties on the page, which imposes a few additional limitations. Since the page is not actually configured, the various Values Keys and static properties will remain constant and are unable to be changed. Be sure to look at the default property values of a content page before using it in a “C Equals” link.

Any Content Page key, including Developer Content Pages, can be referenced in this manner. To see the keys that you can use, go to the Developer Section and use the options to Create a new Page Definition. Select the page you want to use and, instead of clicking to save it, copy the Key provided in the Page’s description.

<!-- Slide number: 4 -->
# Integrating a Custom Page

![](Picture20.jpg)
Special Page Functionality Needed

### Notes:
With this capability, you can now easily integrate and mix your own content pages and visual pages. For example, If you utilized the standard content page tree for an SDRO, it would automatically link to a standard Planned Jobs. If you needed some special functionality, you could simply override the link and provide your own page.

<!-- Slide number: 5 -->
# Integrating a Custom Page

![A screenshot of a computer Description automatically generated](Picture2.jpg)
Navigation in standard Content Pages may be Overridden

Provide a Relative URL
Visual or standard Content Page
Any other URL

Parameters may be Passed (as available)

Page Key on same Hierarchy Level
JobListSpecial ? SystemID = {SystemID}

Page Key back one Hierarchy Level
../JobListSpecial ? SystemID = {SystemID}

### Notes:
To do this, go to the Page Definitions property page and find the “Links” tab. Find the matching Link, in this case the “Job Planned” one, and provide your own relative URL for your new, specialized page. These URLs can even include expression syntax, and can be used to navigate to different layers of your page hierarchy.

Afterwards, if you want to continue to use the rest of the content pages, you can use the “C Equals” syntax on your custom page to take advantage of the easily-deployed Content Page options.

<!-- Slide number: 6 -->
# Content Page Navigation

### Notes:
Let’s look at this in a Demonstration, using the SDRO as an example.
