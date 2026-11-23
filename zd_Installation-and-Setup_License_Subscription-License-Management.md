# Subscription License Management

*Source: https://portal.parsec-corp.com/hc/en-us/articles/26684930743699-Subscription-License-Management*
*Last updated: 2025-12-10T21:53:42Z*

---

Applies To | TrakSYS 12+

### Summary

This article explains how license subscriptions are managed and maintained.

### License JSON

A subscription license is a packet of data that indicates what features are allowed, and when the license expires. A TrakSYS license is imported into the TrakSYS database and is stored in the **tLicense** table where the various components access it to verify allowable capabilities. The license information stored in the table is not human readable and cannot be altered manually.

### Validate Call

TrakSYS, with a subscription license, will regularly attempt to contact Parsec via a REST Web Service call to determine the TrakSYS instance's runnable status. The TrakSYS instance will pass some information to Parsec and the license's status and other information will be returned. This process is referred to as the Validate call.

![Picture2.png](https://portal.parsec-corp.com/hc/article_attachments/26685418824467)

### First Validate Call

After a subscription license is installed, it will not be functional until the first **Validate** call is made and an **OK** status is returned. This is to prevent a second copy of the license from being installed and activated. When a license is first installed, its status will be set to **Unknown** until the first successful **Validate** call is made.

![Picture3.png](https://portal.parsec-corp.com/hc/article_attachments/26691140370707)

### Information sent during Validate Call

The following information is sent from the TrakSYS instance to Parsec on each **Validate** call.

#### Serial Number

The SN1234567890 serial number associated with the license.

#### Serial Number Version

This is an integer that starts with 1 (for each Serial Number) and is incremented each time features are added or removed from a license.

#### Database Server Name

This is the name of the instance’s database server as entered in the connections settings in **Installation Manager**.

#### Database Name

This is the name of the instance’s database as entered in the connections settings in **Installation Manager**.

#### TrakSYS Version

This is the full version number of the instance’s installed TrakSYS.

#### Machine Name

This is the Windows PC/server name for the computer where the **Maintenance Service** is that makes the **Validate** call.

#### Call Mode

This state indicates if the Validate call was made automatically on its scheduled interval, or if a human initiated the call via **Installation Manager**.

### Information Returned to TrakSYS Instance during Validate Call

The following information is returned to the TrakSYS instance from Parsec on each **Validate** call. It is encrypted and stored in the **tLicense** table in the instance’s TrakSYS database.

#### Validate Status

Depending on the situation, one of the following statuses will be returned…

OK / Valid  
The calling instance is valid and can continue operating with no needed actions.

Update Required (Instant)  
The license for the calling instance had been modified (new features added) in a way that is safe for the license to be replaced without restarts. This status will automatically trigger the instance to make an Update call. The details of the Update call are covered in a later section.

Update Required (Deferred)  
The license for the calling instance had been modified (features removed) that requires service and or web restarts before the changes can take effect. This return status will NOT automatically trigger the instance to make an Update call. Instead, a message will appear in Installation Manager notifying an administrative user to stop services and activate the Update call manually (via a button in Installation Manager). The details of the Update call are covered in a later section.

Kill / Shutdown  
Some scenario has occurred whereby the license for the calling instance is no longer valid. This status will cause the immediate invalidation of the license. The web and all TrakSYS services will stop functioning.

Instance Exists  
This status is returned if the calling instance (identified by a combination of the database server and database names) is not the registered active instance in the TrakSYS Cloud license application. More details on this state and the process for moving an instance can be found in the Instance Tracking section later in this document.

#### Next Validate Date/Time (UTC)

This date/time will be set and instruct the local Maintenance service as to the next time it should make the Validate call. This is typically set to **24 hours after the current call UTC** ; however, Parsec can control this from central settings and may periodically change the frequency.

#### Grace Period Date (UTC)

This is the date that after which, the instance will stop functioning. It is typically set to **10 days after the technical subscription end date** ; however, Parsec can control this from the central settings and may alter this on a case-by-case basis.

#### Call Expire Date/Time (UTC)

This is a timestamp that is included to foil attempts at spoofing the Validate call and return message by capturing a copy and continuing to return the same “success” results.

### Frequency and Manual Call

The following describes the frequency that the Validate call is made from a TrakSYS instance to Parsec.

#### Typical Operation

The Validate call is made once per day. The exact time is not standard. The call is scheduled to be made 24 hours after the previous call is successfully made. Note that a successful call in this context is when the Parsec servers are reached, and any status is returned.

#### Failed Connection

If a Validate call fails to connect to the Parsec servers, then a new call will be scheduled 90 minutes in the future. This will continue until successful call is made.

#### Exception Scheduling

For a variety of reasons, Parsec can adjust the next call frequency to any value.

#### Manual Call

A Validate call can be initiated manually at any time by pressing a button in the Installation Manager. If this call succeeds, then the next Validate call will be re-scheduled to manual call + 24 hours.

### Failed or Absence of Validate Calls

The following describes the workflow for when an active subscription license instance fails to check in to Parsec via the Validate call.

#### Scenarios

There are several scenarios that could result in the Parsec servers failing to receive regular Validate calls from an active subscription license.

Failed Connection  
The Validate call fails to connect to the Parsec servers due to some network connectivity or firewall issue.

Maintenance Service Not Running  
If the TrakSYS instance does not have a Maintenance Service running, the Validate call will not be made.

Instance Decommissioned  
If a customer uninstalls TrakSYS, the Validate call will not be made.

#### Parsec Notification

The Parsec license management infrastructure will note the absence of regular Validate calls from an active subscription instance. A Parsec administrator will be notified of subscription instances that are not receiving regular calls.

#### Customer Notification

A Parsec license administrator or commercial representative will contact a customer when an active subscription license is not making regular Validate calls. The intent is to notify them and attempt to resolve the issue preventing the calls from being made.

#### License Deactivation

Licenses are not deactivated solely for failure to make Validate calls. Parsec will continue to troubleshoot with the customer to re-establish connectivity. In the absence of Validate calls, a subscription license will function until the subscription term end date.

### Maintenance Service

The Maintenance Service is the TrakSYS component that makes the scheduled Validate and Update calls to Parsec. It must have visibility to call out to the internet address https://traksys.parsec-corp.com.

When the Validate and Update calls are manually triggered from Installation Manager, they are not being called through the Maintenance Service, but from within the Installation Manager EXE.

![Picture4.png](https://portal.parsec-corp.com/hc/article_attachments/26699212417043)

### No Internet Access

In some cases, a customer instance may be located behind firewalls that prevent the servers from reaching out to the Internet. In these cases, the following options are available:

#### Open Specific Exceptions to Parsec

Convince customer IT to open Internet access to a specific address, from a specific application on a specific TrakSYS server.

![Picture6.png](https://portal.parsec-corp.com/hc/article_attachments/26699427855251)

#### Dedicated Maintenance Service

Install a copy of Maintenance Service on a (small) dedicated server outside the firewall. There will still need to be access to the TrakSYS database opened from the Maintenance Service outside the firewall (port 1433 or whatever is used for SQL).

![Picture7.png](https://portal.parsec-corp.com/hc/article_attachments/26699377534867)

#### Termed Offline License Issued

A license can be created that does not make Validate calls and is set to expire at the end of the subscription term. For this option, a new license must be made and installed/activated each year.

![Picture8.png](https://portal.parsec-corp.com/hc/article_attachments/26699427869843)

#### Termed Offline License Activation

Once the Termed Offline License has been obtained, it can be [manually activated](https://portal.parsec-corp.com/hc/en-us/articles/115000983914) (expiration grace period does not apply).

### License Updates

Subscription licenses benefit from the capability to be updated automatically via the Validate (and Update) calls. Once a license has been modified in the Parsec license infrastructure (after all commercials are complete). The new license is available and will be transferred to the site. There are two main scenarios…

#### Instant (Safe) Update

If a customer adds features to their license, the new license will be made available in the Parsec license infrastructure.

When a customer's Validate call comes in, one of the pieces of information returned to the calling instance is an instruction to make an Update call (if the new license is safe to upgrade, meaning adding new features).

After the Validate call, the calling instance will automatically call Update and pull down the new license, replacing it in the database.

After the Update is called automatically…

\- Local services will have to be restarted to use new features.  
\- The TS Web may have to be refreshed using the Reload command on the Administration | Settings page (it will eventually reload on its own during a random app pool recycle).

![Picture9.png](https://portal.parsec-corp.com/hc/article_attachments/26699525613331)

#### Deferred (Un-Safe) Update

If a customer removes features from their license, the new license will be made available in the Parsec license infrastructure.

When a customer's Validate call comes in, if the new license is a downgrade (removing features), an Update directive will not be returned. Instead, a status will be returned that will cause a message to be displayed in Installation Manager indicating that the Update command must be run manually.

This means that a customer admin must determine when to press a manual Update button in Installation Manager to pull the new license down.

After the Update is called manually…

The customer admin must ensure that the services are not running at the time the Update is requested. A warning will be displayed to the admin user if any services are running when the Update is attempted.  
The TS Web may have to be refreshed using the Reload command on the Administration | Settings page (it will eventually reload on its own during a random app pool recycle).

![Picture10.png](https://portal.parsec-corp.com/hc/article_attachments/26699525620499)

### Expiring Licenses

As a subscription term nears, the following warnings will be made. Note that some of these are from within the software, while others originate in the Parsec license infrastructure and are manually issued.

#### Parsec License Infrastructure

Starting **90 days** from the term date, emails will be sent (**every 7 days**) to the primary customer contact, the associated Partner contact, the associated Parsec contact, and the license infrastructure administrator, indicating that the term date is approaching, and the software will stop functioning at the term date. It will be the responsibility of one of the Parsec or Partner contacts to reach the customer and ensure that a timely renewal is occurring.

#### Early Warning within TrakSYS

Starting **30 days** from the term date, a banner will show at the bottom of all pages inside the **Configuration** , **Developer** and **Administration** sections of the application indicating that the term date is approaching, and the software will stop functioning at the term date.

#### Final Warning within TrakSYS

Starting **10 days** from the term date, a banner will show at the bottom of **all pages** of the application indicating that the term date is approaching, and the software will stop functioning at the term date.

#### Grace Period

By default, there is a **10-day** grace period which will allow a TrakSYS instance to run beyond its term expiration date. This is not advertised, and it may be altered on a per license, case-by-case basis.

#### Expiration State

If a license is not updated before its term end date (plus grace period), the TrakSYS installation will **cease to function**. **Services will stop** and cannot be restarted, and the **TS Web will return a license error message** instead of the intended content on every page.

### Instance Tracking

To prevent subscription licenses from being installed and used in more than one environment at the same time, the license site must track installed instances for each license.

The Parsec license infrastructure will track instance name information for each license (based on database server name and database name). Only **one active instance** is allowed per license. 

### Non-Production Licenses

Non-production licenses (NPLs) will be generated with their own unique serial number, and each call their own Validate and Update calls for management.
