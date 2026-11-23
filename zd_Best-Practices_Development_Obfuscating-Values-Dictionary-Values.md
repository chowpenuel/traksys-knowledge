# Obfuscating Values Dictionary Values

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6824599384211-Obfuscating-Values-Dictionary-Values*
*Last updated: 2025-08-07T21:52:32Z*

---

Applies To | TrakSYS 10+

In some scenarios, it may be required to enter or load sensitive information on a page. Along with being displayed on the page, the value can also be shown within the Values Dictionary when trace is enabled. To help obfuscate the value for security reasons, `.Secure` can be added to the end of the Values Dictionary Key.

For example, within the script of a Visual Page Definition, the following line of code was added:
    
    
    this.Ets.Values["Password"] = "YourPasswordHere";

When the page is previewed and trace is enabled, the value appears as plaintext within the trace:  
  


![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/6828150267155)  
  


However, the value can be obfuscated by adding `.Secure` to the end of the Values Dictionary Key. Therefore, the code would be changed to:  
  

    
    
    this.Ets.Values["Password.Secure"] = "YourPasswordHere";

Now when the page is previewed with trace enabled once again, the value is now obfuscated in trace:  
  


![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/6828292007571)
