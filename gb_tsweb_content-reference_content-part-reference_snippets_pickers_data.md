# Data

#### Target Key | Cache Seconds

Specifies the number of seconds that the part's resultant dataset will be cached before expiring. The **cache key** is the complete SQL statement (string) that is generated for the part. This means that if even a single character in the SQL statement changes, the cached value is not used. If the **cache key** exists, the part will return the cached dataset instead of re-executing the SQL statement. A value of 0 for this property disables caching.

#### Target Key | Cache Dependencies

Specifies the entity that will be referenced for the cached query. When changes are detected for this entity, the existing cached query will be removed and a new cached query will be saved with the changes. These cached queries and their dependencies can be viewed in the TrakSYS Web under **Administration | Diagnostics | Cache**.

{% hint style="info" %}
Changes to Cache Dependencies are only monitored through the TrakSYS API. Therefore, any Dependency changes made directly to the TrakSYS database will not be detected.
{% endhint %}

#### Source | Connection String

Specifies an OLEDB connection string to be used for the database connection against which the SQL statement for this part will be executed. If this property is left empty, the connection to the current TrakSYS database is used by default.

#### Source | Command Timeout

The Command Timeout property determines how long (in seconds) to wait upon command execution before timing out. When the default of -1 is used, the Command Timeout configured in Installation Manager is used.
