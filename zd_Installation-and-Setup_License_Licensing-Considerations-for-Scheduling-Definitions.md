# Licensing Considerations for Scheduling Definitions

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360052014594-Licensing-Considerations-for-Scheduling-Definitions*
*Last updated: 2025-05-21T22:03:43Z*

---

Applies To | TrakSYS 11+

### **Summary**

This article explains the meaning of Production Scheduling Systems in TrakSYS as related to license-sizing decisions.

### **Production Scheduling System**

A Production Scheduling System represents a single system that is included in the scheduling algorithm. This algorithm determines optimal scheduling based on inputs such as systems, jobs, products, and other factors. Additional considerations and custom factors can be added through the use of a Production Scheduling Script Class. In the configuration below, the **Canning** Production Schedule Set contains two (2) Production Scheduling Systems.

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360084937793)

The production scheduling algorithm can be executed manually via the TrakSYS Web user interfaces or programmatically using the TrakSYS Api. The page below is an example of a timeline of jobs that have been scheduled based on various factors. If the results are satisfactory, they can be committed to the installation.

![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360084944133)

If each of the Production Schedule Sets in this configuration contained 2 Systems, the TrakSYS license for this application would have to contain 5 * 2 = **10** Production Scheduling Systems.

### **Conclusion**

When purchasing a TrakSYS license, the number of Production Scheduling Systems must be determined. To estimate the needed number of Production Scheduling Systems, consider the total number of Discrete and Batch Systems that will be needed.
