---
tags:
  - "#databases"
date: 2024-09-01
source: "[[DATA 101]]"
---
**Structured Query Language**, or **SQL** (pronounced “sequel”), is a high-level data transformation language supported by [[Relational Model & Algebra|relational databases]] and other data systems like [[Spark]]. It is [[Declarative Programming Languages|declarative]] rather than imperative.

This course uses a dialect or flavor of SQL called [[PostgreSQL]] (shortened as Postgres, pronounced “POST-gress”). PostgreSQL is also the eponymous free, open-source **database management system ([[Database Management Systems|DBMS]])** that is SQL-compliant. 

The core functionality of SQL is restricted in comparison to, say, Python.

- By design—the system can then _automatically optimize_ the queries.
- Still quite powerful: SQL can do most things you want to do with data.
- …and extensions allow us to bridge the gap.

## Order of Execution

As a declarative language, SQL statements are not evaluated left-to-right, top-to-bottom. Instead, each SQL query is meant to read like English. The execution order, however, evaluates certain _clauses_ in the query before other clauses in the query. Conceptually:

```sql
SELECT S                -- 5
FROM R1, R2, ...        -- 1
WHERE C1                -- 2
GROUP BY A1, A2, ...    -- 3
HAVING C2;              -- 4
```


Order of evaluation:
1. `FROM`: Fetch the tables and compute the [[Cross Product|cross product]] of the relations R1, R2, …
2. `WHERE`: For each tuple from 1, keep only those that satisfy condition C1
3. `GROUP BY`: Create groups of tuples by A1, A2, etc. At this time, for each group, compute all aggregates needed for C2 and S (below).
4. `HAVING`: For each group, check if condition C2 is satisfied.
5. `SELECT`: Add to output based on attribute set S.

Note that `WHERE` is therefore a row filter that happens **before** groups are made, whereas `HAVING` is a group filter that happens **after** groups are made.

__Aggregations__ (aggregate functions) compute a single result from a set of columns.

- COUNT(\*): count all input rows
- SUM
- AVG
- MIN
- MAX

## Query Design

- _Strategy point 1_: Look at the schemas. Which tables have the information that we need? (Hint: use `\d` meta-command in psql)
- _Strategy point 2_: Joins modify records.
	- extending each record w/more attributes, or
	- expanding each table w/more records & attributes.
	- Likely changes what a record represents!!
- _Strategy point 3_: Think about WHERE first, then SELECT. (easier to debug)
- *Strategy point 4*: Consider what makes a query readable based on the originally posed question.



qUESTION 4 ON pROJECT 0