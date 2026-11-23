# Changing Background Color Using CSS

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004655048-Changing-Background-Color-Using-CSS*
*Last updated: 2025-05-21T22:52:07Z*

---

Applies To | TrakSYS 10+

### **Summary**

This article describes how to leverage the built-in CSS Classes and TrakSYS color palette to enhance custom HTML, as well as enhancing existing Content Parts and even the Grid layout where color options are readily available. Some benefits of using CSS Classes over alternative approaches include helping with uniformity (i.e. ability to control the shade of green used across the entire site) and allowing the change of both the background and text colors with one configuration setting.

### **Examples**

#### **Example 1**

The following example shows how to change the default colors of a paragraph of text to a use white font color and light green background color.
    
    
    <p class="tscolor-green-light">The background color is Green - Light</p>
    

#### **Example 2**

This example shows how to change an existing Content Part's background color.

  * Add a `Paragraph` Content Part
  * Set the Text property to "Hello, my background color is light green"
  * Set the Advanced | CSS Class to "tscolor-green-light"
  * Save and/or Preview the results.



#### **See Also**

  * [List of Colors](https://portal.parsec-corp.com/hc/en-us/articles/115004389727-What-is-the-TrakSYS-10-CSS-Color-Palette-)
  * [How do I change text color using CSS](https://portal.parsec-corp.com/hc/en-us/articles/115004655208)


