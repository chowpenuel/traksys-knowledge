# Licensing Considerations for Interface Definitions

*Source: https://portal.parsec-corp.com/hc/en-us/articles/18432445152019-Licensing-Considerations-for-Interface-Definitions*
*Last updated: 2025-05-21T22:03:32Z*

---

Applies To | TrakSYS 12+

### Summary

This article explains the meaning of Interface Definitions in TrakSYS as related to license-sizing decisions around the use of TrakSYS Connect.

### Interface Definitions

An Interface Definition in TrakSYS represents a single connection (pipe) to a 3rd party system. Each Interface Definition can have one inbound message payload and one response message payload associated with it. In general, it’s best to think about an Interface Definition as the way in which TrakSYS will either receive or transmit a defined message to or from a 3rd party system. Considering the number of data movement use cases (scenarios) may provide the best estimate. See example scenarios below.

![Screen](https://portal.parsec-corp.com/hc/article_attachments/18432433105939)

### Example Scenarios

#### ERP (Enterprise Resource Planning) sends Production Order to TrakSYS via Webservice (Synchronous Processing).

In this case a defined message (payload) will be sent from the ERP to TrakSYS. One Interface Definition will be defined to receive this inbound payload and send a simple response back to same call. It does not matter how many payloads are sent through the interface, only that the interface is defined, and that all the payloads are the same structure. The diagram below shows the single Interface Definition in blue.

![Screen](https://portal.parsec-corp.com/hc/article_attachments/18432490084755)

#### ERP sends Production Order to TrakSYS via Webservice (Asynchronous processing via DMS (Data Management Service)).

In this case a defined message (payload) will be sent from the ERP to TrakSYS. One Interface definition will be defined to receive this inbound payload and send a response. Once payload processing is complete TrakSYS will send a response to the ERP via a second Interface. In this case the ERP will need to receive a response payload via a different pipe than that in which it sent the initial payload. In this case two Interface Definitions will need to be created. The diagram below shows the two Interface Definitions in blue.

![Screen](https://portal.parsec-corp.com/hc/article_attachments/18432445132691)

#### TrakSYS updates Material Consumption in ERP via Webservice.

In this case TrakSYS will deliver a message (payload) containing material consumption information to the ERP. This is triggered by a user action. The user action triggers the TrakSYS Connect Interface to start, which calls the ERP webservice endpoint and delivers the message payload. The diagram below shows the single Interface Definition in blue.

![Screen](https://portal.parsec-corp.com/hc/article_attachments/18432433124883)

#### TrakSYS polls location for new file containing updated BOM/recipes from ERP (Asynchronous processing via DMS (Data Management Service)).

In this case the ERP is delivering files to a directory that TrakSYS is monitoring. When TrakSYS finds a new file, it then triggers an Interface Definition to process the data. The diagram below shows the single Interface Definition in blue.

![Screen](https://portal.parsec-corp.com/hc/article_attachments/18432490096147)

### Single-Instance Multi-Site (SIMS)

Interface Definitions cannot be shared across sites when created in SIMS environments. While only a single TrakSYS Connect License is required per SIMS environment, each site will still need their own Interface Definitions configured.

### Conclusion

When purchasing a TrakSYS license, the number of Interface Definitions must be determined. To estimate the number of Interface Definitions required, consider the number of use cases for data transfers. It is also important to consider whether the payload processing will be synchronous or asynchronous, and whether a separate response is required if asynchronous, thus requiring an additional Interface Definition.
