# Configuring Production Scheduling

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360053164333-Configuring-Production-Scheduling*
*Last updated: 2026-01-15T00:47:21Z*

---

Applies To | TrakSYS 11 | TrakSYS 12

### **Summary**

The Production Scheduling engine takes a set of Jobs and Systems, along with accompanying product and scheduling context, and algorithmically determines the optimal order and asset to run each Job. This article explains the necessary steps to set up and configure the different components required to use Production Scheduling. Since there are many possible combinations that can be used with Production Scheduling, this example makes the following assumptions:

  * One or more Systems (Discrete, Batching, or both) have been configured.
  * One or more Product Sets exist with configured Products.



### **Preparing the Job Data**

When the Job data is created in the appropriate tables, there are specific requirements that each record must meet so that it can be used by the Production Scheduling engine:

  * A value is required in the**tJob.PsSetID** field for each record. This value should contain the ID of the Production Schedule Set for the associated System.
  * The **tJob.PsRequestedProductCode** field must contain the Product Code for the configured Product.



**Discrete System Only**

  * The **tJobDiscrete.PlannedCalculationCount** field should contain the planned amount to be produced.
  * A Target Rate (**tProduct.TargetRateCalculationUnitsPerMinute**) must be defined for each Product. The scheduling engine uses this rate to help determine how long a job should be scheduled based on the amount to be produced.



**Batch System Only**

  * A valid Recipe needs to be assigned to the Product associated with the Job record. The Recipe must have a non-zero Planned Duration (Minutes) (**tRecipe.PlannedDurationSeconds**).
  * A value must be set for the Planned Number of Batches (**tRecipe.PlannedNumberOfBatches**) and the Planned Batch Size (**tRecipe.PlannedBatchSize**) fields in the Recipe configuration.
  * A value must be provided for the Planned Batch Size (**tJobBatch.PlannedBatchSize**) associated with the parent Job record.



### **Creating Production Schedule Sets**

Production Schedule Sets allow the grouping of Systems that should be scheduled together against a single Production Schedule Set. Note that an individual System (either Discrete or Batching) can only be assigned to a single Production Schedule Set. The following steps explain how to create a Production Schedule Set.

  1. In the TrakSYS Web, navigate to **Configuration | Production Scheduling | Sets**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19773799476115)  

  2. Click the New button under the Set section of the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19773839214611)  

  3. On the resulting page, specify a Name, Key, and Set Type. Then, click the Save button to apply the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19773913831187)  

  4. Repeat steps 2 and 3 to create additional Production Schedule Sets as needed. For the purposes of this example, 2 Production Schedule Sets have been created.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19773956933651)  

  5. Now that the Production Schedule Sets have been created, they need to be assigned to the appropriate Systems. To do this, navigate to **Configuration | Systems**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19773983837203)  

  6. Select the desired Area and System on the first and second slices. Once the System has been selected, click the Edit button on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774061589907)  

  7. On the System properties page, navigate to the Prod Sched tab to reveal the Production Scheduling properties for the System.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774134274323)  

  8. Click the blue picker button under the Production Schedule Set option and select the desired Set for the System.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774144434195)  

  9. Once the desired Set has been selected, click the Save button to apply the changes.
  10. Repeat steps 6 through 9 as needed to add additional Systems to the Production Schedule Set.
  11. To verify the Systems that have been added to each Production Schedule Set, navigate back to**Configuration | Production Scheduling | Sets**.
  12. Select the configured Set on the first slice to reveal the associated Systems on the second slice. The images below show the Systems assigned to both Sets.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774236002451)  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774328629395)



### **Configuring Changeover Families**

Changeover Families group together products that share similar changeover requirements. Similar to Production Schedule Sets, only one Changeover Family can be assigned to an individual Product. The following steps explain how to create a Changeover Family and assign the Family to a Product.

  1. In the TrakSYS Web, navigate to **Configuration | Products | Changeover Family**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774373972499)  

  2. Click the New button under the Groups section on the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774368102419)  

  3. Specify a Name and Key for the Group. Then, click the Save button to apply the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774385640211)  

  4. Repeat steps 2 and 3 to create additional Changeover Family Groups as needed. For the purpose of this example, 2 Groups have been created.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774389639443)  

  5. Select a newly created Group and click the New button under the Families section in the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774430925843)  

  6. On the resulting page, specify a Name and Key for the Changeover Family. Then, click the Save button to apply the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774479408787)  

  7. Repeat Steps 5 and 6 to add additional Changeover Families as needed.
  8. Now that the Changeover Families have been created, they need to be assigned to the individual Products. To do this, navigate to **Configuration | Products**.
  9. Select the desired Product Set and Product on the first and second slices respectively. Then, click the Edit button on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774568886035)  

  10. On the resulting page, navigate to the Prod Sched tab to reveal the Production Scheduling options.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774635182483)  

  11. Next, click the blue picker under the Changeover Family setting and select the desired Changeover Family. Then, click the Save button the apply the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774644044051)  

  12. Repeat steps 9 through 11 to assign Changeover Families to additional Products as needed.



### **Creating Changeover Types**

Changeover Types are grouped into Sets which can contain a collection of Changeover Family relationships. Each Product Changeover Type can help determine the Pre and Post Duration when going from a specific Changeover Family to another. The steps shown below describe how to create and configure Changeover Types.

  1. In the TrakSYS Web, navigate to **Configuration | Products | Changeover Type**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774776726931)  

  2. Click the New button under the Sets section in the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774765430675)  

  3. On the resulting page, enter a Name and Key for the Changeover Type Set. Then click the Save button to apply the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774821223443)  

  4. Repeat steps 2 and 3 to create additional Product Changeover Type Sets as needed.
  5. Select the newly created Product Changeover Type Set on the first slice and click the New button under the Types section in the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19774910466067)  

  6. Specify a Name and Key for the Changeover Type. Then select Changeover Families that are included in the Changeover Types. If all Changeover Families are included, then choose "Any" for the From and To options. Lastly, specify the length of time (in minutes) that the Changeover Type will take. The Pre Duration adds this additional time before a scheduled job while the Post Duration adds time after it.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19775017411091)  

  7. Click Save to apply the changes.
  8. Repeat steps 5 through 7 to create additional Changeover Types as needed.
  9. Now that the Changeover Types have been created, they need to be assigned to their respective Product Sets. To do this, navigate to **Configuration | Products**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19775040184467)  

  10. Select an existing Product Set in the first slice. Then, click the Edit button on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19775095704723)  

  11. Navigate to the Prod Sched tab within the Product Set properties. Then, specify the Product Changeover Type Set. Finally, click the Save button to apply the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19775115562003)  

  12. Repeat steps 10 and 11 to assign Changeover Type Sets to additional Product Sets as needed.


