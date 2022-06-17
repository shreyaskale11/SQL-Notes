# SQL-Notes


What is the difference between SQL and MySQL?

SQL is a standard language which stands for Structured Query Language based on the English language
SQL is the core of the relational database which is used for accessing and managing database

MySQL is a database management system.
MySQL is an RDMS (Relational Database Management System) such as SQL Server, Informix etc.


What are the different subsets of SQL?
- Data Definition Language (DDL) – It allows you to perform various operations on the database such as CREATE, ALTER, and DELETE objects.
- Data Manipulation Language(DML) – It allows you to access and manipulate data. It helps you to insert, update, delete and retrieve data from the database.
- Data Control Language(DCL) – It allows you to control access to the database. Example – Grant, Revoke access permissions.
### (DDL)

https://social.technet.microsoft.com/wiki/contents/articles/34477.sql-server-commands-dml-ddl-dcl-tcl.aspx
https://www.ibm.com/docs/en/i/7.1?topic=language-creating-altering-materialized-query-table

![image](https://user-images.githubusercontent.com/71918814/174217014-f99f7179-ce57-4dab-876a-68e05563281c.png)

Self join
```
SELECT A.CustomerName AS CustomerName1, B.CustomerName AS CustomerName2, A.City
FROM Customers A, Customers B
WHERE A.CustomerID <> B.CustomerID
AND A.City = B.City
ORDER BY A.City;
```
Inner Join
Then, we can create the following SQL statement (that contains an INNER JOIN), that selects records that have matching values in both tables:
```
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers
ON Orders.CustomerID=Customers.CustomerID;
SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName
FROM ((Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID)
INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID);
```
SQL LEFT JOIN
```
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID
ORDER BY Customers.CustomerName;
```
SQL FULL OUTER JOIN
```
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
FULL OUTER JOIN Orders ON Customers.CustomerID=Orders.CustomerID
ORDER BY Customers.CustomerName;
```

The UNION operator selects only distinct values by default. To allow duplicate values, use UNION ALL
```
SELECT City FROM Customers
UNION
SELECT City FROM Suppliers
ORDER BY City;
```
Note: If some customers or suppliers have the same city, each city will only be listed once, because UNION selects only distinct values. Use UNION ALL to also select duplicate values!


The HAVING clause was added to SQL because the WHERE keyword cannot be used with aggregate functions.
Various Aggregate Functions
1) Count()
2) Sum()
3) Avg()
4) Min()
5) Max()
```
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5
ORDER BY COUNT(CustomerID) DESC;
```

Exists
The EXISTS operator is used to test for the existence of any record in a subquery.

The EXISTS operator returns TRUE if the subquery returns one or more records.
```
SELECT SupplierName
FROM Suppliers
WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price < 20);
```
All Any
https://www.w3schools.com/sql/sql_any_all.asp

The SELECT INTO statement copies data from one table into a new table.
```SELECT * INTO CustomersBackup2017 IN 'Backup.mdb'
FROM Customers;
SELECT Customers.CustomerName, Orders.OrderID
INTO CustomersOrderBackup2017
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```
SQL INSERT INTO SELECT 


Over 
PARTITION BY defines the groups into which the rows are divided
```
SELECT sale_day, sale_time,
       branch, article, quantity, revenue,
       SUM(quantity) OVER (PARTITION BY article) AS total_units_sold
FROM   sales
```


















