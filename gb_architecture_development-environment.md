# Development Environment

TrakSYS includes and supports the concept of a Development Server. The purpose of the Development Server is to enable a parallel TrakSYS server installation that can be used to initiate changes to a configuration, test them without disrupting real data collection, and move those changes to the production server at a convenient time. The Development Server is enabled by adding an optional license component.

## Distribution

Typical implementations have a separate application server hosting the Development Environment. In some cases the database server can be shared with the production environment (with a separate development database). Similarly, the OPC server can be shared between the Development and Production environments, but the load on the OPC server should be considered.

{% hint style="success" %}
For Multi-Site installations utilizing Development Environments, there is typically a separate Development Environment for each site.
{% endhint %}

## Methodology

The main purpose of utilizing a Development Environment is to create and test updates both to the configuration and user interface without disrupting the production environment. Typically, after the Production Environment is implemented and properly functioning, a full database backup will be taken and restored to the Development Environment. From that moment forward, no configuration or user interface changes should be done on the production server. Instead, all changes should be made on the Development Server where they can be properly tested within disrupting production. Once the changes have been approved and an amenable time is chosen to make the push to production, the Transfer tool can be used to transfer the new configuration and user interfaces changes from the Development Environment to Production. See the [Database](../installation-manager/database) topic of the Installation Manager section for more information regarding the Transfer tool.
