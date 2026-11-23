# How Do I Create a TrakSYS Database on a Remote Server?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115001354174-How-Do-I-Create-a-TrakSYS-Database-on-a-Remote-Server*
*Last updated: 2025-05-21T22:00:01Z*

---

Applies To | TrakSYS 10+

There is currently no way for Installation Manager to create a TrakSYS database on a remote server. 

The recommended approach in this case is as follows:

  1. Install TrakSYS on the database server.
  2. Use Installation Manager to create the database.
  3. Once the database is created, uninstall TrakSYS from the database server.
  4. Use Installation Manager on the application server to connect to the remote database.


