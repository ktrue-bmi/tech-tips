Logging In Remotely
====

To give users access outside of localhost, first create a user with access to '%' (see below). You may also need to comment out the line in /etc/mysql/my.cnf to comment out the bind-address option.

Dumping a Table
====

Dumping a table to a MySQL-formatted SQL file:

```bash
mysqldump -u root -p my_database my_table > my_table.sql
```

Dumping a table to a CSV file:

```sql
SELECT
    *
FROM
    mytable
INTO OUTFILE '/tmp/mytable.csv'
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n';
```

Creating New Users
====

```sql
DROP USER demo@'localhost';
DROP USER demo@'%';
CREATE USER 'demo'@'localhost' IDENTIFIED BY 'demo';
CREATE USER 'demo'@'%' IDENTIFIED BY 'demo';
GRANT ALL PRIVILEGES ON *.* TO 'demo'@'localhost' WITH GRANT OPTION;
GRANT ALL PRIVILEGES ON *.* TO 'demo'@'%' WITH GRANT OPTION;
```

Viewing Users
====

```sql
SELECT user, host, password FROM mysql.user;
```

Pretty-printing SQL
====

The following is a nice web-based formatter with several options:

http://www.dpriver.com/pp/sqlformat.htm

STRAIGHT_JOIN
====

STRAIGHT_JOIN is an optimization for joins and is described here:

http://dev.mysql.com/doc/refman/5.0/en/join.html

Configuration
====

Configuration for MySQL can be stored in a file (including optional password) named $HOME/.my.cnf. The file can be as simple as:

    [client]
    password=53cr3t

Alternatively, you can set the MYSQL_PWD environment variable to your password, though this is obviously insecure.

Query Process Management
====

To see all the queries in process:

    show processlist

And to kill one:

    kill query <query ID>

Creating Tables from Queries
====

It's possible to create a table using the derived schema from an arbitrarily complex query. Here's a quick example:

```sql
CREATE TABLE dst_tbl SELECT * FROM src_tbl;
```

There's a bit more information here:

http://answers.oreilly.com/topic/158-how-to-save-query-results-in-a-mysql-table/