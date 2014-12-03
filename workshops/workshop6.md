# Institute of Systems Science National University of Singapore


# NICF - Agile Continuous Delivery


# Workshop 6

Automated migration of database changes

**Objective**: To be able to apply database changes automatically.


**Software**: DBDeploy

## What you will learn:

* Managing database changes to your database
* Migrating between different database versions


## Exercise

* Log into your vagrant box

    `vagrant ssh build`

* Checkout the source code from your forked repository https://github.com/your_name/cd_linux.git
* cd into dbdeploy folder `cd `
* run `ant`
* You should see DB changes being applied on HSQL database
* Check the newly created table called test on the database

```
java -jar lib/hsqldb-1.8.0.7.jar --rcFile sqltool.rc local  
sql> select * from test;
sql>   select * from changelog;
sql> \q
```

## Insert data into table using migration

* Create a file named `deltas/002_insert_data.sql` in the with the following content:

```sql
INSERT INTO Test VALUES (6, 'This is simple text');
INSERT INTO Test VALUES (7, 'This is another text');

--//@UNDO

DELETE FROM Test WHERE id IN (6,7);

```

* Run migration using following command

    `ant update-database`

* Verify your data in the test table

```
java -jar lib/hsqldb-1.8.0.7.jar --rcFile sqltool.rc local
sql>   select * from test;
sql>   select * from changelog;
sql> \d
```

> You should see 2 rows inserted into test table and an entry for 2nd migration in changelog table

## Exercise

* Add another column in test table.
* Rename a column without affecting the data
