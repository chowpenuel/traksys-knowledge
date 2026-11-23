# Using Measures and Conversions

*Source: https://portal.parsec-corp.com/hc/en-us/articles/1500008868021-Using-Measures-and-Conversions*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 11.2.0+

### **Summary**

In TrakSYS 11.2.0, Measures and Conversions were added. This feature provides a way to add different types of predefined measurements and the conversions between them. These Measures can then be applied to existing configuration (such as Tags, Products, Materials, and more).

Each conversion allows a single instance of addition or subtraction and one instance of multiplication or division. Additionally, each conversion is bidirectional. This means that once a conversion has been configured from one measure to another, it is possible to perform the conversion in the opposite direction.

This article explains how to configure and use Measures and Conversions.

### **Procedure**

The following steps show how to configure Measures and Conversions. **Note:** for Multi-Site installations, the configuration can only be found in the Root Site.

  1. Open the TrakSYS Web and navigate to **Configuration | Measures**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18698255067667)  
  

  2. Click the New button under the Groups section on the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18698278866323)  
  

  3. Specify a Name and Key, then click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18698314314387)  
  

  4. Click the newly created Measure Group on the first slice. Then, click the New button under the Measures section of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18698320982931)  
  

  5. Specify a Name, Key, and Abbreviation for the Measure. Then, click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18698394868115)  
  

  6. Repeat steps 4 and 5 to create additional Measures as needed. For the purpose of this example, Measures for Celsius and Kelvin were also added.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18698444052883)  
  

  7. Next, navigate to **Configuration | Measures | Conversions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18698438722963)  
  

  8. Click the New button under the Groups section of the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18698457108499)  
  

  9. Specify a Name and Key. Then, click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18698488450835)  
  

  10. Select the newly created Conversions Group and click the New button under the Conversions section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18698500568083)  
  

  11. Specify values for each of the options presented in the Conversion. The example below will convert Celsius to Fahrenheit. **Note** : Conversions can be used bidirectionally (forwards or backwards).  
  

       * The **From Measure** option specifies the starting Measure for the conversion. In the example below, the Celsius Measure has been selected.
       * The **To Measure** option specifies the resulting Measure once the conversion has occurred. In the example below, the Fahrenheit Measure has been selected.
       * The **Multiplier** option specifies the value that will be multiplied (or divided) to the From Measure value. Since the standard formula for this conversion is **(°C * 9/5) + 32** , the multiplier in this example is 1.8 (the decimal value for 9/5).
       * The **Add Factor** option specifies the value that will be added (or subtracted) for the Conversion. Because of the standard formula above, a value of 32 will be used.
  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18698570902291)  
  

  12. Click Save to apply the changes.
  13. Repeat steps 10 and 11 to add more Conversions as needed. Again, a Conversion only needs to be configured one way. In this example, an additional Conversion from Fahrenheit to Celsius is not needed.



**Using Measures and Conversions**

Conversions can be applied using the TrakSYS API with the `Uom` namespace. The namespace contains methods that can be use to perform the conversions. To perform a conversion in the direction they were configured, the `Uom.Convert()` method can be used. In the example below, the API is being used to convert a value from Celsius to Fahrenheit:
    
    
    // Provide the tConversion.ID value of the desired Conversion
    int conversionID = 5;
    //Provide the value to be converted
    double originalValue = 78;
    // Load the Conversion Object
    var conversion = this.Ets.Api.Data.DbConversion.Load.ByID(conversionID)  
                     .ThrowIfLoadFailed("ConversionID", conversionID);
    // Perform the conversion
    var convertedValue = this.Ets.Api.Uom.**Convert**(originalValue, conversion)  
                         .ThrowIfFailed();
    

For conversions going the opposite direction, the `Uom.ConvertReverse()` method can be used. In this example, the value is now being converted from Fahrenheit to Celsius:
    
    
    // Provide the tConversion.ID value of the desired Conversion
    int conversionID = 5;
    //Provide the value to be converted
    double originalValue = 78;
    // Load the Conversion Object
    var conversion = this.Ets.Api.Data.DbConversion.Load.ByID(conversionID)  
                     .ThrowIfLoadFailed("ConversionID", conversionID);
    // Perform the conversion
    var convertedValue = this.Ets.Api.Uom.**ConvertReverse**(originalValue, conversion)  
                         .ThrowIfFailed();
    
