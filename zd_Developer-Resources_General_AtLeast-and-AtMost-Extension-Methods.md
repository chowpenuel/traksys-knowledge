# AtLeast and AtMost Extension Methods

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004576908-AtLeast-and-AtMost-Extension-Methods*
*Last updated: 2025-05-21T22:50:32Z*

---

Applies To | TrakSYS 10+

### **Summary**

When input is received from the user or other external sources, that value will often need to be within a certain range. In these scenarios, it is ideal to proceed without displaying errors while validating that the input is within the approved range, which can be done with simple code. However, TrakSYS 10 includes two new helper methods, `AtLeast` and `AtMost,` that can turn a few lines of `if / else` into a single line that is more readable.

### **Example**

The following are some common scenarios where these helper methods can be used:
    
    
    // makes sure the integer userInput is never below 1 or never more than 12.
    int bsWidth = userInput.AtLeast(1).AtMost(12);
    
    // make sure input is at least 3.
    int pollSeconds = otherUserInput.AtLeast(3);
    
    // make sure input isn't greater than 255.
    int plcValue = userInput2.AtMost(255);
    

### **Advanced**

These methods leverage a C# language feature called Extension Methods. All of TrakSYS 10's new Extension Methods are declared in the same namespace, regardless of the Assembly in which they are located. By including a single using directive for this namespace, the user can take advantage of all appropriate built-in Extension Methods no matter what application is being used.
    
    
    using ETS.Core.Extensions;
    

The code for these functions is very simple and the actual source code for `AtLeast` is shown below. By leveraging TrakSYS 10 Global Scripts the user can create custom Extension Methods specific to their business domain and/or how their organization writes code. TrakSYS has versions of `AtLeast`/`AtMost` for both integers and doubles. If you need support for more Data Types please [let us know](https://portal.parsec-corp.com/hc/en-us/requests/new).
    
    
    public static int AtLeast(this int val, int minValue)
    {
      if (val < minValue) return minValue;
      return val;
    }
    

#### See Also

  * [Implement and Call a Custom Extension Method : docs.microsoft.com](https://docs.microsoft.com/en-us/dotnet/articles/csharp/programming-guide/classes-and-structs/how-to-implement-and-call-a-custom-extension-method)


