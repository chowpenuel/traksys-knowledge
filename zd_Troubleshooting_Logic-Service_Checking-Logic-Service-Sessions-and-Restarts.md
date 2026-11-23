# Checking Logic Service Sessions and Restarts

*Source: https://portal.parsec-corp.com/hc/en-us/articles/32902349635603-Checking-Logic-Service-Sessions-and-Restarts*
*Last updated: 2025-05-21T23:12:03Z*

---

Applies To | TrakSYS 10+

When performing troubleshooting activities or investigating Logic Service activity, it can be useful to know the exact times of when the Logic Service was stopped, started, restarted, and how long the service was down between restarts. This type of information is available within the `tLogicManagerSession` table.

When viewing the entries, the `tLogicManagerSession.StartDateTime` field indicates when the Logic Service was started. The `tLogicManagerSession.EndDateTime` field indicates when the Logic Service was turned off.

![](https://portal.parsec-corp.com/hc/article_attachments/32918106347155)

The time in between the StartDateTime and EndDateTime fields represents how long the Logic Service was running uninterrupted.

![](https://portal.parsec-corp.com/hc/article_attachments/32918106352787)

Finally, when looking at multiple records, the time between the EndDateTime of a previous record and the StartDateTime of the next record represents the total time that the Logic Service was down.

![](https://portal.parsec-corp.com/hc/article_attachments/32918539857171)

Typically, shorter durations between two rows (similar to what's shown above) indicate that a Logic Service restart occurred. Much larger blocks of time (such as several hours or days) can indicate that the service was turned off and turned on at a much later point in time. This can be common in cases where machine restarts, server maintenance, power outages, and other environment-related events occur.
