# SQL

## What is a Database?

A database is an organized collection of data., Database can be stored in different ways.

## Database Management System(DBMS)

A special software program that helps users create and maintain a database

- Makes it easy to manage large amount of information
- Handles security
- Backups
- Importing/Exporting Data
- Concurrency
- Interacts with software applications

## Database Types

**Relational Databases (SQL)**

- Organize data into one or more tables
    - Each Table has columns and rows
    - A unique key identifies each row
- **Relational Database Management Systems(RBDMS)**
    - Helps users create and maintain a relational Database
    - mySQL, Oracle, PostgreSQL, mariaDB

**Non-Relational Databases (NoSQL)**

- Organize data is anything but a traditional table
    - Key-Value stores
    - Documents(Json, xml, etc)
    - Graphs
    - Flexible tables
- **Non-Relational Database Management Systems(NRBDMS)**
    - Helps users create and maintain a non-relational Database
    - MongoDB, DynamoDB, Apache Cassandra, firebase, etc..

## What is SQL?

**SQL (Structured Query Language)** is a programming language designed for managing data in a **relational database**. 

**SQL** perform C.R.U.D operations, as well as other administrative tasks(user management, security, backup, etc..)

**SQL** has a variety of functions that allow its users to read, manipulate, and change data. 

**SQL** popular with data analysts for a few reasons:

- It's semantically easy to understand and learn.
- Because it can be used to access large amounts of data directly where it's stored, analysts don't have to copy data into other applications.
- Compared to spreadsheet tools, data analysis done in SQL is easy to audit and replicate. For analysts, this means no more looking for the cell with the typo in the formula.

**SQL** is great for performing the types of aggregations that you might normally do in an Excel pivot table—sums, counts, minimums and maximums, etc.—but over much larger datasets and on multiple tables at the same time.

## SQL SELECT

There are two required ingredients in any SQL query: `SELECT` and `FROM`—and they have to be in that order. `SELECT` indicates which columns you'd like to view, and `FROM` identifies the table that they live in.

```sql
SELECT year,
       month

  FROM Database_1
```

If you want to select every column in a table, you can use `*` instead of the column names

If you'd like your results to look a bit more presentable, you can rename columns. For example, if you want the `west` column to appear as `West Region` in the results, you would have to type:

```sql
SELECT west AS West_Region
  FROM DB1
```

## SQL LIMIT

The **limit** restricts how many rows the **SQL** query returns. 

Many analysts use **limits** as a simple way to keep their **queries** from taking too long to return. 

```sql
SELECT *
  FROM DB1
 LIMIT 100
```

## SQL WHERE

The `WHERE` clause is used to filter the data returned by the query.

If you write a `WHERE` clause that filters based on values in one column, you'll limit the results *in all columns* to rows that satisfy the condition. The idea is that each row is one data point or observation, and all the information contained in that row belongs together.

```sql
SELECT *
  FROM DB1
 WHERE month = 1
```

*Note: the clauses always need to be in this order:* `SELECT`, `FROM`, `WHERE`.

## SQL Comparison Operators

The most basic way to filter data is using **comparison operators** on **numerical data** as well as **non-numerical data**.

| Equal to | = |
| --- | --- |
| Not equal to | <> or != |
| Greater than | > |
| Less than | < |
| Greater than or equal to | >= |
| Less than or equal to | <= |

```sql
SELECT *
  FROM DB1
 WHERE west > 30
```

```sql
SELECT *
  FROM tutorial.us_housing_units
 WHERE month_name > 'January'
```

## SQL Arithmetic

 In **SQL** you can only perform arithmetic across columns on values in a given row. To clarify, you can only add values in multiple columns *from the same row* together using `+`—if you want to add values across multiple rows, you'll need to use aggregate functions, which will be covered later.

`+`, `-`, `*`, `/`

```sql
SELECT year,
       month,
       west,
       south,
       west + south AS south_plus_west
  FROM DB1
```

```sql
SELECT year,
month,
west,
south,
west + south - 4 * year AS nonsense_column
FROM DB1
```

## SQL Logical Operators

You’ll likely want to filter data using several conditions—possibly more often than you'll want to filter by only one condition. 

**Logical operators** allow you to use multiple **comparison** operators in one query.

Each **logical operator** is a special snowflake, Here's a quick preview:

- **`LIKE`** allows you to match similar values, instead of exact values.
- **`IN`** allows you to specify a list of values you'd like to include.
- **`BETWEEN`** allows you to select only rows within a certain range.
- **`IS NULL`** allows you to select rows that contain no data in a given column.
- **`AND`** allows you to select only rows that satisfy two conditions.
- **`OR`** allows you to select rows that satisfy either of two conditions.
- **`NOT`** allows you to select rows that do not match a certain condition.

## SQL LIKE

`LIKE` is a **Logical Operator** in SQL that allows you to match on similar values rather than exact ones.

This query will return `"group_name"` starts with "Andrew" and is followed by any number and selection of characters.

```sql
SELECT *
  FROM DB2
 WHERE "group_name" LIKE 'Andrew%'
```

## Wildcards and ILIKE

The `%` used above represents any character or set of characters. In this case, `%` is referred to as a "wildcard." 

In the type of SQL that Mode uses, `LIKE` is case-sensitive, meaning that the above query will only capture matches that start with a capital "A" and lower-case "drew." To ignore case when you're matching values, you can use the `ILIKE` command:

```sql
SELECT *
  FROM DB2
 WHERE "group_name" ILIKE 'andrew%'
```

You can also use `_` (a single underscore) to substitute for an individual character:

```sql
SELECT *
FROM DB2
WHERE artist ILIKE 'dr_ke'
```

## SQL IN

`IN` is a Logical Operator in SQL that allows you to specify a list of values that you'd like to include in the results. 

For example, the following query of data will return results for which the `year_rank` column is equal to one of the values in the list:

```sql
SELECT *
  FROM DB2
 WHERE year_rank IN (1, 2, 3)
```

```sql
SELECT *
  FROM DB2
 WHERE artist IN ('Taylor Swift', 'Usher', 'Ludacris')
```

## SQL BETWEEN

`BETWEEN` is a logical operator in SQL that allows you to select only rows that are within a specific range. It has to be paired with the **`[AND](https://mode.com/sql-tutorial/sql-logical-operators)`** operator. Here's what `BETWEEN` looks like:

```sql
SELECT *
  FROM DB2
 WHERE year_rank BETWEEN 5 AND 10
```

`BETWEEN` includes the range bounds (in this case, 5 and 10) that you specify in the query, in addition to the values between them. So the above query will return the exact same results as the following query:

```sql
SELECT *
  FROM DB@
 WHERE year_rank >= 5 AND year_rank <= 10
```

## SQL IS NULL

`IS NULL` is a Logical Operator in SQL that allows you to exclude rows with missing data from your results.

Some tables contain null values—cells with no data in them at all. In SQL, the implications can be pretty serious. 

You can select rows that contain no data in a given column by using `IS NULL`. 

```sql
SELECT *
  FROM DB2
 WHERE artist IS NULL
```

## SQL AND

`AND` is a Logical Operator in SQL that allows you to select only rows that satisfy two conditions.

```sql
SELECT *
  FROM DB2
 WHERE year = 2012 AND year_rank <= 10
```

```sql
SELECT *
  FROM tutorial.billboard_top_100_year_end
 WHERE year = 2012
   AND year_rank <= 10
   AND "group_name" ILIKE '%feat%'
```

## SQL OR

`OR` is a Logical Operator in SQL that allows you to select rows that satisfy either of two conditions. 

```sql
SELECT *
  FROM DB2
 WHERE year_rank = 5 OR artist = 'Gotye'
```

You can combine `AND` with `OR` using parenthesis. The following query will return rows that satisfy **both** of the following conditions:

```sql
SELECT *
  FROM DB2
 WHERE year = 2013
   AND ("group_name" ILIKE '%macklemore%' OR "group_name" ILIKE '%timberlake%')
```

## SQL NOT

`NOT` is a Logical Operator in SQL that you can put before any conditional statement to select rows for which that statement is false.

```sql
SELECT *
  FROM DB2
 WHERE year = 2013
   AND year_rank NOT BETWEEN 2 AND 3
```

`NOT` is commonly used with `LIKE`

```sql
SELECT *
  FROM DB2
 WHERE year = 2013
   AND "group_name" NOT ILIKE '%macklemore%'
```

`NOT` is also frequently used to identify non-null rows, but the syntax is somewhat special—you need to include `IS` beforehand.

```sql
SELECT *
  FROM DB2
 WHERE year = 2013
   AND artist IS NOT NULL
```

## SQL ORDER BY

The `ORDER BY` clause allows you to reorder your results based on the data in one or more columns.

```sql
SELECT *
  FROM DB2
 ORDER BY artist
```

`ORDER BY` will reorder the results in ascending order by default

If you'd like your results in the opposite order (referred to as descending order), you need to add the `DESC` operator:

```sql
SELECT *
  FROM DB2
 WHERE year = 2013
 ORDER BY year_rank DESC
```

You can also order by multiple columns.

```sql
SELECT *
  FROM DB2
  WHERE year_rank <= 3
 ORDER BY year DESC, year_rank
```

When using `ORDER BY` with a row limit using `LIMIT`, the ordering clause is executed first. This means that the results are ordered **before** limiting to only a few rows.

## Using comments

You can "comment out" pieces of code by adding combinations of characters. 

You can use`--` (two dashes) to comment out everything to the right of them on a given line

```sql
SELECT *  --This comment won't affect the way the code runs
  FROM DB2
 WHERE year = 2013
```

You can also leave comments across multiple lines using `/*` to begin the comment and `*/` to close it:

```sql
/* Here's a comment so long and descriptive that
it could only fit on multiple lines. Fortunately,
it, too, will not affect how this code runs. */
SELECT *
  FROM DB2
 WHERE year = 2013
```

## SQL Aggregate Functions

SQL is excellent at aggregating data

- **`COUNT`** counts how many rows are in a particular column.
- **`SUM`** adds together all the values in a particular column.
- **`MIN`** and **`MAX`** return the lowest and highest values in a particular column, respectively.
- **`AVG`** calculates the average of a group of selected values.

## SQL COUNT

`COUNT` is a SQL Aggregate Function for counting the number of rows in a particular column. 

```sql
SELECT COUNT(*)
  FROM DB3
```

### Counting individual columns

Things start to get a little bit tricky when you want to count individual columns. The following code will provide a count of all of rows in which the `high` column **is not null**.

```sql
SELECT COUNT(high)
  FROM DB3
```

### Counting non-numerical columns

One nice thing about `COUNT` is that you can use it on non-numerical columns:

```sql
SELECT COUNT(date)
  FROM DB3
```

## SQL SUM

`SUM` is a SQL Aggregate Function that totals the values in a given column. Unlike **`[COUNT](https://mode.com/sql-tutorial/sql-count)`**, you can only use `SUM` on columns containing numerical values.

```sql
SELECT SUM(volume)
  FROM DB3
```

An important thing to remember: **aggregators only aggregate vertically**. If you want to perform a calculation across rows, you would do this with simple arithmetic

You don't need to worry as much about the presence of nulls with `SUM` as you would with `COUNT`, as `SUM` treats nulls as 0.

## SQL MIN/MAX

`MIN` and `MAX` are SQL Aggregate Function  that return the lowest and highest values in a particular column.

They're similar to `COUNT` in that they can be used on non-numerical columns. Depending on the column type, `MIN` will return the lowest number, earliest date, or non-numerical value as close alphabetically to "A" as possible. As you might suspect, `MAX` does the opposite—it returns the highest number, the latest date, or the non-numerical value closest alphabetically to "Z."

```sql
SELECT MIN(volume) AS min_volume,
       MAX(volume) AS max_volume
  FROM DB3
```

## SQL AVG

`AVG` is a SQL Aggregate Function that calculates the average of a selected group of values. 

It's very useful, but has some limitations. First, it can only be used on numerical columns. Second, it ignores nulls completely.

