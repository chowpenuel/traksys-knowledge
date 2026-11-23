# Why are there "The given key "{TagName}" was not present in the dictionary[ISourceCodeTag]" messages on Logic Service start?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/20812957262227-Why-are-there-The-given-key-TagName-was-not-present-in-the-dictionary-ISourceCodeTag-messages-on-Logic-Service-start*
*Last updated: 2025-05-28T17:52:46Z*

---

Applies To | TrakSYS 10+

In some cases, it may be possible to see "The given key "{TagName}" was not present in the dictionary[ISourceCodeTag]" messages in the TrakSYS Installation Manager and in the TrakSYS log file when first starting the Logic Service. These messages typically appear when code within a Script Tag references a Tag, but that Tag is not listed as a Prerequisite Tag. 

One possible cause for this behavior is having the Auto Generate Prerequisites option unchecked. This setting can be accessed by going into the TrakSYS Web and navigating to **Configuration | Tags**. Once the Script Tag properties are accessed, the option will be under the General tab (as shown below).

![](https://portal.parsec-corp.com/hc/article_attachments/20816432873491)

If this option is unchecked, check it, save the changes, and restart the Logic Service. This will automatically generate any Tag Prerequisites based on the references in custom code. Repeat this process for all tags that have this option unchecked. If the installation has a large number of Tags, the following query can quickly generate a list of Script Tags with the configuration for this option.
    
    
    SELECT 
      tTag.ID 
      , tTag.Name 
      , tTagScript.AutoGeneratePrerequisites
    FROM            
      tTag 
      INNER JOIN tTagScript ON tTag.ID = tTagScript.TagID
    WHERE 
      tTag.Type = 12
    

A value of 1 in the `AutoGeneratePrerequisites` field means the option is enabled (e.g., the recommended setting), while a value of 0 means it's disabled.

Another common cause for this message is incorrectly using the `Tags[""]` dictionary in custom C# code of a Script Tag or Script Class. When using the dictionary, the literal Tag name **must** be used. For example, the following line of code shows the correct usage:
    
    
    string jobTag = Tags["LINE1.JOB"].ValueString;
    

Variables should not be used in its place. This interferes with the Tag Prerequisite generation and can cause Tags to be improperly referenced in code. The following should **NOT** be used with the Tags dictionary:
    
    
    string tagName = "LINE1.JOB"; 
    string jobTag = Tags[tagName].ValueString;
    

Correcting all instances of this behavior should help the Tag Prerequisite generation and should prevent the error messages from appearing on Logic Service start. **Note** : if any code is modified in Script Tags, the Logic Service must be restarted to apply these changes.
