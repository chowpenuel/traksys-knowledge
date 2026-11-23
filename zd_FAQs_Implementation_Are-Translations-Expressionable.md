# Are Translations Expressionable?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360034354373-Are-Translations-Expressionable*
*Last updated: 2025-05-13T22:27:24Z*

---

When using built-in Content Parts to display data, it is not possible to combine references to all Translations and TrakSYS Expressions all in the same field. Either a resx: translation expression or a TrakSYS expression can be used in a single field, but they cannot be combined. For example, the following **will not** work:

![](https://portal.parsec-corp.com/hc/article_attachments/18542648216467)

As an alternative, both the custom translation and the Values Dictionary value can be obtained with custom code and combined into a single value. This variable can then be inserted into the Values Dictionary and the new Values Dictionary Key can be referenced within the desired part. As an example, something similar to the following code can be used to accomplish this:
    
    
    var text = "resx:ResourceGroup.ResourceItem, db".Translate();
    var value = this.Ets.Values.GetAsObject("myValuesDictionaryKey", null);
    this.Ets.Values["TranslatedText"] = $"{text} {value}";
    

From here, the the new "TranslatedText" Values Dictionary Key can be referenced within the part to display the combined value of both the translation and the Values Dictionary value.

![](https://portal.parsec-corp.com/hc/article_attachments/18542679410323)

**See Also**

  * [Creating and Using Custom Translations](https://portal.parsec-corp.com/hc/en-us/articles/360007652173)