```sql
SELECT AVG(high)
  FROM DB3
 WHERE high IS NOT NULL
```

produces the same result as this:

```sql
SELECT AVG(high)
  FROM tutorial.aapl_historical_stock_price
```

There are some cases in which you'll want to treat null values as 0. For these cases, you'll want to write a statement that changes the nulls to 0

## SQL GROUP BY

SQL Aggregate Function like `COUNT`, `AVG`, and `SUM` have something in common: they all aggregate across the entire table. But what if you want to aggregate only part of a table? For example, you might want to count the number of entries for each year.

In situations like this, you'd need to use the `GROUP BY` clause. `GROUP BY` allows you to separate data into groups, which can be aggregated independently of one another.

```sql
SELECT year,
       COUNT(*) AS count
  FROM DB3
 GROUP BY year
```

You can group by multiple columns, but you have to separate column names with commas—just as with **`[ORDER BY](https://mode.com/sql-tutorial/sql-order-by)`**

### Using GROUP BY with ORDER BY

The order of column names in your `GROUP BY` clause doesn't matter—the results will be the same regardless. If you want to control how the aggregations are grouped together, use `ORDER BY`. Try running the query below, then reverse the column names in the `ORDER BY` statement and see how it looks:

```sql
SELECT year,
       month,
       COUNT(*) AS count
  FROM DB3
 GROUP BY year, month
 ORDER BY month, year
```

### Using GROUP BY with LIMIT

There's one thing to be aware of as you group by multiple columns: SQL evaluates the aggregations before the `LIMIT` clause. If you don't group by any columns, you'll get a 1-row result—no problem there. If you group by a column with enough unique values that it exceeds the `LIMIT` number, the aggregates will be calculated, and then some rows will simply be omitted from the results.

## SQL HAVING

The `WHERE` clause doesn't allow you to filter on aggregate columns—that's where the `HAVING` clause comes in:

```sql
SELECT year,
       month,
       MAX(high) AS month_high
  FROM DB3
 GROUP BY year, month
HAVING MAX(high) > 400
 ORDER BY year, month
```

*Note:* `HAVING` *is the "clean" way to filter a query that has been aggregated, but this is also commonly done using a subquery.*

## Query clause order

The order in which you write the clauses is important. Here's the order for everything we've learned so far:

1. `SELECT`
2. `FROM`
3. `WHERE`
4. `GROUP BY`
5. `HAVING`
6. `ORDER BY`

## SQL CASE

The `CASE` statement is SQL's way of handling if/then logic. The `CASE` statement is followed by at least one pair of `WHEN` and `THEN` statements. 

Every `CASE` statement must end with the `END` statement. The `ELSE` statement is optional, and provides a way to capture values not specified in the `WHEN`/`THEN` statements. 

```sql
SELECT player_name,
       year,
       CASE WHEN year = 'SR' THEN 'yes'
            ELSE NULL END AS is_a_senior
  FROM DB4
```

Here's what's happening:

1. The `CASE` statement checks each row to see if the conditional statement—`year = 'SR'` is true.
2. For any given row, if that conditional statement is true, the word "yes" gets printed in the column that we have named `is_a_senior`.
3. In any row for which the conditional statement is false, nothing happens in that row, leaving a null value in the `is_a_senior` column.
4. At the same time all this is happening, SQL is retrieving and displaying all the values in the `player_name` and `year` columns.

### Adding multiple conditions to a CASE statement

You can also define a number of outcomes in a `CASE` statement by including as many `WHEN`/`THEN` statements as you'd like:

```sql
SELECT player_name,
       weight,
       CASE WHEN weight > 250 THEN 'over 250'
            WHEN weight > 200 THEN '201-250'
            WHEN weight > 175 THEN '176-200'
            ELSE '175 or under' END AS weight_group
  FROM DB2
```

In the above example, the `WHEN`/`THEN` statements will get evaluated in the order that they're written. So if the value in the `weight` column of a given row is 300, it will produce a result of "over 250." Here's what happens if the value in the `weight` column is 180, SQL will do the following:

1. Check to see if `weight` is greater than 250. 180 is not greater than 250, so move on to the next `WHEN`/`THEN`
2. Check to see if `weight` is greater than 200. 180 is not greater than 200, so move on to the next `WHEN`/`THEN`
3. Check to see if `weight` is greater than 175. 180 **is** greater than 175, so record "175-200" in the `weight_group` column.

While the above works, it's really best practice to create statements that don't overlap. `WHEN weight > 250` and `WHEN weight > 200` overlap for every value greater than 250, which is a little confusing. A better way to write the above would be:

```sql
SELECT player_name,
       weight,
       CASE WHEN weight > 250 THEN 'over 250'
            WHEN weight > 200 AND weight <= 250 THEN '201-250'
            WHEN weight > 175 AND weight <= 200 THEN '176-200'
            ELSE '175 or under' END AS weight_group
  FROM DB2
```

You can also string together multiple conditional statements with `AND` and `OR` the same way you might in a `WHERE` clause:

```sql
SELECT player_name,
       CASE WHEN year = 'FR' AND position = 'WR' THEN 'frosh_wr'
            ELSE NULL END AS sample_case_statement
  FROM DB2
```

### A quick review of CASE basics:

1. The `CASE` statement always goes in the `SELECT` clause
2. `CASE` must include the following components: `WHEN`, `THEN`, and `END`. `ELSE` is an optional component.
3. You can make any conditional statement using any conditional operator (like **`[WHERE](https://mode.com/sql-tutorial/sql-where)`** ) between `WHEN` and `THEN`. This includes stringing together multiple conditional statements using `AND` and `OR`.
4. You can include multiple `WHEN` statements, as well as an `ELSE` statement to deal with any unaddressed conditions.

### Using CASE with aggregate functions

`CASE`'s slightly more complicated and substantially more useful functionality comes from pairing it with aggregate functions. For example, let's say you want to only count rows that fulfill a certain condition. Since `count` ignores nulls, you could use a `CASE` statement to evaluate the condition and produce null or non-null values depending on the outcome:

```sql
SELECT CASE WHEN year = 'FR' THEN 'FR'
            ELSE 'Not FR' END AS year_group,
            COUNT(1) AS count
  FROM benn.college_football_players
 GROUP BY CASE WHEN year = 'FR' THEN 'FR'
               ELSE 'Not FR' END
```

| year_group | count |
| --- | --- |
| Not FR | 1000 |
| FR | 500 |

Using the `WHERE` clause only allows you to count one condition.

```sql
SELECT COUNT(1) AS fr_count
  FROM benn.college_football_players
 WHERE year = 'FR'
```

Here's an example of counting multiple conditions in one query:

```sql
SELECT CASE WHEN year = 'FR' THEN 'FR'
            WHEN year = 'SO' THEN 'SO'
            WHEN year = 'JR' THEN 'JR'
            WHEN year = 'SR' THEN 'SR'
            ELSE 'No Year Data' END AS year_group,
            COUNT(1) AS count
  FROM DB2
 GROUP BY 1
```

The above query is an excellent place to use numbers instead of columns in the `GROUP By` clause because repeating the `CASE` statement in the `GROUP BY` clause would make the query obnoxiously long. Alternatively, you can use the column's alias in the `GROUP BY` clause like this:

```sql
SELECT CASE WHEN year = 'FR' THEN 'FR'
            WHEN year = 'SO' THEN 'SO'
            WHEN year = 'JR' THEN 'JR'
            WHEN year = 'SR' THEN 'SR'
            ELSE 'No Year Data' END AS year_group,
            COUNT(1) AS count
  FROM DB2
 GROUP BY year_group
```

Combining `CASE` statements with aggregations can be tricky at first. It's often helpful to write a query containing the `CASE` statement first and run it on its own. Using the previous example, you might first write:

```sql
SELECT CASE WHEN year = 'FR' THEN 'FR'
            WHEN year = 'SO' THEN 'SO'
            WHEN year = 'JR' THEN 'JR'
            WHEN year = 'SR' THEN 'SR'
            ELSE 'No Year Data' END AS year_group,
            *
  FROM DB2
```

The above query will show all columns, as well as a column showing the results of the `CASE` statement. From there, you can replace the `*` with an aggregation and add a `GROUP BY` clause. 

```sql
-- Write a query that counts the number of 300lb+ players for each of the following regions: 
-- West Coast (CA, OR, WA),Texas, and Other (everywhere else).
SELECT CASE when state in ('CA','OR','WA') then 'West Coast'
            when state = 'TX' then 'Texas'
            ELSE 'Everyone else' End as regions,
            count(1) as players
  FROM DB2
  where weight >= 300
  group by 1
```

```sql
-- Write a query that calculates the combined weight of all underclass players (FR/SO) in California 
-- as well as the combined weight of all upperclass players (JR/SR) in California.
SELECT CASE when year in ('FR','SO') then 'underclass'
            when year in ('JR','SR') then 'upperclass' end as playersclass,
            sum(weight) as players_weight
  FROM benn.college_football_players
  where state = 'CA'
  group by 1
```

### Using CASE inside of aggregate functions

In the previous examples, data was displayed vertically, but in some instances, you might want to show data horizontally. This is known as "pivoting”.

```sql
SELECT CASE WHEN year = 'FR' THEN 'FR'
            WHEN year = 'SO' THEN 'SO'
            WHEN year = 'JR' THEN 'JR'
            WHEN year = 'SR' THEN 'SR'
            ELSE 'No Year Data' END AS year_group,
            COUNT(1) AS count
  FROM DB2
 GROUP BY 1
```

And re-orient it horizontally:

```sql
SELECT COUNT(CASE WHEN year = 'FR' THEN 1 ELSE NULL END) AS fr_count,
       COUNT(CASE WHEN year = 'SO' THEN 1 ELSE NULL END) AS so_count,
       COUNT(CASE WHEN year = 'JR' THEN 1 ELSE NULL END) AS jr_count,
       COUNT(CASE WHEN year = 'SR' THEN 1 ELSE NULL END) AS sr_count
  FROM DB2
```

It's worth noting that going from horizontal to vertical orientation can be a substantially more difficult problem depending on the circumstances.

```sql
-- Write a query that displays the number of players in each state, with FR, SO, JR, and SR players in separate columns 
-- and another column for the total number of players. Order results such that states with the most players come first.

SELECT state,
       COUNT(CASE WHEN year = 'FR' THEN 1 ELSE NULL END) AS fr_count,
       COUNT(CASE WHEN year = 'SO' THEN 1 ELSE NULL END) AS so_count,
       COUNT(CASE WHEN year = 'JR' THEN 1 ELSE NULL END) AS jr_count,
       COUNT(CASE WHEN year = 'SR' THEN 1 ELSE NULL END) AS sr_count,
       COUNT(1) AS total_players
  FROM benn.college_football_players
 GROUP BY state
 ORDER BY total_players DESC
```

```sql
-- Write a query that shows the number of players at schools with names that start with A through M, 
-- and the number at schools with names starting with N - Z.

Select Count(CASE WHEN full_school_name BETWEEN 'A' AND 'M' THEN 1 ELSE NULL END) as A_to_M_schools,
      COUNT(CASE WHEN full_school_name BETWEEN 'N' AND 'Z' THEN 1 ELSE NULL END) as N_to_Z_schools
FROM DB2

SELECT CASE WHEN school_name < 'n' THEN 'A-M'
            WHEN school_name >= 'n' THEN 'N-Z'
            ELSE NULL END AS school_name_group,
       COUNT(1) AS players
  FROM DB2
 GROUP BY 1
```

## SQL DISTINCT

You can use DISTINCT to select unique values in a particular column.

```sql
SELECT DISTINCT month
  FROM DB3
```

If you include two (or more) columns in a `SELECT DISTINCT` clause, your results will contain all of the unique pairs of those two columns:

```sql
SELECT DISTINCT year, month
  FROM DB3
```

`DISTINCT` can be particularly helpful when exploring a new data set. In many real-world scenarios, you will generally end up writing several preliminary queries in order to figure out the best approach to answering your initial question. Looking at the unique values on each column can help identify how you might want to group or filter the data.

