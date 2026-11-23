# Using The Tab Strip Content Part

*Source: https://portal.parsec-corp.com/hc/en-us/articles/4409084953491-Using-The-Tab-Strip-Content-Part*
*Last updated: 2025-05-21T22:43:06Z*

---

Applies To | TrakSYS 10+

### Summary

The Tab Strip Part can be used to display and hide web elements depending on the selected tab. The part relies on Tab Selectors, which use CSS classes to show or hide other parts. This is useful for limiting options and user input based on specific tab selections.

This article provides an example of how to use the Tab Strip Part and how it can be used with other parts on the page.

### Example

  1. On a new Visual Page Definition, go into the page properties and click the Grid tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18622648008083)  
  

  2. Select the existing Column and click the Add Column Before link  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18622640890899)  
  

  3. Set the first column to a width of 2 and the second column to a width of 8. Then click Save.
  4. Next, in the Grid editor, select the column with a Width of 8 and click Add Column After.
  5. Make sure that the columns have widths of 2, 8, 2 respectively. Note that this follows the User Interface Design Best Practices as mentioned [**here**](https://portal.parsec-corp.com/hc/en-us/articles/360009094974-User-Interface-Design). The final result should look similar to the image below:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18622732001811)  
  

  6. Next, navigate to the Parts tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18622786818835)  
  

  7. Add the following parts in order.  
  

       * A Tab Strip Part (`ETS.Forms.TsTabStrip`) with an ID of `TabStripPart` to the first column.
       * A Forms Text Box Part (`ETS.Forms.TsInputText`) with an ID of `TextBox` to the second column.
       * A Header Part (`ETS.TsHeader`) with an ID of `Header` to the second column.
       * A Buttons Part (`ETS.TsButtons`) with an ID of `Buttons` to the second column.
  
The final result should look similar to the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18622914439443)  
  

  8. Go into the properties of the Tab Strip Part.  
  
In the General tab, there will be three columns of interest: Caption, Anchor Key, and TabSelector.  
  

       * The **Caption** is the text that will display for the user on a particular tab.
       * The **Anchor Key** is the anchor name of the tab. The same name may be used for both the Caption and the Anchor Key.
       * The **Tab Selector** is a CSS Selector that is used to look for parts with the same CSS class. This is how the Tab Strip will choose which web parts will be displayed or hidden.
  
For this example, 3 different tabs will be created:  
  

       * For the first row, enter "Text Box" for Caption, "TextBoxKey" for Anchor Key, and ".tab-text-box" for the Tab Selector.
       * For the second row, enter "Button" for Caption, "ButtonKey" for Anchor Key, and ".tab-button" for the Tab Selector.
       * For the third row, enter "Header" for Caption, "HeaderKey" for Anchor Key, and leave the Tab Selector blank.
  
![](https://portal.parsec-corp.com/hc/article_attachments/18623016483859)  
  

  9. Click the Save button to save the changes. Then, go into the properties of the Text Box Part.
  10. Navigate to the Advanced tab and enter "tab-text-box" in the CSS Class field. Then, click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18623359221395)  
  

  11. Next, go into the properties of the Buttons Part and navigate to the Advanced tab.
  12. In the CSS Class field, enter "tab-button" and click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18623367082003)  
  

  13. Go into the Header Part properties and enter a value for the Text field under the General tab. For this example, "Header Text" is being used. Then, click the Save button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18623410318611)  
  

  14. Click the Preview button to view the page.



As each tab is clicked, the various elements will be shown or hidden based on the parts that have the matching Tab Selector. Parts that do not match the Tab Selector of the current tab will automatically be hidden. The Header Part will appear in all three tabs by default as no Tab Selector was defined for this part.

#### **Selecting different Layout Modes**

Depending on the implementation requirements, it may be desirable to display the Tab Strip navigation elements horizontally instead of vertically. The Tag Strip Part allows the tabs to be displayed horizontally with left, right, and center justification. This is possible by selecting the appropriate option on the Layout Mode setting. This setting can be found within the Part properties under the Appearance section of the General tab.

![](https://portal.parsec-corp.com/hc/article_attachments/18623524267795)

Continuing from the example from the previous section, the Tab Strip Part was moved from the first column to the second column for this demonstration. The final result is shown below:

![](https://portal.parsec-corp.com/hc/article_attachments/18623593489427)

The Layout Mode setting was then changed to display the tabs horizontally. As the names suggest, the Horizontal Left option will display the tabs with left justification. the Horizontal Right option will display the tabs with right justification, and the Horizontal Justified option will center the tabs. Note that the tabs will resize to fill the entire width of the column (which is 8) when the Horizontal Justified option is selected. Examples of all three options are shown below:

**Horizontal Left**

![](https://portal.parsec-corp.com/hc/article_attachments/18623644564243)

**Horizontal Right**

![](https://portal.parsec-corp.com/hc/article_attachments/18623648338835)

**Horizontal Justified**

![](https://portal.parsec-corp.com/hc/article_attachments/18623696915987)

#### **Selecting Default Tabs On Navigation**

When navigating to a page with a Tab Strip Part, the contents of the first tab will automatically be displayed. However, it is possible to pre-select specific tabs using the pound sign (`#`) and referencing the desired Anchor Key. This information should be included in the URL when redirecting the user.

For example, when a user navigates to the example page created above, the contents for the Text Box tab will be displayed.

![](https://portal.parsec-corp.com/hc/article_attachments/18623777011091)

![](https://portal.parsec-corp.com/hc/article_attachments/18623779896723)

Since this example included three Anchor Keys, #ButtonKey can be appended to the end of the URL. This will automatically display the contents of the Button tab on page load.

![](https://portal.parsec-corp.com/hc/article_attachments/18623834825619)

![](https://portal.parsec-corp.com/hc/article_attachments/18623839127955)
