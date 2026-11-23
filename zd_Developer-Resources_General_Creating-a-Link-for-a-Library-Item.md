# Creating a Link for a Library Item

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004358707-Creating-a-Link-for-a-Library-Item*
*Last updated: 2025-05-21T22:50:13Z*

---

Applies To | TrakSYS 10+

### **Summary**

If you need to use custom images, PDFs, documents, CSS files, JavaScript files or any other file, you can create a TrakSYS Library Item. This will store the file inside the TrakSYS database and then allow any user access to that file for download or viewing through the TrakSYS portal.

You can add files in the Developer Section of the TrakSYS Web. For users familiar with previous versions of TrakSYS, this functionality is very similar to WEBTrak Web Resources.

### **Overview**

Once you have uploaded the file you will most likely want to link to and/or display the file/url. The default link provided is not very stable (`~/library/?libraryitemID=1`).

When setting Content Properties, the format for the url should be
    
    
    ~/library/{siteKey}/{groupKey}/{libraryName}
    

#### **Example**

The following example will show you how to upload an image to the TrakSYS Library Items and then display the image using the Image Part. The example assumes that the site key is `home`. (i.e. you should be able to navigate to `http://server/ts/pages/home/` successfully).

  * Create a new Library Group (navigate to the Developer section) and set the Key to "Images". (The name is user-defined, but is recommended to be Images).
  * Select the Group and create a new Item. Upload a jpg file, specify the name as `test.jpg`. (Note if you want to upload a different image type, you can do so, but have the name match the file extension of the uploaded file).
  * Save the Library Item.
  * Create a Visual Content Page and add a `Image` Part.
  * Set the Image URL to:


    
    
    ~/library/home/images/test.jpg

  * Save and/or Preview the results.
  * You should see the uploaded image inside of the web page.