### Using DISTINCT in aggregations

You can use `DISTINCT` when performing an aggregation. You'll probably use it most commonly with the `COUNT` function.

In this case, you should run the query below that counts the unique values in the `month` column.

```sql
SELECT COUNT(DISTINCT month) AS unique_months
  FROM DB3
```

You'll notice that `DISTINCT` goes inside the aggregate function rather than at the beginning of the `SELECT` clause. Of course, you can `SUM` or `AVG` the distinct values in a column, but there are fewer practical applications for them. For `MAX` and `MIN`, you probably shouldn't ever use `DISTINCT` because the results will be the same as without `DISTINCT`, and the `DISTINCT` function will make your query substantially slower to return results.

### DISTINCT performance

It's worth noting that using `DISTINCT`, particularly in aggregations, can slow your queries down quite a bit. 

```sql
-- Write a query that counts the number of unique values in the month column for each year.

SELECT year,
      COUNT(DISTINCT month) AS unique_months
  FROM tutorial.aapl_historical_stock_price
  GROUP BY year
  ORDER BY year
```

```sql
-- Write a query that separately counts the number of unique values in the month column
-- and the number of unique values in the `year` column.

SELECT COUNT(DISTINCT month) AS unique_months,
      COUNT(DISTINCT year) AS unique_years
  FROM tutorial.aapl_historical_stock_price
```

## SQL JOINS

The real power of SQL comes from working with data from multiple tables at once. The tables we’ve been working with up to this point are all part of the same schema in a relational database. The term "relational database" refers to the fact that the tables within it "relate" to one another—they contain common identifiers that allow information from multiple tables to be combined easily.

Let's say we want to figure out which conference has the highest average weight. Given that information is in two separate tables, how do you do that? A join!

```sql
SELECT teams.conference AS conference,
       AVG(players.weight) AS average_weight
  FROM benn.college_football_players players
  JOIN benn.college_football_teams teams
    ON teams.school_name = players.school_name
 GROUP BY teams.conference
 ORDER BY AVG(players.weight) DESC
```

### **Aliases in SQL**

When performing joins, it's easiest to give your table names aliases. `benn.college_football_players` is pretty long and annoying to type—`players` is much easier. You can give a table an alias by adding a space after the table name and typing the intended name of the alias. As with column names, best practice here is to use all lowercase letters and underscores instead of spaces.

### **JOIN and ON**

After the `FROM` statement, we have two new statements: `JOIN`, which is followed by a table name, and `ON`, which is followed by a couple column names separated by an equals sign.

Though the `ON` statement comes after `JOIN`, it's a bit easier to explain it first. `ON` indicates how the two tables (the one after the `FROM` and the one after the `JOIN`) relate to each other. 

The two columns that map to one another, are referred to as "foreign keys" or "join keys." Their mapping is written as a conditional statement:

```sql
ON teams.school_name = players.school_name
```

## SQL INNER JOIN

Inner joins, which can be written as either `JOIN DB2` or `INNER JOIN DB2` Inner joins eliminate rows from both tables that do not satisfy the join condition set forth in the `ON` statement. In mathematical terms, an inner join is the *intersection* of the two tables.

![Untitled](Images/Untitled.png)

### Joining tables with identical column names

When you join two tables, it might be the case that both tables have columns with identical names. In the below example, both tables have columns called `school_name`:

```sql
SELECT players.*,
       teams.*
  FROM DB1_PLAYERS players
  JOIN DB2_TEAMS teams
    ON teams.school_name = players.school_name
```

The results can only support one column with a given name—when you include 2 columns of the same name, the results will simply show the exact same result set for both columns **even if the two columns should contain different data**. You can avoid this by naming the columns individually. It happens that these two columns will actually contain the same data because they are used for the join key, but the following query technically allows these columns to be independent:

```sql
SELECT players.school_name AS players_school_name,
       teams.school_name AS teams_school_name
  FROM DB1_PLAYERS players
  JOIN DB2_TEAMS teams
    ON teams.school_name = players.school_name
```

```sql
-- Write a query that displays player names, school names and conferences for schools in the "FBS (Division I-A Teams)" division.
SELECT players.player_name AS player_name,
       players.school_name  AS school_name,
       teams.conference AS conferebces
  FROM DB1_PLAYERS players
  JOIN DB2_TEAMS teams
    ON teams.school_name = players.school_name
    WHERE teams.division = 'FBS (Division I-A Teams)'
```

## SQL OUTER JOINS

Outer joins are joins that return matched values **and** unmatched values from either or both tables. There are a few types of outer joins:

- **`LEFT JOIN` returns only unmatched rows from the left table**, as well as matched rows in both tables.
- **`RIGHT JOIN` returns only unmatched rows from the right table** , as well as matched rows in both tables.
- **`FULL OUTER JOIN` returns unmatched rows from both tables,** as well as matched rows in both tables.

### Outer joins vs. Inner join

When performing an **inner join**, rows from either table that are unmatched in the other table are not returned. In an outer join, unmatched rows in one or both tables can be returned.

![Untitled](Images/Untitled%201.png)

## SQL LEFT JOIN

![Untitled](Images/Untitled%202.png)

`LEFT JOIN` command tells the database to return all rows in the table in the `FROM` clause, regardless of whether or not they have matches in the table in the `LEFT JOIN` clause.

```sql
SELECT companies.permalink AS companies_permalink,
       companies.name AS companies_name,
       acquisitions.company_permalink AS acquisitions_permalink,
       acquisitions.acquired_at AS acquired_date
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_acquisitions acquisitions
    ON companies.permalink = acquisitions.company_permalink
```

```sql
-- Write a query that performs an inner join between the tutorial.crunchbase_acquisitions table and the tutorial.crunchbase_companies table, 
-- but instead of listing individual rows, count the number of non-null rows in each table.

SELECT COUNT(companies.permalink) AS companies_rowcount,
       COUNT(acquisitions.company_permalink) AS acquisitions_rowcount
FROM tutorial.crunchbase_companies companies
INNER JOIN tutorial.crunchbase_acquisitions acquisitions
  ON companies.permalink = acquisitions.company_permalink
```

```sql
-- Count the number of unique companies (don't double-count companies) and unique acquired companies by state.
-- Do not include results for which there is no state data, and order by the number of acquired companies from highest to lowest.

SELECT companies.state_code as state_code,
       COUNT(DISTINCT companies.permalink) AS unique_companies,
       COUNT(DISTINCT acquisitions.company_permalink) AS unique_companies_acquired
FROM tutorial.crunchbase_companies companies
LEFT JOIN tutorial.crunchbase_acquisitions acquisitions
  ON companies.permalink = acquisitions.company_permalink
  WHERE state_code IS NOT NULL 
  GROUP BY state_code
  ORDER BY unique_companies_acquired DESC
```

## SQL RIGHT JOIN

Right joins are similar to left joins except they return all rows from the table in the `RIGHT JOIN` clause and only matching rows from the table in the `FROM` clause.

![Untitled](Images/Untitled%203.png)

`RIGHT JOIN` is rarely used because you can achieve the results of a `RIGHT JOIN` by simply switching the two joined table names in a `LEFT JOIN`.

The convention of always using `LEFT JOIN` probably exists to make queries easier to read and audit, but beyond that there isn't necessarily a strong reason to avoid using `RIGHT JOIN`.

It's worth noting that `LEFT JOIN` and `RIGHT JOIN` can be written as `LEFT OUTER JOIN` and `RIGHT OUTER JOIN`, respectively.

```sql
-- Rewrite the previous practice query in which you counted total and acquired companies by state, but with a RIGHT JOIN instead of a LEFT JOIN.
-- The goal is to produce the exact same results.

SELECT companies.state_code as state_code,
       COUNT(DISTINCT companies.permalink) AS unique_companies,
       COUNT(DISTINCT acquisitions.company_permalink) AS unique_companies_acquired
FROM tutorial.crunchbase_acquisitions acquisitions
RIGHT JOIN tutorial.crunchbase_companies companies
  ON companies.permalink = acquisitions.company_permalink
  WHERE state_code IS NOT NULL 
  GROUP BY state_code
  ORDER BY unique_companies_acquired DESC
```

## SQL JOINS Using WHERE or ON

## Filtering in the ON clause

Normally, filtering is processed in the **`WHERE`** clause once the **two tables have already been joined**. It's possible, though that you might want to filter one or both of the tables *before* joining them. For example, you only want to create matches between the tables under certain circumstances.

```sql
SELECT companies.permalink AS companies_permalink,
       companies.name AS companies_name,
       acquisitions.company_permalink AS acquisitions_permalink,
       acquisitions.acquired_at AS acquired_date
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_acquisitions acquisitions
    ON companies.permalink = acquisitions.company_permalink
   AND acquisitions.company_permalink != '/company/1000memories'
 ORDER BY 1
```

What's happening above is that the conditional statement `AND...` is evaluated before the join occurs. You can think of it as a `WHERE` clause that only applies to one of the tables. You can tell that this is only happening in one of the tables because the 1000memories permalink is still displayed in the column that pulls from the other table:

![Untitled](Images/Untitled%204.png)

### Filtering in the WHERE clause

If you move the same filter to the `WHERE` clause, you will notice that the filter happens after the tables are joined. The result is that the 1000memories row is joined onto the original table, but then it is filtered out entirely (in both tables) in the `WHERE` clause before displaying results.

```
SELECT companies.permalink AS companies_permalink,
       companies.name AS companies_name,
       acquisitions.company_permalink AS acquisitions_permalink,
       acquisitions.acquired_at AS acquired_date
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_acquisitions acquisitions
    ON companies.permalink = acquisitions.company_permalink
 WHERE acquisitions.company_permalink != '/company/1000memories'
    OR acquisitions.company_permalink IS NULL
 ORDER BY 1

```

You can see that the 1000memories line is not returned (it would have been between the two highlighted lines below). Also note that filtering in the `WHERE` clause can also filter null values, so we added an extra line to make sure to include the nulls.

![Untitled](Images/Untitled%205.png)

```sql
-- Write a query that shows a company's name, "status" (found in the Companies table), and the number of unique investors in that company.
-- Order by the number of investors from most to fewest. 
-- Limit to only companies in the state of New York.

SELECT companies.name AS company_name,
       companies.status AS company_status,
       COUNT(DISTINCT investments.investor_name) as investor_count
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_investments investments
  ON companies.permalink = investments.company_permalink 
  WHERE companies.state_code = 'NY'
  GROUP BY companies.name,companies.status
  ORDER BY investor_count DESC
```

```sql
-- Write a query that lists investors based on the number of companies in which they are invested. 
-- Include a row for companies with no investor, and order from most companies to least.

SELECT CASE WHEN investments.investor_name IS NULL THEN 'No Investors'
            ELSE investments.investor_name END AS investor,
       COUNT(DISTINCT companies.permalink) AS companies_invested_in
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_investments investments
    ON companies.permalink = investments.company_permalink
 GROUP BY 1
 ORDER BY 2 DESC
```

## SQL FULL OUTER JOINS

We’re not likely to use `FULL JOIN` (which can also be written as `FULL OUTER JOIN`) too often, but it's worth covering anyway. **`LEFT JOIN`** and **`RIGHT JOIN`** each return unmatched rows from one of the tables—`FULL JOIN` returns unmatched rows from both tables. It is commonly used in conjunction with aggregations to understand the amount of overlap between two tables.

```sql
SELECT COUNT(CASE WHEN companies.permalink IS NOT NULL AND acquisitions.company_permalink IS NULL
                  THEN companies.permalink ELSE NULL END) AS companies_only,
       COUNT(CASE WHEN companies.permalink IS NOT NULL AND acquisitions.company_permalink IS NOT NULL
                  THEN companies.permalink ELSE NULL END) AS both_tables,
       COUNT(CASE WHEN companies.permalink IS NULL AND acquisitions.company_permalink IS NOT NULL
                  THEN acquisitions.company_permalink ELSE NULL END) AS acquisitions_only
  FROM tutorial.crunchbase_companies companies
  FULL JOIN tutorial.crunchbase_acquisitions acquisitions
    ON companies.permalink = acquisitions.company_permalink
```

