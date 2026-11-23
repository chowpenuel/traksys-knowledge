# Programmatically Changing the Value of a Single Virtual Tag

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004248713-Programmatically-Changing-the-Value-of-a-Single-Virtual-Tag*
*Last updated: 2025-05-21T23:10:23Z*

---

Applies To | TrakSYS 10+

Using C#, the value of a single Virtual Tag can be changed using either the UpdateVirtualTagByName() or UpdateVirtualTagByID() methods.

For example, if a Discrete Float Tag was created and a user wanted to programmatically change the value referencing the name of the tag, the following can be used:
    
    
    this.Ets.Api.Tags.UpdateVirtualTagByName("Tag Name", 2.1);
    

This will change the tag value to 2.1 when the code is executed.

Similarly, the tag value can be changed referencing the Tag ID. For example, if the tag has an ID of 219, the following can be used:
    
    
    this.Ets.Api.Tags.UpdateVirtualTagByID(219, 2.1);
    

This will also change the tag value to 2.1 when the code is executed.
