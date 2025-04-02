Used to authenticate and interact with mySQL/MariaDB database.

#### General knowledge
```shell-session
$ mysql -u root -p
```
Flags:
- -u is username
- -p is password (in example no password is sent so we can be prompted to enter it - this prevents saving in the bash history). If using -p, there should be no space between '-p' and the password.
- -P is for port (default is 3306)
- -h to specify host. If none specified, defaults to localhost

```shell-session
mysql> CREATE DATABASE users;
```
Creates a database

```shell-session
mysql> SHOW DATABASES;

+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| users              |
+--------------------+

mysql> USE users;

Database changed
```

SHOW DATABASES shows all the databases, and USE [db] specifies which database to access

Note: SQL statements (CREATE, SHOW, USE, etc) are not case sensitive, but database names are (users vs Users vs USERS, etc).

Common datatypes are numbers, strings, date, time, binary data. Complete list: https://dev.mysql.com/doc/refman/8.0/en/data-types.html

```sql
CREATE TABLE logins (
    id INT,
    username VARCHAR(100),
    password VARCHAR(100),
    date_of_joining DATETIME
    );
```
Example of table creation with different data types

```shell-session
mysql> DESCRIBE logins;

+-----------------+--------------+
| Field           | Type         |
+-----------------+--------------+
| id              | int          |
| username        | varchar(100) |
| password        | varchar(100) |
| date_of_joining | date         |
+-----------------+--------------+
4 rows in set (0.00 sec)
```
Example of DESCRIBE statement, showing the fields and types of a table

#### Table Properties
Properties can be set for tables and columns during creation

```sql
id INT NOT NULL AUTO_INCREMENT,
```
AUTO_INCREMENT increments id by 1 for every new item

```sql
username VARCHAR(100) UNIQUE NOT NULL,
```
NOT NULL ensures a column is never empty (required field). UNIQUE constraint ensures inserted item is unique.

```sql
date_of_joining DATETIME DEFAULT NOW(),
```
DEFAULT sets the default value. In example, NOW() is used as the default value

```sql
PRIMARY KEY (id)
```
Specify the column to be used as the primary key

```sql
CREATE TABLE logins (
    id INT NOT NULL AUTO_INCREMENT,
    username VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(100) NOT NULL,
    date_of_joining DATETIME DEFAULT NOW(),
    PRIMARY KEY (id)
    );
```
This is the final create table query with all the parameters above

#### SQL Statements

##### Insert
```sql
INSERT INTO table_name VALUES (column1_value, column2_value, column3_value, ...);
```
INSERT adds new records into table

```shell-session
mysql> INSERT INTO logins VALUES(1, 'admin', 'p@ssw0rd', '2020-07-02');

Query OK, 1 row affected (0.00 sec)
```
Example of INSERT with sample values

```sql
INSERT INTO table_name(column2, column3, ...) VALUES (column2_value, column3_value, ...);
```
INSERT can be used to add records with only specific fields specified (if fields with NOT NULL parameter are omitted, will result in error)

```shell-session
mysql> INSERT INTO logins(username, password) VALUES('administrator', 'adm1n_p@ss');

Query OK, 1 row affected (0.00 sec)
```
Example of INSERT with specific fields and values

##### Select
```sql
SELECT * FROM table_name;
```
General syntax to view all data in a table

```sql
SELECT column1, column2 FROM table_name;
```
Selects specific columns from a table

##### Drop
```shell-session
mysql> DROP TABLE logins;

Query OK, 0 rows affected (0.01 sec)


mysql> SHOW TABLES;

Empty set (0.00 sec)
```
DROP is used to remove tables and databases

##### Alter
```shell-session
mysql> ALTER TABLE logins ADD newColumn INT;

Query OK, 0 rows affected (0.01 sec)
```
ALTER is used to change a table name or name of fields, and to add/remove columns. Example shows adding a new column.

```shell-session
mysql> ALTER TABLE logins RENAME COLUMN newColumn TO newerColumn;

Query OK, 0 rows affected (0.01 sec)
```
Example of renaming a column

```shell-session
mysql> ALTER TABLE logins MODIFY newerColumn DATE;

Query OK, 0 rows affected (0.01 sec)
```
Example of modifying a column's datatype

```shell-session
mysql> ALTER TABLE logins DROP newerColumn;

Query OK, 0 rows affected (0.01 sec)
```
Example of dropping a column

##### Update
```sql
UPDATE table_name SET column1=newvalue1, column2=newvalue2, ... WHERE <condition>;
```
UPDATE is used to update specific records. Must specify table, column, values, and condition

```shell-session
mysql> UPDATE logins SET password = 'change_password' WHERE id > 1;

Query OK, 3 rows affected (0.00 sec)
Rows matched: 3  Changed: 3  Warnings: 0


mysql> SELECT * FROM logins;

+----+---------------+-----------------+---------------------+
| id | username      | password        | date_of_joining     |
+----+---------------+-----------------+---------------------+
|  1 | admin         | p@ssw0rd        | 2020-07-02 00:00:00 |
|  2 | administrator | change_password | 2020-07-02 11:30:50 |
|  3 | john          | change_password | 2020-07-02 11:47:16 |
|  4 | tom           | change_password | 2020-07-02 11:47:16 |
+----+---------------+-----------------+---------------------+
4 rows in set (0.00 sec)
```
Example of updating password fields in a table to a specific value based on id value

