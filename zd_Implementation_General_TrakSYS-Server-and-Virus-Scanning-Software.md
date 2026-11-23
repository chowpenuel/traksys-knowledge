# TrakSYS Server and Virus Scanning Software

*Source: https://portal.parsec-corp.com/hc/en-us/articles/223281887-TrakSYS-Server-and-Virus-Scanning-Software*
*Last updated: 2025-05-21T22:10:10Z*

---

Applies To | TrakSYS 10+

### Summary

If any virus scanning software is running on the TrakSYS server, it is highly recommended to **NOT** scan database type files (e.g., file extensions such as .MDF, .LDF, .NDF, and .TRN). If these file types are scanned on change, then all TrakSYS database operations will be significantly affected. Additionally, varied database server response times will be experienced.

In a majority of scenarios, providing these exclusions will help prevent performance issues caused by virus scanning software. However, if performance issues still occur, the following exclusions can also be added to help prevent the behavior:

  1. File folders for TS Web content: 
     * ~\Parsec\TrakSYS\TS
  2. .NET Framework Config Folders: 
     * C:\Windows\Microsoft.NET\Framework\v2.0.50727\CONFIG
     * C:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG
     * C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config
     * C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config
  3. ASP.NET Temp Files Folders: 
     * C:\Windows\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files
     * C:\Windows\Microsoft.NET\Framework64\v2.0.50727\Temporary ASP.NET Files
     * C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files
     * C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Temporary ASP.NET Files
  4. IIS Config Folder (see source if using IIS shared configuration): 
     * %SystemDrive%\Windows\System32\inetsrv\Config
  5. IIS Temporary Compressed Files Folder 
     * %SystemDrive%\inetpub\temp\IIS Temporary Compressed Files


