# TestLink Docker Compose

This little project aimed to make the setup of [TestLink](http://testlink.org) a breeze - but did not succeed. It uses [Docker Compose](https://docs.docker.com/compose/) to set up the application and database.

## Installation

Make sure you have [Docker installed](https://docs.docker.com/install/) and it is working.

### Change credentials
Before launching the containers you may want to change the root password and user credentials in `docker-compose.yml`. Please make sure to use the right credentials in the later step when setting up the database configuration in the TestLink installation.

### Launching containers
First we have to bring up the containers calling
```shell
docker-compose up
```

### Set-up TestLink
Once all containers are up, go to <localhost:5001> to start the installation workflow.

1. Click on "New Installation"
2. Read through the license and check "I agree to the terms set out in this license."
3. Click "Continue"
4. Scroll to the bottom of the "Verification of System and configuration requirements" and click "Continue"
5. Change the database host to match the `docker-compose.yml`. By default the database host is `db:3306`.
6. Provide the root credentials for the database admin login and password. By default this is `root` for database admin login and `test` for database admin password.
7. Set the TestLink DB login and password. Make sure to remember the credentials to complete the installation later on.
8. Click on "Process TestLink Setup!"

The installation via the guide is now complete.

### Complete database setup

We now need to enable the connection to the database. Go to <http://localhost:8080> to launch the *Adminer*.

1. Use `root` for the Username
2. Enter the root password as configured in `docker-compose.yml`. By default this is `test`.
3. Enter `testlink` as Database
4. Click on "Login"
5. Click on "Priviledges"
6. Click on "Create user"
7. Enter the username and password that you provided in step 7. to setup TestLink DB.
8. Check the options SELECT, INSERT, UPDATE, and DELETE for Table.
9. Click "Save"

Alternatively one can also execute the following SQL command directly to skip steps 5-9:

```sql
CREATE USER '<username>'@'%' IDENTIFIED BY '<password>';
GRANT DELETE, INSERT, SELECT, UPDATE ON `testlink`.* TO 'testlink'@'%'
```

where `<username>` and `<password>` are the credentials provided in step 7. to setup the TestLink DB that need to be replaced.

### Completing installation

Follow the instructions given by TestLink