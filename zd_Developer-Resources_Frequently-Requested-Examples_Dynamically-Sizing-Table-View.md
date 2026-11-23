# Dynamically Sizing Table View

*Source: https://portal.parsec-corp.com/hc/en-us/articles/27653335897107-Dynamically-Sizing-Table-View*
*Last updated: 2024-07-24T18:41:10Z*

---

### **Introduction**

This article provides Page Definitions of a Frequently Requested Example (FRE). The pages provided are intended to provide a starting point for Developers who are looking to use more complex Development Tools. This is intended to augment the existing Training Information and Reference Documentation, but is not intended to be implemented directly into a production environment. 

Attached to this article is a zipped folder that contains one or more Page Definitions. The intended way to implement these pages as well as a short description of the capability they are meant to display are listed below. Additional information about the use and purpose of the Page Definitions is included on the Pages and can be viewed once they have been imported.

### **Capability**

This page creates a Table View that has a programmatically determined number of rows and columns. For example purposes, the Table View was designed to show a comparison of the Systems within an Area and the Products within their Product Sets to help visualize the production capabilities of the different Systems. Additionally, the cells of the table are dynamically colored to match the contents of the cell.

This is a more complex example to provide a starting point for those interested in creating their own dynamically sizing table views. It is done in a series of steps, listed below.

  1. The script will take a set of AreaIDs, loop through them, find all of the Areas and their child Areas, and then find any Systems within the parent or child Areas. Those Systems are used to create the Columns of the Table View.
  2. Next, the script will find all Product Sets for the related Systems, distilling it to a list of Unique Product Codes, which become the Rows for the columns. 
  3. The Table View and Data Source are then created, which are designed to show which Systems can produce which Products. 
  4. Additional JS and CSS are added to the page to highlight the cells based upon their contents. 



Everything is dynamically driven based upon properties at the top of the Script Editor. This includes the creation of the data source, the creation of the table view, the addition of the JS, and the addition of the CSS. It is intended to be maintainable through the properties alone.

This is only meant as an example and is limited to the provided use-case. The pattern can be extrapolated and expanded for other use-cases.

### **Page Deployment**

There is only a single page attached. It can be deployed anywhere. The page expects a comma-delimited list of Area IDs to function, which should be provided through the Values Key **AreaIDs**. For example, the demonstration uses the following for testing purposes:
    
    
    ?AreaIDs=17,18
    
    
    ?AreaIDs=86

This can be used with any Area in an implementation, as long as the Area has at least 1 System, which has at least 1 Product in its Product Set.

#### **Revisions**

21st March 2024- Initial Publication (v12.0.2)

Contact the [Parsec Applications Department](mailto:applications@parsec-corp.com) for any questions, comments, or concerns.
