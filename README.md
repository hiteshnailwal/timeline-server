# TimelineServer

This server is created with expressJS version 4.17.1 & okta auth SSO.
The actual URL of total steps of development are here in
`https://developer.okta.com/blog/2019/08/16/angular-mysql-express`

## Setting up server

To create the Express server, navigate into a directory of your choice and create a new folder called `timeline-server`. Open a terminal in this directory and initialize the Node project using npm.

`npm init`

Answer all the questions using the default answer and when asked about the entry point, set it to `src/index.js`. Next, install some libraries you will need.

`npm install --save-exact express@4.17.1 cors@2.8.5 mysql@2.17.1`

## Running the server

Run `node src/index.js` by opening the terminal in the project directory.
You might see an error when you run this command.
To fix the error, log into MySQL and execute the following SQL
(where password is the value you used for your password):
`ALTER USER 'timeline'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';`

## Setting up MySQL

Install MySQL in your local machine from MySQL website.

Maybe system tell you to install some dependent software for this like .net, sql additional software & etc.

once all done then an applicatio `MySQL Command Line Client` will be visible in your application.

Now open the MySQL command line and create the database that you will use in this tutorial. Log into the database using the MySQL client using the login details of the database administrator.

`$ mysql -u root -p`

The -p option indicates that you are required to supply a password when connecting to the MySQL server. You might not need this option, depending on how the database is set up on your system. You should now see the MySQL command line prompt.

`mysql>`

Create a new database and switch into it by using the following command.

`create database timeline;`
`use timeline;`

Next, create a user associated with this database. It is always a good idea to have separate users for each database on the system. The following commands will create the user and grant them all permissions on the timeline database.

`create user 'timeline'@'localhost' identified by 'password';`
`grant all on timeline.* to 'timeline'@'localhost';`

In the first line, replace password with a more complex password. The rest of this tutorial assumes you used “password”, so if you change it, please make sure and change it in all the code snippets below.

Now you are ready to create the events table in the new database by specifying the data schema.

`create table events (id INT AUTO_INCREMENT, owner VARCHAR(255) NOT NULL, name VARCHAR(255) NOT NULL, description TEXT, date DATE, PRIMARY KEY (id), INDEX (owner, date));`

## Setting up OKTA

signup or create an OKTA account.

After completing your registration you will see your Okta dashboard.

To create a new application, select the Applications link in the top menu and click on the green Add Application button. Next, you will see a screen with several options. Select Single-Page App and click Next.

The next screen lets you edit the application settings. For the client you will use Angular, so make sure that the base URI points to `http://localhost:4200/`. You will also need to set the Login Redirect URI to `http://localhost:4200/implicit/callback`, where the user will be redirected after a successful login. After you click the Done button you will see a screen with a client ID you will need below.

`npm install --save-exact express-bearer-token@2.4.0 @okta/jwt-verifier@1.0.0`

