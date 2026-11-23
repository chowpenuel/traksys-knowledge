# Why is there a "Detected [Amazon RDS or Azure SQL]: the license may become deactivated" message within the Installation Manager?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/48279834008979-Why-is-there-a-Detected-Amazon-RDS-or-Azure-SQL-the-license-may-become-deactivated-message-within-the-Installation-Manager*
*Last updated: 2026-01-16T20:06:22Z*

---

Applies To | TrakSYS 10.2.0+

When using Amazon RDS or Azure SQL to host the TrakSYS database, it may be possible to see the following warning within the License tab of the TrakSYS Installation Manager:

![](https://portal.parsec-corp.com/hc/article_attachments/48279846607379)

If Azure SQL is used instead, the warning may display the following message:
    
    
    "Detected Azure SQL: the license may become deactivated."

This message can appear when the Cloud Database Mode was not properly configured when the license was activated. Because of how databases are hosted in both 3rd party platforms, this property needs to be configured before activating the license to ensure that the TrakSYS license does not become deactivated. This property can be set by opening the TrakSYS Installation Manager and following the steps shown in the image below:

![](https://portal.parsec-corp.com/hc/article_attachments/48280230782739)

If Azure SQL is being used, then the Cloud Database Mode should be set to Azure SQL instead:

![](https://portal.parsec-corp.com/hc/article_attachments/48280227032595)

Once this setting is changed, the license will need to be reactivated. If additional activations are needed for the license, please submit a [License Activation Increase Request](https://portal.parsec-corp.com/hc/en-us/requests/new?ticket_form_id=13514752992275). Once the license is successfully reactivated, this warning should no longer appear within the TrakSYS Installation Manager.
