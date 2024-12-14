---
tags:
  - databases
date: 2024-10-29
source: "[[DATA 101]]"
---

Transforming JSON to Rectangular Data comes with tradeoffs
- Repeating information
- Joining across multiple tables

#### JSON (Semistructured Data)

###### Pros:
- Flexibility in attributes
	- Very easy to add new tuple without adjusting any fixed schema
- Avoid unnecessary joins
	- Denormalization, i.e capturing info across multiple relations
- Easy to read data

###### Cons:
-  Update/delete anomalies
	- Redundancy of relation data due to denormalization/nesting
	- No constraints or validations
- Finding information about one relation still requires examining the entire JSON.
	- Depending on the outer nesting, could make it tricky to find inner-nested information
	- e.g., Person→Order→Product means Product information is hard to find
- Harder to make compact due to “self-describing” nature
	- Repeated keys occupy space!
	- For fixes, see: binary JSON representations, or assuming fixed structure of specific tuples


#### XML: eXtensible Markup Language

A lot of effort went into developing XML formalism and query languages

- Schema specification: 
	- Simple: DTD (document type definition)
	- More powerful: XML Schema
- Query languages
	- Simple: XPath: a “path” based query language
	- (because XML is also tree-structured) Path from root to specific node with certain characteristics
	- More powerful: XQuery


### Data Models for Semi-Structured Data

Key Value Stores
- e.g. Amazon DynamoDB, Redis, Voldemort, Memcached
    
Document Stores
- Popular Formats: JSON, XML
- e.g. MongoDB, CouchDB, SimpleDB


While semi-structured data models existed prior to structured data, it is clear that relational databases “won” in the long term.

Several reasons for why nested relations fell out of DBMS vogue:
- Complex and cumbersome to traverse nested relations to find specific bits of data
	- (e.g., traversing a film hierarchy just to find information about actors)

- Nested model mixes physical and logical data organization.
	- In the relational model, we can rearrange the data on disk and the relation would still be equivalent (e.g., CLUSTER).
	- For nested models, however, we can’t; therefore we can’t optimize it for queries.

- Lots of redundancy, leading to update and deletion anomalies.

However, many data transfer lake/lakehouse applications means that we will have to work with semi-structured data somehow!


#### Document Stores

Document Stores are data systems that primarily operate on JSON.
A document: Each JSON element. Basic unit of retrieval in document stores.

Document stores support a set of operations:
- Searching across documents (essentially, selections / filters)
- Primitive aggregation
- However, typically no joins (beyond what is already done via denormalization)
- Possibly primitive indexing, e.g., to retrieve documents based on certain criteria.

#### When to use document stores ?

It makes sense to use document stores if our data is inherently denormalized, and
- We only want to operate on the denormalized data as a whole.
	- I.e., we rarely want to look at pieces of the data 
	- Example: If data is organized by film→Actors, and we never want to look at Actors.
    
- We don’t need the full power of SQL.
	- e.g., “simple” queries, by primary key
	- e.g., no joins needed
    
- The schema often changes, and yet we rarely update old data.
	- i.e., having redundancy doesn’t create issues.


### Storing JSON in RDBMS

Many Relational Database Systems (RDBMSes) also provide support for JSON as a type.

- `CREATE TABLE nobel_prizes(nobel json);`
	- Declares a column nobel to contain json (or, can specify JSON binary: jsonb)
	- Creates a row per document

- Can allow for mixing of relational and semi-structured syntax, e.g.,
    
```sql
SELECT * FROM nobel_prizes  
WHERE nobel @>'{"year": "1990"}';
```

- Can turn into a full table with JSON_TABLE(), and even build indexes on JSON columns.

