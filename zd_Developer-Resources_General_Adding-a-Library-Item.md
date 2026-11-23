# Adding a Library Item

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360009367873-Adding-a-Library-Item*
*Last updated: 2025-05-21T22:50:06Z*

---

Applies To | TrakSYS 10+

### **Summary**

Starting in TrakSYS 10, Library Items were added as a way to store files within the TrakSYS database. Examples of the types of files that can be stored include JavaScript files, CSS files, company logos, images in different formats (e.g. .png, .jpeg, .img, etc.), and much more. These files can then be referenced and used within other areas of the installation by [creating links](https://portal.parsec-corp.com/hc/en-us/articles/115004358707) to the Library Items.

Another benefit of Library Items is that the stored files are also transferred when using the [Database Transfer](https://portal.parsec-corp.com/hc/en-us/articles/115004492907-TrakSYS-10-Database-Transfer-Guide) process. This means that the files can be created or updated on the development environment and transferred to production. This can be useful in situations where custom JavaScript or CSS files are stored as Library Items, updates are made to the files on development, and the updated files need to be pushed to production.

Please note that since Library Items are overwritten during the Database Transfer process, attachments that are not meant be overwritten should not be stored as Library Items. In these cases, the files should instead be stored as Blob Items. This article describes the standard procedure for adding Library Items within the TrakSYS Web.

### **Procedure**

  1. Open the TrakSYS Web and navigate to **Developer | Library**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18854918716051)  
  

  2. Within the first slice, click the New button under the Groups section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18854907827603)  
  

  3. On the resulting page, enter a Name and Key for the Library Item Group. For the purposes of this example, the word "images" was used for both fields.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18854928680851)  
  

  4. Click the Save button to apply the changes.
  5. Click the newly created Library Item Group and click the New button under the Items section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18854939271187)  
  

  6. On the resulting page, select the desired file using the blue file picker button under the File field. Then, enter a Name for the Library Item. When creating a name, it is recommended to include the file extension at the end.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18855072386707)  
  

  7. Click the Save button to apply the changes.
  8. The new Library Item should now appear under the Items section of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18855444638355)



Repeat steps 5 through 7 to add additional Library Items as needed. Once the Items have been added, they can now be referenced in other areas of the installation.

#### **See Also**

  * [Creating a Link for a Library Item](https://portal.parsec-corp.com/hc/en-us/articles/115004358707)
  * [TrakSYS Database Transfer Guide](https://portal.parsec-corp.com/hc/en-us/articles/115004492907)


