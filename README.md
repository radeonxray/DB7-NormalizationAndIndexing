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

-----

### Ex 3

-----

### Ex 4

-----

### Ex 5
