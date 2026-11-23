# Licensing Considerations for Process Definitions

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360052014434-Licensing-Considerations-for-Process-Definitions*
*Last updated: 2025-05-21T22:03:50Z*

---

Applies To | TrakSYS 11.1+

### Summary

This article explains the meaning of Process Definitions in TrakSYS as related to license-sizing decisions.

### Process Definitions

A Process Definition in TrakSYS represents the steps and transition logic for a given business process, for display in a single real-time Visual Workflow. The Visual Workflow can be executed manually from the web via user interfaces or programmatically using the TrakSYS API.

In the configuration below, three (3) Process Definitions have been created for various purposes.

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360084791173)

If each of the Workflow Groups shown above contained 3 Process Definitions, then the TrakSYS license for this application must contain 3 x 3 = **9** Process Definitions.

### Visual Workflow Diagram

The steps and transition logic for each Process Definition are defined in its Workflow diagram. Each step can contain multiple Step Connectors that can lead to different paths.

The Workflow diagram below is associated with the **Production Workflow** Process Definition shown in the screenshot above. The diagram splits into two paths and follows both processes as each condition is met.

![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360084801193)

The number of Steps and Step Connectors are **NOT** factors in counting for licensing purposes. For licensing purposes, only the total number of Process Definitions are counted.

### Conclusion

When purchasing a TrakSYS license, the number of Process Definitions must be determined. To estimate the needed number of Process Definitions, consider the total number of Visual Workflows that will be needed.