## SQL UNION

SQL joins allow you to combine two datasets side-by-side, but `UNION` allows you to stack one dataset on top of the other. Put differently, `UNION` allows you to write two separate `SELECT` statements, and to have the results of one statement display in the same table as the results from the other statement.

```sql
SELECT *
  FROM tutorial.crunchbase_investments_part1

 UNION

 SELECT *
   FROM tutorial.crunchbase_investments_part2
```

Note that `UNION` only appends distinct values. More specifically, when you use `UNION`, the dataset is appended, and any rows in the appended table that are exactly identical to rows in the first table are dropped. If you'd like to append all the values from the second table, use `UNION ALL`. You'll likely use `UNION ALL` far more often than `UNION`.

```sql
SELECT *
  FROM tutorial.crunchbase_investments_part1

 UNION ALL

 SELECT *
   FROM tutorial.crunchbase_investments_part2
```

SQL has strict rules for appending data:

1. Both tables must have the same number of columns
2. The columns must have the same data types in the same order as the first table

While the column names don't necessarily have to be the same, you will find that they typically are. This is because most of the instances in which you'd want to use `UNION` involve stitching together different parts of the same dataset.

Since you are writing two separate `SELECT` statements, you can treat them differently before appending. For example, you can filter them differently using different `WHERE` clauses.

```sql
-- Write a query that appends the two crunchbase_investments datasets above (including duplicate values).
-- Filter the first dataset to only companies with names that start with the letter "T", 
-- and filter the second to companies with names starting with "M" (both not case-sensitive). 
-- Only include the company_permalink, company_name, and investor_name columns.
SELECT company_permalink, company_name, investor_name
  FROM tutorial.crunchbase_investments_part1
WHERE company_name ILIKE 'T%'
 UNION ALL

 SELECT company_permalink,company_name,investor_name
   FROM tutorial.crunchbase_investments_part2
   WHERE company_name ILIKE '%M'
```
```sql
-- Write a query that shows 3 columns. The first indicates which dataset (part 1 or 2) the data comes from, 
-- the second shows company status, and the third is a count of the number of investors.

-- Hint: you will have to use the tutorial.crunchbase_companies table as well as the investments tables. 
-- And you'll want to group by status and dataset.

SELECT 'investments_part1' AS dataset_name,
       companies.status,
       COUNT(DISTINCT investments.investor_permalink) AS investors
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_investments_part1 investments
    ON companies.permalink = investments.company_permalink
 GROUP BY 1,2

 UNION ALL
 
 SELECT 'investments_part2' AS dataset_name,
       companies.status,
       COUNT(DISTINCT investments.investor_permalink) AS investors
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_investments_part2 investments
    ON companies.permalink = investments.company_permalink
 GROUP BY 1,2
```

## SQL JOINS With Comparison Operators

We’ve only joined tables by exactly matching values from both tables. However, you can enter any type of conditional statement into the `ON` clause. Here's an example using `>` to join only investments that occurred more than 5 years after each company's founding year:

```sql
SELECT companies.permalink,
       companies.name,
       companies.status,
       COUNT(investments.investor_permalink) AS investors
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_investments_part1 investments
    ON companies.permalink = investments.company_permalink
   AND investments.funded_year > companies.founded_year + 5
 GROUP BY 1,2,3
```

This technique is especially useful for creating date ranges as shown above. 

It's important to note that this produces a different result than the following query because it only joins rows that fit the `investments.funded_year > companies.founded_year + 5` condition rather than joining all rows and then filtering:

```sql
SELECT companies.permalink,
       companies.name,
       companies.status,
       COUNT(investments.investor_permalink) AS investors
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_investments_part1 investments
    ON companies.permalink = investments.company_permalink
 WHERE investments.funded_year > companies.founded_year + 5
 GROUP BY 1,2,3
```

## SQL JOINS on Multiple Keys

There are couple reasons you might want to join tables on multiple foreign keys. 

- The first has to do with accuracy.
- The second reason has to do with performance.

SQL uses "indexes" (essentially pre-defined joins) to speed up queries. It can occasionally make your query run faster to join on multiple fields, even when it does not add to the accuracy of the query. 

For example, the results of the following query will be the same with or without the last line. However, it is possible to optimize the database such that the query runs more quickly with the last line included:

```sql
SELECT companies.permalink,
       companies.name,
       investments.company_name,
       investments.company_permalink
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_investments_part1 investments
    ON companies.permalink = investments.company_permalink
   AND companies.name = investments.company_name
```

## SQL Self Joins

Sometimes it can be useful to join a table to itself. 

Let’s say you wanted to identify companies that received an investment from Great Britain following an investment from Japan.

```sql
SELECT DISTINCT japan_investments.company_name,
	   japan_investments.company_permalink
  FROM tutorial.crunchbase_investments_part1 japan_investments
  JOIN tutorial.crunchbase_investments_part1 gb_investments
    ON japan_investments.company_name = gb_investments.company_name
   AND gb_investments.investor_country_code = 'GBR'
   AND gb_investments.funded_at > japan_investments.funded_at
 WHERE japan_investments.investor_country_code = 'JPN'
 ORDER BY 1

```

Note how the same table can easily be referenced multiple times using different aliases—in this case, `japan_investments` and `gb_investments`.

## **SQL Data Types**

In previous lessons, you learned that certain functions work on some data types, but not others. For example, `Count` works with any data type, but `SUM` only works for numerical data. 

This is actually more complicated than it appears: in order to use `SUM`, the data must appear to be numeric, but it must also be **stored in the database** in a numeric form.

You might run into this, for example, if you have a column that appears to be entirely numeric, but happens to contain spaces or commas.

Generally, numeric column types in various SQL databases *do not* support commas or currency symbols. To make things more complicated, SQL databases can store data in many different formats with different levels of precision.

The `INTEGER` data type, for example, only stores whole numbers—no decimals. The `DOUBLE PRECISION` data type, on the other hand, can store between 15 and 17 significant decimal digits. 

