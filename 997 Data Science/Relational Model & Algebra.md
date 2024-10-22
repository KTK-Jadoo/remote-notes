---
tags:
  - databases
date: 2024-09-05
source: "[[DATA 101]]"
---

Theory of operations that help us transform relations.

- Relations are operands

Introduced by _Edgar F. Codd_ (Relational Model for Data For Large Data Banks): 

- [[SQL]]: first commercial language using Codd's Model

__Table/ Relation:__ A [[Set Theory|set]] of tuples with a predefined set of attributes
- Each attribute has a type, called domain.
- Each domain is atomic.
- Each tuple in the relation has values for each attribute.

__Schema:__ The structure, format, or scaffolding defining a relation.
- Relation name, attribute names, attribute domains

__Relation Algebra Notation:__
$$\text{Songs (name String, artist, String, album String,  peak Integer, …)}$$


There are six primitive RA operations, from which all others can be built:

- selection
- projection
- renaming
- cartesian product (or simply, product)
- union
- difference


## Primitive Operators

### Selection (Cross out rows)

Operators that
- take in exactly one operand, a relation $R$
- and output the relation $S$
$$S = f(R)$$



### Projection (Cross out columns)




### Renaming

$$\rho_{S}({A_{1}, A_{2}, A_{3}...A_{n}})$$



Summary: 

![[Pasted image 20240905100255.png]]


[[SQL#Order of Execution]]
- WHERE --> Selection
- SELECT --> Project
- AS --> Rename


### Cross Product 
$$R \times R$$


### Union


- Schema isn't changed.



### Difference

- Schema isn't changed.



## Non-Primitive Operators

### Intersection
 TO-DO



### Theta Join (Equi Join)
$$R_{1}\bowtie_\theta R_{2}$$
- Theta Join is SQL _Inner join_.
- A cross Product of $R_1$ and $R_2$, followed by a selection on $\theta$

### Natural Join
- Equi Join + Rename
- drops one of the duplicate columns and renames

```sql
SELECT *
FROM Crew
	NATURAL JOIN
People;
```


### Outer Join and Extended RA



### Relational Algebra and [[Database Management Systems]]


__Dataframe:__ (Pandas, R)
Abstraction/API to represent, clean, and structure your data
- Incremental, composable operations
- Embedded into common PLs (pandas: “Python Data Analysis Library”)
- Originally emerged in the late 70s when statisticians wanted to operate on heterogeneous datasets

__Relational Database:__ (Postgres, SQLite, My SQL)
Traditional, time-tested solutions to managing data at scale
- SQL
- Declarative
- Originated in the 70s via parallel efforts at IBM and UC Berkeley

__[[Spark]]:__ 
Distributed, parallel computing framework
- Supports various interfaces, all of which are relation-like:
- Pandas-like DataFrame API, Spark DataFrame API, SQL
- Originally developed at UC Berkeley in 2012

### Bag/Set Operations with subqueries


