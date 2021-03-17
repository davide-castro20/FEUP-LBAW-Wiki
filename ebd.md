# EBD: Database Specification Component

Our website aims to help customers get what then need when they need it during these troubling times with an enjoyable browsing experience.

## A4: Conceptual Data Model

The Fneuc shop website provides a reliable shopping service for the general public with easy access.
This artefact contains the conceptual data model for the platform, including business rules.

### 1. Class diagram

![Class Diagram](./images/A4/UML.png)  
Figure 1: Class Diagram.

### 2. Additional Business Rules


Additional business rules are represented as UML notes in the class diagram.

---


## A5: Relational Schema, validation and schema refinement

> Brief presentation of the product.  
> Brief presentation of the artefact goals.

### 1. Relational Schema

| Relation referenct | Relation Compact Notation                                    |
| ------------------ | ------------------------------------------------------------ |
| R01                | user(<ins>userID</ins>, name <b>NN</b>, username <b>UK NN </b>, email <b>UK NN </b>, password <b>NN</b>, billingAddr&#8594;address, shippingAddr&#8594;address) |
| R02                | admin(<u>userID</u>&#8594;user )                             |
| R03                | authenticated(<u>userID</u>&#8594;user, balance **DF** 0)    |
| R04                | review(<u>id</u>, userID&#8594;authenticated, comment, date **DF** Today, rating **NN CK** rating > 0 AND rating < = 5) |
| R05                | category(<u>categoryID</u>, category)                        |
| R06                | detail(<u>id</u>, detailName **NN UK**)                      |
| R07                | item(<u>itemID</u>, name **NN**, stock **NN CK** stock >= 0, brief_description, description **NN**, price **NN CK** price> 0, isNumber **DF** False, category&#8594;category) |
| R08                | ban(<u>adminID</u>&#8594;admin,<u>userID&#8594;</u>authenticacted, date **DF** Today, reason **NN**) |
| R09                | country(<u>id</u>, countryName **NN**)                       |
| R10                | address(<u>id</u>, city **NN**, street **NN**, zipCode **NN**, country&#8594;country) |
| R11                | purchase(<u>id</u>, date **DF** Today)                       |
| R12                | purchaseInfo(purchaseID&#8594;purchase, <u>itemID</u>&#8594;item, purchasePrice **NN**, quantity **NN**) |
| R13                | photo(<u>photoID</u>, path **NN**)                           |
| R14                | advertisement(<u>id</u>, title **NN UK**, beginDate **DF** Today, endDate **CK** endDate > beginDate) |
| R15                | itemPhoto(<u>photoID</u>&#8594;photo, itemID&#8594;item)     |
| R16                | addvertisementPhoto(<u>photoID</u>&#8594;photo, advertisementID&#8594;advertisement) |
| R17                | cart(<u>userID</u>&#8594;user, <u>itemID</u>&#8594;item, addDate **DF** Today, quantity **CK** quantity > 0) |
| R18                | wishlist(<u>userID</u>&#8594;user, <u>itemID</u>&#8594;item, addDate **DF** Today) |
| R19                | notification(<u>userID</u>&#8594;user,itemID&#8594;item, date **DF** Today, isSeen **DF** False, type **NN**) |
| R20                | discount(<u>id</u>, percentage **CK** percentage > 0 && percentage < 100, beginDate **DF** Today, endDate **CK** endDate > beginDate) |
| R21                | applyDiscount(i<u>temID</u>&#8594;item, <u>discountID</u>&#8594;discount) |
| R22                | itemDetail(<u>itemID</u>&#8594;item, <u>detailID</u>&#8594;detail, detailInfo **NN**) |
| R23                | categoryDetail(<u>categoryID</u>&#8594;category, <u>detailID</u>&#8594;detail) |
| R24                | discountNotification(<u>notificationID</u>&#8594;notification, discountID&#8594;discount) |
| R25                | stockNotification(<u>notificationID</u>&#8594;notification)  |

### 2. Domains

| Domain Name | Domain Specification                               |
| ----------- | -------------------------------------------------- |
| Today       | DATE DEFAULT CURRENT_DATE                          |
| Status      | ENUM ('Processing', 'Delivered', 'Shipped','Lost') |

### 3. Functional Dependencies and schema validation

> To validate the Relational Schema obtained from the Conceptual Model, all functional dependencies are identified and the normalization of all relation schemas is accomplished. Should it be necessary, in case the scheme is not in the Boyce–Codd Normal Form (BCNF), the relational schema is refined using normalization.  

| **TABLE R01**   | User               |
| --------------  | ---                |
| **Keys**        | { id }, { email }  |
| **Functional Dependencies:** |       |
| FD0101          | id → {email, name} |
| FD0102          | email → {id, name} |
| ...             | ...                |
| **NORMAL FORM** | BCNF               |

> If necessary, description of the changes necessary to convert the schema to BCNF.  
> Justification of the BCNF.  

### 4. SQL Code

> SQL code necessary to build (and rebuild) the database.  
> This code should also be included in the group's git repository as an SQL script, and a link include here.  


---


## A6: Indexes, triggers, user functions, transactions and population

> Brief presentation of the product.  
> Brief presentation of the artefact goals.

### 1. Database Workload

> A study of the predicted system load (database load), organized in subsections.  

#### 1.1. Tuple Estimation

> Estimate of tuples at each relation.  

| **Relation reference** | **Relation Name** | **Order of magnitude**        | **Estimated growth** |
| ------------------ | ------------- | ------------------------- | -------- |
| R01                | Table1        | units|dozens|hundreds|etc | order per time |
| R02                | Table2        | units|dozens|hundreds|etc | dozens per month |
| R03                | Table3        | units|dozens|hundreds|etc | hundreds per day |
| R04                | Table4        | units|dozens|hundreds|etc | no growth |

#### 1.2. Frequent Queries

> Most important queries (SELECT) and their frequency.  

| **Query**       | SELECT01                               |
| ---             | ---                                    |
| **Description** | One sentence describing the query goal |
| **Frequency**   | magnitude per time                     |
| `SQL code`                                              ||

#### 1.3. Frequent Updates

> Most important updates (INSERT, UPDATE, DELETE) and their frequency.  

| **Query**       | UPDATE01                               |
| ---             | ---                                    |
| **Description** | One sentence describing the query goal |
| **Frequency**   | magnitude per time                     |
| `SQL code`                                              ||

### 2. Proposed Indices

#### 2.1. Performance Indices

> Indices proposed to improve performance of the identified queries.  

| **Index**           | IDX01                                  |
| ---                 | ---                                    |
| **Related queries** | SELECT01, ...                          |
| **Relation**        | Relation where the index is applied    |
| **Attribute**       | Attribute where the index is applied   |
| **Type**            | B-tree, Hash, GiST or GIN              |
| **Cardinality**     | Attribute cardinality: low/medium/high |
| **Clustering**      | Clustering of the index                |
| **Justification**   | Justification for the proposed index   |
| `SQL code`                                                  ||

#### 2.2. Full-text Search Indices 

> The system being developed must provide full-text search features supported by PostgreSQL. Thus, it is necessary to specify the fields where full-text search will be available and the associated setup, namely all necessary configurations, indexes definitions and other relevant details.  

| **Index**           | IDX01                                  |
| ---                 | ---                                    |
| **Related queries** | SELECT01, ...                          |
| **Relation**        | Relation where the index is applied    |
| **Attribute**       | Attribute where the index is applied   |
| **Type**            | B-tree, Hash, GiST or GIN              |
| **Clustering**      | Clustering of the index                |
| **Justification**   | Justification for the proposed index   |
| `SQL code`                                                  ||

### 3. Triggers

> User-defined functions and trigger procedures that add control structures to the SQL language or perform complex computations, are identified and described to be trusted by the database server. Every kind of function (SQL functions, Stored procedures, Trigger procedures) can take base types, composite types, or combinations of these as arguments (parameters). In addition, every kind of function can return a base type or a composite type. Functions can also be defined to return sets of base or composite values.  

| **Trigger**      | TRIGGER01                              |
| ---              | ---                                    |
| **Description**  | Trigger description, including reference to the business rules involved |
| `SQL code`                                             ||

### 4. Transactions

> Transactions needed to assure the integrity of the data.  

| SQL Reference   | Transaction Name                    |
| --------------- | ----------------------------------- |
| Justification   | Justification for the transaction.  |
| Isolation level | Isolation level of the transaction. |
| `Complete SQL Code`                                   ||

### 5. Complete SQL Code

> The database script must also include the SQL to populate a database with test data with an amount of tuples suitable for testing and with plausible values for the fields of the database.  
> This code should also be included in the group's git repository as an SQL script, and a link include here.  

#### 5.1. Database schema

#### 5.2. Database population


---


## Revision history

Changes made to the first submission:
1. Item 1
1. ..

***
GROUP21gg, DD/MM/2021

* Group member 1 name, email (Editor)
* Group member 2 name, email
* ...