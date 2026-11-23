# Components Distribution

The TrakSYS components are flexible and support a variety of distributed scenarios. Below are some typical examples of component distribution (although architectures are not limited to these examples). In these examples, the Application server hosts the TS Web application and Services, the Database server hosts the TrakSYS database, and the OPC server hosts the OPC data connections. Additionally, TrakSYS can be used within various Development Environments; see the [Development Environment](../development-environment) topic for more information.

## Shared

### Shared Server for All Components

In some simple scenarios, the TrakSYS Web, Services, Database, and OPC Server can all be hosted on the same server. Depending on the size of the installation and its requirements,this may require robust hardware, but is the simplest set up.

## Distributed

While every implementation can vary, it is important to determine where the majority of the load exists between the various components of a TrakSYS installation. For example, having a single server handle all of the load for an entire site can impact performance. Therefore, understanding if an installation has many transactions between the TrakSYS Services and the OPC Server or between the TrakSYS Services and the Database can help determine which components to distribute and cater more resources toward.

### Shared Application & Database Server – Distributed OPC Server

Many implementations have an already established OPC Server. Therefore, the Application Server and Database Server are shared with view of the OPC Server so the Application Server can still connect.

{% hint style="info" %}
When using a distributed OPC Server, typically Logic Service must be run as an account with permissions on both the TrakSYS Application Server and the OPC Server. Also, DCOM settings between the OPC Server and the TrakSYS Application Server must be considered.
{% endhint %}

### Shared Application & OPC Server – Distributed Database Server

Many implementations have an already established Database server. Therefore the Application Server and OPC Server are shared with view of the Database Server so the Application Server can still connect.

### Distributed Application Server – Distributed Database Server – Distributed OPC Server

In some implementations the components are hosted separately. As long as the servers are within view of each other either on the same network or through firewalls, the components can function harmoniously.

### Centralized TrakSYS & Components

To consolidate equipment and maintenance requirements, the TrakSYS Web, Applications, and Database can be hosted centrally within a corporate WAN. OPC connectivity must of course be considered in this scenario.

### Centralized TrakSYS – Distributed Components

To achieve centrally hosted Multi-Site implementations or to partially consolidate equipment and maintenance demands, the TrakSYS Web Server and Database can be hosted centrally within a corporate WAN while the TrakSYS Services (e.g. Logic Service) can be ran on the server on-site. Again, network considerations for connecting to the OPC server should be taken into consideration.

{% hint style="info" %}
When introducing distributed components in any scenario, network performance becomes a much larger consideration as it can impact functionalities such as page load times, report rendering times, and Logic Service scan periods.
{% endhint %}

## Network Considerations

In environments where there are two distinct networks (automation and business), the network location/placement of the TrakSYS server must be considered. The primary challenge is that automation data sources (PLCs) and clients are typically located on the automation network, while business data sources (ERP) and clients are located on the business network. These networks are typically separated by restrictive firewalls. The TrakSYS server must have clear communication paths to all of these.

### TrakSYS on Automation Network

Placing the TrakSYS server on the automation network eases the connectivity to the PLCs and plant floor devices; however, interactions with business systems such as ERP and client devices on the business network are complicated.

_**Pros**_

* Connections with OPC Servers (DCOM) is simplified, as they will be located on the same domain/workgroup as the TrakSYS server.
* Client devices on the automation network can access the TrakSYS web application easily over port 80.

_**Cons**_

* Communication with business systems such as ERP that are located on the business network must be negotiated. The exact ports/changes to the firewalls are dependent on the type of connection and protocols used for communication.
* Port 80 communication on the firewall(s) must be opened to allow client devices on the business network to access the TrakSYS web application.
* Customer IT departments sometimes do not support servers installed on the automation network. This can lead to difficulty in server procurement and installation.

## TrakSYS on Business Network

Placing the TrakSYS server on the business network eases the connectivity to the business systems such as ERP and client devices; however, interactions with PLCs and plant floor devices on the automation network are complicated.

_**Pros**_

* Connections with business systems such as ERP that are located on the business network is simplified, as they will be located on the same domain/workgroup as the TrakSYS server.
* Client devices on the automation network can access the TrakSYS web application easily over port 80.
* Customer IT departments will typically support servers installed on the business network.

_**Cons**_

* Connections with OPC Servers (DCOM) is complicated, as they will be located on a different domain and on the other side of a firewall from the TrakSYS server. It is common for there to be resistance to opening the ports necessary to allow OPC DCOM traffic through the firewall. Alternative solutions involve setting up an OPC tunnel using OPC UA, which crosses the firewall on port 80 (easier to open).
* Port 80 communication on the firewall(s) must be opened to allow client devices on the automation network to access the TrakSYS web application.
