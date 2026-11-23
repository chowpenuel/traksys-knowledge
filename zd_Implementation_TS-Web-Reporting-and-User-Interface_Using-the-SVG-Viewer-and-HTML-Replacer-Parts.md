# Using the SVG Viewer and HTML Replacer Parts

*Source: https://portal.parsec-corp.com/hc/en-us/articles/40816541752723-Using-the-SVG-Viewer-and-HTML-Replacer-Parts*
*Last updated: 2026-03-11T17:04:52Z*

---

Applies To | TrakSYS 13+

### Summary

Starting in TrakSYS 13, an SVG Viewer part is now available. The part exposes an editor property, which can be used to create, import, and modify SVGs that can be displayed.

An HTML Replacer part was also introduced and designed with the SVG Viewer in mind, allowing for manipulation of the SVG on either page load or at regular intervals in real-time.

This article will provide a high-level overview of the parts and includes a Page Definition with a self-contained example that can be imported to better understand the SVG Viewer and HTML Replacer parts. The Page Definition will be used as reference in second section.

### Importing an SVG

The SVG Viewer part allows for SVG creation from a blank slate or importing already existing SVGs. This article will be focusing on importing an SVG. If creating an SVG entirely in the editor, many of the properties exposed are similar to common image editors.

  1. Begin by placing the SVG Viewer part on a Visual Page.
  2. Select the SVG Editor property box to open the editor.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41044184363795)
  3. Select the SVG icon in the editor to open the raw SVG content.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41044184375955)
  4. Paste the contents of the desired SVG that will be imported into the part, then select "Apply Changes".  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49631816622355)
  5. The SVG content should now display in the preview window.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49631831556115)
  6. Select "Save and Close" in the editor, then preview the page:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/49631831557267)



The SVG image should now be displayed on the Page Definition via the SVG viewer part.

### Using the HTML Replacer with the SVG Viewer part

In this section, a high-level overview will be provided on how the HTML Replacer part can interact with the SVG Viewer Part, using the attached Page Definition with a pre-configured example as reference. 

The Selector and Attribute properties below specify CSS Selectors and HTML attributes. For more technical information on each HTML Replacer property, please refer to the [part Reference Documentation](https://docs.parsec-corp.com/tsweb/content-reference/content-part-reference/html-replacer).

![](https://portal.parsec-corp.com/hc/article_attachments/49639405899155)

The Values properties grid shown contains 6 rows: 3 targeting the `fill` attribute of individual SVG alarm bell elements, and 3 targeting the text content of package status label elements. Because the Attribute column is left blank for the `#pkg_txt` rows, the HTML Replacer part will update those elements' text directly rather than an attribute. The values assigned reference Values Dictionary items, meaning on page load, all six elements are updated at once during part initialization.

Two buttons are placed on the attached page to adjust the Values Dictionary item values for demonstration purposes, allowing the alarm bell colors and status labels to change interactively.

While Values Dictionary items are retrieved once on initialization, a similar configuration can be achieved using the Tags properties instead. Using Tags allows element values to update on a recurring interval rather than only at load time. The visual below shows the same SVG elements mapped using Tags, with an Interval Seconds value of 2, meaning each tag-bound element is updated every 2 seconds with the Tags' value.

![](https://portal.parsec-corp.com/hc/article_attachments/49639405900563)

When leveraging both parts together, SVGs can be configured to reflect live data for presenting dynamic visual information.
