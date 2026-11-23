# Licensing Considerations for Sample Definitions

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360052375253-Licensing-Considerations-for-Sample-Definitions*
*Last updated: 2025-05-21T22:04:20Z*

---

Applies To | TrakSYS 10+

### Summary

This article explains the meaning of Sample Definitions in TrakSYS as related to license-sizing decisions.

#### Sample Definition

A Sample Definition is a placeholder for SPC values to be recorded for a given System. Sample Definitions may be configured to collect quantitative values (weight, temperature, height) or item attributes (damaged, defective, good) against an associated set of Target and Limit values.

Each unique type of value or attribute will require their own Sample Definition within TrakSYS. In the configuration below, a Sample Definition has been configured to record **Fill Weights** for a specific machine or asset.

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360081719154)

#### 

#### Sample Definition Relationships

Sample Definitions are associated with specific TrakSYS Systems, and are not created for general-purpose use throughout the application. The values recorded for a Sample Definition are specific to the System that they are associated with. A System may contain one or more Sample Definitions based on the requirements for SPC data collection.

In the configuration below, the **Packaging 1** System will record SPC data values for the following named Sample Definitions:

  * **Fill Weights  
  
**
  * **Bottle Inspection**



This configuration represents two (2) Sample Definitions.

![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360081719174)  
  
If there are 10 different physical Packaging Lines modeled in the configuration, and SPC data for Fill Weights and Bottle Inspection must be collected for each Line, then the TrakSYS license for this application must contain 10 x 2 = **20** Sample Definitions. Note that Sample Definitions configured under a Template Parent System do not count against license limits.

### Conclusion

When purchasing a TrakSYS license for SPC data collection and analysis, the number of required Sample Definitions per System must be determined. To estimate the required number of Sample Definitions, calculate the total number of data values to be collected for SPC analysis in each System.
