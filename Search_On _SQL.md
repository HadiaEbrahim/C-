-- MySQL DATE_FORMAT() Function
--Format Date
```sql
SELECT DATE_FORMAT("2017-06-15", "%Y"); 
```
-- Run: 2017
-- Stntax 
DATE_FORMAT(date, format) 
-- هي المسؤوله عن تحويل شكل التاريخ الخام الي تنسيق سهل القراءه

%a	Abbreviated weekday name (Sun to Sat)

%b	Abbreviated month name (Jan to Dec)

%c	Numeric month name (0 to 12)

%D	Day of the month as a numeric value, followed by suffix (1st, 2nd, 3rd, ...)

%d	Day of the month as a numeric value (01 to 31)

%e	Day of the month as a numeric value (0 to 31)

%f	Microseconds (000000 to 999999)

%H	Hour (00 to 23)

%h	Hour (00 to 12)

%I	Hour (00 to 12)

%i	Minutes (00 to 59)

%j	Day of the year (001 to 366)

%k	Hour (0 to 23)

%l	Hour (1 to 12)

%M	Month name in full (January to December)

%m	Month name as a numeric value (00 to 12)

%p	AM or PM

%r	Time in 12 hour AM or PM format (hh:mm:ss AM/PM)

%S	Seconds (00 to 59)

%s	Seconds (00 to 59)

%T	Time in 24 hour format (hh:mm:ss)

%U	Week where Sunday is the first day of the week (00 to 53)

%u	Week where Monday is the first day of the week (00 to 53)

%V	Week where Sunday is the first day of the week (01 to 53). Used with %X

%v	Week where Monday is the first day of the week (01 to 53). Used with %x

%W	Weekday name in full (Sunday to Saturday)

%w	Day of the week where Sunday=0 and Saturday=6

%X	Year for the week where Sunday is the first day of the week. Used with %V

%x	Year for the week where Monday is the first day of the week. Used with %v

%Y	Year as a numeric, 4-digit value

%y	Year as a numeric, 2-digit value

Examples : 
```sql
SELECT DATE_FORMAT("2020-06-15", "%M %d %Y");
SELECT DATE_FORMAT("2017-06-15", "%W %M %e %Y");
SELECT DATE_FORMAT(BirthDate, "%W %M %e %Y") FROM Employees;
```

_________________________________________________________________________________________________________________________________________________________________
--SQL Aliases
_ طريقه لاعطاء اسم تدليل مؤقت لعمود أو جدول هذا الاسم لا يؤثر علي الاسم في قاعده البيانات وانما هو للسهوله علي القارئ لفهم الجدول او العمود وخاصه ان كان اسمه في الداتا بيز غير مفهوم
1. Column Aliases
A column alias is used to rename a column just for the output of a query. They are useful when:

displaying aggregate data
Making results more readable
Performing calculations

 Syntax:
```sql
SELECT column_name AS alias_name
FROM table_name;
 Example:
SELECT CustomerID AS id
FROM Customer;
```
2. Table Aliases
A table alias is used when you want to give a table a temporary name for the duration of a query.
Table aliases are especially helpful in JOIN operations to simplify queries, particularly when the same table is referenced multiple times (like in self-joins).

 Example:
```sql
SELECT c1.CustomerName, c1.Country
FROM Customer AS c1, Customer AS c2
WHERE c1.Age = c2.Age AND c1.Country = c2.Country;
```
Combining Column and Table Aliases
We want to fetch customers who are aged 21 or older and rename the columns for better clarity. We will use both table and column aliases.

Query:
```sql
SELECT c.CustomerName AS Name, c.Country AS Location
FROM Customer AS c
WHERE c.Age >= 21;
```
________________________________________________________________________________________________________________________________________________________________

LIMIT – Restricting Number of Rows Returned
بتستخدم لكي تحدد عدد الصفوف الي هيرجعها الكويري مثال : جدول بيانات لطلاب الكليه ونريد اخراج الطلاب الاوائل فقط 

How to Limit Rows in a SQL Server?

To limit rows in SQL Server, use the TOP clause in the SELECT statement.
Using the TOP clause in SQL Server, users can limit the number of rows in the results set.

Example1:
```sql
SELECT TOP(2) * FROM Participant 
ORDER BY Percentage DESC;
```
سيقوم بالترتيب ثم اخراج اول صفين

