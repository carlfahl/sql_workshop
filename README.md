## SQL workshop.  Using MySQL

### Step 1: Install and configure MySQL
On Mac OS X mysql can be installed via homebrew:
```
brew update
brew info mysql
brew install mysql
```

Add the mysql installation dir to your path

```

```

Use homebrew to start mysql:

```
brew tap homebrew/services
brew services run mysql
```

to stop mysql: `brew services stop mysql`

setup a root password for mysql server:

```
mysqladmin -u root password [new password]
```

Make sure the mysql is not running under the root user.
`ps aux | grep mysql`

Use the mysql client to connect to database: `mysql -u root -p`, enter root password that you set.

Create a non-privilaged user:

```SQL
CREATE USER '<username>'@'localhost' IDENTIFIED BY '<password>';
GRANT SHOW DATABASES ON *.* TO '<username>'@'localhost' with GRANT OPTION;
GRANT SELECT,INSERT,UPDATE ON login.* TO '<dbname>'@'localhost' with GRANT OPTION;
```

Not advised (essentially creates another root user): `GRANT ALL PRIVILEGES ON *.* TO '<dbname>'@'<hostname' with GRANT OPTION;`

View all users: `SELECT User from mysql.user`

### Step 2: create a database and a table

show the databases: `show databases;`
Create a new database to use:

```SQL
create database <dbname>;
use <dbname>;
```

```SQL
show tables;
describe <table_name>;
create table <table_name>(<list of feild descriptions>);
```

example:

```SQL
create table bears(id INT NOT NULL AUTO_INCREMENT, name CHAR(40), weight FLOAT, age INT, attitude CHAR(40), location CHAR(40), species CHAR(40), PRIMARY KEY (id));

describe bears;
```
outputs:
```
+----------+----------+------+-----+---------+----------------+
| Field    | Type     | Null | Key | Default | Extra          |
+----------+----------+------+-----+---------+----------------+
| id       | int(11)  | NO   | PRI | NULL    | auto_increment |
| name     | char(40) | YES  |     | NULL    |                |
| weight   | float    | YES  |     | NULL    |                |
| age      | int(11)  | YES  |     | NULL    |                |
| attitude | char(40) | YES  |     | NULL    |                |
| location | char(40) | YES  |     | NULL    |                |
| species  | char(40) | YES  |     | NULL    |                |
+----------+----------+------+-----+---------+----------------+
7 rows in set (0.12 sec)
```

### Step 3: Add data to a table with INSERT and read with SELECT

```SQL
INSERT into <table_name> values(<list of values>);
SELECT * from <table_name>;
SELECT <list of columns> from <table_name>;
```

Example:

```SQL
insert into bears values(0, 'yogi', 300, 30, 'nice', 'yellowstone', 'black');
insert into bears values(0, 'yogi', 300, 30, 'nice', 'yellowstone', 'black');
select * from bears;
```
outputs:
```
+----+------+--------+------+----------+-------------+---------+
| id | name | weight | age  | attitude | location    | species |
+----+------+--------+------+----------+-------------+---------+
|  1 | yogi |    300 |   30 | nice     | yellowstone | black   |
|  2 | yogi |    300 |   30 | nice     | yellowstone | black   |
+----+------+--------+------+----------+-------------+---------+
2 rows in set (0.00 sec)
```

Notice that the id column increases by 1 for each insert.

To select from a specific row of the table, add `WHERE` to the `SELECT` command.

```SQL
insert into bears values(0, 'bobo', 200, 15, 'nice', 'bozeman', 'brown');
select name, age, location from bears where name='bobo';
```

outputs:
```
+------+------+----------+
| name | age  | location |
+------+------+----------+
| bobo |   15 | bozeman  |
+------+------+----------+
1 row in set (0.04 sec)
```

### Step 4: Change values with the UPDATE command.  Alter a table with the ALTER command

To change the value of a feild:

```SQL
update bears set attitude='nasty' where name='bobo';
select * from bears where name='bobo';
```
outputs:
```
+----+------+--------+------+----------+----------+---------+
| id | name | weight | age  | attitude | location | species |
+----+------+--------+------+----------+----------+---------+
|  3 | bobo |    200 |   15 | nasty    | bozeman  | brown   |
+----+------+--------+------+----------+----------+---------+
1 row in set (0.00 sec)
```

To Add a column to the table:

```SQL
ALTER table bears ADD column favoriteFood CHAR(40) AFTER attitude;
select * from bears;
```
outputs:
```
+----+------+--------+------+----------+--------------+-------------+---------+
| id | name | weight | age  | attitude | favoriteFood | location    | species |
+----+------+--------+------+----------+--------------+-------------+---------+
|  1 | yogi |    300 |   30 | nice     | NULL         | yellowstone | black   |
|  2 | yogi |    300 |   30 | nice     | NULL         | yellowstone | black   |
|  3 | bobo |    200 |   15 | nice     | NULL         | bozeman     | brown   |
+----+------+--------+------+----------+--------------+-------------+---------+
3 rows in set (0.02 sec)
```

To remove a column from the table:

```SQL
ALTER table bears DROP column favoriteFood;
Query OK, 0 rows affected (0.87 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select * from bears;
+----+------+--------+------+----------+-------------+---------+
| id | name | weight | age  | attitude | location    | species |
+----+------+--------+------+----------+-------------+---------+
|  1 | yogi |    300 |   30 | nice     | yellowstone | black   |
|  2 | yogi |    300 |   30 | nice     | yellowstone | black   |
|  3 | bobo |    200 |   15 | nice     | bozeman     | brown   |
+----+------+--------+------+----------+-------------+---------+
3 rows in set (0.00 sec)
```

### Step 5: Using the mysql node module

Install the mysql module for node: `npm install --save mysql`

```js
var mysql = require('mysql');

var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'carlfahl', // Database username
  password : 'password', // Database password
  database : 'test',
});

connection.connect();

connection.query(sql_st, function(err, rows) {
  if (err) throw err;
});
```

### Step 5: More Advanced SQL

#### One to Many relationships.

#### Table JOINS

#### Table UNION
