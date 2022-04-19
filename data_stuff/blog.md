# Data stuff.

Hopefully you have been able to store and access your data without significant problems. If not, perhaps you have tried to investigate further and recognized you are lost in a world of weird acronyms.

Here I aim to demystify few basic concepts commonly used when discussing data storage. 

## But hey, I don't really care about this stuff

Ok, move on. But before you do, recognize that even if you are not an database engineer this information might be of use. 

If you are an application developer, it is necessary to have basic understanding about underlying structure to build performant applications. And in case you have a role of solution architect, it is vital to understand key concepts behind available architecture building blocks when designing the solution.

## Definitions

### Data Architecture

Structure and relations of different type of data and data resources within enterprise. 

### Database

Place you store data.

### Data Warehouse

Relational database optimised for storing / analyzing data

### Data Lake

Flat-file database optimised for storage

### Data lakehouse

Abstraction built on top of data lake to enable similar functionalities as in relational database

## Database types

### Relational databases

Data is stored in tables and the records in different tables can relate to each other.

Example use case: Incidents, problems, CIs, and their relations.

SQL is the query language used with relational databases.

These are the most common databases. Simple to use, performance might be a problem on some scenarios.

### NOSQL databases

"Not just SQL" databases. Which means all the other database types.

### Document databases

Data is stored in separate, tree-like, documents. There is little or no relations between documents.

Example use case: CVs.

### Graph databases

Used to store graph like data, where various entities relate to each other in various ways.

Example use case: Social networks.

### Network database

Like graph, but a schema is enforced which limits what type of relations entities might have. A schema might require that "user" can not directly be related to "food", but that it should be represented "user"-->"allergy"-->"food".


