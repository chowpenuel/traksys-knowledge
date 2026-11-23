# Implementing Custom Translations

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360007652173-Implementing-Custom-Translations*
*Last updated: 2025-05-21T22:09:29Z*

---

Applies To | TrakSYS 10+

### **Summary**

Custom translations can be added within the TrakSYS Web to translate certain words or phrases based on a user's Locale. These translations can then be referenced programmatically though the code behind of a Page Definition or directly within the properties of a Part and displayed to the user. These translations are created as Resource Strings, which can either be compiled into files or added directly into the TrakSYS database. These Resource Strings can be referenced and used on all Page and Part types.

Before creating translations, Locales must be created for each language that a word or phrase will be translated. Each Locale is represented by the standard Microsoft culture abbreviations (e.g. Spanish is abbreviated as es-ES).

Please note that only words or phrases specified in the Translations section of the TrakSYS Web will be translated for custom Parts and Pages. The translations specified in this section will not translate built-in pages, parts, and navigation elements. To translate built-in content for the TrakSYS Web, **[TrakSYS language packs](https://portal.parsec-corp.com/hc/en-us/sections/360009025714-Translations)** will have to be **[installed](https://portal.parsec-corp.com/hc/en-us/articles/115005265807-Language-Translation-File-Installation-Instructions-TrakSYS-10-)**. This article explains the standard procedure for creating custom translations in the TrakSYS Web.

### **Procedure**

#### **Prerequisite: Creating Locales**

  1. Open the TrakSYS Web and navigate to **Configuration | Translations | Locales**.   
**Note** : If a Multi-Site installation is being used, the Translations Hub will only appear on the Root Site.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18552670991891)  
  

  2. Click the New button under the Locales section on the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18552687953939)  
  

  3. In the Culture Name field of the resulting page, enter the Microsoft culture abbreviation for the desired language. In the example below, the culture code for Spanish (es-ES) was entered.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18552708566547)  
  

  4. Click Save to apply the changes
  5. The newly created Locale should now appear under the Locales section in the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18552753494675)  
  

  6. Repeat steps 2 through 4 to create additional Locales as needed. For this example, an additional Locale for French (fr-FR) has been created.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18552741872787)



#### **Creating Resource Groups, Resource Items, and Translations**

Now that the Locales have been created, the Resource Groups/Items and the translations for each Item can now be created. Please note that a separate translation will have to be created for each Locale for every word or phrase that will be translated. This way, when a user with a matching Locale accesses the TrakSYS Web, they will see the translated word or phrase when viewing Page Definitions.

  1. In the TrakSYS Web, navigate to **Configuration | Translations**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18552775140499)  
  

  2. Click the New button under the Resource Groups section in the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18552801663507)  
  

  3. On the resulting page, type a Name and Key for the Resource Group.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18552821864979)  
  

  4. Click Save to apply the changes.
  5. The newly created Group should now appear under the Resource Groups section on the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18552811238803)  
  

  6. Select the newly created Resource Group. Then, click the New button under the Items section of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18552874811667)  
  

  7. On the resulting page, enter the word or phrase to be translated in the Default Value field. Also enter a Key for the Resource Item. In general, it is recommended to enter a Key that is similar to or well represents the word or phrase, as this will be used in the translation process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18552903538451)  
  

  8. Click Save to apply the changes.
  9. The newly created Resource Item should now appear under the Items section of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18552905830035)  
  

  10. Select the Resource Item and click the Translations button under the Related field in the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18552952275219)  
  

  11. Click the New button under the Translations section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18552927894547)  
  

  12. On the resulting page, select a configured Locale, then type the translated value in the Value field. In the example below, the Spanish translation for the word "Translation" was entered.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18553137795475)  
  

  13. Click Save to apply the changes.
  14. The newly created translation should now appear under the Translations section of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18553129083155)  
  

  15. Repeat steps 11 through 13 to create additional translations for other locales as needed. In this example, an additional translation for the French locale was created.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18553161913875)



