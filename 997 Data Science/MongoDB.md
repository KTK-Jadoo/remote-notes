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

## MongoDB Query Language

There are three main types of query in the __MongoDB Query Language__, or MQL:

1. __Retrieval queries__: Restricted queries of the form SELECT-WHERE-ORDER-BY-LIMIT
2. __Aggregation queries__: A general pipeline of operators
	1. A bit of a misnomer; can capture retrievals as a special case
3. __Update queries__



All queries are invoked as `db.collection.operation1(...).operation2(...)`

- Object-oriented and pipelined
	- “input”: a name of a collection (e.g., named collection) in database db
	- output: collection
- Looks like pandas DataFrames, not SQL!	    
- Syntax (again) similar-ish to JavaScript

PyMongo: [https://pymongo.readthedocs.io/en/stable/](https://pymongo.readthedocs.io/en/stable/) 

Note: MongoDB Atlas is the integrated MongoDB database suite on the cloud (AWS, Azure, GCP). We are using local mongo.


### Retrieval Queries

Retrieval queries are called via methods on a specific document collection within a database.

- Returns documents (or single one, as in find_one() that match \<predicate\>).
-  Optional: keep fields as specified in \<projection\>.
- Parameter types: both \<predicate\> and \<projection\> expressed as objects.

To return all documents in the collection: collection.find({})

collection.find(predicate, projection) 

- The optional projection parameter indicates the fields to in/exclude in each document of the output collection.
- 1s: indicate fields that you want, OR
- 0s: indicate fields that you don’t want.
    

Exception: the primary key _id is always present unless explicitly excluded.


![[Pasted image 20241031095544.png]]


### Aggregation Queries

**Aggregation queries** are composed of a **linear pipeline of stages**.

• Each stage manipulates the output collection of the prior stage in some way.
• Note: aggregation queries do not modify the input collection! _(For more information, see Update queries.)_


**Aggregation Pipeline Operators include:**

• \$match
• \$project
• \$sort / $limit
• \$group
• \$unwind
• \$lookup


These operators are similar to selection/projection in .find() retrieval queries but are more expressive. Some operators, like $unwind and $lookup, are new and provide additional functionalities.

Example:
Using the zipcodes, find states with population >15M and list the state, population in descending order.


SQL: 
```sql
SELECT state AS id,
   SUM(pop) AS totalPop 
FROM zips 
GROUP BY state 
HAVING totalPop >= 15000000
ORDER BY totalPop DESC;
```

MongoDB:
```python
db.zips.aggregate( [    

{ $group: { _id: "$state", totalPop: {$sum: "$pop" } } },        

{ $match: { totalPop: { $gte: 15000000 } } }, 

{ $sort : { totalPop : -1 } }

] )
```

Recall that a valid collection needs to have an _id.

$group syntax therefore specifies:
- The _id, which are the attributes to group by._
- .aggregate() takes an array of pipeline stages.
- Each stage in the pipeline “outputs” a valid collection to “input” into the next stage.

Note the the two uses of $!

- Mongo Query Language (MQL) keywords,  
    e.g., stage names, agg func names; and
    
- Attribute names on the value side  
    of field-value pairs. Note the quotes!

Additional fields as aggregation functions.

$group stage Accumulator Operators:

- $sum, $avg, $max are standard, plus:
- $first: first expression value per group
- e.g., if performed after sort, then docs are in a specific order.
    
- $push: array of expression values per group
- Not possible in relational context, where values are atomic!
- $addToSet: like $push, but eliminates duplicates

#### Other Aggregation functions

##### $unwind “unrolls” arrays, similar to pd.melt().

Unwind expands an array by constructing documents one per element of the array.

```python
db.inventory.aggregate( [ 
  { $unwind : "$tags" }, 
  { $project : {_id : 0, instock: 0}}  
] )

```

This is impossible to do in a traditional relational model, as relational values are atomic (i.e., no arrays).

(note: some RDBMSes nowadays do indeed support arrays, e.g., Postgres [link](https://www.postgresql.org/docs/current/arrays.html)).

Suppose we want to find the total quantity per item across location.

```python
db.inventory.aggregate(

   [{ $unwind: "$instock" },

    { $group: {

        _id: "$item",

        totalqty: { $sum: "$instock.qty" }

       }
     }
   ] )
```

![[Pasted image 20241031102116.png]]

![[Pasted image 20241031102135.png]]

The value for a $group stage is a collection of agg. attributes to return per document in the output collection.

##### $lookup performs a (somewhat gross) left outer equi-join.

```python
{ $lookup: { 

    from: <collection to join>, 

    localField: <referencing field>, 

    foreignField: <referenced field>, 

    as:  <output array field> 

} }
```

```python
db.inventory.aggregate( [ 

{ $lookup : {from : "inventory", 

       localField : "instock.loc", 

     foreignField : "instock.loc", 

               as :"otheritems"}},  

{ $project : {_id : 0,

             tags : 0,

              dim : 0,  
  "otheritems._id": 0} } 

] )
```

Conceptually, $lookup performs the following  
for each document:

- Find documents from the other collection
- local field must match foreign field exactly
- place each of the matches in an array

