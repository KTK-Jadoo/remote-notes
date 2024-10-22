---
tags:
  - "#databases"
date: 2024-09-01
source: "[[DATA 101]]"
---
**Structured Query Language**, or **SQL** (pronounced "sequel"), is a high-level data transformation language supported by relational databases and other data systems like Spark. It is **declarative** rather than imperative, meaning:

*   Describes what rather than how
*   It's query-centric rather than code-centric

## PostgreSQL

This course uses a dialect or flavor of SQL called **PostgreSQL** (also known as Postgres; [see pronunciation](https://wiki.postgresql.org/wiki/FAQ#What_is_PostgreSQL.3F_How_is_it_pronounced.3F_What_is_Postgres.3F)). PostgreSQL is also the eponymous free, open-source **database management system (DBMS)** that is SQL-compliant. We'll discuss DBMSes thoroughly throughout this course.

We draw broadly from the [PostgreSQL documentation](https://www.postgresql.org/docs/current/index.html) for much of the SQL syntax, conventions, and concepts in this course. When in doubt, clarify with the official documentation. If there is an inconsistency between the documentation and the course notes, please post on our course forums so we can update the course notes. Thanks!

## SQL Query Order of Execution

You have likely had some experience with other SQL dialects---perhaps duckDB, or SQLite. This note therefore starts with a quick refresher of the **SQL query structure**, to make for easy reference. The rest of this note follows with conceptual explanations and details.

As a declarative language, SQL statements are not evaluated left-to-right, top-to-bottom.
Instead, each SQL query is meant to read like English. The execution order, however, evaluates certain *clauses* in the query before other clauses in the query. Conceptually:

```
SELECT S                -- 5
FROM R1, R2, ...        -- 1
WHERE C1                -- 2
GROUP BY A1, A2, ...    -- 3
HAVING C2;              -- 4
```

Order of evaluation:
1. `FROM`: Fetch the tables and compute the cross product of the relations R1, R2, …
1. `WHERE`: For each tuple from 1, keep only those that satisfy condition C1
1. `GROUP BY`: Create groups of tuples by A1, A2, etc. At this time, for each group, compute all aggregates needed for C2 and S (below).
1. `HAVING`: For each group, check if condition C2 is satisfied.
1. `SELECT`: Add to output based on attribute set S.

Note that `WHERE` is therefore a row filter that happens **before** groups are made,
whereas `HAVING` is a group filter that happens **after** groups are made.

```{note}
By convention, SQL keywords are in all caps, e.g., `SELECT *`, while attributes are in lowercase.
```

```{note}
End queries with a semicolon.
```

## The Relational Data Model

Let's start with terminology drawn from the **relational data model**.
The relational data model is the primary abstraction of the SQL landscape.

A **relation** is a collection of tuples, each with a predefined collection of **attributes**. Each attribute has a type, called a domain, which must be atomic (e.g., string or integer). The order of the tuples in a relation does not matter. Relational algebra, the theoretical foundation of SQL, assumes that relations are sets of tuples. Generally, SQL relations allow for duplicate tuples, but also does not guarantee that tuples are stored in a particular order.

The **schema** of a relation is a list of attribute names and their domains (the data types associated with each attribute). The schema often includes the relation name itself, if it exists. For example, in the IMDb dataset, the schema for the `title` relation is:

```sql
title (title_id String, ordering Integer, title String,
        region String, language String...)
```

An **instance** is a specific instantiation of the relation, i.e., tuples with specific values. This word is used less often, but we define it here to draw attention to the idea that a relation could hold different tuples over time.

In general, think relation as a table of data whose columns (i.e., attributes) are organized according to a specific relational schema. You will hear "relation" and "table" used interchangeably, though the former is more specific (as we will see when we discuss Relational Algebra). A **relational database** is a collection of relations, which are often related to each other according to some **database schema** or **relational schema**.

## SELECT-FROM-WHERE (SFW)

Let's start simple. Below is the `SELECT FROM WHERE` (**SFW**) query structure, the most standard SQL query structure to extract records from a relation:

```sql
SELECT attributes
FROM tables
WHERE condition about tuples in tables;
```

Remember---SQL is a declarative language! Instead of evaluating the SQL query from first to last line, it is evaluated like so:

1. `FROM` clause: lists the table
1. `WHERE` clause: filters for the matching tuples
1. `SELECT` clause: filters for the specified attributes.

### SELECT list of expressions

`SELECT` can employ:
* Renamed attributes with `AS`
* Expressions
* Case statements
* Many more functions (string, date-time…)

### FROM clause

The FROM clause can include either table names separated by commas (implying a cross join, or cross product of all tuples), or expressions involving table JOINs. We cover JOINs in a separate section.

### WHERE clause

The WHERE clause can include logical operators (e.g., AND, OR, NOT) or comparison operators (=, >=, <> equivalently !=, etc.). Postgres documentation:
* [Section 9.1](https://www.postgresql.org/docs/current/functions-logical.html)
* [Section 9.2](https://www.postgresql.org/docs/current/functions-comparison.html)

The attributes used in the WHERE clause do not necessarily need to be included in the SELECT list, but they should be discoverable from the tables (or their aliases, if they exist) identified in the `FROM` clause.

**Scalar subquery**: We discuss subqueries in much more detail in a separate section, but note that you can use SELECT-FROM-WHERE subqueries in the WHERE condition, provided that they are **scalar**. A scalar subquery returns a single value (e.g., a single tuple with a single attribute value) and can subsequently be treated as a scalar in a larger expression.

To find the ids of stops with the oldest individuals:

```sql
SELECT s1.id
FROM stops AS s1
WHERE s1.age >= (
    SELECT MAX(age) FROM stops AS s2
);
```

Note that we alias the second stops relation.

## Aggregations

We can also **aggregate** a column in a `SELECT` clause according to a particular aggregation function: `SUM`, `MIN`, `MAX`, `AVG`, `COUNT`, etc.

```sql
SELECT MAX(age), AVG (age)
FROM stops;
```

The above query computes the minimum and maximum values of the `age` attribute from the `stops` relation. To be more specific, the return value of the above SQL query is an unnamed relation with a single tuple; the relation schema contains two numeric types:

```
 max | avg
-----+------
 32  | 25.3

```

The precise attribute names (above, "max" and "avg") varies based on SQL flavor and may contain the atribute itself (e.g., "MAX(age)", "avg(age)", etc.).

`COUNT(*)` uses the special asterisk symbol (`*`) to count the number of tuples.

```
SELECT COUNT(*) FROM stops;
```

returns the number of tuples in the Stops relation.

### Aggregation Examples

Aggregation expression can include SQL keywords and even subqueries (we discuss subqueries in much more detail in a separate section).

**NULL** values are not involved in aggregation:
The below query counts total rows, counts non-null ages, and computes average age. The first two attributes could have different values if there are NULL ages.

```sql
SELECT COUNT(*), COUNT(age), AVG(age)
FROM stops;
```

**DISTINCT** removes duplicates prior to aggregation. [Read more](https://www.postgresql.org/about/featurematrix/detail/392/) about how NULL values are considered.

```sql
SELECT COUNT(DISTINCT location)
FROM stops;
```

## Grouping

In some cases, we may want to compute an aggregate for each "group" of tuples as opposed to an overall COUNT, MAX or SUM. To do so, we add a `GROUP BY` clause after the SELECT-FROM-WHERE. For example, say we wanted to find average and minimum ages for each location:

```sql
SELECT location, AVG(age) AS avgage, MIN (age) as minage
FROM stops
GROUP BY location;
```

Notably, if aggregation is used, then each element of the SELECT clause **must either be an aggregate or an attribute in the GROUP BY list**. This is because if an attribute is not being aggregated or being grouped, we have no way to "squish" the values down per group.

Also note that `AVG` (and other aggregations) ignore null values; we discuss this more below.

Postgres supports many aggregate statistics: standard deviation, covariance, regression slope/intercept, correlation coefficient, and more. Say we wanted to find the median age of stopped people:

```
SELECT zip, PERCENTAGE_DISC(0.5)
WITHIN GROUP (ORDER BY age)
FROM stops;
```

We can also use more sophisticated syntax in GROUP BYs; for example, the following query computes the average ages of stops across various days for West Oakland and Rockridge individually:

```sql
SELECT days,
    AVG (CASE WHEN location = 'West Oakland' THEN age ELSE NULL END) AS west_oakland_avg,
    AVG (CASE WHEN location = 'Rockridge' THEN age ELSE NULL END) AS rockridge_avg
FROM stops
GROUP BY days;
```

In the above query, we compute the averages using a `CASE` statement.

### HAVING

Suppose we want to filter a GROUP BY on some condition. We can use a HAVING clause, which typically precedes a GROUP BY. The HAVING condition is applied to each group, and groups not satisfying the condition are eliminated. For example, say we wanted to compute the locations with at least 30 stops:

```sql
SELECT location, COUNT (*)
FROM stops
GROUP BY location
HAVING COUNT (*) > 30;
```

Similarly to SELECT clauses, each attribute mentioned in a HAVING clause
must either be part of the GROUP BY or be aggregated.


## Symbols and Additional Keywords

### The asterisk (`*`)

The asterisk (`*`) is a wildcard character that selects all attributes from the table. It can be used in place of any explicit parameter. For example:

```sql
SELECT *
FROM Title;
```

The above query effectively gets all tuple and all attributes from the `Title` table by doing the following:
* `FROM`: Gets the `Title` table
* `WHERE`: Applies the all-pass filter onto tuples
* `SELECT *`: Gets all attributes

It can also be used in aggregations to denote no explicit parameter, e.g., `COUNT(*)`.

Read more in the PostgreSQL docs, [Section 4.1.4](https://www.postgresql.org/docs/current/sql-syntax-lexical.html#SQL-SYNTAX-SPECIAL-CHARS).

### AS

The AS keyword serves several purposes. In the SELECT and FROM clauses, it functions as a renamer, which creates aliases for attributes or tables, respectively.

```sql
SELECT
  a.title_id AS title_id,
  a.title AS aka_title,
  t.title AS orig_title
FROM
  akas AS a,
  titles AS t;
```

As a syntactic shortcut, the AS keyword can sometimes be omitted, as above in the FROM clause. See the "[Omitting the AS keyword](https://www.postgresql.org/docs/current/sql-select.html)" section of the Postgres documentation. Based on the [Mozilla SQL style guide](https://docs.telemetry.mozilla.org/concepts/sql_style), best practices are to prefer explicit use of AS.

Depending on when/where you create an alias using AS, you may need to use that alias throughout the query:
* In the FROM clause, the table alias completely hides the actual name of the table, and the alias must be used throughout in WHERE, SELECT, etc.
* In the SELECT clause, the alias is not created until the SELECT list of expressions is computed.
* For more, read the official [SELECT SQL Command documentation](https://www.postgresql.org/docs/current/sql-select.html#SQL-SELECT-LIST) and search for "alias".

### CAST

Casting converts one attribute type to another. For example, suppose that `runtime_minutes` were an integer, and we wanted to compute `runtime_hours`, with reasonable precision. Also suppose that `premiered` was a string, but should be interpreted as an integer `year`:

```sql
SELECT primary_title, type,
     CAST(premiered AS INTEGER) AS release_year,
     runtime_minutes,
     CAST(runtime_minutes AS
         DOUBLE PRECISION)/60 AS
         runtime_hours
FROM titles;
```

See [Chapter 8](https://www.postgresql.org/docs/current/datatype.html) of the Postgres documentation for a list of valid data types.

### NULL

Tuples can have NULL values for attributes (e.g., if missing, inapplicable to the current tuple, or unknown), which we need to take note of when performing queries. SQL uses a three-logical system, meaning that NULLs do not satisfy boolean conditions. For example, if a tuple value is `NULL`, `born < 2023` and `born >= 2023` will both evaluate to `FALSE`. This leads to some unintuitive behavior, for example:

```sql
SELECT born FROM people WHERE born < 2023 OR born >= 2023;
```

The above query will return all tuples that don't have a `NULL` born value, not all the tuples in the relation! If we want all the tuples, we need to explicitly test for `NULL`:

```sql
SELECT born FROM people WHERE born < 2023 OR born IS NULL;
```

For aggregations, `NULL` values are generally excluded. For example, the average of a column will be the average of all the non-null values in that column. However, if all the values in the column are `NULL`, the aggregation will also return `NULL`.

Read more about the [three-valued logic system of SQL](https://www.postgresql.org/docs/current/functions-logical.html).

### CASE

The CASE keyword enables conditional expressions. We refer you to the PostgreSQL docs [Section 9.18](https://www.postgresql.org/docs/current/functions-conditional.html) for more information.

### DISTINCT

The DISTINCT keyword removes duplicate rows from the current result set. The following query returns all unique `(title, title_id)` tuples from the `titles` table:

```sql
SELECT DISTINCT primary_title, title_id
FROM titles;
```

DISTINCT may also be used in aggregation. The following counts all distinct years by removing duplicates prior to aggregation:

```sql
SELECT COUNT(DISTINCT premiered)
FROM titles;
```

To specify distinctness on a subset of attributes, see the [DISTINCT Postgres documentation](https://www.postgresql.org/docs/current/sql-select.html#SQL-DISTINCT).


See also:
- [[String Manipulation]]
- [[Truncating Relations]]

# Creating Tables and Views from Data
## Copying Data to new Tables

Suppose we want the result of a SQL query to act as a new table that we can query. For example, the following query turns a `SELECT` statement into another table:

```sql
CREATE TABLE citation_stops AS (
    SELECT gender, citation
    FROM stops
    WHERE citation = True
);
```

After running this command, we now can query `citation_stops` directly. But if the **base table**, in this case the `stops` table, changes (e.g., gets new records), we have to recreate `citation_stops` to reflect the new changes!

Similarly, we should be careful that if we were to modify the rows of `citation_stops`, there would be no updates to our base table.

## Creating (Virtual) Views

To avoid manually recreating derived tables, we can instead define a **view**, as follows:

```sql
CREATE VIEW citation_stops AS (
    SELECT gender, citation
    FROM stops
    WHERE citation = True
);
```

In views (also known as virtual views), outputs are not stored, and any time a user queries the view (i.e., `citation_stops`), the output is computed on demand. Think of this as a variable or as a virtual relation that is more convenient to query than the base table.

## Materialized Views

On the flip side, suppose we want to create a view and query it frequently. The naive method of creating a view might be slow because the view is computed on demand every time a query is run. To solve this issue, we can define a **materialized view**, as follows:

```sql
CREATE MATERIALIZED VIEW citation_stops AS (
    SELECT gender, citation
    FROM Stops
    WHERE citation = True
);
```

In materialized views, outputs are stored just like they are in regular tables (but not like in virtual views). Materialized views are _sometimes_ automatically updated as base tables change, but since they must be
rematerialized frequently, they might add unnecessary overhead to base table updates. So, data engineers (you!) must be thoughtful about what views to keep materialized and what views to keep virtual.

**Note:** In PostgreSQL, materialized views are _not_ automatically updated when the base table changes. You must [manually refresh][refresh_docs] the view periodically.

Materialized Views are great for scenarios that have complex queries which are frequently used, but _data_ that changes infrequently. For example, you might create a materialized view "prior_month_stops_in_location_x".


# Common Table Expressions (CTE)

Sometimes, we may only want to create a view and query it right away---as part
of breaking down a larger SQL query. A **common table expression** (CTE) is a type of
temporary table which exists only for the duration of one query. We can define a CTE as follows:

```sql
    WITH citation_stops AS (
      SELECT gender, citation
      FROM stops
      WHERE citation = True
    )
    SELECT * FROM citation_stops;
```

Like virtual views, CTEs are computed on demand. But unlike virtual views, their lifetime is restricted to the query. However, compared to subqueries, we can use the same CTE (e.g. `citation_stops`) as many times as we need within a longer query, without having to recompute the result.

<!-- TODO: Introduce Recursive CTEs -->


# Subqueries
A parenthesized SQL query statement (a **subquery**) can be used as a value in various places of a larger SQL query. We could use subqueries as scalars or sets.
## Scalar Subqueries

If a subquery returns a single tuple with a single attribute value, it can be treated as a scalar in expressions. Suppose we want to collect all the stops that happened at the same location as `id = 123`. We could issue a query as follows, with the parenthesized statement as the subquery:

```sql
SELECT S1.id, S1.race, S1.location
FROM stops S1
WHERE S1.location = (
    SELECT S2.location FROM stops S2 WHERE S2.id = 123
);
```

Note that when using subqueries, it's important to define relations with relevant variables (i.e., S1 and S2) such that when accessing attributes, it's clear which relation's attribute is being accessed. We could also rewrite this query to use a CTE (i.e., `WITH` statement) instead of a subquery:

```sql
WITH location_123 AS (
    SELECT location FROM Stops WHERE id = 123
)
SELECT S1.id, S1.race, S1.location
FROM Stops as S1, location_123
WHERE S1.location = location_123.location;
```

## EXISTS

We can use the `EXISTS` or `NOT EXISTS` keywords in `WHERE` clauses to use results of a subquery in set form. For example, suppose we want to determine all the Stops that are the only one in their zipcode:

```sql
WITH stops_zips AS (
    SELECT * FROM stops NATURAL JOIN zips
)
SELECT *
FROM stops_zips SZ1
WHERE NOT EXISTS (
    SELECT *
    FROM stops_zips SZ2
    WHERE SZ1.zipcode = SZ2.zipcode
            AND SZ1.id != SZ2.id
);
```

In the above query, the subquery returns a set of all zips that have more that one stop, i.e. the `WHERE` keyword finds all the tuples that have the same zipcode as another, but with a unique ID, which is then used with the `NOT EXISTS` keyword to return locations of stops that do not have an entry in the subquery set.