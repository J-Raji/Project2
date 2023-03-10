# LEMP STACK IMPLEMENTATION(PROJECT2)

## Installing Nano Editor

`sudo apt install nano`
`sudo apt update`

![Image to installed nano](./Images/nano.png)


[]In windows ternimal
`cd downoads`

`ssh -i "my-first-instance.pem" ubuntu@ec2-52-70-123-188.compute-1.amazonaws.com`

![Image to connect instance](./Images/connectinstance.png)

---
## Install NGINX

`sudo apt update`
`sudo apt install nginx`

![Image to installed nginx](./Images/nginx.png)

---
## Nginx status

`sudo systemctl status nginx`

![Image to status nginx](./Images/NGINXStat.png)

----
## Launch localhost

`curl http://localhost:80`

![Image to launch localhost](./Images/launch.png)

---
## check IP
`curl -s http://169.254.169.254/latest/meta-data/public-ipv4`

![Image to check ip](./Images/checkip.png)


---
## install mysql server

`sudo apt install mysql-server`

![Image to mysqlserver installed](./Images/mysqlserver.png)

---
## open mysql server
`sudo mysql`
![Image to mysqlserver log](./Images/mysqlserver.PNG)

---
## install mysql server

`sudo apt install mysql-server`

![Image to mysqlserver installed](./Images/mysqlserver.png)

---
# INSTALL PHP

`sudo apt install php-fpm php-mysql`

![Image to PHP two packages installed](./Images/php2package.png)

----
## connect nginx with php

`sudo mkdir /var/www/projectLEMP`
`sudo chown -R $USER:$USER /var/www/projectLEMP`
`sudo nano /etc/nginx/sites-available/projectLEMP`

#/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}

Here’s what each of these directives and location blocks do:

---
>To save
Type CTRL+X and
Then Y
ENTER
--
Error found,resolved by clearing "Here’s what each of these directives and location blocks do:"

`sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`
`sudo systemctl status nginx`
`sudo systemctl reload nginx`

![Image to nginx with php](./Images/nginxinnano.png)

---
## open in browser
`sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html`

![Image to open in browser](./Images/nginxsite.png)

---

## open NGINX using IP address
 	[NGINX Site](http://52.70.123.188:80)

![Image to nginx view](./Images/nginxview.png)

---
## PHP WITH NGINX TEST
`sudo nano /var/www/projectLEMP/info.php`
--
<?php
phpinfo();
--

![Image to installed nginx](./Images/nginx.png)

---
## Nginx status
`sudo systemctl status nginx`

![Image to status nginx](./Images/NGINXStat.png)

----

## RETRIEVING DATA FROM MYSQL USING PHP

`sudo mysql`

`mysql> CREATE DATABASE `example_database`;`

`mysql>  CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';`
`mysql> GRANT ALL ON example_database.* TO 'example_user'@'%';`

![Image to create database](./Images/creatdb.png)

----
## Checking with password

`mysql -u example_user -p`

![Image to log in](./Images/passmysql.png)

----
## show database
`mysql -u example_user -p`
![Image to view database](./Images/showdb.PNG)

----
## Blocker error while granting privilege to emample_user
ERROR 1142

## Resolve with 

`CREATE USER 'example_user'@'localhost' IDENTIFIED BY 'password';`
`GRANT ALL ON example_database.* TO 'example_user'@'localhost';`

![Image to Error 1142 resolved](./Images/Blkerror1142.png)

------------------

## Creating DAtabase and Table

`CREATE DATABASE 'example_database';
--
`CREATE TABLE example_database.todo_list (
item_id INT AUTO_INCREMENT,
content VARCHAR(255),
PRIMARY KEY(item_id)
);`

![Image to create db and tbl](./Images/createdb-tbl.png)

----
## Insert into table

`INSERT INTO example_database.todo_list (content) VALUES ("My first important item");`
`INSERT INTO example_database.todo_list (content) VALUES ("My second important item");`
`INSERT INTO example_database.todo_list (content) VALUES ("My third important item");`
`INSERT INTO example_database.todo_list (content) VALUES ("My fourth important item");`

## show content of table

`SELECT * FROM example_database.todo_list;`

![Image to show content](./Images/insert-show.png)

## Insert into nano file

`nano /var/www/projectLEMP/todo_list.php`

## Edit file

`<?php
$user = "example_user";
$password = "password";
$database = "example_database";
$table = "todo_list";

try {
  $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
  echo "<h2>TODO</h2><ol>";
  foreach($db->query("SELECT content FROM $table") as $row) {
    echo "<li>" . $row['content'] . "</li>";
  }
  echo "</ol>";
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}`
### Save

CTRL+X then yes.enter

## Launch Site

[Nano file link] http://18.212.182.33/todo_list.php

![Image to nano site](./Images/insert-show.png)
