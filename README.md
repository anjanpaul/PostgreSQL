## Step 1 — Installing PostgreSQL

To install PostgreSQL, first refresh your server’s local package index:
```
sudo apt update

```

Then, install the Postgres package along with a -contrib package that adds some additional utilities and functionality:

```
sudo apt install postgresql postgresql-contrib

```
Ensure that the service is started:

```
sudo systemctl start postgresql.service

```

## Step 2 — Using PostgreSQL Roles and Databases
By default, Postgres uses a concept called “roles” to handle authentication and authorization. These are, in some ways, similar to regular Unix-style users and groups.

Upon installation, Postgres is set up to use ident authentication, meaning that it associates Postgres roles with a matching Unix/Linux system account. If a role exists within Postgres, a Unix/Linux username with the same name is able to sign in as that role.

The installation procedure created a user account called postgres that is associated with the default Postgres role. There are a few ways to utilize this account to access Postgres. One way is to switch over to the postgres account on your server by running the following command:

```
sudo -i -u postgres

```

Then you can access the Postgres prompt by running:

```
psql

```

This will log you into the PostgreSQL prompt, and from here you are free to interact with the database management system right away.

To exit out of the PostgreSQL prompt, run the following:

```
\q

```
This will bring you back to the postgres Linux command prompt. To return to your regular system user, run the exit command:

```
exit

```

Another way to connect to the Postgres prompt is to run the psql command as the postgres account directly with sudo:

```
sudo -u postgres psql

```

This will log you directly into Postgres without the intermediary bash shell in between.

Again, you can exit the interactive Postgres session by running the following:

```
\q

```
## Step 3 — Creating a New Role

If you are logged in as the postgres account, you can create a new role by running the following command:

```
createuser --interactive

```
If, instead, you prefer to use sudo for each command without switching from your normal account, run:

```
sudo -u postgres createuser --interactive

```
Either way, the script will prompt you with some choices and, based on your responses, execute the correct Postgres commands to create a user to your specifications.

```
Output
Enter name of role to add: sammy
Shall the new role be a superuser? (y/n) y

```
====================================================================================

## Creating user, database and adding access on PostgreSQL

As the default configuration of Postgres is, a user called postgres is made on and the user postgres has full superadmin access to entire PostgreSQL instance running on your OS.

```
sudo -u postgres psql

```

The above command gets you the psql command line interface in full admin mode.

In the following commands, keep in mind the < angular brackets > are to denote variables you have to set yourself. In the actual command, omit the <>

## Creating user

```
 sudo -u postgres createuser <username>

```

## Creating Database

```
sudo -u postgres createdb <dbname>

```

## Giving the user a password

```
$ sudo -u postgres psql
psql=# alter user <username> with encrypted password '<password>';

```

## Granting privileges on database

```
psql=# grant all privileges on database <dbname> to <username> ;

```

And yeah, that should be pretty much it !

## Doing purely via psql

Your OS might not have the createuser or createdb binaries, or you may, for some reason want to do it purely via psql, then these are the three magic commands —

```
CREATE DATABASE yourdbname;
CREATE USER youruser WITH ENCRYPTED PASSWORD 'yourpass';
GRANT ALL PRIVILEGES ON DATABASE yourdbname TO youruser;

```