Example 2:
```sql
SELECT TOP(2) * FROM Participant 
WHERE ID != 58 
ORDER BY Percentage;
```
اضافه شرط سيقوم باخراج اول صفين باثتثناء الطالب الي ID=58

TOP : جيد في استخدام جداول البيانات الضخمة 

__________________________________________________________________________________________________________________________________________________________________
Operators Between , in , not in

SQL Between Operator
The SQL BETWEEN operator is used to test whether a value falls within a given range of values (inclusive). The values can be text, date, or numbers. 
It can be used in a SELECT, INSERT, UPDATE or DELETE statement. 
The SQL BETWEEN Condition will return the records where the expression is within the range of value1 and value2.

Syntax:
```sql
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```
Key Features:

Inclusive of both boundary values (value1 and value2).
Simplifies queries when working with continuous ranges.

Example:
```sql
SELECT Name
FROM Emp
WHERE Salary
BETWEEN 30000 AND 45000;
```

SQL IN Operator
IN operator allows us to easily test if the expression matches any value in the list of values.
It is used to remove the need for multiple OR conditions in SELECT, INSERT, UPDATE, or DELETE. We can also use NOT IN to exclude the rows in our list. 
We should note that any kind of duplicate entry will be retained. 

Syntax:
```sql
SELECT column_name(s)
FROM table_name
WHERE column_name IN (list_of_values);
```
Key Features:

Ideal for filtering non-sequential values.
Handles duplicates in the list of values.

Exanple:
```sql
SELECT Name
FROM Emp
WHERE Salary IN (30000, 40000, 25000);
```
Using the NOT Operator with IN
Find the Fname and Lname of all the Employees who has a Salary not equal to 25000 or 30000. 
This query excludes employees with salaries of 25000 and 30000.
The NOT IN clause ensures that all other employees are included in the result set.

Example :
```sql
SELECT Name
FROM Emp
WHERE Salary NOT IN (25000, 30000);
```
____________________________________________________________________________________________________________________________________________________________________

SQL Aggregate Functions

SQL Aggregate Functions allow summarizing large sets of data into meaningful results, making it easier to analyze patterns and trends across many records.
They return a single output value after processing multiple rows in a table.

Perform calculations like totals, averages, minimum or maximum values on data.
Ignore NULL values in most functions except COUNT(*), improving result accuracy.
Work with clauses such as GROUP BY, HAVING and ORDER BY for analysis.

1. Count()
COUNT(*): Counts all rows.
COUNT(column_name): Counts non-NULL values in the specified column.
COUNT(DISTINCT column_name): Counts unique non-NULL values in the column.

Example:
```sql
-- Total number of records in the table
SELECT COUNT(*) AS TotalRecords FROM Employee;

-- Count of non-NULL salaries
SELECT COUNT(Salary) AS NonNullSalaries FROM Employee;

-- Count of unique non-NULL salaries
SELECT COUNT(DISTINCT Salary) AS UniqueSalaries FROM Employee;
```

2. SUM()
It is used to calculate the total of a numeric column.
It adds up all non-NULL values in that column for Example, SUM(column_name) returns sum of all non-NULL values in the specified column.

Exaple:
```sql
-- Calculate the total salary
SELECT SUM(Salary) AS TotalSalary FROM Employee;

-- Calculate the sum of unique salaries
SELECT SUM(DISTINCT Salary) AS DistinctSalarySum FROM Employee;
```

3. AVG()
It is used to calculate average value of a numeric column.
It divides sum of all non-NULL values by the number of non-NULL rows for Example,
AVG(column_name) returns average of all non-NULL values in the specified column.

Example:
```sql
-- Calculate the average salary
SELECT AVG(Salary) AS AverageSalary FROM Employee;

-- Average of distinct salaries
SELECT AVG(DISTINCT Salary) AS DistinctAvgSalary FROM Employee;
```
4. MIN() and MAX()
The MIN() and MAX() functions return the smallest and largest values, respectively, from a column.

Example:
```sql
-- Find the highest salary
SELECT MAX(Salary) AS HighestSalary FROM Employee;

-- Find the lowest salary
SELECT MIN(Salary) AS LowestSalary FROM Employee;
```
