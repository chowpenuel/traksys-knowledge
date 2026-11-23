# OPC Access Name Read on Connect Types

*Source: https://portal.parsec-corp.com/hc/en-us/articles/1500003776902-OPC-Access-Name-Read-on-Connect-Types*
*Last updated: 2025-05-21T22:45:50Z*

---

Applies To | TrakSYS 11+

### Summary

When Read on Connect is enabled for an Access Name, Logic Service forces a synchronous read from all the Tags under that Access Name, either upon first connection on startup or on reconnection. Read On Connect is intended for scenarios where the OPC server is not behaving as it should (i.e. a successful connection to the OPC Server is made but the Tags subscription does not return the current values).

OPC Servers that comply with the OPC Specification typically return current Tag values on connection even if the Read On Connect options described below are not enabled. In general, it is best practice to use the default Read On Connect option of **No**.

### Read on Connect Options

There are three options available for Read on Connect: No, Sync, and Sync on Reconnect.

![](https://portal.parsec-corp.com/hc/article_attachments/18694827505683)

#### **No**

Logic Service does not force a synchronous Tag read when the connection is first made during Logic Service Startup. **This is the recommended option**.

#### **Sync on Reconnect**

Logic Service forces a read from all the Tags under the Access Name whenever a reconnection to the Access Name takes place. A forced read will not occur on Logic Service Startup and should not negatively affect Logic Service scan times. This option should only be in scenarios where the OPC server is not behaving as it should (i.e. a successful reconnection to the OPC Server is made but the Tags subscription does not return the current values).

#### **Sync**

Logic Service forces a read from all the Tags under the Access Name when the connection is first made during Logic Service Startup. This option should only be used in scenarios where the OPC server is not behaving as it should (i.e. a successful connection to the OPC Server is made but the Tags subscription does not return the current values).

**Note:** Depending on the number of configured OPC Tags this setting can cause significant delays in Logic Service Startup times.

### Read on Connect Type

When the Sync or Sync on Reconnect options are selected, the Type option determines the kind of synchronous read that occurs. The two options are Cache Read and Device Read.

![](https://portal.parsec-corp.com/hc/article_attachments/18694857646867)

#### **Cache Read**

Reads values from the OPC server's memory (the last known value that has been read from the device). This is the default option.

![](https://portal.parsec-corp.com/hc/article_attachments/18694876294803)

#### **Device Read**

Forces the OPC server to query the physical device for the current value (this option can be slower).

![](https://portal.parsec-corp.com/hc/article_attachments/18694891531923)
