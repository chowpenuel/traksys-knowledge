# 2022-06-14 Windows DCOM Server Security Feature Bypass Changes

*Source: https://portal.parsec-corp.com/hc/en-us/articles/7077369737107-2022-06-14-Windows-DCOM-Server-Security-Feature-Bypass-Changes*
*Last updated: 2023-10-27T09:48:45Z*

---

To address the security vulnerability described in [CVE-2021-26414](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-26414), Microsoft has implemented some hardening changes in DCOM which will impact communication with remote OPC DA Servers in TrakSYS versions prior to [11.2.3](https://portal.parsec-corp.com/hc/en-us/articles/1500011645841). 

As outlined in [KB5004442](https://support.microsoft.com/en-us/topic/kb5004442-manage-changes-for-windows-dcom-server-security-feature-bypass-cve-2021-26414-f1400b52-c141-43d2-941e-37ed901c769c), Windows Updates rolled out starting on June 14th, 2022 will have these hardening changes enabled by default. Once these updates are installed, TrakSYS applications using versions 11.2.2 and earlier will not be able to connect to remote OPC DA Servers. To restore communication, the hardening changes must be disabled via registry key on the OPC Server (see [KB5004442](https://support.microsoft.com/en-us/topic/kb5004442-manage-changes-for-windows-dcom-server-security-feature-bypass-cve-2021-26414-f1400b52-c141-43d2-941e-37ed901c769c) for more details and procedure).

Microsoft plans to enable the hardening changes permanently on March 14th, 2023. Our recommendation is to upgrade to [TrakSYS 11.2.3](https://portal.parsec-corp.com/hc/en-us/articles/1500011645841) (at minimum) well before that date.
