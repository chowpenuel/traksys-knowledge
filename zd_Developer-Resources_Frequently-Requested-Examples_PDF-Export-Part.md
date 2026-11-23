# PDF Export Part

*Source: https://portal.parsec-corp.com/hc/en-us/articles/12185997805843-PDF-Export-Part*
*Last updated: 2024-07-24T18:55:28Z*

---

### **Introduction**

This article provides a Custom Content Part of a Frequently Requested Example (FRE). The part provided is intended to provide a starting point for Developers who are looking to use more complex Development Tools. This is intended to augment the existing Training Information and Reference Documentation, but is not intended to be implemented directly into a production environment without proper vetting. 

Attached to this article is a zipped folder that contains a Content Part. The part is intended to be implemented as part of the Content Parts Library, found under the Developer Section, in the Content Hub. Additional information about the use and purpose of the Content Part can be found below.

### **Capability**

This Content Part is designed using the TsButtons part as the base. It is designed to mimic the TsExcelExport Part's capabilities, but for the TrakSYS PDF Export capability. The standard PDF Export capabilities can be seen in the [Export Pages to PDF](https://portal.parsec-corp.com/hc/en-us/articles/360051910014-Exporting-Pages-to-PDF) article. The parameters defined in that article have been condensed into this Content Part with a few added properties for ease of use.

The properties on the Part are detailed below, by group.

General Properties

  * **File Name** : determines the name of the resulting file from the PDF Export.
  * **Target Url** : defines the target for the PDF Export. If left blank, it uses the current page.



Button Properties

  * **Button Css** : allows for added CSS to the button rendering.
  * **Button Icon** : determines the icon that is displayed on the button.
  * **Show During Print** : determines if the button is shown or hidden when the PDF is made.



Page Layout

  * **Orientation** : determines if the PDF is in the Portrait or Landscape orientation.
  * **Page Size** : assigns the desired PDF size according to applicable common sizing options



Page Margins

  * **Measurement Type** : determines the measurement used when assigning margin values, limited to Inches, Centimeters, or Points. 
  * **Margin Top/Right/Bottom/Left** : assigns a margin width, according to the measurement defined by the margin type.



#### **Revisions**

15th December 2022 - Initial Publication (v11.2.3)

Contact the [Parsec Applications Department](mailto:applications@parsec-corp.com) for any questions, comments, or concerns.
