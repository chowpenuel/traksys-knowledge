# Using Custom Translations in a View Fragment Part

*Source: https://portal.parsec-corp.com/hc/en-us/articles/12803996407059-Using-Custom-Translations-in-a-View-Fragment-Part*
*Last updated: 2025-08-07T21:52:32Z*

---

Applies To | TrakSYS 10+

In the TrakSYS Web, [Custom Translations](https://portal.parsec-corp.com/hc/en-us/articles/360007652173-Implementing-Custom-Translations) can be used to provide translations for custom content and pages. For all built-in pages and content, the official [TrakSYS Language Packs](https://portal.parsec-corp.com/hc/en-us/articles/1500007183742-TrakSYS-11-2-Translations) can be used. When using View Fragment Parts on a page, it may be desirable to provide dynamic translations within the HTML. Similar to referencing Custom Translations within C# code, the `resx:` syntax can also be used to display translations in HTML. Instructions and examples for using the `resx:` syntax can be found within the "Using Custom Translations with Parts and Pages" section of the first article linked above. For displaying Custom Translations within the HTML of a View Fragment part, the following syntax can be used:
    
    
    <div><%: "resx:ResourceGroupKey.ResourceItemKey, AssemblyKey".Translate() %></div>

As an example, a Custom Translation has been created in Spanish for the word "Page." In this case, the Resource Group Key is "**esRes** " and the Resource Item Key is "**Page**." Therefore, the following has been placed within the HTML of a View Fragment Part:

![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/14429662411667)

When the page is viewed with a different language, the word "Page" is displayed.

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/14429642719891)

However, when a user with the es-ES locale views the same page, the Spanish translation is rendered as expected:

![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/14429659055123)
