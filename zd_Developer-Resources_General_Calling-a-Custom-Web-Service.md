# Calling a Custom Web Service

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004224848-Calling-a-Custom-Web-Service*
*Last updated: 2025-05-21T22:50:26Z*

---

Applies To | TrakSYS 10+

### **Summary**

The following article describes how to call a web service created and deployed through TrakSYS by leveraging jQuery and Microsoft's Web API 2.0 technologies.

###  **Sample Web Service Call**

This example calls the web service made in the [Creating a Custom Web Service](https://portal.parsec-corp.com/hc/en-us/articles/115003923447) article. If not already done, it is recommended to follow the steps in that article first. For the purpose of this example, the site key is "home".

  1. On a Visual Page Definition, add a **Tile (Dynamic Width)** content part (**TsTileDynamic**).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18881147225491)  
  

  2. In the **Click** section of the **General** tab of the Tile's Properties, set the **On Client Click** property to:  
  
`return exampleMathAdd();`  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18881481978259)  
  

  3. Click **Save**.
  4. Click **JS** to load the page's JavaScript editor.
  5. In the editor, add the following code:  
  

         
         function exampleMathAdd() {
           var url = ets.rootPath + '/api/home/custom/math/addnumbers?a=10&b=32';
           var p = $.get(url).done(function(data){ 
             ets.ui.alert('Adding the numbers 10 + 32 is ' + data);    
           });
         
           p.fail(function() {
             ets.ui.alert('An error occured while retrieving the data', 'ERROR');
           });
           return false; // prevents button from posting back.  
          }

  6. Click **Preview** to load the page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18881497125011)  
  

  7. Click the blue tile to call the web service.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18881521344659)  
  




In this example, when the tile is clicked, the `jQuery.get()` function will make an HTTP GET request to the server. The passed-in parameter (url) is a string containing the URL where the request is sent. The way this string is constructed enables the Web API framework to correctly route the request to the method that adds the two numbers.

**Additional Resources**

  * [Creating a Custom Web Service](https://portal.parsec-corp.com/hc/en-us/articles/115003923447)
  * [jQuery.get() : jquery.com](http://api.jquery.com/jQuery.get/)


