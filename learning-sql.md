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
