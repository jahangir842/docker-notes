# redmine-docker-mariadb
*******************************************************************
************ Redmine docker installation with mariadb *************
*******************************************************************


Steps:
1.  Create directories for persistent data:
    
    `mkdir redmine_data redmine_plugin mariadb_data`

2.  Start the containers using Docker Compose:
    
    `sudo docker-compose up -d`

3.  Access Redmine in your web browser:

Open your web browser and go to http://localhost:3000. You should see the Redmine setup page.

4.    Configure Redmine:

Follow the on-screen instructions to configure Redmine. When prompted for the database configuration, use the following:

    Database adapter: MySQL
    Database host: db
    Database name: redmine
    Database username: root
    Database password: your_mysql_root_password_here

Complete the setup process, and you should have Redmine running with MySQL on Docker.

Note: Make sure to replace placeholders like your_mysql_password_here and your_mysql_root_password_here with your actual passwords. Also, consider using more secure passwords in a production environment.

*************************************************
****************** Volumes **********************
*************************************************

Redmine path: 
    /usr/src/redmine/plugins
    /usr/src/redmine/files

Redmine path: 
    /var/lib/mysql