##### Sorting Results
```shell-session
mysql> SELECT * FROM logins ORDER BY password;

+----+---------------+------------+---------------------+
| id | username      | password   | date_of_joining     |
+----+---------------+------------+---------------------+
|  2 | administrator | adm1n_p@ss | 2020-07-02 11:30:50 |
|  3 | john          | john123!   | 2020-07-02 11:47:16 |
|  1 | admin         | p@ssw0rd   | 2020-07-02 00:00:00 |
|  4 | tom           | tom123!    | 2020-07-02 11:47:16 |
+----+---------------+------------+---------------------+
4 rows in set (0.00 sec)
```
ORDER BY is used to sort by a column. Sort order is ascending by default.

```shell-session
mysql> SELECT * FROM logins ORDER BY password DESC;

+----+---------------+------------+---------------------+
| id | username      | password   | date_of_joining     |
+----+---------------+------------+---------------------+
|  4 | tom           | tom123!    | 2020-07-02 11:47:16 |
|  1 | admin         | p@ssw0rd   | 2020-07-02 00:00:00 |
|  3 | john          | john123!   | 2020-07-02 11:47:16 |
|  2 | administrator | adm1n_p@ss | 2020-07-02 11:30:50 |
+----+---------------+------------+---------------------+
4 rows in set (0.00 sec)
```
Can be sorted descending.

```shell-session
mysql> SELECT * FROM logins ORDER BY password DESC, id ASC;

+----+---------------+-----------------+---------------------+
| id | username      | password        | date_of_joining     |
+----+---------------+-----------------+---------------------+
|  1 | admin         | p@ssw0rd        | 2020-07-02 00:00:00 |
|  2 | administrator | change_password | 2020-07-02 11:30:50 |
|  3 | john          | change_password | 2020-07-02 11:47:16 |
|  4 | tom           | change_password | 2020-07-02 11:50:20 |
+----+---------------+-----------------+---------------------+
4 rows in set (0.00 sec)
```
Can be sorted by multiple columns

##### Limit results
LIMIT used to limit results based on conditions

```shell-session
mysql> SELECT * FROM logins LIMIT 2;

+----+---------------+------------+---------------------+
| id | username      | password   | date_of_joining     |
+----+---------------+------------+---------------------+
|  1 | admin         | p@ssw0rd   | 2020-07-02 00:00:00 |
|  2 | administrator | adm1n_p@ss | 2020-07-02 11:30:50 |
+----+---------------+------------+---------------------+
2 rows in set (0.00 sec)
```
Example showing limiting to 2 results

```shell-session
mysql> SELECT * FROM logins LIMIT 1, 2;

+----+---------------+------------+---------------------+
| id | username      | password   | date_of_joining     |
+----+---------------+------------+---------------------+
|  2 | administrator | adm1n_p@ss | 2020-07-02 11:30:50 |
|  3 | john          | john123!   | 2020-07-02 11:47:16 |
+----+---------------+------------+---------------------+
2 rows in set (0.00 sec)
```
Example showing limit with an offset. Offset defined prior to LIMIT count, and starts at 0 (in this case offset 1 is id 1)

##### Where
Filters/searches based on condition

```sql
SELECT * FROM table_name WHERE <condition>;
```
Basic syntax

```shell-session
mysql> SELECT * FROM logins WHERE id > 1;

+----+---------------+------------+---------------------+
| id | username      | password   | date_of_joining     |
+----+---------------+------------+---------------------+
|  2 | administrator | adm1n_p@ss | 2020-07-02 11:30:50 |
|  3 | john          | john123!   | 2020-07-02 11:47:16 |
|  4 | tom           | tom123!    | 2020-07-02 11:47:16 |
+----+---------------+------------+---------------------+
3 rows in set (0.00 sec)
```
Condition where id is greater than 1

```shell-session
mysql> SELECT * FROM logins where username = 'admin';

+----+----------+----------+---------------------+
| id | username | password | date_of_joining     |
+----+----------+----------+---------------------+
|  1 | admin    | p@ssw0rd | 2020-07-02 00:00:00 |
+----+----------+----------+---------------------+
1 row in set (0.00 sec)
```
Condition where username is admin

##### Like
LIKE filters by matching a pattern

```shell-session
mysql> SELECT * FROM logins WHERE username LIKE 'admin%';

+----+---------------+------------+---------------------+
| id | username      | password   | date_of_joining     |
+----+---------------+------------+---------------------+
|  1 | admin         | p@ssw0rd   | 2020-07-02 00:00:00 |
|  4 | administrator | adm1n_p@ss | 2020-07-02 15:19:02 |
+----+---------------+------------+---------------------+
2 rows in set (0.00 sec)
```
Example of LIKE matching the 'admin%' pattern. The % symbol is a wildcard used to match zero or more characters. The \_ symbol is used to match exactly one character.

```shell-session
mysql> SELECT * FROM logins WHERE username like '___';

+----+----------+----------+---------------------+
| id | username | password | date_of_joining     |
+----+----------+----------+---------------------+
|  3 | tom      | tom123!  | 2020-07-02 15:18:56 |
+----+----------+----------+---------------------+
1 row in set (0.01 sec)
```
Example of the \_ symbol being used as a wildcard, matching usernames with exactly 3 characters