# WordPress

In the following I want to practice some of the previous learned skills to set up a running development environment with a WordPress installation.

## 1. Minimal vagrant file + direct installation
As a starting point I want to use the minimal `Vagrantfile` namely
``` vagrant
Vagrant.configure("2) do | config |
  config.vm.box = "hashicorp/bionic64"
end
```
and manually install all the necessary software e.g. a full LAMP stack.

### Resources
* https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-ubuntu-18-04
* https://www.vagrantup.com/docs/networking/basic_usage
* https://wordpress.org/support/article/how-to-install-wordpress/
* https://wordpress.org/support/article/creating-database-for-wordpress/


### Installing the LAMP stack
First of all we have to install the LAMP stack. This is done by a simple set of `apt` commands
``` bash
sudo apt update
sudo apt install apache2
sudo apt install mysql-server
sudo apt install php libapache2-mod-php php-mysql
```
With our current `Vagrantfile` setup we are only forwarding part 22 (SSH) to our host machine. To also forward port 80, e.g. HTTP, to the host machine, we have to modify the `Vagrantfile` on the local machine in the following way
``` vagrant
Vagrant.configure("2) do | config |
  config.vm.box = "hashicorp/bionic64"
  config.vm.network "forward_port", guest:80, host:8888
end
```
Now we can visit the default Apache page on `localhost:8888`.

### Creating a database for WordPress

To create a MySQL database for WordPress to be used, we have to issue the following commands
1) Enter the MySQL prompt
```bash
mysql -u adminusername -p
```
2) Create the database
``` mysql
CREATE DATABASE databasename;
```
3) Create a user and give the permissions to interact with the database to the user
``` mysql
GRANT ALL PRIVILIGES ON databasename.* TO "wordpressusername"@"localhast" IDENTIFIED BY "password";
```
4) Update the privileges
``` mysql
FLUH PRIVILEGES
```
In the above example a `databasename`, a `wordpressusername` and a `password` have to been chosen accordingly.

### Prepare WordPress for the installation process
To install WordPress we have to download the WordPress files using
``` bash
wget https://wordpress.org/latest.tar.gz
tar -xzvf latest.tar.gz
```
Next, we have to move the extracted files to `/var/www/html`, where the files are, that are serverd by our Apache server. To this end, we use
``` bash
cp -R /wordpress/* /var/wwww/html/
```
At last, we have to prepare the wp-config.php file. To this end, we create the file using the sample file using `cp wp-config-sample.php wp-config.php`. Now, we have to fill in our previously defined values for `databasename`, `wordpressusername` and `password` in the newly created `wp-config.php` file.
At last we have to enter the secret key values. Those can be created automatically using this [webpage](https://api.wordpress.org/secret-key/1.1/salt/).
Now, we can start the initialization of the WordPress blog by navigating to `localhost:8888/wp-admin/install.php`.


### (Optional) Install CiviCRM
For my personal purpose I would like to install CiviCRM. To this end we need to download the zip file 
