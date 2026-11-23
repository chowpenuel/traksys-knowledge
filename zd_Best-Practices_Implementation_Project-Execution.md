# Project Execution

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360009045394-Project-Execution*
*Last updated: 2025-06-30T23:42:54Z*

---

### Summary

This article covers high-level and strategic recommendations for general TrakSYS project execution.

### Development and Test Environments

TrakSYS provides the option for adding additional instance licenses for development and testing servers. Once an application is deployed into production, it is very difficult to modify configuration and user interfaces in the production instance without disrupting the application users. Adding at least one additional environment is highly recommended for any solution.

Using developer and test instances, changes can be made and testing in a duplicate application environment, allowing the production instance to continue running the stable business functions.

When using multiple instances, TrakSYS provides a Database Transfer tool that allows pushing configuration and user interfaces changes from one instance to another. This alleviates mistakes that can occur when manually transferring many changes.

### Lifecycle Management Tools

During the development and deployment of a complex TrakSYS solution, it is recommended that one or more Lifecycle Management tools be employed to assist with organization of requirements, tasks, and project collateral.

While the specific tools chosen may vary, the functionality provided should cover two main areas. First, structures for defining requirements, configuration and development tasks, and issues are a must. Second, a solution should be available for shared storage and access of collateral such as configuration lists, equipment layouts, and other project documentation.

Some tool recommendations based on past positive experiences include Azure DevOps and SharePoint (Office 365). As with any tool, there are learning curves to setting these up and configuring, however if used regularly for multiple projects, these can be worthwhile investments. Other tools being used by Parsec partners include:

  * Jira
  * Basecamp
  * Smartsheet
  * Mavenlink



The selection of tools and platform should take into consideration that TrakSYS implementations typically include team members from two or more different organizations (Customer, Partner and Parsec). Tools that allow users from different organizations and remote locations are preferred.

### Template Approaches

When plans call for deploying TrakSYS to a number of customer sites with similar functionality, the conversations quickly lead to creating some sort of central "template" that can be developed once and rolled out with some cost savings. There are several elements of this approach that should be considered.

#### Governance

With this approach, it is essential that the customer have a central group that will assume long term ownership of the "template". Note that this is different than technical ownership of the template (which usually falls to the implementation team). The customer must stay engaged with the long term management and decision making of a multi-site template.

#### Technical

There are many options for implementing a common template across multiple TrakSYS sites. The high level options include a common starting point (customized and diverged at each site), deployed Content Page libraries that are configured at each site, and even App-compiled content that is locked from any changes. In many cases a variety of these techniques may be combined.

#### Updates and Divergence

Any templated solution must take into account the inevitable need to be updated. This includes tracking changes and updates to template content, as well as the need to path and update the TrakSYS platform at different rates throughout the organization. Finally, it is common and practical that sites will have to diverge from following templates 100%. This should be accounted for and guidance/procedures should be in place for when this occurs.

### Customer Project Team

A critical part of TrakSYS project success is adequate participation from the customer team. As a TrakSYS solution is essentially a business process, timely and regular input from the process owners is critical.

Some of the most successful TrakSYS implementations come from situations where the correct quantity and quality of customer team participation occurs. Of course the exact nature of participation depends on the type of project and functionality.

One of the most important and often time lacking customer roles, is that of final decision maker. There are frequent points during design and implementation where specific judgement calls on functionality (business or even user experience) must be made. All too often, situations arise where different groups (implementers and even different customer groups) end up looking at each other waiting for final guidance and decisions. Early and clear establishment of decision making team members is key for successful and efficient implementations.

### Cloud Sandbox for Collaboration

Early in the project lifecycle (before final customer environments are available), there is often need for collaboration on configuration and user interface concepts. Traditionally, implementation partners have setup the development environment at their site, and invite the customer team to view concepts over remote meeting sessions.

With the advent of cloud hosted servers, a more efficient and flexible option is to stand-up a "sandbox" TrakSYS environment in a neutral location (Azure or AWS) where both implementation and customer team members can easily access the environment for testing, configuration and education.

There are several options when setting this up. Partners may choose to setup cloud servers with their own Azure or AWS accounts and utilize their Partner development license. Customers may take ownership using their secondary development or test TrakSYS licenses, or Parsec will offer the rental of a "sandbox" environment. For a monthly fee, Parsec will setup and maintain the environment for as long as required.

