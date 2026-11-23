# What are the standard TrakSYS Ports?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/14879162467603-What-are-the-standard-TrakSYS-Ports*
*Last updated: 2025-05-21T21:59:08Z*

---

Applies To | TrakSYS 10+

TrakSYS has the ability to host distributed components across multiple machines. This can include separating components such as SQL Server, the TrakSYS Web Application Pool, the TrakSYS services, and more. The software can also be hosted on services such as Amazon AWS and Azure. However, these types of architectures require specific ports on the network to be open. TrakSYS uses the following ports by default:

  * The default TrakSYS port is `80` for HTTP and `443` for HTTPS.
  * The SQL Server TCP port is `1433`.
  * The OPC TCP port is `135`.
  * The standard OPC UA port is `4840`.



**Note:** Some OPC UA servers allow users to specify different ports. If this feature is used on the OPC UA server, then that port should be used instead.

  * The default MQTT port is `1883`.
  * The default secure MQTT port (for TLS authentication) is `8883`.



**Note:** If a different port has been specified for secure TLS authentication within the environment, then that port should be used instead.
