# Examining the database in SQL injection attacks.

[https://sandunigfdo.medium.com/examining-the-database-in-sql-injection-attacks-d8aab382cba9](https://sandunigfdo.medium.com/examining-the-database-in-sql-injection-attacks-d8aab382cba9)

Your ultimate goal of attacking a web application is to extract interesting data from the database. To do that, you must gather some information about the database. Such as,

- Database type and version
- Names of the tables and columns that contain the data you want to access.

Different databases have different ways of querying their type and version. In Order to find that information in a particular web application, you need to try out different queries to find the one that works.

The queries to determine the type and it’s version are as follows:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/SQL_Injection/images/c6c9a03c7e64_001.png)

You can find the names of database tables and columns by querying the table `information_schema.columns`, which contains details of all tables and column names within the database.

`information_schema` is designed to hold database metadata and it is supported by `MS-SQL, MySQL, PostgreSQL` etc. However when you target an Oracle database, you can obtain the same information with slightly different queries.

## Labs

- [Listing the database contents on Oracle database.](./Listing_the_database_contents_on_Oracle_database..md)
- [Listing the database contents on non-Oracle databases.](./Listing_the_database_contents_on_non-Oracle_databases..md)
- [Querying the database type and version on Oracle](./Querying_the_database_type_and_version_on_Oracle.md)
- [querying the database type and version on MySQL and Microsoft SQL Server](./querying_the_database_type_and_version_on_MySQL_and_Microsoft_SQL_Server.md)