### Agreed upon Documentation

Documentation requirements for TrakSYS project implementation can vary greatly depending on the manufacturing industry and functionality being implemented. For small data collection only projects, required documentation may be minimal. On the other end of the spectrum, MES/MOM type projects in regulated industries such as pharma, likely contain heavy documentation and procedural expectations.

In any of situations, it is recommended that the required documentation be agreed upon early in the project process (as early as the proposal and scope phase if possible). Topics to be clarified are the exact types of documents needed for the project, as well as the preferred formats. Should customer or partner templates be used?

It is recommended that implementation partners create standard document templates for commonly requested items, to offer customers as a starting point alternative. This presents well and can save time when no customer standards are available.

### Trial Early / Allow Time for Adjustments

A TrakSYS project implementation (like other software of this type), can be a flurry of activity. Customer resources are temporarily re-directed to assisting the project, commercial agreements are put in place to ensure 3rd party assistance, and production integration is carefully scheduled. Once the "formal" project is complete, there is typically a steep drop-off in attention and resources available to adjust the solution.

As this is the typical process, it is important to account for production trials of the solution, and adequate time and resources to make adjustments to the solution. Regardless of how much design and specification that is done prior to rollout, most organizations are not in a position to predict their needs so accurately. This is normal, and should be expected, rather than reacted to without preparation.

This recommendation includes deferring final testing (and possibly user training) until after these reviews and adjustments can be made. This recommendation can be challenging to realize in regulated projects where the lifecycle is more strict, however every effort should be made, so that a less than adequate solution does not get locked in, simply because of time/resource constraints.

### Local Expertise and Ownership

While TrakSYS implementations are typically done by 3rd party (partner or Parsec), the most successful deployments and long term sustainable solutions are guided by strong internal customer ownership/product expertise. It is highly recommended that customers designate a solution owner (or group) and have at least one semi-technical resource partially or fully dedicated to the TrakSYS solution.

Customers often send technical resources to TrakSYS training courses (which is a great start), however their job responsibilities once back at the site, do not really include regular interaction with the TrakSYS system. It is not realistic to retain technical TrakSYS knowledge without regular exposure.

Customers who employ one or more dedicated resources to maintaining and adjusting the TrakSYS solution, report more user and business satisfaction, as they are able to adapt the deployment after the initial implementation activity subsides.

### Testing Approaches

The following are some recommendations and guidance when deciding on a formal testing strategy with TrakSYS projects.

Because TrakSYS implementations typically span several business systems and technologies (ERP to PLC), the most common approach is traditional "scenario based" test scripts. These can be organized using paper-based documentation, but can be better managed using a SDLC tool or test suite.

While automated code unit testing is possible by setting up a complex development environment with Visual Studio, this arrangement is expensive (time) and limits how and when implementers can interact and modify configuration and script. It is not usually recommended except for in specific circumstances or when customers demand it.

Automated testing tools do exist that can externally "script" browser execution and clicks (such as Selenium). This would be the recommended approach for automating most test scenarios within TrakSYS.

### Infrastructure Landmines

The following list some common infrastructure challenges when setting up and executing TrakSYS deployments. Appropriate time and resource should be allocated.

#### Remote Connection

Enabling a remote connection from the external implementers environment (partner or Parsec) is a must. This allows for a more efficient pre-setup and deployment, and provides a mechanism for post rollout support. In many cases, the process of establishing these remote connections can be underestimated. Often times, this process stretches out over weeks and requires significant communications and paperwork to complete.

#### OPC / Automation Connectivity

Allow adequate time for installing, configuring OPC servers. This includes troubleshooting OPC DA DCOM security issues, and verification of Tag existence and values. It is strongly recommended that all connectivity is verified before engaging in on-site deployment rollout activities.

#### Cross Network Visibility (Plant vs. Business Network)

A common customer network topology involves separate networks for automation and business networks. While the TrakSYS Application and Database components can technically reside on either network, the easier path typically lies in locating TrakSYS on the automation network. In this scenario, the main ports requiring opening to the business network are port 80 (probably already open), and the SQL Server port(s). The converse involves opening low-level automation protocols over the firewall, something with which customer IT has less experience and comfort.
