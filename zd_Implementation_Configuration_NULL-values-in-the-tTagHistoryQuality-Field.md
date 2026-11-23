# NULL values in the tTagHistory.Quality Field

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6824819078163-NULL-values-in-the-tTagHistory-Quality-Field*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

When using the [Historian](https://portal.parsec-corp.com/hc/en-us/articles/360005775213-How-to-Use-the-TrakSYS-Historian) functionality, a majority of the records should display a `NULL` value in the `tTagHistory.Quality` field for each table.

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/6856506364819)

A `NULL` value is stored in this field when the tag quality is "Good" or "192" at the time the record is created. In general, `NULL` values take up less disk space than strings or integer values. Since it is expected that a vast majority of the Historian records will contain a good quality, the `NULL` values represent this good status while optimizing the use of disk space. This can be important especially for scenarios where a large amount of tags are historized and records are created very frequently.

Any records that contain an integer value in this field indicate that the tag had a different status when the value was recorded. For example, a value of 0 in the `tTagHistory.Quality` field means that the `tTag.Quality` field contained a value of 0 when the tag value was historized.
