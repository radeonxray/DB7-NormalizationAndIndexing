# DB7-NormalizationAndIndexing
Database Assignment 7

Assignment: https://github.com/datsoftlyngby/soft2019spring-databases/blob/master/assignments/Assignment7.md

Slides: https://github.com/datsoftlyngby/soft2019spring-databases/blob/master/lecture_notes/07_NormalizationAndIndex.ipynb

------ 

### Ex 1

*First Normal Form*

First normal form might be considered voilated in the given example, due to customerName being presented as one complete column, and not separat colums for firstName and LastName.

Secondly, the same logic could be applied to contactName and repName.

*Second Normal Form*

Second Normal Form is violated clearly, due to information regarding the rep being shown directly int he table. This should have ben rectified by only mentioning either the reps name or rep number, and linking to another table.


*Third Normal Form*
As mentioned in *Second Normal Form*, there are several columns that not dependent on the primary-key, since reps have been tied directly to customer.


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

-----

### Ex 4

***[Not Completed]***

-----

