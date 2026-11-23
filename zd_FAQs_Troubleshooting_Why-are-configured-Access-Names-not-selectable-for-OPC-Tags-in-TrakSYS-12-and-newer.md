# Why are configured Access Names not selectable for OPC Tags in TrakSYS 12 and newer?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/16379021167507-Why-are-configured-Access-Names-not-selectable-for-OPC-Tags-in-TrakSYS-12-and-newer*
*Last updated: 2025-05-21T21:52:50Z*

---

Applies To | TrakSYS 12+

Configured Access Names may not be selectable when configuring OPC DA Tags or OPC UA Tags if a Logic Service Instance is not assigned to the Access Name Group. If an Instance is not assigned, then the associated Access Names will not be selectable when creating or modifying OPC Tags. This is true even if the Access Names exist and have been correctly configured. After a Logic Service Instance has been assigned to the Access Name Group, the Access Names should be selectable when creating OPC Tags.

#### **See Also**

  * [Logic Service Instance Assignment for Access Name Groups and Tag Groups in TrakSYS 12](https://portal.parsec-corp.com/hc/en-us/articles/15877066249747-TrakSYS-12-Logic-Service-Instance-Assignment-for-Access-Name-Groups-and-Tag-Groups-in-TrakSYS-12)


