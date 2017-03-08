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
GRANT SHOW DATABASES ON *.* TO 'xdb'@'localhost' with GRANT OPTION;
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

### Step 3: Add data to a table with INSERT and read with SELECT


### Step 4: Using the mysql node module


### Step 5: More Advanced SQL

#### Table JOINS

####
