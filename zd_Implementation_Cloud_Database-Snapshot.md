# Database Snapshot

*Source: https://portal.parsec-corp.com/hc/en-us/articles/53263659277715-Database-Snapshot*
*Last updated: 2026-07-23T20:34:19Z*

---

Applies To | TrakSYS 14.0.0+

### Summary

Database Snapshot tracks changes to TrakSYS configuration and UI over time. It remotely triggers a Database Transfer Export from TrakSYS Cloud for a specific installation, scans the resulting `.transfer` file, and stores the relevant data in a Git repository, where users can compare snapshots to see what changed. TrakSYS Cloud also keeps a modified copy of the transfer file. Snapshot data requires access to both TrakSYS Cloud and the Git repository — access to one alone isn't enough.

Requirements:  


  * No additional license feature or cost is required.
  * TrakSYS Cloud must be enabled and configured on the license. See [**Using TrakSYS Cloud**](https://portal.parsec-corp.com/hc/en-us/articles/45236735222931-Using-TrakSYS-Cloud).
  * An active internet connection is **required**. Specifically, the TrakSYS Agent Service needs internet access to communicate with TrakSYS Cloud.
  * The TrakSYS Agent Service must run version 1400.0.2 (for TrakSYS 14.0.0), 1401.0.2 (for TrakSYS 14.0.1), or later. Newer Agent Service versions are automatically compatible. It is always recommended to use the latest available version.

  * The TrakSYS Agent Service must stay running for TrakSYS Web to trigger snapshots remotely.




### Creating and Configuring a Repository

Database Snapshot needs a Git repository to store each snapshot's configuration data. This has been tested with GitHub and Azure DevOps, but should work with any Git-compatible host.

The following links describe how to create a repository:

  * [Creating a new Repository on GitHub](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository)
  * [Creating a new Repository on Azure DevOps](https://learn.microsoft.com/en-us/azure/devops/repos/git/create-new-repo?view=azure-devops)



Some Git hosts require repository initialization before snapshot data can be recorded. If a host other than GitHub or Azure DevOps is being used, check that host's documentation for setup steps.

### Configuring a Time Zone

Database Snapshot needs a configured time zone in TrakSYS Cloud. This time zone determines when automated snapshots run, if automation is enabled.

To configure the time zone:

  1. Open the TrakSYS Cloud Web Portal.
  2. In the first slice, select Deployments.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53307464246035)  

  3. Select the Deployment from the list in the second slice.
  4. Click Details in the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53307501112339)  

  5. Click Edit next to General in the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53307464247443)  

  6. Select the desired time zone from the Time Zone dropdown. This example uses Pacific Time (Los Angeles).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53307501112851)  
**NOTE** : Only time zones that fall on the hour are supported. Time zones on the half hour (e.g., 8:30) or quarter hour (e.g., 8:15, 8:45) are not.  

  7. Click Save.
  8. The Deployment Details now show the new time zone.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53307684316947)



### Configuring Database Snapshot

To configure the Snapshot Repository and Snapshot Schedule for a license:

  1. Open the TrakSYS Cloud Web Portal.
  2. In the first slice, select Deployments.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53307464246035)  

  3. Select the Deployment from the list in the second slice.
  4. Select Licenses [Active] in the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53307464248979)  

  5. Select the license to include. This example uses the Non-Production development license.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53307501113619)  

  6. Click Details in the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53307989612051)  

  7. The page now shows licensing information, feature lines, and Database Snapshot settings.
  8. Click Edit next to Snapshot Repository.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53308144334099)  

  9. Enter the Git Project URL and**** Branch Name.  
  
**Git Project URL** is required to generate snapshots. Leave it blank to disable Database Snapshot. This is useful for installations that no longer need a change history.  
  
**Branch Name** sets which branch stores snapshots. If left blank, snapshots go to the repository's default branch (usually `main`).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53327446133651)  


  10. Click Save.
  11. The Snapshot Repository section now shows the updated values.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53327446138131)  

  12. Click Edit next to Personal Access Token to give TrakSYS Cloud write access to the repository.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53327980862355)  

  13. Enter the token value and click Set.  
  
**NOTE** : The Personal Access Token field is write-only. Once saved, the value is encrypted and can't be retrieved. If the token is lost, generate a new one through the Git provider and re-enter it here.  

  14. Once saved, the field shows five stars, regardless of the token's actual length. This is done to obfuscate the actual length of the token.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53328895705107)  

  15. Click Edit next to Snapshot Schedule to set an automated schedule.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53328934382483)  

  16. Set a snapshot time for each day, or select the dash (`-`) value to disable snapshots that day. Times use 24-hour format and reference configured the time zone. This example schedules Monday through Friday and disables Saturday and Sunday.  
  
**NOTE** : Snapshots can only run on the hour (e.g., 08:00, 09:00). Times like 08:15, 09:45, 10:17, etc. are not supported. Only one snapshot per day is supported. Daylight Saving Time and leap years are handled automatically.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53329335701267)  


  17. Click Save.
  18. The full schedule for automated snapshots now displays.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53329335702419)



### Manually Executing a Database Snapshot

Automated scheduling is recommended, but you can also trigger a snapshot manually at any time. This section assumes Database Snapshot is already configured, as described above.

  1. Open the Deployments page in TrakSYS Cloud.
  2. Select Licenses [Active] in the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53307464248979)  

  3. Select the license to include. This example uses the Non-Production development license.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53307501113619)  

  4. Click DB Snapshot under Actions in the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53333069312147)  

  5. Confirm the Snapshot Repository settings, then click Execute DB Snapshot.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53333268144531)  

  6. The status page shows operation progress and updates automatically. Select a step in the Steps slice to see its details in the Step Data slice. A message appears at the bottom of the Steps slice when the operation finishes, showing success or failure.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53333206031379)  


  7. OPTIONAL: After the operation completes, click Download File under Actions in the first slice to download the exported transfer file.  
  
**NOTE** : This file is intentionally modified and can't be imported into a TrakSYS installation. It is intended to be used only for verification and troubleshooting. It also doesn't honor excluded tables and fields from Installation Manager, so importing it would bring in content meant to be excluded. Modifying it to force an import is **not recommended** and **not supported**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53333703243539)  


  8. The snapshot data now appears in the Git repository. Compare snapshots there to see what changed between them.



### Checking Previous Database Snapshot Operations

TrakSYS Cloud logs every snapshot operation and its steps, giving an audit trail of when each snapshot ran, what changed, and who triggered it. This log is also useful for troubleshooting failed operations or unexpected configuration changes.

To view this information:

  1. Open the Deployments page in TrakSYS Cloud.
  2. Select the Deployment from the list in the second slice.
  3. Click Operation History under Related in the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53337340799123)  

  4. Database Snapshot operations show "DB Transfer Export" in the Type column.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53340423430931)  
  
The Info column shows "DB Snapshot" for each entry. Automated snapshots show TrakSYS Cloud as the user. Manual snapshots show the user who triggered them.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/53340423431827)  

  5. Click an entry to see its details on the Operation Details page. This is the same page shown in Step 6 of the "Manually Executing a Database Snapshot" section.  



