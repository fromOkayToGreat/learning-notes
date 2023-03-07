# Learning SQL

Increase profitability and realize opportunities by using SQL to analyze data.

What is data? It is the plural of Datum. A datum is a single piece of information. Data is a collection of facts from observations or measurements.

Database is a collection of data organized in various ways.

Table is a collection of data organized in rows and columns.

Rows are records. Columns represent specific attributes of that data.

SQL: Structured Query Language is a language used to communicate with a database.

SELECT statement us the to specify the columns that we want to get from the table and include in the results.

The software used to compose SQL statements is called a relational database management system (RDBMS).

SQL Comment

Plain or natural way to describe a query. There are two types of comments in SQL:

-   Single line comments start with two dashes (--) and end at the end of the line.
-   Multi-line comments start with a forward slash and an asterisk (/_) and end with an asterisk and a forward slash (_/).

```sql

-- This is a single line comment

/* This is a multi-line comment and how to write a comment in SQL

CREATED BY: fromOkayToGreat
CREATED DATE: MM/DD/YYYY
MODIFIED BY: fromOkayToGreat
MODIFIED DATE: MM/DD/YYYY
DESCRIPTION: This is a multi-line comment and how to write a comment in SQL
 */

```

### Considerations for writing a SQL statement or script

What table within the database are we requesting data from?
What fields within that table are we interested in?
Do we want to exclude any data or filter or omit any range or time period?
What does our query do?

## Aliases

An alias is a way to improve the communication of a query result to a business audience by allowing us to rename a column to a more appropriate business name. Use the AS keyword to create an alias. The alias can be enclosed in square brackets or single quotes if it contains spaces. Otherwise, the alias can be written without quotes.

```sql

SELECT
    first_name AS [Customer First Name],
    last_name AS 'Customer Last Name',
    email AS EMAIL
FROM
    customers;

```

### ORDER BY

The ORDER BY clause is used to sort the result-set in ascending or descending order. The ORDER BY clause sorts the records in ascending order by default. To sort the records in descending order, use the DESC keyword.

```sql

SELECT
    first_name AS [Customer First Name],
    last_name AS 'Customer Last Name',
    email AS EMAIL
FROM
    customers
ORDER BY
    first_name DESC;

```

### LIMIT

The LIMIT clause is used to specify the maximum number of records the query will return.

```sql

SELECT
    first_name AS [Customer First Name],
    last_name AS 'Customer Last Name',
    email AS EMAIL
FROM
    customers
ORDER BY
    first_name DESC
LIMIT 10;

```

### WHERE

The WHERE clause is used to filter records. Only the records that fulfill the condition are returned.

```sql

SELECT
    first_name AS [Customer First Name],
    last_name AS 'Customer Last Name',
    email AS EMAIL
FROM
    customers
WHERE
    first_name = 'John';

```

### % wildcard

The % wildcard represents zero, one, or multiple characters.

```sql

SELECT
    first_name AS [Customer First Name],
    last_name AS 'Customer Last Name',
    email AS EMAIL
FROM
    customers
WHERE
    first_name LIKE 'J%';

```

### \* wildcard

(\*) is a wildcard character that is used as a shorthand for selecting all columns in a table. When used in the SELECT statement, the asterisk tells the database to return all columns from the table that is being queried.

### CASE (if then else)

The CASE statement is used to create different outputs (usually in the SELECT statement). It is similar to an IF-THEN-ELSE statement in other programming languages.

```sql

SELECT
	InvoiceDate,
	BillingAddress,
	BillingCity,
	total,
    CASE
        WHEN total < 2.00 THEN 'Baseline'
        WHEN total BETWEEN 2.00 AND 6.99 THEN 'Low'
        WHEN total BETWEEN 7.00 AND 15.00 THEN 'Target'
        ELSE 'Top'
    END AS PurchaseType
FROM
	Invoice
ORDER BY
	PurchaseType

```

## JOINS

### INNER JOIN

An INNER JOIN only returns matching records. Any unmatched data from either table is ignored.

### LEFT OUTER JOIN

A LEFT OUTER JOIN combines all the records from the left table with any matching records from the right table.

### RIGHT OUTER JOIN

A RIGHT OUTER JOIN combines all the records from the right table with any matching records from the left table. **This JOIN is not supported by SQLite.**

## Functions

### Concatenate (||)

The CONCAT function is used to combine two or more columns into a single column.

```sql

SELECT
	FirstName || ' ' ||
	LastName || ' ' ||
	Address || ' ' ||
	City || ' ' ||
	State || ' ' ||
	PostalCode AS MailingAddress
FROM
	Customer
WHERE
	Country = 'USA'

```

### SUBSTR

The SUBSTR function is used to extract a substring from a string. The SUBSTR function takes three arguments: the string, the starting position, and the number of characters to extract.

```sql

SELECT
    PostalCode,
    SUBSTR(PostalCode, 1, 2) AS StateCode
FROM
    Customer
WHERE
    Country = 'USA'

```

### LOWER and UPPER

The LOWER and UPPER function simply take a string of text and convert it to all lowercase or uppercase.

```sql

SELECT
    FirstName,
    UPPER(FirstName) AS FirstNameUpper,
    LOWER(FirstName) AS FirstNameLower
FROM
    Customer

```

### Strftime

Returns the date formatted according to the format string specified in argument first. The second parameter is used to mention the time string and followed by one or more modifiers can be used to get a different result.

```sql

SELECT
    start_date,
    strftime('%Y',start_date) as "Year",
    strftime('%m',start_date) as "Month",
    strftime('%d',start_date) as "Day"
FROM
    job_history;

```

### SUM, AVG, MAX, MIN, COUNT

SUM: This function returns the sum of all the values in a column. For example, if you want to find the total revenue generated by a company, you can use the SUM function on the revenue column.

AVG: This function returns the average value of a column. For example, if you want to find the average salary of employees in a company, you can use the AVG function on the salary column.

MAX: This function returns the maximum value in a column. For example, if you want to find the highest sales amount in a company, you can use the MAX function on the sales column.

MIN: This function returns the minimum value in a column. For example, if you want to find the lowest temperature recorded in a city, you can use the MIN function on the temperature column.

COUNT: This function returns the number of rows in a table or the number of non-null values in a column. For example, if you want to find the number of orders placed by customers, you can use the COUNT function on the orders table.

```sql

SELECT
	total,
	SUM(total) AS 'Total Sales',
	AVG(total) AS 'Average Sales',
	MAX(total) AS 'Max Sale',
	MIN(total) AS 'Min Sale',
	COUNT(*) AS 'Sales Count'
FROM
	Invoice

```


## WHERE vs HAVING

The WHERE clause is used to filter rows from a table based on conditions that are applied before any groupings are made. The HAVING clause is used to filter rows based on conditions that are applied after groupings have been made.


## Subqueries

### SELECT subquery

A subquery is a query within a query. A subquery is used to return data that is used in the main query. The subquery is enclosed in parentheses and is placed after the FROM clause.

```sql

SELECT
	InvoiceDate,
	BillingAddress,
	BillingCity,
	Total
FROM
	Invoice
WHERE
	Total < (
		SELECT
			AVG(Total)
		FROM
			Invoice
	)
ORDER BY
	Total DESC

```

