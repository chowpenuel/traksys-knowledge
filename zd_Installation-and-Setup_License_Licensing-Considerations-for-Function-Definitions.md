# Licensing Considerations for Function Definitions

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360051603534-Licensing-Considerations-for-Function-Definitions*
*Last updated: 2025-05-21T22:04:28Z*

---

Applies To | TrakSYS 10+

### Summary

This article explains the meaning of Function Definitions in TrakSYS as related to license-sizing decisions.

#### Function Definition

A Function Definition in TrakSYS represents a single possible operation or capability for an instance of a Batch System in the configuration. It is a key feature to using much of the Batching functionality in TrakSYS. In the configuration below, the **Blender** Sub-System has been created under **Batching 1**.

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360082843453) ![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360081703934)

This Sub-System is capable of two different operations, **Load** and **Blend**. This represents two Function Definitions.   
  
![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/360082843613)  
  
If the configuration was made up of 10 different physical Blenders, then it would contain 10 x 2 = **20** Function Definitions. Note that Function Definitions configured under a Template Parent System do not count against license limits.

#### Function vs. Recipe Step Definition

When configuring Recipes in TrakSYS, the Function Definitions of the physical equipment are assigned order and planned duration. In some cases, a single equipment Function Definition may need to be executed more that one time within a Recipe. In the following Recipe, the **Load** and **Blend** Function Definitions are each called multiple times during the Batch execution.   
  
![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/360082845053)  
  
The number of times a Function Definition is referenced within a Recipe AND the number of Recipes that a Function Definition is used in, are **NOT** factors in counting for licensing purposes. For licensing purposes, the Function Definition count is simply the total number configured under the Batch Systems and Sub-Systems.

### Conclusion

When purchasing the TrakSYS Batching license, the number of Function Definitions must be determined. To estimate the needed number of Function Definitions, consider the number of different operations or functions that will be required for tracking/control in each Batch System.
