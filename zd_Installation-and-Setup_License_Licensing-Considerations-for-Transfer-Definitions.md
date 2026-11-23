# Licensing Considerations for Transfer Definitions

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360051603814-Licensing-Considerations-for-Transfer-Definitions*
*Last updated: 2025-05-21T22:04:35Z*

---

Applies To | TrakSYS 10+

### Summary

This article explains the meaning of Transfer Definitions in TrakSYS as related to license-sizing decisions.

#### Transfer Definition

A Transfer Definition in TrakSYS represents a single possible transfer of material in or out of an instance of a Storage System. Transfer Definitions create a historical record of material movements through a Storage System and update the real-time material quantity available in the System. Transfers may be initiated automatically by logical expressions based on TrakSYS Tags or manually via TrakSYS Web user interfaces. In the configuration below, the **Silo 1** System is under the **Storage Zone 3** Area. 

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360081720074)

This System will monitor and record the following named material transfers:

  * **Receive Shipment  
  
**
  * **Transfer to Molding 1  
  
**
  * **Transfer to Molding 2  
  
**
  * **Transfer to Molding 3  
  
**
  * **Clean Silo**



This configuration represents five (5) Transfer Definitions.

![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360081725514)   
  
If the configuration was made up of 10 different physical Silos, then it would contain 10 x 5 = **50** Transfer Definitions. Note that Transfer Definitions configured under a Template Parent System do not count against license limits.

#### Transfer Definition Relationships

The number of Transfer Definitions required for a single Storage System can vary depending upon several factors. Transfer Definitions may be configured to track material transfers to our from a specific System in the model. This may result in multiple Transfer Definitions into our out of the Storage System being configured if TrakSYS must record the source or destination of a transfer.

In the configuration below, the Transfer Definition has been configured to record transfers **Out** of the Storage System to the Destination System **Molding 1**.  
  
![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360081891194)  
  
Multiple Transfer Definitions of a particular direction may also be required for a Storage System if multiple material transfers can be active simultaneously. For example when a System has multiple entry or exit points, or if there is a need to track different reasons for transfers.

For licensing purposes, the total number of Transfer Definitions configured for all Storage Systems in the configuration determines the final licensing count to be purchased.

### Conclusion

When purchasing the TrakSYS license for storage and inventory management, the number of Transfer Definitions must be determined. To estimate the needed number of Transfer Definitions, consider the total number of different named material transfers required for tracking in each Storage System.
