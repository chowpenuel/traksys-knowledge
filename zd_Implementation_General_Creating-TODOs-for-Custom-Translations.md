# Creating TODOs for Custom Translations

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360013027794-Creating-TODOs-for-Custom-Translations*
*Last updated: 2025-05-21T22:09:23Z*

---

Applies To | TrakSYS 10+

### **Summary**

TODOs provide a special syntax that can be used as placeholders to create future Resource Strings. This allows words or phrases to be inserted into Content Parts, Visual Pages, and custom scripting without having to first create the custom translations.

When the time comes to create the custom translations, a full list of all TODOs will be displayed in the TrakSYS Web under **Configuration | Translations | TODOs**. Each TODO will give the option to either navigate to the location of the TODO or convert it into a Resource Item.

This article explains how to create TODOs and convert them into Resource Items. Please note that TODOs only work with custom translations and not with TrakSYS language packs. For an explanation of how to create and use Custom Translations, see **[here](https://portal.parsec-corp.com/hc/en-us/articles/360007652173-Creating-and-Using-Custom-Translations).**

### **Creating a TODO in a Content Part**

TODOs can be created in Content Parts that accept expressions in the Text property. For example: the Div, Header, and Paragraph Parts. When creating a TODO, the following syntax can be used:
    
    
    TODO: ValueHere

As an example, if a user would like to create a TODO for the word "Translation" within the Text field of a Header Part, it would look similar to the screenshot shown below.

![](https://portal.parsec-corp.com/hc/article_attachments/18550620764691)

When the changes are saved and the page is previewed, only the word "Translation" is actually displayed.

![](https://portal.parsec-corp.com/hc/article_attachments/18550615298707)

Now that the TODO has been created, navigating to **Configuration | Translations | TODOs** will display it as in the screenshot below. Each entry displays the name of the Page Definition (Entity) that contains the TODO, along with the actual text.

![](https://portal.parsec-corp.com/hc/article_attachments/18550692023699)

**Creating a TODO in Script**

TODOs can also be created in script within Page Definitions and Script Classes. The syntax is similar to the **resx:** expression syntax used to reference custom translations:
    
    
    TODO:ResourceGroupKey.ResourceItemKey, AssemblyKey

The **ResourceGroupKey** and **ResourceItemKey** determines which Resource Group and Resource Item to look up when referencing the translation. The **AssemblyKey** suffix determines where to look up the Resource. Possible values include Core, Ts.Core, and Db. These concepts are further explained in the **[custom translations article](https://portal.parsec-corp.com/hc/en-us/articles/360007652173-Creating-and-Using-Custom-Translations)** mentioned above.

Continuing the example from the previous section, the following code can be used within the Script tab of a Visual Page Definition to create a TODO for the word "Translated":
    
    
    string text = "TODO:ReportTrans.Translated, Db";
    

Once the changes are saved, another entry should appear within the TODOs page under the Configuration section.

![](https://portal.parsec-corp.com/hc/article_attachments/18550732117395)

**Creating a Resource Item from a TODO**

Now that the TODOs have been created, they can be converted into Resource Items. Please note that this example assumes that Resource Groups have been configured. These can be found under **Configuration | Translations**. To create a Resource Item, click the Create button on an existing TODO entry.

![](https://portal.parsec-corp.com/hc/article_attachments/18550734648595)

On the resulting page, select a configured Resource Group and enter a Key. The Default Value can be left as is. Once the changes have been made, click the Use button. Repeat this process for each TODO.

![](https://portal.parsec-corp.com/hc/article_attachments/18550843397395)

The Resource Items can then be viewed by navigating to **Configuration | Translations** and selecting the Resource Group in which they were created. In this example, both of the available TODOs were converted into Resource Items.

![](https://portal.parsec-corp.com/hc/article_attachments/18550910651155)

Additionally, the text used to create the TODOs is automatically updated to use the **resx:** syntax to reference the new Resource Item. For this example, the updated text for the Header part and in the code-behind of the Visual Page Definition is shown below:

**In the Header part** :

![](https://portal.parsec-corp.com/hc/article_attachments/18550943133843)

**In the code-behind** :

![](https://portal.parsec-corp.com/hc/article_attachments/18550988962835)

**See Also**

  * [Creating and Using Custom Translations](https://portal.parsec-corp.com/hc/en-us/articles/360007652173-Creating-and-Using-Custom-Translations)


