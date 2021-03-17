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
| R01                | country(<ins>countryID</ins>, name **NN**)                   |
| R02                | address(<ins>addressID</ins>, city **NN**, street **NN**, zip_code **NN**, country&#8594;country) |
| R03                | photo(<ins>photoID</ins>, path **NN**)                       |
| R04                | user(<ins>userID</ins>, first_name <b>NN</b>, last_name <b>NN</b>, username <b>UK NN </b>, email <b>UK NN </b>, password <b>NN</b>, billingAddr&#8594;address, shippingAddr&#8594;address,photoID&#8594;photo) |
| R05                | admin(<ins>userID</ins>&#8594;user)                          |
| R06                | authenticated(<ins>userID</ins>&#8594;user, balance **DF** 0) |
| R07                | review(<ins>reviewID</ins>, userID&#8594;authenticated, comment, date **DF** Today, rating **NN CK** rating > 0 AND rating < = 5) |
| R08                | category(<ins>categoryID</ins>, name **UK**)                 |
| R09                | detail(<ins>detailID</ins>, name **NN UK**)                  |
| R10                | item(<ins>itemID</ins>, name **NN**, stock **NN CK** stock >= 0, brief_description, description **NN**, price **NN CK** price> 0, isArchived **DF** False, category&#8594;category) |
| R11                | ban(<ins>adminID</ins>&#8594;admin, <ins>userID&#8594;</ins>authenticated, date **DF** Today, reason **NN**) |
| R12                | purchase(<ins>purchaseID</ins>, userID&#8594;authenticated, date **DF** Today) |
| R13                | purchaseItem(<ins>purchaseID</ins>&#8594;purchase, <ins>itemID</ins>&#8594;item, purchasePrice **NN**, quantity **NN**) |
| R14                | advertisement(<ins>advertisementID</ins>, title **NN UK**, beginDate **DF** Today, endDate **CK** endDate > beginDate, photoID&#8594;photo) |
| R15                | itemPhoto(<ins>photoID</ins>&#8594;photo, itemID&#8594;item) |
| R16                | cart(<ins>userID</ins>&#8594;user, <ins>itemID</ins>&#8594;item, addDate **DF** Today, quantity **CK** quantity > 0) |
| R17                | wishlist(<ins>userID</ins>&#8594;user, <ins>itemID</ins>&#8594;item, addDate **DF** Today) |
| R18                | discount(<ins>discountID</ins>, percentage **CK** percentage > 0 && percentage < 100, beginDate **DF** Today, endDate **CK** endDate > beginDate) |
| R19                | notification(<ins>notificationID</ins>, userID&#8594;user, itemID&#8594;item, date **DF** Today, isSeen **DF** False) |
| R20                | discountNotification(<ins>notificationID</ins>&#8594;notification, discountID&#8594;discount) |
| R21                | stockNotification(<ins>notificationID</ins>&#8594;notification) |
| R22                | applyDiscount(i<ins>temID</ins>&#8594;item, <ins>discountID</ins>&#8594;discount) |
| R23                | itemDetail(<ins>itemID</ins>&#8594;item, <ins>detailID</ins>&#8594;detail, detailInfo **NN**) |
| R24                | categoryDetail(<ins>categoryID</ins>&#8594;category, <ins>detailID</ins>&#8594;detail) |

### 2. Domains

| Domain Name | Domain Specification                               |
| ----------- | -------------------------------------------------- |
| Today       | DATE DEFAULT CURRENT_DATE                          |
| Status      | ENUM ('Processing', 'Delivered', 'Shipped','Lost') |

### 3. Functional Dependencies and schema validation

> To validate the Relational Schema obtained from the Conceptual Model, all functional dependencies are identified and the normalization of all relation schemas is accomplished. Should it be necessary, in case the scheme is not in the Boyce–Codd Normal Form (BCNF), the relational schema is refined using normalization.  

| **TABLE R01** | user              |
| --------------  | ---                |
| **Keys**        | { userID }, { email }, { username } |
| **Functional Dependencies:** |       |
| FD0101          | { userID } → { email, name, username, password, billingAddr, shippingAddr,photoID } |
| FD0102          | { email } → { userID }                                       |
| FD0103                       | { username } → { userID } |
| **NORMAL FORM** | BCNF               |

| **TABLE R02**                | admin      |
| ---------------------------- | ---------- |
| **Keys**                     | { userID } |
| **Functional Dependencies:** | None       |
| **NORMAL FORM**              | BCNF       |

| TABLE R03                    | authenticated            |
| ---------------------------- | ------------------------ |
| **Keys**                     | { userID }               |
| **Functional Dependencies:** |                          |
| FD0301                       | { userID } → { balance } |
| **NORMAL FORM**              | BCNF                     |

| **TABLE R0**4                | review                                           |
| :--------------------------- | :----------------------------------------------- |
| **Keys**                     | { reviewID }, { userID }                         |
| **Functional Dependencies:** |                                                  |
| FD0401                       | { reviewID } → { userID, comment, date, rating } |
| **NORMAL FORM**              | BCNF                                             |

| **TABLE R05**                | category                 |
| ---------------------------- | ------------------------ |
| **Keys**                     | { categoryID }           |
| **Functional Dependencies:** |                          |
| FD0501                       | { categoryID} → { name } |
| **NORMAL FORM**              | BCNF                     |

| TABLE R06                    | detail                  |
| ---------------------------- | ----------------------- |
| **Keys**                     | { detailID }            |
| **Functional Dependencies:** |                         |
| FD0601                       | { detailID } → { name } |
| **NORMAL FORM**              | BCNF                    |

| **TABLE R07**                | item                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| **Keys**                     | { itemID }                                                   |
| **Functional Dependencies:** |                                                              |
| FD0701                       | { itemID } → { name, stock, description, price, brief_description, price, isArchived, category} |
| **NORMAL FORM**              | BCNF                                                         |

| **TABLE R08**                | ban                                    |
| ---------------------------- | -------------------------------------- |
| **Keys**                     | { adminID, userID }                    |
| **Functional Dependencies:** |                                        |
| FD0801                       | { adminID, userID } → { date, reason } |
| **NORMAL FORM**              | BCNF                                   |

| **TABLE R09**                | country                  |
| ---------------------------- | ------------------------ |
| **Keys**                     | { countryID }            |
| **Functional Dependencies:** |                          |
| FD0901                       | { countryID } → { name } |
| **NORMAL FORM**              | BCNF                     |

| **TABLE R10**                | address                                             |
| ---------------------------- | --------------------------------------------------- |
| **Keys**                     | { addressID }                                       |
| **Functional Dependencies:** |                                                     |
| FD1001                       | { addressID } → { city, street, zip_code, country } |
| **NORMAL FORM**              | BCNF                                                |

| **TABLE R11**                | purchase                  |
| ---------------------------- | ------------------------- |
| **Keys**                     | { purchaseID }            |
| **Functional Dependencies:** |                           |
| FD1101                       | { purchaseID } → { date } |
| **NORMAL FORM**              | BCNF                      |

| **TABLE R12**                | purchaseItem                                         |
| ---------------------------- | ---------------------------------------------------- |
| **Keys**                     | { purchaseID, itemID }                               |
| **Functional Dependencies:** |                                                      |
| FD1201                       | { purchaseID, itemID } → { purchasePrice, quantity } |
| **NORMAL FORM**              | BCNF                                                 |

| **TABLE R13**                | photo                  |
| ---------------------------- | ---------------------- |
| **Keys**                     | { photoID }            |
| **Functional Dependencies:** |                        |
| FD1301                       | { photoID } → { path } |
| **NORMAL FORM**              | BCNF                   |

|  TABLE R014                  | advertisement                           |
| ---------------------------- | --------------------------------------- |
| **Keys**                     | { advertisementID }, { title }          |
| **Functional Dependencies:** |                                         |
| FD1401                       | { id } → { title, beginDate,  endDate } |
| FD1402                       | { title } -> { id }                     |
| **NORMAL FORM**              | BCNF                                    |

| TABLE R015                   | itemPhoto                |
| ---------------------------- | ------------------------ |
| **Keys**                     | { photoID }              |
| **Functional Dependencies:** |                          |
| FD1501                       | { photoID } → { itemID } |
| **NORMAL FORM**              | BCNF                     |

| TABLE R016                   | cart                                           |
| ---------------------------- | ---------------------------------------------- |
| **Keys**                     | { userID, itemID }                             |
| **Functional Dependencies:** |                                                |
| FD1601                       | { userID, itemID } → { addDate, isSeen, type } |
| **NORMAL FORM**              | BCNF                                           |

| TABLE R017                   | wishlist                         |
| ---------------------------- | -------------------------------- |
| **Keys**                     | { userID, itemID }               |
| **Functional Dependencies:** |                                  |
| FD1701                       | { userID, itemID } → { addDate } |
| **NORMAL FORM**              | BCNF                             |

| TABLE R018                   | notification                                   |
| ---------------------------- | ---------------------------------------------- |
| **Keys**                     | { userID, itemID }                             |
| **Functional Dependencies:** |                                                |
| FD1801                       | { userID, itemID } → { addDate, isSeen, type } |
| **NORMAL FORM**              | BCNF                                           |

| TABLE R019                   | discountNotification          |
| ---------------------------- | ----------------------------- |
| **Keys**                     | { notificationID, discountID} |
| **Functional Dependencies:** |                               |
| (none)                       |                               |
| **NORMAL FORM**              | BCNF                          |

| TABLE R020                   | stockNotification  |
| ---------------------------- | ------------------ |
| **Keys**                     | { notificationID } |
| **Functional Dependencies:** |                    |
| (none)                       |                    |
| **NORMAL FORM**              | BCNF               |

| TABLE R021                   | discount                                    |
| ---------------------------- | ------------------------------------------- |
| **Keys**                     | { id }                                      |
| **Functional Dependencies:** |                                             |
| FD1901                       | { id } → { percentage, beginDate, endDate } |
| **NORMAL FORM**              | BCNF                                        |

| TABLE R022                   | applyDiscount          |
| ---------------------------- | ---------------------- |
| **Keys**                     | { itemID, discountID } |
| **Functional Dependencies:** |                        |
| (none)                       |                        |
| **NORMAL FORM**              | BCNF                   |

| TABLE R023                   | itemDetail                             |
| ---------------------------- | -------------------------------------- |
| **Keys**                     | { itemID, detailID }                   |
| **Functional Dependencies:** |                                        |
| FD2101                       | { itemID, detailID } -> { detailInfo } |
| **NORMAL FORM**              | BCNF                                   |

| TABLE R024                   | categoryDetail                         |
| ---------------------------- | -------------------------------------- |
| **Keys**                     | { categoryID, detailID }               |
| **Functional Dependencies:** |                                        |
| FD2101                       | { itemID, detailID } -> { detailInfo } |
| **NORMAL FORM**              | BCNF                                   |





> If necessary, description of the changes necessary to convert the schema to BCNF.  
> Justification of the BCNF.  

### 4. SQL Code

> SQL code necessary to build (and rebuild) the database.  
> This code should also be included in the group's git repository as an SQL script, and a link include here.  

```sql
CREATE TABLE country (
    countryID SERIAL PRIMARY KEY,
    name text NOT NULL CONSTRAINT country_name_uk UNIQUE
);  

CREATE TABLE "address" (
    addressID SERIAL PRIMARY KEY,
    city text NOT NULL,
    street text NOT NULL,
    zip_code text NOT NULL,
    countryID INTEGER REFERENCES "country" (countryID) ON UPDATE CASCADE
);

CREATE TABLE photo (
    photoID SERIAL PRIMARY KEY,
    path text NOT NULL DEFAULT "./images/noImage.png"
);

CREATE TABLE user (
    userID SERIAL PRIMARY KEY,
    username text NOT NULL CONSTRAINT username_uk UNIQUE,
    email text NOT NULL CONSTRAINT user_email_uk UNIQUE,
    first_name text NOT NULL,
    last_name text NOT NULL,
    password text NOT NULL,
    img INTEGER REFERENCES "photo" (photoID) ON UPDATE CASCADE,
    billingAddress INTEGER REFERENCES "address" (addressID) ON UPDATE CASCADE,
    shippingAddress INTEGER REFERENCES "address" (addressID) ON UPDATE CASCADE
);

CREATE TABLE admin (
    adminID INTEGER REFERENCES "user" (userID) ON UPDATE CASCADE PRIMARY KEY
);

CREATE TABLE authenticated (
    authenticatedID INTEGER REFERENCES "user" (userID) ON UPDATE CASCADE PRIMARY KEY,
    balance money DEFAULT 0 NOT NULL,
);
 

CREATE TABLE review (
    reviewID SERIAL PRIMARY KEY,
    userID INTEGER REFERENCES "authenticated" (authenticatedID) ON UPDATE CASCADE,
    comment text
    "date" TIMESTAMP WITH TIME zone DEFAULT now() NOT NULL,
    rating INTEGER NOT NULL CONSTRAINT rating_ck CHECK (((rating > 0) AND (rating <= 5)))
);

CREATE TABLE category (
    categoryID SERIAL PRIMARY KEY,
    name text NOT NULL CONSTRAINT name_uk UNIQUE
);
 
CREATE TABLE detail (
    detailID SERIAL PRIMARY KEY,
    name text NOT NULL CONSTRAINT name_uk UNIQUE
);
 
CREATE TABLE item (
    itemID SERIAL PRIMARY KEY,
    name text NOT NULL,
    stock INTEGER NOT NULL CONSTRAINT pos_stock CHECK stock >= 0,
    brief_description text,
    description text NOT NULL,
    price MONEY NOT NULL CONSTRAINT pos_price CHECK price >= 0,
    isArchived BOOLEAN NOT NULL DEFAULT false,
    categoryID INTEGER REFERENCES "category" (categoryID) ON UPDATE CASCADE,
    CONSTRAINT year_positive_ck CHECK (("year" > 0))
);
 
CREATE TABLE ban (
    adminID INTEGER NOT NULL REFERENCES admin (adminID) ON UPDATE CASCADE,
    userID INTEGER NOT NULL REFERENCES user (userID) ON UPDATE CASCADE,
    "date" TIMESTAMP WITH TIME zone DEFAULT now() NOT NULL,
    reason text NOT NULL,
    PRIMARY KEY (adminID, userID)
);

CREATE TABLE purchase (
    purchaseID SERIAL PRIMARY KEY,
    userID INTEGER REFERENCES "authenticated" (authenticatedID) ON UPDATE CASCADE,
    "date" TIMESTAMP WITH TIME zone DEFAULT now() NOT NULL
);
 
CREATE TABLE purchaseItem (
    purchaseID INTEGER NOT NULL REFERENCES "purchase" (purchaseID) ON UPDATE CASCADE,
    itemID INTEGER NOT NULL REFERENCES "item" (itemID) ON UPDATE CASCADE,
    price MONEY NOT NULL,
    quantity INTEGER NOT NULL CONSTRAINT quantity_more_zero CHECK quantity > 0,
    PRIMARY KEY (purchaseID, itemID)
);

CREATE TABLE advertisement (
    advertisementID INTEGER PRIMARY KEY,
    title text NOT NULL,
    beginDate TIMESTAMP WITH TIME zone DEFAULT now() NOT NULL,
    endDate TIMESTAMP WITH TIME zone NOT NULL,
    photoID INTEGER REFERENCES "photo" (photoID) ON UPDATE CASCADE,
    CONSTRAINT ad_dates_ck CHECK (beginDate < endDate)
);

CREATE TABLE itemPhoto (
    photoID INTEGER NOT NULL REFERENCES "photo" (photoID) ON UPDATE CASCADE PRIMARY KEY,
    itemID INTEGER NOT NULL REFERENCES "item" (itemID) ON UPDATE CASCADE

);
 
CREATE TABLE cart (
    userID INTEGER REFERENCES "authenticated" (authenticatedID) ON UPDATE CASCADE,
    itemID INTEGER NOT NULL REFERENCES "item" (itemID) ON UPDATE CASCADE,
    addDate TIMESTAMP WITH TIME zone DEFAULT now() NOT NULL,
    quantity INTEGER NOT NULL CONSTRAINT quantity_more_zero CHECK quantity > 0
    PRIMARY KEY (userID, itemID)
);
 
CREATE TABLE wishlist (
    userID INTEGER REFERENCES "authenticated" (authenticatedID) ON UPDATE CASCADE,
    itemID INTEGER NOT NULL REFERENCES "item" (itemID) ON UPDATE CASCADE,
    addDate TIMESTAMP WITH TIME zone DEFAULT now() NOT NULL,
    PRIMARY KEY (userID, itemID)
);
 
CREATE TABLE discount (
    discountID SERIAL PRIMARY KEY,
    "percentage" INTEGER NOT NULL CONSTRAINT valid_percentage CHECK ((("percentage" > 0) AND ("percentage" <= 100))),
    beginDate TIMESTAMP WITH TIME zone DEFAULT now() NOT NULL
    endDate TIMESTAMP WITH TIME zone NOT NULL
    CONSTRAINT ad_dates_ck CHECK (beginDate < endDate)
);

CREATE TABLE "notification" (
    notificationID SERIAL PRIMARY KEY,
    
);

CREATE TABLE discountNotification (
    notificationID INTEGER NOT NULL REFERENCES discount (discountID) ON UPDATE CASCADE PRIMARY KEY,
    discountID INTEGER NOT NULL REFERENCES discount (discountID) ON UPDATE CASCADE
);

CREATE TABLE stockNotification (
    notificationID SERIAL PRIMARY KEY
);

CREATE TABLE applyDiscount (
    itemID INTEGER NOT NULL REFERENCES "item" (itemID) ON UPDATE CASCADE,
    discountID INTEGER NOT NULL REFERENCES discount (discountID) ON UPDATE CASCADE,
    PRIMARY KEY (itemID, discountID)
);

CREATE TABLE itemDetail (
    itemID INTEGER NOT NULL REFERENCES "item" (itemID) ON UPDATE CASCADE,
    detailID INTEGER NOT NULL REFERENCES "detail" (detailID) ON UPDATE CASCADE,
    detailInfo text NOT NULL,
    PRIMARY KEY (detailID, itemID)
);

CREATE TABLE categoryDetail (
    categoryID INTEGER NOT NULL REFERENCES "category" (categoryID) ON UPDATE CASCADE,
    detailID INTEGER NOT NULL REFERENCES "detail" (detailID) ON UPDATE CASCADE,
    PRIMARY KEY (categoryID, detailID)
);
```




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