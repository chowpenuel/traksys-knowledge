# Configuring Product Specifications

*Source: https://portal.parsec-corp.com/hc/en-us/articles/33545839594771-Configuring-Product-Specifications*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 12.0.3+

### Summary

In TrakSYS 12.0.3, a new entity called Product Specification Definitions was introduced. Previously, Product-Specific SPC limits were typically set in Product Attributes. This new feature provides a dedicated entity for storing Product-Specific SPC limits, allowing for better organization and management while freeing up Product Attribute fields. This article explains how to create and use Product Specification Definitions.

### Procedure

#### Configuring Product Specification Definitions

  1. Open the TrakSYS Web and navigate to **Configuration | Products | Specification Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33546944621075)  
  

  2. Click the New button under the Specification Definition Groups section on the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33546936863507)  
  

  3. Specify a Name for the group, then click the Save button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/34283734784915)  
  

  4. Select the newly created group and click the New button under the Specification Definitions section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/34283734800019)  
  

  5. Specify a value for the Name field, then click the Save button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33550048491667)  
  

  6. The Product Specification Definition should now appear within the list. Repeat steps 4 and 5 to add additional Definitions.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/34283721028243)  
  




#### Configuring Specifications

  1. Open the TrakSYS Web and navigate to **Configuration | Products**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33546936880147)  
  

  2. Select a Product Set and click the Edit button under the Third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33546944659219)  
  

  3. Select a Product Specification Definition Group and click the Save button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/34283721030419)  
  

  4. Select an existing Product under the Product Set and click the Specifications button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33547085924115)  
  

  5. Click the New button under the Specifications section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33550048499091)  
  

  6. Select the Product Specification Definition, and define the Product SPC limits and other properties as needed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33550042249235)  
  

  7. The Product Specification should now appear within the list. Repeat steps 4 through 6 to add additional Product Specifications.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33550048501907)  
  

  8. Note that when using Product Specifications, it is generally assumed there will be at least one unique Specification for each Product in the Product Set. So you will want to repeat 4-7 for each Product in the set.  
  




#### Configuring Sample Definitions with Product Specifications

For this example, we will be using a Batch System. The flow for performing the following may be slightly different for Discrete Systems. 

  1. Open the TrakSYS Web and navigate to **Configuration | Systems**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33550042251411)  
  

  2. Select an Area and Batch System that has a Product Set with a Production Specification assigned to it, then click the Sub-Systems button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33550048504851)  
  

  3. Select a Sub-System under the second slice, and click the Sample Definitions button under the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33550042263059)  
  

  4. Select a Sample Definition under the second slice, and click the Edit button under the third slice. This assumes a Sample Definition exists. If not, you can instead create a new Sample Definition and continue to Step 5.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33550042264467)  
  

  5. Select a Product Specification Definition and then click Save. You will also need to specify a name if creating a new Sample Definition.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33550042268947)  
  




Now you create Sample Sub-Groups pre-populated with Product Specific Limits and Values using the following method:
    
    
    Api.Spc.CreateFromSampleDefinitionAndProductSpec(DbSampleDefinition sampleDef, DbProductSpec productSpec)