#### **Using Custom Translations with Parts and Pages**

The translations can now be referenced directly in Parts and within the code-behind of Page Definitions. The translations can be referenced using a special resx syntax that includes the Resource Group Key and Resource Item Key. When referencing translations with the resx syntax, the following can be used:
    
    
    resx:ResourceGroupKey.ResourceItemKey, AssemblyKey
    

  * The prefix **resx:** denotes that the string is a translatable Resource String Item. 
  * The **ResourceGroupKey** and **ResourceItemKey** determines which Resource Group and Resource Item to look up when referencing the translation.
  * The **AssemblyKey** suffix determines where to look up the Resource. Possible values include Core, Ts.Core, and Db. Since custom translations are stored in the TrakSYS database, the Db Assembly Key will be used.



More technical information about custom translations and the resx syntax can be found in the [**TrakSYS** Reference Documentation](https://docs.parsec-corp.com/).

The examples below show how to use this syntax to reference the custom translations.

#### **Example #1 : Referencing Custom Translations in Code**

Translations can be referenced from the code-behind of Visual Page Definitions. The code example shown below uses the resx syntax to reference the custom translations configured in previous seconds of this article. It then sends this value to a Values Dictionary Key, which then can be referenced by other parts on the page or in other locations within the code of the Page Definition.
    
    
    protected override bool ContentPage_Init()
    {
      var text = "resx:ReportTrans.Translation, Db";
      var translatedText = text.Translate();
      this.Ets.Values["Translation"] = translatedText;
      return true;
    }
    

When the page is previewed and Trace is enabled on the page, the value should appear with the appropriate Values Dictionary Key. If a user logs in with a Locale that has no configured value for the word or phrase, then the default value will be displayed to the user. In the example below, no value has been set for the English (en-US) Locale so the default value specified in the Resource Item is automatically displayed.

![](https://portal.parsec-corp.com/hc/article_attachments/360010023053)

However, if a user logs in with a Locale that has a configured value for the translation, then the corresponding translated value should appear instead. Since a Locale has been configured for Spanish (es-ES) and French (fr-FR) in a previous section of this article, the translated value should appear when a user with either of these locales logs into the TrakSYS Web and views the page.

**Spanish (es-ES)**

![](https://portal.parsec-corp.com/hc/article_attachments/360009975454)

**French (fr-FR)**

![](https://portal.parsec-corp.com/hc/article_attachments/360010023613)

#### **Example #2 : Referencing Custom Translations within Parts**

Similar to the example shown above, the resx expression can be used within Parts to translate words or phrases based on the user's locale. Depending on the Part that is being used, the expression can be typed in the Text or Display Name fields within the Part properties. For this example, a Header Part has been placed on a Visual Page Definition.

![](https://portal.parsec-corp.com/hc/article_attachments/18553243608595)

In the properties of the Header Part, the same resx expression used in the first example can be inserted directly into the Text field of the Part.

![](https://portal.parsec-corp.com/hc/article_attachments/18553249211155)

After saving the changes and previewing the page, the word or phrase should change based on the user's locale. Similar to the first example, if a user logs in with a locale that has no configured value for the word or phrase, then the default value specified in the Resource Item should be displayed.

![](https://portal.parsec-corp.com/hc/article_attachments/360009978114)

However, if a user has a locale that contains a translation for the word or phrase, then the corresponding translation should appear on the Part. For this example, the following translated values are displayed when a user with a Spanish (es-ES) or French (fr-FR) locale accesses the TrakSYS Web and views the page:

**Spanish (es-ES)**

![](https://portal.parsec-corp.com/hc/article_attachments/18553356967315)

**French (fr-FR)**

![](https://portal.parsec-corp.com/hc/article_attachments/18553359201811)

**See Also**

  * [Creating TODOs for Custom Translations](https://portal.parsec-corp.com/hc/en-us/articles/360013027794-Creating-TODOs-for-Custom-Translations)


