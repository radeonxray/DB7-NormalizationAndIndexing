# DB7-NormalizationAndIndexing
Database Assignment 7

Assignment: https://github.com/datsoftlyngby/soft2019spring-databases/blob/master/assignments/Assignment7.md

Slides: https://github.com/datsoftlyngby/soft2019spring-databases/blob/master/lecture_notes/07_NormalizationAndIndex.ipynb

------ 

### Pre-setup
Remember to `stop` any previous containers that are running on port 3306 

`docker stop [container]`

Command to see containers:

```
docker ps
docker ls
docker container ls --all
```

------
## Setup

#### The Docker Container
Assignment done using Vagrant, Docker and Workbench

Run the following command with Docker to create the container:

`docker run --name my_db7mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=iphone2019 -d mysql`


Access the Docker container:

`docker exec -it my_db7mysql bash`


Within the Docker Container, run the following 2 commands to update the container and download 7zip:

```shell
apt-get update

apt-get install wget p7zip-full -y

apt-get install unzip
```


Download the Data **Heads-up: You might want to start making some coffee while the data is being downloaded**:

```
wget https://archive.org/download/stackexchange/coffee.stackexchange.com.7z

wget http://www.mysqltutorial.org/wp-content/uploads/2018/03/mysqlsampledatabase.zip

wget https://raw.githubusercontent.com/radeonxray/DB-Assignment6/master/CreateTables.sql
```


Extract the Data **Heads-up: You might want to start running a marathon while the data is being extracted**:

```
7z e coffee.stackexchange.com.7z 
unzip mysqlsampledatabase.zip
```

-----

#### Connect to the Database through WorkBench

To connect to the Database through Workbench, make sure you have the latest version of the [MySQL Workbench](https://dev.mysql.com/downloads/workbench/)

My Default information to connect to the Docker Container:

*IP*: `192.168.33.10`

*Port*: `3306`

*User*: `root`

*Password*: `iphone2019`

-----

#### Setup Mysql And The Database 

Start MySQL in the container:

`mysql -u root -piphone2019 --local-infile`

When inside the mysql:

```
source ./CreateTables.sql;
source ./mysqlsampledatabase.sql

use classicmodels;
```




-----

### Ex 1

*First Normal Form*

First normal form might be considered voilated in the given example, due to contactName being presented as one complete column, and not separat colums for firstName and LastName.

Secondly, the same logic could be applied to contactName and repName.

*Second Normal Form*

Second Normal Form is violated clearly, due to information regarding the rep being shown directly int he table. This should have ben rectified by only mentioning either the reps name or rep number, and linking to another table.


*Third Normal Form*
As mentioned in *Second Normal Form*, there are several columns that not dependent on the primary-key, since reps have been tied directly to customer. Since *Second Normal Form* is violated, *Third Normal Form* can never be correct.


-----

### Ex 2

Since we have to look pass using the customerNumber as a unique identifer for this ex., one could suggest a combination of customerName and contactPhone, or customerName and customerAdress, but even then, there might be very rare cases where such combinations could come up multiple times, breaking their uniqueness.

All this being said, none of the columns really qualify to being used as the unqiue identifier, hence we would be breaking *First Normal Form*

-----

### Ex 3

The "keyword" for this ex. is the "where"-clause, which helpes creating "safe" updates. To create theese "safe"-updates, the "where"-clause must be used on specific data that cannot and will not change in the table, such as a unique identifier like a primary key, or in our case, the customerNumber.

An "unsafe" update would be trying to using the "where"-clause in conjunction to search for a customer with "cutstomerName = X" and find a matching phoneNumber with "customerContact = Y". These data values can potentially be changed or altered, making them "unsafe" to use as identifiers.

Updating the phone number for a employee using the "safe" approach thus would be:

```mysql 
UPDATE employees SET repPhone = 85858585 WHERE employees.employeeNumber = ?;
```

On the other hand, a "unsafe" approache would be:

```mysql
UPDATE employees SET repPhone = 85858585 WHERE employees.customerName = ?;
```

As for the repEmail, the following statement will perform a not properly update (unsafe update), because the "where"-clause is used on data that might change:

```mysql
update CustomerOverview set repEmail = “theNewEmail@gmail.com” where customerName = "Signal Gift Stores" and repName = "Leslie Jennings"
```

-----

### Ex 4

***[Not Completed]***

-----

