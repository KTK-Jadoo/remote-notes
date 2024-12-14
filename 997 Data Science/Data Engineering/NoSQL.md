---
tags:
  - databases
  - sql
date: 2024-10-29
source: "[[DATA 101]]"
---
NoSQL was a *hip* name for [[Semistructured Data|document stores]].

- Literally, “No SQL used” in database design.
- Ability to store semi-structured AND unstructured data.
- Reduced functionality with simpler data model

 Restricted queries/updates, but optimized for querying and scaling.

- Without the rectangular / structured data constraints, NoSQL databases can (more) easily be distributed across different data stores
- Horizontally scalable! (e.g. can easily scale to millions of users)
	- Meaning we can have many servers in parallel

- With NoSQL, we don’t perform joins or ensure consistency
	- Upcoming: Don’t provide / use transactions
	- Fewer guarantees made across multiple updates to data
- Only have to guarantee __eventual consistency__
	- Data will be “eventually” consistent, i.e. not immediately
	- Used to guarantee that the system would be __highly available__

With NoSQL, we don’t perform joins or ensure strong consistency.

- __Consistency:__ Guarantee that any transactions started in the future necessarily see the effects of other transactions committed in the past.
- In other words, the database always reflects the most current changes.

Instead, with NoSQL we only have to guarantee eventual consistency.

- In other words, transactions will eventually be consistent across the database.
- Used to guarantee that the system would be highly available.
- Two approaches to scaling, both of which are used (sometimes in combination) __partitioning__ and __replication__.

--- 

Relational models are difficult to replicate/partition.

- Partition: we may be forced to join across servers, sometimes there is no easy way to partition a single table
    
- Replication: local copy has inconsistent versions
  

Relational databases are _required_ to maintain consistency!

- Consistency is hard in both cases!
    
- Scalability in relational databases is a very challenging problem which makes for a complex database architecture

---

