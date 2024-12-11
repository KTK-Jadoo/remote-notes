---
course: "[[DATA 101]]"
tags:
  - "#databases"
  - data
---

***E***xtract: Scrape raw data from all the source systems, e.g., transactions, sensors, log files, experiments, tables, bytestreams etc.

***T***ransform: Apply a series of rules or functions, wrangle data into schema(s)/format(s)

***L***oad: Load data into a data storage solution

### ETL (Traditional Warehouses)

_Extract_ or scraping from API or log file, 
_transform_ into common schema/format, 
_load_ in parallel to “data warehouse”

### ELT (e.g. Snowflake)

_Extract_ or scraping from API or log file, 
_Load_ without doing a lot of transformation, 
with *transform*ations done in SQL 

 Faster to get going, and more scalable, but requires more data warehousing knowledge (& may be more expensive).

### ET (Data Lakes)

No need to “manage” data. _Extract_ directly into a Data Lake, later _transform_ for specific use cases.

Data is dumped in cheaply and massaged as needed for various use-cases
Usually code-centric (Spark)

#### Data Warehouses ~ 1990s
- “Single source of truth”: A central, organized repository of data used for analytics throughout an enterprise.
- Design the uber-schema up-front of all of the rectangular tables you’d ever want.
- _Extract_ from trusted sources
- _Transform_ to warehouse schema using custom tools
- _Load_ data warehouse
- Old school ETL solution: Informatica
- Warehouses expect structure
- Transformation is costly, not necessarily just computing but engineering time

#### Data Lake ~ 2010s
- Emerged during Hadoop/Spark revolution
- “Landing zone”: unconstrained storage for any and all data
- Data is then analyzed on demand
- _Extract_ into files/storage
- _Load_ into storage (easy!)
- _Transform_ on demand for any use.
- Create new files in the lake, catalog files as they go for reuse
- Often code-centric

>[!NOTE] ETLT & the Lakehouse
>Modern solutions are likely Many-to-Many. Sometimes start with a data lake. Empower data scientists to work on ad-hoc use cases .Allow for datasets that “graduate” to a carefully managed warehouse. Some datasets may directly be loaded into a data warehouse.
>
>Databricks uses a _Lakehouse_ which make managing such a system much easier.

### Important Considerations
##### Data Discovery, Data Assessment
- Ad-Hoc: End-users land data, explore it, label it
- Systematic: Crawl/index the data lake for files
- E.g., for CSV/JSON 
- Very content-centric: really a form of analytics/prediction
- Try to figure out what type of data you have.
- AI + People!

##### Data Quality & Integrity
- Boolean Integrity checks
- Often specified by people, also “mined” by AI
- Data changes ALL the time, especially from clients.
- Enforced: can “reject” or “sequester” data that violate.
- e.g no two products that have the same product ID!

##### Application Metadata:
- Data entities (e.g. students, courses, employees for a university)
- Relationships between data
- Constraints

##### Behavioral Metadata:
- Data Lineage – where did it come from?
- Audit Trails of Usage – who ran this job, and what did it do?

##### Change Metadata
- Version info for all the above
- Timestamps

##### Operationalization (Ops): 
- When do jobs kick off, and what do they do?
- How are tests registered, exceptions handled, people alerted?
- How do experiments “graduate” into processes?

##### Feedback:
- Some are datasets in their own right. If you produce a table, that’s also data!
- Many are new processes that generating new data feeds!
- ML models: Constantly yielding predictions.
- Compare old predictions to new predictions?

