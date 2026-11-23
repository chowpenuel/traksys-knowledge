# S95SystemType Values

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004511168-S95SystemType-Values*
*Last updated: 2025-05-21T22:50:40Z*

---

Applies To | TrakSYS 10+

### **Summary**

The following article is an overview of the different values and extension methods for the S95 System Type, which leverages the standards for identifying different types of production equipment. 

#### **ProductionLine**

In TrakSYS this is represented by a **Discrete System** with an integer value of **1**. You can also use the Extension Method `IsDiscrete` in your code to provide more readable logic:
    
    
    bool isDiscrete = sys.S95SystemType.IsDiscrete();
    

#### **ProcessCell**

In TrakSYS this is represented by a **Batch System** with an integer value of **2**. You can also use the Extension Method `IsBatching` in your code to provide more readable logic:
    
    
    bool isBatch = sys.S95SystemType.IsBatching();
    

#### **StorageZone**

In TrakSYS this is represented by a **Storage System** with an integer value of **4**. You can also use the Extension Method `IsStorage` in your code to provide more readable logic:
    
    
    bool isStorage = sys.S95SystemType.IsStorage();
    
