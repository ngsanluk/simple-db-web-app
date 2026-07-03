# Building a Simple Database Web Application

![](./images/banner.jpg)

This page gives you a step-by-step guide to starting a simple MySQL database web application using Node.js and Express. By the end of this guide, you will have a basic web application that can perform CRUD (Create, Read, Update, Delete) operations on a MySQL database.

# Installing Docker Desktop

Using Docker Desktop is the easiest way to get started with MySQL. Docker allows you to run applications in containers, which are lightweight and portable.

Click the link below to download and install Docker Desktop for your operating system:

[Docker Desktop Download](https://www.docker.com/products/docker-desktop/)

Once installed, start Docker Desktop from your Apps List. You can verify that Docker is running by opening PowerShell (for Windows) or Terminal (for Mac) and typing:

```
docker ps
```

If you see terminal outputs like below, it measns Docker is running successfully:

```
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

While if you see an error message like below, it means Docker is not running:

```
failed to connect to the docker API at  ...
```

# Starting a MySQL Database in Docker

Run the following command in your terminal to start a MySQL database container in background:

```
docker run --name docker-mysql -e MYSQL_ROOT_PASSWORD=12345678 -p 3306:3306 -d mysql
```

Type `docker ps` again to verify that the MySQL container is running. You should see an output similar to this:

```
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                    NAMES
d1f3e5c6b7a8   mysql     "docker-entrypoint.s…"   10 seconds ago   Up 9 seconds    0.0.0.0:3306->3306/tcp   docker-mysql
```

# Download and Start MySQL Workbench

You've just started a MySQL database in Docker. Now, you need a clienttool to connect and manage your database. MySQL Workbench is a popular choice for this purpose.

![](https://www.mysql.com/common/images/products/MySQL_Workbench_Mainscreen_Windows.gif)

[Download MySQL Workbench](https://www.mysql.com/products/workbench/)

You can also connect by using the command line tool `mysql` that comes with MySQL.

First you have to connect to the container running MySQL.

```
docker exec -it docker-mysql bash
```

Then run the following command to start sql client and connect to the MySQL server:

```
mysql -h localhost -u root -p
```

You have to input the password you set when starting the MySQL container, which is `12345678` in this case.

# Frequent Used MySQL Commands

MySQL CLI commands are case-insensitive, but it is a good practice to write them in uppercase. Here are some frequently used commands. These commands are quite self-explanatory, but you can find more details in the [MySQL Documentation](https://dev.mysql.com/doc/).

**Note:** The semicolon `;` at the end of each command is required to execute the command.

```
SHOW DATABASES;
```

```
CREATE DATABASE mydb;
```

```
USE mydb;
```

```
SHOW TABLES;
```

# Creating a Table

Run the followng commands to create a table named `todos`

```
DROP TABLE IF EXISTS `todos`;
CREATE TABLE `todos` (
  `id` int NOT NULL AUTO_INCREMENT,
  `todo` varchar(50) NOT NULL,
  `completed` int DEFAULT '0',
  PRIMARY KEY (`id`),
  UNIQUE KEY `id_UNIQUE` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=11 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

If you run `SHOW TABLES;` command again, you should see the `todos` table listed.

# Run the following command to insert some sample data into the `todos` table.

```
INSERT INTO `todos`
VALUES
(1,'Task 1 ...',1),
(2,'Task 2 ...',1),
(3,'Task 3 ...',1),
(4,'Task 4 ...',0),
(5,'Task 5 ...',0),
(6,'Task 6 ...',0),
(7,'Task 7 ...',0),
(8,'Task 8 ...',0),
(9,'Task 9 ...',0),
(10,'Task 10 ...',0);
```

# Run these SQL statements to verify that the data has been inserted correctly.

```
SELECT * FROM `todos`;
```

```
SELECT * FROM `todos` WHERE `completed` = 1;
```

```
SELECT * FROM `todos`  WHERE `completed` = 0;
```

You can also practice updating and deleting records in the `todos` table using the following commands:

```
UPDATE `todos` SET `completed` = 1 WHERE `id` = 4;
```

```
DELETE FROM `todos` WHERE `id` = 10;
```

Or to insert more new records into the `todos` table:

```
INSERT INTO `todos` (`todo`, `completed`) VALUES ('Task 11 ...', 0);
```
