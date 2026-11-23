# To What Windows Folders Does the TrakSYS Web Need Full-Control Access?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115001169674-To-What-Windows-Folders-Does-the-TrakSYS-Web-Need-Full-Control-Access*
*Last updated: 2025-05-21T21:59:37Z*

---

Applies To | TrakSYS 10+

Because of the way TrakSYS does ASP.NET code, web resources, web scripts, and image files, it needs the ability to write to file locations in the **TS** folder(s). The TrakSYS Web needs Full Control access to these locations. During installation to the default location, access to **Everyone** is typically enabled. These permissions will need to be set if the TS folder is moved or TrakSYS is installed to a non-default location.

The following is a list of folders for the TrakSYS Web that must have Full Control access:

#### **TrakSYS 12+**

…\Program Files\Parsec\TrakSYS\ts\Code  
…\Program Files\Parsec\TrakSYS\ts\bin  
…\Program Files\Parsec\TrakSYS\ts\Content\ChartImages

…\Program Files\Parsec\TrakSYS\ts\Content\Resources

#### **TrakSYS 11.2.5 and older**

…\Program Files (x86)\Parsec\TrakSYS\ts\Code  
…\Program Files (x86)\Parsec\TrakSYS\ts\bin  
…\Program Files (x86)\Parsec\TrakSYS\ts\Content\ChartImages

…\Program Files (x86)\Parsec\TrakSYS\ts\Content\Resources

If the Legacy WEBTrak feature is being used, then the following folders must also have Full Control access. **Note** : Legacy WEBTrak is no longer available starting with TrakSYS 12.

#### **TrakSYS 11.2.5 and older (Legacy WEBTrak)**

...\Program Files (x86)\Parsec\TrakSYS\WEBTrak\bin

...\Program Files (x86)\Parsec\TrakSYS\WEBTrak\Resources

...\Program Files (x86)\Parsec\TrakSYS\WEBTrak\dashboards\Chart Images

...\Program Files (x86)\Parsec\TrakSYS\WEBTrak\dashboards\Gauge Images

...\Program Files (x86)\Parsec\TrakSYS\WEBTrak\dashboards\Code
