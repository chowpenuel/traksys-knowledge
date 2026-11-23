# Using the Tree View Content Part

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360009376093-Using-the-Tree-View-Content-Part*
*Last updated: 2025-05-21T22:43:33Z*

---

Applies To | TrakSYS 10.2.4+

### **Summary**

A tree view is a way of representing the hierarchical nature of a structure in graphical form. The tree elements are called nodes, each one consisting of a value. The root node is the starting node at the topmost level of the tree. Branches, or branch nodes, are parent nodes that extend from the root or other branches and can contain one or more child nodes. Leaves, or leaf nodes, are child nodes that extend from the root or a branch and cannot contain any further nodes.

The Tree View Content Part leverages this concept to display meaningful data in a variety of different applications. There are three different Tree View Content Parts: the List Tree View, the Forms Tree View, and the Filter Tree View. Each of these Parts contains two data provider parts: one for branches and one for leaves. 

There can be many branches to create a multi-layered view, but the Part must contain at least one branch. A data provider part for branches is required to display data in a Tree View.

Leaves are not required to be on the tree, therefore a leaf data provider part is optional.

Branches and leaves have separate data provider parts so that creating entries for both types of nodes is easier to configure. In general, it's simpler to write two separate queries to return branches and leaves than it is to try and write a single query that efficiently returns all branches and leaves.

This article explains the standard procedure for configuring a Filter Tree View. This procedure can also be used to create and configure a Form or List Tree View. **Please note:** the example shown utilizes a data provider part for leaf nodes, which is not required for the Tree View Part to function.

### **Procedure**

The following example will demonstrate how to display configured Areas and Systems as branches and leaves on the Filter Tree View Part. This procedure may also be followed for the List and Form Tree View Parts. However, some options might be slightly different between each of the Parts.

  1. From a Visual Page Definition, add a Custom SQL Data Table Part.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18656732357395)  
  

  2. Enter a value for the Part ID field. Then, enter a query to return rows for the branches.   
  
The query shown below is returning a list of configured Areas. Since this example uses data provider parts for branches and leaves, the Key field must be unique across both. Therefore, the literal string "Area" was appended to the Key field. This helps prevent the possibility of having the same value in this field for both the branch and leaf Data Tables. This literal string was also appended to the ParentKey field to create a unique Parent Key for this data table.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18656877454227)  
  
The Keys and Parent Keys will help determine which Areas are root Nodes and which Areas will be placed under other Areas. As an example, a sample output of the query above is shown below.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360025174993)  
  
Notice how the PLC Area does not have a Parent Key. This is because the Area is meant to be a root Node and does not have any Areas above it. The next Area, OCWidgets, has the same Parent Key as the Key for the PLC. This signifies that OCWidgets will be under the PLC at the second level of the Tree View.  
  
Similarly, the Parent Keys for the Batching, Goo Storage, and Extrusion and Packaging Areas are the same as the Key for OCWidgets. This would put these Areas under OCWidgets at the third level of the tree. This is illustrated below:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360025191793)  
  

  3. Navigate to the Data tab and enter a value in the Target Values Key field.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18656956861075)  
  

  4. Navigate to the Advanced tab and set the Initialization Order to 1.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18656964826387)  
  

  5. Click Save to apply the changes.
  6. Repeat step 1 and add a second Custom SQL Data Table to the page.
  7. Enter a value for the Part ID field. Then, enter a query to return rows for the Leaves.  
  
The query shown below is returning a list of configured Systems. Similar to the data table for Areas, a unique literal string ("SYS") is being appended to the Key field in order to eliminate the possibility of having duplicate values between the two data provider parts. Unlike the Key field, the value returned in the ParentKey field for the Systems data table must match the value returned in the ParentKey field for the Area data table. This will determine which System gets placed under its respective Area.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18657085214995)  
  
When viewing the results of the query, the Key field will show the IDs of the Systems while the ParentKey field will display the IDs of the Areas in which the Systems will be placed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360025196013)  
  
Referring to the screenshot of the output for the Areas data table, "Area4" represents the Batching Area, "Area5" is the Goo Storage Area, and "Area6" is the Extrusion and Packaging Area. Therefore, each System will be placed under the appropriate Area based on the value contained in the ParentKey field.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360025195913)  
  
Remember that since the Systems are leaves, they will always be at the lowest levels of the branch. Therefore, there will be no Areas or Systems below the Systems that are used in the leaf data table.  
  
As mentioned in the Summary of this article, two separate data tables are used to make the process of returning Areas (branches) and Systems (leaves) easier. With this Part, it is easier to write two separate queries to return both entities and have the Tree View Part join the data provider parts than it is to write a single query that returns all the data and having to manually join them in a specific way.  
  

  8. Navigate to the Data tab and enter a value in the Target Values Key field.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18657168309907)  
  

  9. Navigate to the Advanced tab and set the Initialization Order to 1.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18657212006035)  
  

  10. Click Save to apply the changes.
  11. Next, add a Filter Tree View Part to the page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18657277014035)  
  

  12. Enter a value for the Part ID field. Then navigate to the Data tab. Enter a Source Key for the Node Branch and Node Leaf Source Value Key Fields. These values should match the Target Values Keys entered for the respective data tables in steps 3 and 8.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18657327813267)  
  

  13. Next, Navigate to the Node Branch tab and enter a TrakSYS Expression in the Text field to reference a column to be displayed for the Areas (or branches). In the example below, the AreaName column of the query is being referenced.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18657393813139)
  14. Navigate to the Node Leaf tab and repeat step 13, referencing a column of the query for the Systems (or Leaves) data table.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18657690286355)  
  

  15. **OPTIONAL** : under both the Node Branch and Node Leaf tabs, there are options to perform certain actions when a user clicks or double clicks an Area (branch) or System (leaf).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18657700191763)  
![](https://portal.parsec-corp.com/hc/article_attachments/18657718523923)  
  
The URL field will redirect the user to a specified page when the user clicks or double clicks a Node. The On Client Click and On Server Click fields will execute client-side or server-side code whenever a Node is clicked.  
  

  16. Click Save to apply the changes.
  17. Now, when the page is previewed the top level Area(s) should appear.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18657730623507)  
  

  18. As the options are expanded, the additional levels of Areas and Systems should appear.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18657800697107)