The complete list of Data Types in SQL, **[click here](https://www.w3schools.com/sql/sql_datatypes_general.asp)**.

### Changing a column's data type

It's certainly best for data to be stored in its optimal format from the beginning, but if it isn't, you can always change it in your query. It's particularly common for dates or numbers, for example, to be stored as strings. This becomes problematic when you want to sum a column and you get an error because SQL is reading numbers as strings. When this happens, you can use `CAST` or `CONVERT` to change the data type to a numeric one that will allow you to perform the sum.

You can actually achieve this with two different type of syntax. For example, `CAST(column_name AS integer)` and `column_name::integer` produce the same result.

You could replace `integer` with any other data type that would make sense for that column—all values in a given column must fit with the new data types.

```sql
-- Convert the funding_total_usd and founded_at_clean columns in the tutorial.crunchbase_companies_clean_date table
-- to strings (varchar format) using a different formatting function for each one.

SELECT CAST(funding_total_usd AS varchar) AS funding_total_usd_string,
       founded_at_clean::varchar AS founded_at_string
  FROM tutorial.crunchbase_companies_clean_date
```

## SQL Date Format

### Why dates are formatted year-first

Both MM-DD-YYYY and DD-MM-YYYY are bad formats. The problem with both of these formats is that when they are stored as strings, they don't sort in chronological order. 

For example, here's a date field stored as a string. Because the month is listed first, the `ORDER BY` statement doesn't produce a chronological list:

```sql
SELECT permalink,
       founded_at
  FROM tutorial.crunchbase_companies_clean_date
 ORDER BY founded_at

```

You might think that converting these values from `string` to `date` might solve the problem, but it's actually not quite so simple. most relational databases format dates as YYYY-MM-DD, a format that makes a lot of sense because it will sort in the same order whether it's stored as a date or as a string. 

Here's an example from the same table, but with a field that has a cleaned date. Note that the cleaned date field is actually stored as a string, but still sorts in chronological order anyway:

```sql
SELECT permalink,
       founded_at,
       founded_at_clean
  FROM tutorial.crunchbase_companies_clean_date
 ORDER BY founded_at_clean

```

### Crazy rules for dates and times

Assuming you've got some dates properly stored as a `date` or `time` data type, you can do some pretty powerful things. Maybe you'd like to calculate a field of dates a week after an existing field. Or maybe you'd like to create a field that indicates how many days apart the values in two other date fields are. These are trivially simple, but it's important to keep in mind that the data type of your results will depend on exactly what you are doing to the dates.

When you perform arithmetic on dates (such as subtracting one date from another), the results are often stored as the `interval` data type—a series of integers that represent a period of time. 

The following query uses date subtraction to determine how long it took companies to be acquired. Note that because the `companies.founded_at_clean` column is stored as a string, it must be cast as a timestamp before it can be subtracted from another timestamp.

```sql
SELECT companies.permalink,
       companies.founded_at_clean,
       acquisitions.acquired_at_cleaned,
       acquisitions.acquired_at_cleaned -
         companies.founded_at_clean::timestamp AS time_to_acquisition
  FROM tutorial.crunchbase_companies_clean_date companies
  JOIN tutorial.crunchbase_acquisitions_clean_date acquisitions
    ON acquisitions.company_permalink = companies.permalink
 WHERE founded_at_clean IS NOT NULL

```

In the example above, you can see that the `time_to_acquisition` column is an interval, not another date.

You can introduce intervals using the `INTERVAL` function as well:

```sql
SELECT companies.permalink,
       companies.founded_at_clean,
       companies.founded_at_clean::timestamp +
         INTERVAL '1 week' AS plus_one_week
  FROM tutorial.crunchbase_companies_clean_date companies
 WHERE founded_at_clean IS NOT NULL

```

The interval is defined using plain-English terms like '10 seconds' or '5 months'. Also note that adding or subtracting a `date` column and an `interval` column results in another `date` column as in the above query.

You can add the current time (at the time you run the query) into your code using the `NOW()`function:

```sql
SELECT companies.permalink,
       companies.founded_at_clean,
       NOW() - companies.founded_at_clean::timestamp AS founded_time_ago
  FROM tutorial.crunchbase_companies_clean_date companies
 WHERE founded_at_clean IS NOT NULL
```

## SQL Date Functions

**The most frequently used date functions and business scenarios where they come in handy:**

- Rounding off timestamps with `DATE_TRUNC` function
- Finding events relative to the present time with `NOW()` and `CURRENT_DATE` functions
- Isolating hour-of-day and day-of-week with `EXTRACT` function
- Calculating time elapsed with `AGE` function

### **Rounding off timestamps with `DATE_TRUNC` function**

The `DATE_TRUNC` function rounds a timestamp value to a specified interval, which allows you to count events. You can round off a timestamp to the following units of time:

- microsecond
- millisecond
- second
- minute
- hour
- day
- week
- month
- quarter
- year
- decade
- century
- millennium

The `DATE_TRUNC` syntax looks like this: `DATE_TRUNC('interval',timestamp)`.

For example, `SELECT DATE_TRUNC('day','2015-04-12 14:44:18')` would return a result of `2015-04-12 00:00:00`.

**Example: How has web traffic changed over time?**

Try `DATE_TRUNC` for yourself by querying this table, which contains sample records of website visits, including an `occurred_at` column. You can isolate the month of the visit with `DATE_TRUNC`.

```sql
SELECT DATE_TRUNC('month',occurred_at) AS month
  FROM demo.web_events
 WHERE occurred_at BETWEEN '2015-01-01' AND '2015-12-31 23:59:59'
```

To return a count of web visits each month by channel, add the `channel` column and a `COUNT` to the `SELECT` statement, then group by `month` and `channel`. (Since month and channel are the first two values in your `SELECT` statement, you can `GROUP BY 1,2`), like this:

```sql
SELECT DATE_TRUNC('month',occurred_at) AS month,
       channel,
       COUNT(id) AS visits
  FROM demo.web_events
 WHERE occurred_at BETWEEN '2015-01-01' AND '2015-12-31 23:59:59'
 GROUP BY 1,2
```

Finally, use `ORDER BY 1,2` to organize your results chronologically (by month) and alphabetically (by channel).

```sql
SELECT DATE_TRUNC('month',occurred_at) AS month,
       channel,
       COUNT(id) AS visits
  FROM demo.web_events
 WHERE occurred_at BETWEEN '2015-01-01' AND '2015-12-31 23:59:59'
 GROUP BY 1,2
 ORDER BY 1,2
```

### **Finding events relative to the present time with `NOW()` and `CURRENT_DATE` functions**

The `NOW()` date function returns the current timestamp in UTC (if the time zone is unspecified). You can subtract intervals from `NOW()` to pull events that happened within the last hour, the last day, the last week, etc.

Running `SELECT NOW()` at 9:00am UTC on October 11th, 2016 would result in `2016-10-11 09:00:00`.

The `CURRENT_DATE` function only returns the current date, not the whole timestamp. Running `SELECT CURRENT_DATE` at 9:00am UTC on October 11th, 2016 would return `2016-10-11`.

**Example: What orders were placed in the last 7 years?**

To find orders placed in the last 7 years, use a `WHERE` clause to return only orders that were placed after or exactly at (`>=`) the current timestamp (`NOW()`) minus an interval of 7 years.

```sql
SELECT *
  FROM demo.orders
 WHERE occurred_at >= NOW() - interval '7 year'
```

In addition to `year`, you can use any of the following intervals:

- microseconds
- milliseconds
- second
- minute
- hour
- day
- week
- month
- year
- decade
- century
- millennium

You can also combine different intervals in the same expression like this:
`interval '4 hours 3 minutes'`

**Example: What orders were placed this day a 7 years ago?**

You can use the same table to find orders placed on this day seven year ago by combining the `DATE_TRUNC` and `CURRENT_DATE` functions.

Start by using a `DATE_TRUNC` function to round your `occurred_at` values by day (since we want to know if something happened this *day*). Then use a `WHERE` clause to return only values where the `occurred_at` day is equal to the current date (using the `CURRENT_DATE` function) minus an interval of 7 years.

```sql
SELECT *
  FROM demo.orders
 WHERE DATE_TRUNC('day',occurred_at) = CURRENT_DATE - interval '7 year'
```

### Isolating hour-of-day and day-of-week with EXTRACT

The `EXTRACT` date function allows you to isolate subfields such as year or hour from timestamps. Essentially it allows you to extract parts of a date from a datetime expression.

Here's the syntax: `EXTRACT(subfield FROM timestamp)`. Running `EXTRACT(month FROM '2015-02-12')` would return a result of `2`.

**Example: How many orders are placed each hour of the day?**

A company running a fulfillment center might want to staff more employees when the bulk of orders comes in. To figure out when orders are placed throughout the day, you can use the `EXTRACT` function and the `hour` subfield to isolate the hour-of-day (from 0 to 23) in which an order occurred.

Use the `COUNT` function to tally orders, and then ****`GROUP BY` hour. (Since hour is the first value in your `SELECT` statement, you can `GROUP BY 1`).

Finally, to organize your results sequentially, use `ORDER BY 1`.

```sql
SELECT EXTRACT(hour from occurred_at) AS hour,
       COUNT(*) AS orders
  FROM demo.orders
 GROUP BY 1
 ORDER BY 1
```

**Example: What's the average weekday order volume?**

To determine the average volume of orders that occurred by weekday, use `EXTRACT` and the `dow` (day of the week) subfield to isolate the day-of-week (from 0-6, where 0 is Sunday) in which an order occurred.

Next, round the order timestamps by day with `DATE_TRUNC`. Taking a `COUNT` of orders grouped by `dow` and `day` will return the number of orders placed each day along with the corresponding day-of-week.

To find the average weekday order volume, use the previous query as a **subquery** (aliased as `a`). Take the average of orders (using the `AVG()` function), and then use a `WHERE` clause to filter out Saturdays and Sundays.

```sql
SELECT AVG(orders) AS avg_orders_weekday
  FROM (
SELECT EXTRACT(dow from occurred_at) AS dow,
       DATE_TRUNC('day',occurred_at) AS day,
       COUNT(id) AS orders
  FROM demo.orders
 GROUP BY 1,2) a
 WHERE dow NOT IN (0,6)
```

### Calculating time elapsed with AGE

The `AGE` date function calculates how long ago an event occurred. It returns a value representing the number of years, months, and days an event happened or the difference between two given arguments.

The syntax is pretty straightforward: apply `AGE()` to a single timestamp, and your query will return the amount of time since that event took place. Running `SELECT AGE( '2010-01-01' )` on January 1st, 2011 would return a result of `1 years 0 months 0 days`.

`AGE()` can also determine how much time passed between two events. Instead of putting a single timestamp inside the parentheses, insert both timestamps (starting with the most recent timestamp) and separate them with a comma. Running `SELECT AGE( '2012-12-01','2010-01-01')` would return `2 years 11 months 0 days`.

Note that this application of the `AGE` function is equivalent to subtracting the timestamps: `SELECT '2012-12-01' - '2010-01-01'`.

**Example: How old is a customer account?**

Suppose your sales team wants to personalize greetings based on how long the customer has been using your product. You can find how much time has elapsed since account creation using the `AGE` function.

Select the column of account names `name` and apply the `AGE()` function to the column of timestamps showing when each account was created `created`.

```sql
SELECT name,
       AGE(created) AS account_age
  FROM modeanalytics.customer_accounts
```

**Example: How long does it take users to complete their profile each month, on average?**

To find the average time to complete a profile each month, start by finding the time it took each user to complete a profile as well as the month in which the profile creation process was started. First, round the `started_at` timestamp by month, using the `DATE_TRUNC` function. Next, find the time elapsed from `started_at` to `ended_at` for each profile using the `AGE` function.

Find the average for each month by applying the `AVG` function to the elapsed time value (your `AGE` statement) and grouping by month.

```sql
SELECT DATE_TRUNC('month',started_at) AS month,
       AVG(AGE(ended_at,started_at)) AS avg_time_to_complete
  FROM modeanalytics.profile_creation_events
 GROUP BY 1
 ORDER BY 1
```

To return values in a consistent unit for charting, apply the `EXTRACT` function and `EPOCH` subfield to your values to return results as a count of seconds.

```sql
SELECT DATE_TRUNC('month',started_at) AS month,
       EXTRACT(EPOCH FROM AVG(AGE(ended_at,started_at))) AS avg_seconds
  FROM modeanalytics.profile_creation_events
 GROUP BY 1
 ORDER BY 1
```

```sql
-- Write a query that counts the number of companies acquired within 3 years, 5 years, and 10 years of being founded (in 3 separate columns). 
-- Include a column for total companies acquired as well. Group by category and limit to only rows with a founding date.

SELECT companies.category_code as category,
       COUNT(CASE WHEN AGE(acquisitions.acquired_at_cleaned::TIMESTAMP, companies.founded_at_clean::TIMESTAMP) <= INTERVAL '3 year' THEN 1 END) as acquired_3year,
       COUNT(CASE WHEN AGE(acquisitions.acquired_at_cleaned::TIMESTAMP, companies.founded_at_clean::TIMESTAMP) <= INTERVAL '5 year' THEN 1 END) as acquired_5year,
       COUNT(CASE WHEN AGE(acquisitions.acquired_at_cleaned::TIMESTAMP, companies.founded_at_clean::TIMESTAMP) <= INTERVAL '10 year' THEN 1 END) as acquired_10year,
       COUNT(acquisitions.acquired_at_cleaned) as no_companies_acquired
  FROM tutorial.crunchbase_companies_clean_date companies
  JOIN tutorial.crunchbase_acquisitions_clean_date acquisitions
    ON acquisitions.company_permalink = companies.permalink
    AND companies.founded_at_clean IS NOT NULL
GROUP BY category
ORDER BY no_companies_acquired DESC
```

## Data Wrangling with SQL


**Data wrangling** (or munging) is the process of programmatically transforming data into a format that makes it easier to work with. This might mean modifying all of the values in a given column in a certain way, or merging multiple columns together. The necessity for data wrangling is often a biproduct of poorly collected or presented data. 

Data that is entered manually by humans is typically fraught with errors; data collected from websites is often optimized to be displayed on websites, not to be sorted and aggregated.

## Using SQL String Functions to Clean Data

Most of the functions presented in this lesson are specific to certain data types. However, using a particular function will, in many cases, change the data to the appropriate type. `LEFT`, `RIGHT`, and `TRIM` are all used to select only certain elements of strings, but using them to select elements of a number or date will treat them as strings for the purpose of the function.

### **LEFT, RIGHT, and LENGTH**

You can use `LEFT` to pull a certain number of characters from the left side of a string and present them as a separate string. The syntax is `LEFT(string, number of characters)`.

As a practical example, we can see that the `date` field in this dataset begins with a 10-digit date, and include the timestamp to the right of it. The following query pulls out only the date `01/31/2014 08:00:00 AM +0000 => 01/31/2014`

```sql
SELECT incidnt_num,
       date,
       LEFT(date, 10) AS cleaned_date
  FROM tutorial.sf_crime_incidents_2014_01

```

`RIGHT` does the same thing, but from the right side:

```sql
SELECT incidnt_num,
       date,
       LEFT(date, 10) AS cleaned_date,
       RIGHT(date, 17) AS cleaned_time
  FROM tutorial.sf_crime_incidents_2014_01

```

`RIGHT` works well in this case because we know that the number of characters will be consistent across the entire `date` field. If it wasn't consistent, it's still possible to pull a string from the right side in a way that makes sense. The `LENGTH` function returns the length of a string. So `LENGTH(date)` will always return `28` in this dataset. Since we know that the first 10 characters will be the date, and they will be followed by a space (total 11 characters), we could represent the `RIGHT` function like this:

```sql
SELECT incidnt_num,
       date,
       LEFT(date, 10) AS cleaned_date,
       RIGHT(date, LENGTH(date) - 11) AS cleaned_time
  FROM tutorial.sf_crime_incidents_2014_01

```

When using functions within other functions, it's important to remember that the innermost functions will be evaluated first, followed by the functions that encapsulate them.

### **TRIM**

The `TRIM` function is used to remove characters from the beginning and end of a string. Here's an example:

```sql
SELECT location,
       TRIM(both '()' FROM location)
  FROM tutorial.sf_crime_incidents_2014_01

```

The `TRIM` function takes 3 arguments. First, you have to specify whether you want to remove characters from the beginning ('**leading**'), the end ('**trailing**'), or both ('**both**', as used above). 

Next you must specify all characters to be trimmed. Any characters included in the single quotes will be removed from both beginning, end, or both sides of the string. Finally, you must specify the text you want to trim using `FROM`.

### **POSITION and STRPOS**

`POSITION` allows you to specify a substring, then returns a numerical value equal to the character number (counting from left) where that substring first appears in the target string. 

For example, the following query will return the position of the character 'A' (case-sensitive) where it first appears in the `descript` field:

```sql
SELECT incidnt_num,
       descript,
       POSITION('A' IN descript) AS a_position
  FROM tutorial.sf_crime_incidents_2014_01

```

You can also use the `STRPOS` function to achieve the same results—just replace `IN` with a comma and switch the order of the string and substring:

```sql
SELECT incidnt_num,
       descript,
       STRPOS(descript, 'A') AS a_position
  FROM tutorial.sf_crime_incidents_2014_01

```

Importantly, both the `POSITION` and `STRPOS` functions are case-sensitive. If you want to look for a character regardless of its case, you can make your entire string a single by using the `UPPER` or `LOWER` functions.

### **SUBSTR**

`LEFT` and `RIGHT` both create substrings of a specified length, but they only do so starting from the sides of an existing string. If you want to start in the middle of a string, you can use `SUBSTR`. The syntax is `SUBSTR(*string*, *starting character position*, *# of characters*)`:

```sql
SELECT incidnt_num,
       date,
       SUBSTR(date, 4, 2) AS day
  FROM tutorial.sf_crime_incidents_2014_01
```

```sql
-- Write a query that separates the `location` field into separate fields for latitude and longitude. 
-- You can compare your results against the actual `lat` and `lon` fields in the table.
-- Location (37.709725805163, -122.413623946206)
SELECT location,
       TRIM(leading '(' FROM LEFT(location, POSITION(',' IN location) - 1)) AS lattitude,
       TRIM(trailing ')' FROM RIGHT(location, LENGTH(location) - POSITION(',' IN location) ) ) AS longitude
  FROM tutorial.sf_crime_incidents_2014_01
```

### **CONCAT**

You can combine strings from several columns together (and with hard-coded values) using `CONCAT`. Simply order the values you want to concatenate and separate them with commas. If you want to hard-code values, enclose them in single quotes. Here's an example:

```sql
SELECT incidnt_num,
       day_of_week,
       LEFT(date, 10) AS cleaned_date,
       CONCAT(day_of_week, ', ', LEFT(date, 10)) AS day_and_date
  FROM tutorial.sf_crime_incidents_2014_01
```

Alternatively, you can use two pipe characters (`||`) to perform the same concatenation:

```sql
SELECT incidnt_num,
       day_of_week,
       LEFT(date, 10) AS cleaned_date,
       day_of_week || ', ' || LEFT(date, 10) AS day_and_date
  FROM tutorial.sf_crime_incidents_2014_01
```

```sql
-- Concatenate the lat and lon fields to form a field that is equivalent to the location field.
-- (Note that the answer will have a different decimal precision.)
-- lon 37.7097, lat -122.4136 , new_location (37.709725805163, -122.413623946206)

SELECT lat,
       lon,
       CONCAT('(',lat,', ',lon,')') AS new_location
  FROM tutorial.sf_crime_incidents_2014_01

-- Create the same concatenated location field, but using the || syntax instead of CONCAT.
SELECT lat,
       lon,
       location,
       '(' || lat || ', ' || lon || ')' AS new_location
  FROM tutorial.sf_crime_incidents_2014_01
```

```sql
-- Write a query that creates a date column formatted YYYY-MM-DD.
-- old-date 01/31/2014 08:00:00 AM +0000
-- new-date 2014-01-31

SELECT CONCAT(SUBSTR(date, 7, 4), '-', SUBSTR(date, 1, 2), '-', SUBSTR(date, 4, 2)) AS new_date
  FROM tutorial.sf_crime_incidents_2014_01

```

### **Changing case with UPPER and LOWER**

You can use `LOWER` to force every character in a string to become lower-case. Similarly, you can use `UPPER` to make all the letters appear in upper-case:

```sql
SELECT incidnt_num,
       address,
       UPPER(address) AS address_upper,
       LOWER(address) AS address_lower
  FROM tutorial.sf_crime_incidents_2014_01
```

```sql
-- Write a query that returns the `category` field, but with the first letter capitalized and the rest of the letters in lower-case.

SELECT CONCAT(UPPER(LEFT(category,1)), 
              LOWER(RIGHT(category, LENGTH(category) - 1))) AS category_reform
  FROM tutorial.sf_crime_incidents_2014_01
```

There are a number of variations of these functions, as well as several other string functions not covered here. Different databases use subtle variations on these functions, so be sure to look up the appropriate database's syntax. This is **[Postgres literature](http://www.postgresql.org/docs/9.1/static/functions-string.html)** contains the related functions.

### Turning strings into dates

Dates are some of the most commonly screwed-up formats in SQL. This can be the result of a few things:

- The data was manipulated in Excel at some point, and the dates were changed to MM/DD/YYYY format or another format that is not compliant with SQL's strict standards.
- The data was manually entered by someone who use whatever formatting convention he/she was most familiar with.
- The date uses text (Jan, Feb, etc.) instead of numbers to record months.

In order to take advantage of all of the great date functionality (`INTERVAL`, as well as some others), you need to have your date field formatted appropriately. This often involves some text manipulation, followed by a `CAST`. 

```sql
-- Convert the date(string) column into a date format
-- old_date => 01/31/2014 08:00:00 AM +0000, new_date => 2014-01-31 00:00:00
SELECT incidnt_num,
       date,
       (SUBSTR(date, 7, 4) || '-' || LEFT(date, 2) ||
        '-' || SUBSTR(date, 4, 2))::date AS cleaned_date
  FROM tutorial.sf_crime_incidents_2014_01
```

```sql
-- Write a query that creates an accurate timestamp using the date and time columns in tutorial.sf_crime_incidents_2014_01. 
-- Include a field that is exactly 1 week later as well.
-- time contains the hour:mins

SELECT incidnt_num,
       date,
       (SUBSTR(date, 7, 4) || '-' || 
       LEFT(date, 2) || '-' || 
       SUBSTR(date, 4, 2) || ' ' ||
       timetime || ':00')::TIMESTAMP AS cleaned_date,
       (SUBSTR(date, 7, 4) || '-' || 
       LEFT(date, 2) || '-' || 
       SUBSTR(date, 4, 2) || ' ' ||
       time || ':00')::TIMESTAMP + INTERVAL '1 week' AS week_after
  FROM tutorial.sf_crime_incidents_2014_01
```

### Turning dates into more useful dates

You've learned how to construct a date field, but what if you want to deconstruct one? You can use `EXTRACT` to pull the pieces apart one-by-one:

```sql
SELECT cleaned_date,
       EXTRACT('year'   FROM cleaned_date) AS year,
       EXTRACT('month'  FROM cleaned_date) AS month,
       EXTRACT('day'    FROM cleaned_date) AS day,
       EXTRACT('hour'   FROM cleaned_date) AS hour,
       EXTRACT('minute' FROM cleaned_date) AS minute,
       EXTRACT('second' FROM cleaned_date) AS second,
       EXTRACT('decade' FROM cleaned_date) AS decade,
       EXTRACT('dow'    FROM cleaned_date) AS day_of_week
  FROM tutorial.sf_crime_incidents_cleandate

```

You can also round dates to the nearest unit of measurement. This is particularly useful if you don't care about an individual date, but do care about the week (or month, or quarter) that it occurred in. The `DATE_TRUNC` function rounds a date to whatever precision you specify. The value displayed is the first value in that period. So when you `DATE_TRUNC` by year, any value in that year will be listed as January 1st of that year:

```sql
SELECT cleaned_date,
       DATE_TRUNC('year'   , cleaned_date) AS year,
       DATE_TRUNC('month'  , cleaned_date) AS month,
       DATE_TRUNC('week'   , cleaned_date) AS week,
       DATE_TRUNC('day'    , cleaned_date) AS day,
       DATE_TRUNC('hour'   , cleaned_date) AS hour,
       DATE_TRUNC('minute' , cleaned_date) AS minute,
       DATE_TRUNC('second' , cleaned_date) AS second,
       DATE_TRUNC('decade' , cleaned_date) AS decade
  FROM tutorial.sf_crime_incidents_cleandate
```

```sql
-- Write a query that counts the number of incidents reported by week. Cast the week as a date to get rid of the hours/minutes/seconds.
  
  SELECT DATE_TRUNC('week', cleaned_date)::date AS week_beginning,
       COUNT(*) AS incidents
  FROM tutorial.sf_crime_incidents_cleandate
 GROUP BY 1
 ORDER BY 1
```

What if you want to include today's date or time? You can instruct your query to pull the local date and time at the time the query is run using any number of functions. Interestingly, you can run them without a `FROM` clause:

```sql
SELECT CURRENT_DATE AS date,
       CURRENT_TIME AS time,
       CURRENT_TIMESTAMP AS timestamp,
       LOCALTIME AS localtime,
       LOCALTIMESTAMP AS localtimestamp,
       NOW() AS now

```

You can make a time appear in a different time zone using `AT TIME ZONE`:

```sql
SELECT CURRENT_TIME AS time,
       CURRENT_TIME AT TIME ZONE 'PST' AS time_pst

```

For a complete list of time zones, **[look here](http://www.postgresql.org/docs/7.2/static/timezones.html)**. This functionality is pretty complex because timestamps can be stored with or without time zone metadata. For a better understanding of the exact syntax, we recommend checking out the **[Postgres documentation](http://www.postgresql.org/docs/9.2/static/functions-datetime.html#FUNCTIONS-DATETIME-ZONECONVERT)**.

```sql
-- Write a query that shows exactly how long ago each indicent was reported. 
-- Assume that the dataset is in Pacific Standard Time (UTC).

SELECT NOW() AT TIME ZONE 'UTC' AS now,
        cleaned_date,
        AGE(cleaned_date) as time_since_incident
  FROM tutorial.sf_crime_incidents_cleandate
```

## COALESCE

Occasionally, you will end up with a dataset that has some nulls that you'd prefer to contain actual values. This happens frequently in numerical data (displaying nulls as 0 is often preferable), and when performing outer joins that result in some unmatched rows. In cases like this, you can use `COALESCE` to replace the null values:

```sql
SELECT incidnt_num,
       descript,
       COALESCE(descript, 'No Description')
  FROM tutorial.sf_crime_incidents_cleandate
 ORDER BY descript DESC

```

## Writing Subqueries in SQL

## Subquery basics

**Subqueries** (also known as inner queries or nested queries) are a tool for performing operations in multiple steps. 

For example, if you wanted to take the sums of several columns, then average all of those values, you'd need to do each aggregation in a distinct step.

**Subqueries** can be used in several places within a query, but it's easiest to start with the `FROM` statement. Here's an example of a basic subquery:

```sql
SELECT sub.*
  FROM (
        SELECT *
          FROM tutorial.sf_crime_incidents_2014_01
         WHERE day_of_week = 'Friday'
       ) sub
 WHERE sub.resolution = 'NONE'

```

Let's break down what happens when you run the above query:

First, the database runs the "inner query"—the part between the parentheses:

```sql
SELECT *
  FROM tutorial.sf_crime_incidents_2014_01
 WHERE day_of_week = 'Friday'

```

If you were to run this on its own, it would produce a result set like any other query. It might sound like a no-brainer, but it's important: your inner query must actually run on its own, as the database will treat it as an independent query. Once the inner query runs, the outer query will run *using the results from the inner query as its underlying table*:

```sql
SELECT sub.*
  FROM (
       <<results from inner query go here>>
       ) sub
 WHERE sub.resolution = 'NONE'

```

Subqueries are required to have names, which are added after parentheses **the same way you would add an alias to a normal table**. In this case, we've used the name "sub."

A quick note on formatting: The important thing to remember when using subqueries is to provide some way to for the reader to easily determine which parts of the query will be executed together. Most people do this by indenting the subquery in some way. 

```sql
-- Write a query that selects all Warrant Arrests from the tutorial.sf_crime_incidents_2014_01 dataset,
-- then wrap it in an outer query that only displays unresolved incidents.

SELECT sub.*
FROM (SELECT *
      FROM tutorial.sf_crime_incidents_2014_01
      WHERE descript = 'WARRANT ARREST') AS sub
WHERE sub.resolution != 'NONE'
```

The above examples, as well as the practice problem don't really require subqueries—they solve problems that could also be solved by adding multiple conditions to the `WHERE` clause. These next sections provide examples for which subqueries are the best or only way to solve their respective problems.

### Using subqueries to aggregate in multiple stages

What if you wanted to figure out how many incidents get reported on each day of the week? Better yet, what if you wanted to know how many incidents happen, on average, on a Friday in December? In January? There are two steps to this process: counting the number of incidents each day (inner query), then determining the monthly average (outer query):

```sql
SELECT LEFT(sub.date, 2) AS cleaned_month,
       sub.day_of_week,
       AVG(sub.incidents) AS average_incidents
  FROM (
        SELECT day_of_week,
               date,
               COUNT(incidnt_num) AS incidents
          FROM tutorial.sf_crime_incidents_2014_01
         GROUP BY 1,2
       ) sub
 GROUP BY 1,2
 ORDER BY 1,2

```

If you're having trouble figuring out what's happening, try running the inner query individually to get a sense of what its results look like. In general, it's easiest to write inner queries first and revise them until the results make sense to you, then to move on to the outer query.

```sql
-- Write a query that displays the average number of monthly incidents for each category.

SELECT sub.category,
      AVG(sub.incidents_count) as avg_incidents_month
  FROM (
        SELECT LEFT(date, 2) AS cleaned_month,
                category,
                COUNT(incidnt_num) as incidents_count
          FROM tutorial.sf_crime_incidents_2014_01
        GROUP BY 1,2
      ) sub
GROUP BY 1
```

### Subqueries in conditional logic

You can use **subqueries** in conditional logic (in conjunction with `WHERE`, `JOIN`/`ON`, or `CASE`). The following query returns all of the entries from the earliest date in the dataset.

```sql
SELECT *
  FROM tutorial.sf_crime_incidents_2014_01
 WHERE Date = (SELECT MIN(date)
                 FROM tutorial.sf_crime_incidents_2014_01
              )

```

The above query works because the result of the subquery is only one cell. Most conditional logic will work with subqueries containing one-cell results. However, `IN` is the only type of conditional logic that will work when the inner query contains multiple results:

```sql
SELECT *
  FROM tutorial.sf_crime_incidents_2014_01
 WHERE Date IN (SELECT DISTINCT date
                 FROM tutorial.sf_crime_incidents_2014_01
                ORDER BY date
                LIMIT 5
              )

```

**Note** that you should not include an alias when you write a subquery in a conditional statement. This is because the subquery is treated as an individual value (or set of values in the `IN` case) rather than as a table.

### Joining subqueries

You may remember that you can **filter queries in joins**. It's fairly common to join a subquery that hits the same table as the outer query rather than filtering in the `WHERE` clause. The following query produces the same results as the previous example:

```sql
SELECT *
  FROM tutorial.sf_crime_incidents_2014_01 incidents
  JOIN ( SELECT DISTINCT date
           FROM tutorial.sf_crime_incidents_2014_01
          ORDER BY date
          LIMIT 5
       ) sub
    ON incidents.date = sub.date

```

This can be particularly useful when combined with aggregations. When you join, the requirements for your subquery output aren't as stringent as when you use the `WHERE` clause. 

For example, your inner query can output multiple results. The following query ranks all of the results according to how many incidents were reported in a given day. It does this by aggregating the total number of incidents each day in the inner query, then using those values to sort the outer query:

```sql
SELECT incidents.*,
       sub.incidents AS incidents_that_day
  FROM tutorial.sf_crime_incidents_2014_01 incidents
  JOIN ( SELECT date,
          COUNT(incidnt_num) AS incidents
           FROM tutorial.sf_crime_incidents_2014_01
          GROUP BY 1
       ) sub
    ON incidents.date = sub.date
 ORDER BY sub.incidents DESC, time
```

```sql
-- Write a query that displays all rows from the three categories with the fewest incidents reported.

SELECT incidents.*,
       sub.incidents_count
  FROM tutorial.sf_crime_incidents_2014_01 incidents
  JOIN ( SELECT category,
          COUNT(incidnt_num) AS incidents_count
           FROM tutorial.sf_crime_incidents_2014_01
          GROUP BY 1
          ORDER BY 2 
          LIMIT 3
       ) sub
    ON incidents.category = sub.category
```

Subqueries can be very helpful in improving the performance of your queries. 

Imagine you'd like to aggregate all of the companies receiving investment and companies acquired each month. You could do that without subqueries if you wanted to, but **don't actually run this as it will take minutes to return**:

```sql
SELECT COALESCE(acquisitions.acquired_month, investments.funded_month) AS month,
       COUNT(DISTINCT acquisitions.company_permalink) AS companies_acquired,
       COUNT(DISTINCT investments.company_permalink) AS investments
  FROM tutorial.crunchbase_acquisitions acquisitions
  FULL JOIN tutorial.crunchbase_investments investments
    ON acquisitions.acquired_month = investments.funded_month
 GROUP BY 1

```

Note that in order to do this properly, you must join on date fields, which causes a massive "data explosion." Basically, what happens is that you're joining every row in a given month from one table onto every month in a given row on the other table, so the number of rows returned is incredibly great. Because of this multiplicative effect, you must use `COUNT(DISTINCT)` instead of `COUNT` to get accurate counts. You can see this below:

The following query shows 7,414 rows:

```sql
SELECT COUNT(*) FROM tutorial.crunchbase_acquisitions

```

The following query shows 83,893 rows:

```sql
SELECT COUNT(*) FROM tutorial.crunchbase_investments

```

The following query shows 6,237,396 rows:

```sql
    SELECT COUNT(*)
      FROM tutorial.crunchbase_acquisitions acquisitions
      FULL JOIN tutorial.crunchbase_investments investments
        ON acquisitions.acquired_month = investments.funded_month

```

If you'd like to understand this a little better, you can do some extra research on **[cartesian products](http://en.wikipedia.org/wiki/Cartesian_product)**. It's also worth noting that the `FULL JOIN` and `COUNT` above actually runs pretty fast—it's the `COUNT(DISTINCT)` that takes forever. 

Of course, you could solve this much more efficiently by aggregating the two tables separately, then joining them together so that the counts are performed across far smaller datasets:

```sql
SELECT COALESCE(acquisitions.month, investments.month) AS month,
       acquisitions.companies_acquired,
       investments.companies_rec_investment
  FROM (
        SELECT acquired_month AS month,
               COUNT(DISTINCT company_permalink) AS companies_acquired
          FROM tutorial.crunchbase_acquisitions
         GROUP BY 1
       ) acquisitions

  FULL JOIN (
        SELECT funded_month AS month,
               COUNT(DISTINCT company_permalink) AS companies_rec_investment
          FROM tutorial.crunchbase_investments
         GROUP BY 1
       )investments

    ON acquisitions.month = investments.month
 ORDER BY 1 DESC

```

Note: We used a `FULL JOIN` above just in case one table had observations in a month that the other table didn't. We also used `COALESCE` to display months when the `acquisitions` subquery didn't have month entries (presumably no acquisitions occurred in those months). 

```sql
-- Write a query that counts the number of companies founded and acquired by quarter starting in Q1 2012. 
-- Create the aggregations in two separate queries, then join them.

SELECT COALESCE(acquisitions.acquired_quarter, investments.funded_quarter) AS quarter,
       acquisitions.companies_acquired,
       investments.companies_rec_investment
  FROM (
        SELECT acquired_quarter,
               COUNT(DISTINCT company_permalink) AS companies_acquired
          FROM tutorial.crunchbase_acquisitions
          WHERE acquired_quarter >= '2012-Q1'
         GROUP BY 1
         
       ) acquisitions

  FULL JOIN (
        SELECT funded_quarter,
               COUNT(DISTINCT company_permalink) AS companies_rec_investment
          FROM tutorial.crunchbase_investments
          WHERE funded_quarter >= '2012-Q1'
         GROUP BY 1
       )investments

    ON acquisitions.acquired_quarter = investments.funded_quarter
 ORDER BY 1 DESC
```

## Subqueries and UNIONs

```sql
SELECT *
  FROM tutorial.crunchbase_investments_part1

 UNION ALL

 SELECT *
   FROM tutorial.crunchbase_investments_part2

```

It's certainly not uncommon for a dataset to come split into several parts, especially if the data passed through Excel at any point (Excel can only handle ~1M rows per spreadsheet). The two tables used above can be thought of as different parts of the same dataset—what you'd almost certainly like to do is perform operations on the entire combined dataset rather than on the individual parts. You can do this by using a subquery:

```sql
SELECT COUNT(*) AS total_rows
  FROM (
        SELECT *
          FROM tutorial.crunchbase_investments_part1

         UNION ALL

        SELECT *
          FROM tutorial.crunchbase_investments_part2
       ) sub

-- result 83898 rows same as above
```

```sql
-- Write a query that ranks investors from the combined dataset above by the total number of investments they have made.

SELECT investor_name,
        COUNT(investor_name) AS no_investments
  FROM (
        SELECT *
          FROM tutorial.crunchbase_investments_part1

         UNION ALL

        SELECT *
          FROM tutorial.crunchbase_investments_part2
       ) sub
  GROUP BY 1
  ORDER by 2 DESC
```

```sql
-- Write a query that does the same thing as in the previous problem, except only for companies that are still operating. 
-- Hint: operating status is in tutorial.crunchbase_companies.

SELECT investments.investor_name,
        COUNT(investments.investor_name) AS no_investments
  FROM (
        SELECT *
          FROM tutorial.crunchbase_investments_part1

         UNION ALL

        SELECT *
          FROM tutorial.crunchbase_investments_part2
       ) investments
  INNER JOIN tutorial.crunchbase_companies companies
  ON investments.company_permalink = companies.permalink 
  AND companies.status = 'operating'
  GROUP BY 1
  ORDER by 2 DESC
```

## SQL Window Functions

### Intro to window functions

PostgreSQL's documentation does an excellent job of **[introducing the concept of Window Functions](https://www.postgresql.org/docs/9.1/tutorial-window.html)**:

> A window function performs a calculation across a set of table rows that are somehow related to the current row. This is comparable to the type of calculation that can be done with an aggregate function. But unlike regular aggregate functions, use of a window function does not cause rows to become grouped into a single output row — the rows retain their separate identities. Behind the scenes, the window function is able to access more than just the current row of the query result.
> 

The most practical example of this is a running total:

```sql
SELECT duration_seconds,
       SUM(duration_seconds) OVER (ORDER BY start_time) AS running_total
  FROM tutorial.dc_bikeshare_q1_2012

```

You can see that the above query creates an aggregation (`running_total`) without using `GROUP BY`. Let's break down the syntax and see how it works.

### Basic windowing syntax

The first part of the above aggregation, `SUM(duration_seconds)`, looks a lot like any other aggregation. Adding `OVER` designates it as a window function. You could read the above aggregation as "take the sum of `duration_seconds` *over* the entire result set, in order by `start_time`."

If you'd like to narrow the window from the entire dataset to individual groups within the dataset, you can use `PARTITION BY` to do so:

```sql
SELECT start_terminal,
       duration_seconds,
       SUM(duration_seconds) OVER
         (PARTITION BY start_terminal ORDER BY start_time)
         AS running_total
  FROM tutorial.dc_bikeshare_q1_2012
 WHERE start_time < '2012-01-08'

```

The above query groups and orders the query by `start_terminal`. Within each value of `start_terminal`, it is ordered by `start_time`, and the running total sums across the current row and all previous rows of `duration_seconds`. 

Scroll down until the `start_terminal` value changes and you will notice that `running_total` starts over. That's what happens when you group using `PARTITION BY`.

In case you're still stumped by `ORDER BY`, it simply orders by the designated column(s) the same way the `ORDER BY` clause would, except that it treats every partition as separate. It also creates the running total—without `ORDER BY`, each value will simply be a sum of all the `duration_seconds` values in its respective `start_terminal`. Try running the above query without `ORDER BY` to get an idea:

```sql
SELECT start_terminal,
       duration_seconds,
       SUM(duration_seconds) OVER
         (PARTITION BY start_terminal) AS start_terminal_total
  FROM tutorial.dc_bikeshare_q1_2012
 WHERE start_time < '2012-01-08'

```

The `ORDER` and `PARTITION` define what is referred to as the "window"—the ordered subset of data over which calculations are made.

**Note**: You can't use window functions and standard aggregations in the same query. More specifically, you can't include window functions in a `GROUP BY` clause.

```sql
-- Write a query modification of the above example query that shows the duration of each ride as 
-- a percentage of the total time accrued by riders from each start_terminal

SELECT start_terminal,
       duration_seconds,
      SUM(duration_seconds) OVER
        (PARTITION BY start_terminal) AS start_terminal_total,
      (duration_seconds / SUM(duration_seconds) OVER (PARTITION BY start_terminal)) * 100 AS percentage
  FROM tutorial.dc_bikeshare_q1_2012
   WHERE start_time < '2012-01-08'
   ORDER BY 1, 4
```

### The usual suspects: SUM, COUNT, and AVG

When using window functions, you can apply the same aggregates that you would under normal circumstances—`SUM`, `COUNT`, and `AVG`. The easiest way to understand these is to re-run the previous example with some additional functions. 

```sql
SELECT start_terminal,
       duration_seconds,
       SUM(duration_seconds) OVER
         (PARTITION BY start_terminal) AS running_total,
       COUNT(duration_seconds) OVER
         (PARTITION BY start_terminal) AS running_count,
       AVG(duration_seconds) OVER
         (PARTITION BY start_terminal) AS running_avg
  FROM tutorial.dc_bikeshare_q1_2012
 WHERE start_time < '2012-01-08'

```

Alternatively, the same functions with `ORDER BY`:

```sql
SELECT start_terminal,
       duration_seconds,
       SUM(duration_seconds) OVER
         (PARTITION BY start_terminal ORDER BY start_time)
         AS running_total,
       COUNT(duration_seconds) OVER
         (PARTITION BY start_terminal ORDER BY start_time)
         AS running_count,
       AVG(duration_seconds) OVER
         (PARTITION BY start_terminal ORDER BY start_time)
         AS running_avg
  FROM tutorial.dc_bikeshare_q1_2012
 WHERE start_time < '2012-01-08'

```

```sql
-- Write a query that shows a running total of the duration of bike rides (similar to the last example), 
-- but grouped by end_terminal, and with ride duration sorted in descending order.

SELECT end_terminal,
       duration_seconds,
       SUM(duration_seconds) OVER
         (PARTITION BY end_terminal ORDER BY duration_seconds DESC)
         AS running_total
  FROM tutorial.dc_bikeshare_q1_2012
 WHERE start_time < '2012-01-08'
```

`MAX` works in the same way as `SUM` so I’m going to spice up the example with some more advanced syntax. Let’s say that I want to see how a current order stacks up against the highest order quantity among the previous 5 orders for `gloss_qty`. We can do this by adding in some additional syntax in our `ORDER BY` clause.

```sql
   SELECT o.id,
          o.occurred_at,
          o.gloss_qty,
          MAX(gloss_qty) OVER(ORDER BY o.occurred_at
                         ROWS BETWEEN 5 PRECEDING AND 1 PRECEDING) as max_order
FROM demo.orders o
```

After we specify the field to order by, we add a definition for our window size: `ROWS BETWEEN 5 PRECEDING AND 1 PRECEDING`. This clause is essentially saying, "look back across the previous 5 orders (not including the current order) and take the maximum value."

This syntax is flexible and can define any window across your dataset. The syntax typically looks like:

```sql
 ORDER BY [order_var] ROWS BETWEEN window_start AND window_end
```

where `window_start` and `window_end` take on one of the following values:

- `UNBOUNDED PRECEDING` (i.e. all rows before the current row)
- `[VALUE] PRECEDING` (where [VALUE] = # of rows behind the current row to consider)
- `CURRENT ROW`
- `[VALUE] FOLLOWING` (where [VALUE] = # of rows ahead of the current row to consider)
- `UNBOUNDED FOLLOWING` (i.e. all rows after the current row)

### ROW_NUMBER()

`ROW_NUMBER()` does just what it sounds like—displays the number of a given row. It starts at 1 and numbers the rows according to the `ORDER BY` part of the window statement. `ROW_NUMBER()` does not require you to specify a variable within the parentheses:

```sql
SELECT start_terminal,
       start_time,
       duration_seconds,
       ROW_NUMBER() OVER (ORDER BY start_time)
                    AS row_number
  FROM tutorial.dc_bikeshare_q1_2012
 WHERE start_time < '2012-01-08'

```

Using the `PARTITION BY` clause will allow you to begin counting 1 again in each partition. The following query starts the count over again for each terminal:

```sql
SELECT start_terminal,
       start_time,
       duration_seconds,
       ROW_NUMBER() OVER (PARTITION BY start_terminal
                          ORDER BY start_time)
                    AS row_number
  FROM tutorial.dc_bikeshare_q1_2012
 WHERE start_time < '2012-01-08'

```

### RANK() and DENSE_RANK()

`RANK()` is slightly different from `ROW_NUMBER()`. If you order by `start_time`, for example, it might be the case that some terminals have rides with two identical start times. In this case, they are given the same rank, whereas `ROW_NUMBER()` gives them different numbers. In the following query, you notice the 4th and 5th observations for `start_terminal` 31000—they are both given a rank of 4, and the following result receives a rank of 6:

```sql
SELECT start_terminal,
       duration_seconds,
       RANK() OVER (PARTITION BY start_terminal
                    ORDER BY start_time)
              AS rank
  FROM tutorial.dc_bikeshare_q1_2012
 WHERE start_time < '2012-01-08'

```

You can also use `DENSE_RANK()` instead of `RANK()` depending on your application. Imagine a situation in which three entries have the same value. Using either command, they will all get the same rank. For the sake of this example, let's say it's "2." Here's how the two commands would evaluate the next results differently:

- `RANK()` would give the identical rows a rank of 2, then skip ranks 3 and 4, so the next result would be 5
- `DENSE_RANK()` would still give all the identical rows a rank of 2, but the following row would be 3—no ranks would be skipped.

```sql
-- Write a query that shows the 5 longest rides from each starting terminal, ordered by terminal,
-- and longest to shortest rides within each terminal. Limit to rides that occurred before Jan. 8, 2012.

SELECT *
FROM (
      SELECT start_terminal,
             duration_seconds,
             start_time,
             ROW_NUMBER() OVER (PARTITION BY start_terminal
                          ORDER BY duration_seconds DESC)
                    AS longest_rides
              FROM tutorial.dc_bikeshare_q1_2012
             WHERE start_time < '2012-01-08'
             ) sub 
WHERE sub.longest_rides <= 5
```

### NTILE

You can use window functions to identify what percentile (or quartile, or any other subdivision) a given row falls into. The syntax is `NTILE(*# of buckets*)`. In this case, `ORDER BY` determines which column to use to determine the quartiles (or whatever number of 'tiles you specify). For example:

```sql
SELECT start_terminal,
       duration_seconds,
       NTILE(4) OVER
         (PARTITION BY start_terminal ORDER BY duration_seconds)
          AS quartile,
       NTILE(5) OVER
         (PARTITION BY start_terminal ORDER BY duration_seconds)
         AS quintile,
       NTILE(100) OVER
         (PARTITION BY start_terminal ORDER BY duration_seconds)
         AS percentile
  FROM tutorial.dc_bikeshare_q1_2012
 WHERE start_time < '2012-01-08'
 ORDER BY start_terminal, duration_seconds

```

Looking at the results from the query above, you can see that the `percentile` column doesn't calculate exactly as you might expect. If you only had two records and you were measuring percentiles, you'd expect one record to define the 1st percentile, and the other record to define the 100th percentile. Using the `NTILE` function, what you'd actually see is one record in the 1st percentile, and one in the 2nd percentile. You can see this in the results for `start_terminal` 31000—the `percentile` column just looks like a numerical ranking. If you scroll down to `start_terminal` 31007, you can see that it properly calculates percentiles because there are more than 100 records for that `start_terminal`. If you're working with very small windows, keep this in mind and consider using quartiles or similarly small bands.

```sql
-- Write a query that shows only the duration of the trip and the percentile into which that duration falls 
-- (across the entire dataset—not partitioned by terminal).

SELECT duration_seconds,
       NTILE(100) OVER
         (ORDER BY duration_seconds)
         AS percentile
  FROM tutorial.dc_bikeshare_q1_2012
 WHERE start_time < '2012-01-08' 
 ORDER BY duration_seconds DESC
```

### LAG and LEAD

It can often be useful to compare rows to preceding or following rows, especially if you've got the data in an order that makes sense. You can use `LAG` or `LEAD` to create columns that pull values from other rows—all you need to do is enter which column to pull from and how many rows away you'd like to do the pull. `LAG` pulls from previous rows and `LEAD` pulls from following rows:

```sql
SELECT start_terminal,
       duration_seconds,
       LAG(duration_seconds, 1) OVER
         (PARTITION BY start_terminal ORDER BY duration_seconds) AS lag,
       LEAD(duration_seconds, 1) OVER
         (PARTITION BY start_terminal ORDER BY duration_seconds) AS lead
  FROM tutorial.dc_bikeshare_q1_2012
 WHERE start_time < '2012-01-08'
 ORDER BY start_terminal, duration_seconds

```

This is especially useful if you want to calculate differences between rows:

```sql
SELECT start_terminal,
       duration_seconds,
       duration_seconds -LAG(duration_seconds, 1) OVER
         (PARTITION BY start_terminal ORDER BY duration_seconds)
         AS difference
  FROM tutorial.dc_bikeshare_q1_2012
 WHERE start_time < '2012-01-08'
 ORDER BY start_terminal, duration_seconds

```

The first row of the `difference` column is null because there is no previous row from which to pull. Similarly, using `LEAD` will create nulls at the end of the dataset. If you'd like to make the results a bit cleaner, you can wrap it in an outer query to remove nulls:

```sql
SELECT *
  FROM (
    SELECT start_terminal,
           duration_seconds,
           duration_seconds -LAG(duration_seconds, 1) OVER
             (PARTITION BY start_terminal ORDER BY duration_seconds)
             AS difference
      FROM tutorial.dc_bikeshare_q1_2012
     WHERE start_time < '2012-01-08'
     ORDER BY start_terminal, duration_seconds
       ) sub
 WHERE sub.difference IS NOT NULL

```

### Defining a window alias

If you're planning to write several window functions in to the same query, using the **same window,** you can create an **alias**. Take the `NTILE` example above:

```sql
SELECT start_terminal,
       duration_seconds,
       NTILE(4) OVER
         (PARTITION BY start_terminal ORDER BY duration_seconds)
         AS quartile,
       NTILE(5) OVER
         (PARTITION BY start_terminal ORDER BY duration_seconds)
         AS quintile,
       NTILE(100) OVER
         (PARTITION BY start_terminal ORDER BY duration_seconds)
         AS percentile
  FROM tutorial.dc_bikeshare_q1_2012
 WHERE start_time < '2012-01-08'
 ORDER BY start_terminal, duration_seconds

```

This can be rewritten as:

```sql
SELECT start_terminal,
       duration_seconds,
       NTILE(4) OVER ntile_window AS quartile,
       NTILE(5) OVER ntile_window AS quintile,
       NTILE(100) OVER ntile_window AS percentile
  FROM tutorial.dc_bikeshare_q1_2012
 WHERE start_time < '2012-01-08'
WINDOW ntile_window AS
         (PARTITION BY start_terminal ORDER BY duration_seconds)
 ORDER BY start_terminal, duration_seconds

```

The `WINDOW` clause, if included, should always come after the `WHERE` clause.

## Advanced windowing techniques

You can check out a complete list of window functions in Postgres (the syntax Mode uses) in the **[Postgres documentation](http://www.postgresql.org/docs/8.4/static/functions-window.html)**. If you're using window functions on a **[connected database](https://mode.com/help/articles/connecting-mode-to-your-database/)**, you should look at the appropriate syntax guide for your system.

If you're interested, we rounded up the **[top five most popular window functions](https://mode.com/blog/most-popular-window-functions-and-how-to-use-them/?utm_medium=referral&utm_source=mode-site&utm_campaign=sql-tutorial)** and expand on the commonalities of **[window functions in Python and SQL](https://mode.com/blog/bridge-the-gap-window-functions/?utm_medium=referral&utm_source=mode-site&utm_campaign=sql-tutorial)**.

[Common Table Expressions (CTE) to Keep Your SQL Clean](https://mode.com/blog/use-common-table-expressions-to-keep-your-sql-clean)

## Performance Tuning SQL Queries

## Pivoting Data in SQL