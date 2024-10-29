---
tags:
  - databases
date: 2024-10-29
source: "[[DATA 101]]"
---
MongoDB is a very popular[[Semistructured Data#Document Stores| Document Store]].

- Short for hu*mongo*us
- Facebook crosses 150 million users.
- Amazon profit jumps ~70%.
- IPO in 2017

MongoDB quickly evolved to meet a need.

- Early versions focused on storing and querying JSON documents quickly.
	- No joins
	- Limited query options
- Now, built to use JSON-like schemas.
- Now supports left outer joins
- Still limited query options, but many improvements compared to earlier versions.

In a MongoDB database,

- There are multiple collections.
- Each collection contains multiple documents of type object.
- Each object of which consists of field-value pairs.

Example document in some collection:

```json
{ _id: ObjectId("5fb55fad3d993"), qty : 1,  status : "D",

                        size : {h : 14, w : 21}, tags : ["a", "b"] }
```

![[Pasted image 20241029101811.png]]

\_id is a special field in each document.

- The primary key (indexed by default).
- First field of each document.

If \_id is not present during ingest (database load), then it will be added.
Special operation during projections (more later)


There are three main types of query in the __MongoDB Query Language__, or MQL:

1. Retrieval queries: Restricted queries of the form SELECT-WHERE-ORDER-BY-LIMIT
2. Aggregation queries: A general pipeline of operators
	- A bit of a misnomer; can capture retrievals as a special case
3. Update queries



All queries are invoked as `db.collection.operation1(...).operation2(...)`

- Object-oriented and pipelined
	- “input”: a name of a collection (e.g., named collection) in database db
	- output: collection
- Looks like pandas DataFrames, not SQL!	    
- Syntax (again) similar-ish to JavaScript

PyMongo: [https://pymongo.readthedocs.io/en/stable/](https://pymongo.readthedocs.io/en/stable/) 

Note: MongoDB Atlas is the integrated MongoDB database suite on the cloud (AWS, Azure, GCP). We are using local mongo.


### MongoDB Notation

#### $
When $ is used on the “field” side of a field-value expression,  
it indicates a special keyword.

- E.g., $gt, $lte, $add, $elemMatch, …
    

If binary operator: `{LOperand : { $keyword : ROperand}} {“qty” : {$gt : 30}}`

If multi-argument operator, generally arrays:

`{$keyword : [argument_{list]} {$add : [1, 2]} 
`
Another example, if you’re curious:

`db.prizes.find(  {"overallMotivation": {"$exists": 1} })`


#### Dot(.)

The dot "." is used to drill deeper into nested objects/arrays

- Recall a value is a primitive, a nested object, or an array of primitives/objects.

"<expr>.Y"
	- <expr> as a nested object: Y is a field within that object
	- <expr> as an array of nested objects: Y is a field within objects of that array

"<expr>.n"]
	- n is the n-th value (0-indexed) in the <expr> array

Note: For mongo CLI, the dot notation expression must be in quotes [[link](https://www.mongodb.com/docs/v7.0/tutorial/query-arrays/#query-for-an-element-by-the-array-index-position)].


collection.find(predicate, projection) 

- The optional projection parameter indicates the fields to in/exclude in each document of the output collection.
    

- 1s: indicate fields that you want, OR
    
- 0s: indicate fields that you don’t want.
    
- Exception: the primary key _id is always present unless explicitly excluded.