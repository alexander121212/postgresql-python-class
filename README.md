# postgresql-python-class


###Prerequisites

To work with this tutorial, we must have Python language, PostgreSQL database and psycopg2 language binding installed on our system.
$ sudo apt-get install postgresql
On an Ubuntu based system we can install the PostgreSQL database using the above command.
$ sudo update-rc.d -f postgresql remove
 Removing any system startup links for /etc/init.d/postgresql ...
   /etc/rc0.d/K21postgresql
   /etc/rc1.d/K21postgresql
   /etc/rc2.d/S19postgresql
   /etc/rc3.d/S19postgresql
   /etc/rc4.d/S19postgresql
   /etc/rc5.d/S19postgresql
   /etc/rc6.d/K21postgresql
If we install the PostgreSQL database from packages, it is automatically added to the start up scripts of the operating system. If we are only learning to work with the database, it is unnecessary to start the database each time we boot the system. The above command removes any system startup links for the PostgreSQL database.

$ /etc/init.d/postgresql status
Running clusters: 9.1/main

$ service postgresql status
Running clusters: 9.1/main 
We check if the PostgreSQL server is running. If not, we need to start the server.

$ sudo service postgresql start
 * Starting PostgreSQL 9.1 database server        [ OK ]
On Ubuntu Linux we can start the server with the service postgresql start command.

$ sudo service postgresql stop
[sudo] password for nester: 
 * Stopping PostgreSQL 9.1 database server        [ OK ] 
We use the service postgresql stop command to stop the PostgreSQL server.

$ sudo apt-get install python-psycopg2
Here we install the psycopg2 module on a Ubuntu system.

$ sudo -u postgres createuser nester
Shall the new role be a superuser? (y/n) n
Shall the new role be allowed to create databases? (y/n) y
Shall the new role be allowed to create more new roles? (y/n) n
We create a new role in the PostgreSQL system. We allow it to have ability to create new databases. A role is a user in a database world. Roles are separate from operating system users. We have created a new user without the -W option, e.g. we have not specified a password. This enables us to connect to a database with this user without password authentication. Note that this works only on localhost.

$ sudo -u postgres createdb testdb -O nester
The createdb command creates a new PostgreSQL database with the owner nester.

## Usage

To start using class you need to import the class and initialize with 4 required parameters: host, user, password, database
```python
from postgresqlclass import PostgresqlDBManagementSystem
db = PostgresqlDBManagementSystem(host='localhost', user='nester', password='parapapam', database='testdb')
```
### Create method
For creating table you could put in args name of table and it's struct.
```python
db.create_table('Auto', '(id INT PRIMARY KEY, name TEXT, price INT, mark TEXT)')
```
### Select method

If you want to get information from one specific table and use one condition, you could use select method where args argument is for referencing the columns you need to obtain.

```python
db.select('car', conditional_query, 'id_car', 'car_text', car_make='nissan')
```
###Insert method

Inserting data is really simple and intuitive, where we are going to reference the column and the values

  result = connect_msyql.insert('car', car_make='ford', car_model='escort', car_year='2005')
Result: The function return the last row id was inserted.

### Update method

To update data just needs the table, conditional query and specify the columns you want update

```python
db.insert('Auto', id=1, name='audi', price='300000', mark='a6')
db.insert('Auto', id=2, name='BMW', price='400000', mark='x5')
```

###Delete method

Delete data is really simple like insert, just reference the column as condition and table.
```python
db.delete('Auto', 'name=%s', 'BMW')
```
