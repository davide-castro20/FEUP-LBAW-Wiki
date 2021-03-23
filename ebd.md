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

In this artifact our website's database relational schema is presented as well as it's valitation and refinements.

### 1. Relational Schema

| Relation referenct | Relation Compact Notation                                    |
| ------------------ | ------------------------------------------------------------ |
| R01                | country(<ins>country_id</ins>, name **NN**)                  |
| R02                | address(<ins>address_id</ins>, city **NN**, street **NN**, zip_code **NN**, country&#8594;country) |
| R03                | photo(<ins>photoID</ins>, path **NN**)                       |
| R04                | users(<ins>user_id</ins>, first_name , last_name, username <b>UK </b>, email <b>UK</b>, password, billing_addr&#8594;address, shipping_addr&#8594;address,photo_id&#8594;photo, deleted **DF** False) |
| R05                | admin(<ins>user_id</ins>&#8594;user)                         |
| R06                | authenticated(<ins>user_id</ins>&#8594;user, balance **DF** 0) |
| R07                | review(<ins>review_id</ins>, user_id&#8594;authenticated, comment, date **DF** Today, rating **NN CK** rating > 0 AND rating < = 5) |
| R08                | category(<ins>category_id</ins>, name **UK**)                |
| R09                | detail(<ins>detail_id</ins>, name **NN UK**)                 |
| R10                | item(<ins>item_id</ins>, name **NN**, stock **NN CK** stock >= 0, brief_description, description **NN**, price **NN CK** price> 0, isArchived **DF** False, category&#8594;category) |
| R11                | ban(<ins>admin_id</ins>&#8594;admin, <ins>user_id&#8594;</ins>authenticated, date **DF** Today, reason **NN**) |
| R12                | purchase(<ins>purchase_idD</ins>, user_id&#8594;authenticated, date **DF** Today) |
| R13                | purchase_item(<ins>purchase_id</ins>&#8594;purchase, <ins>item_id</ins>&#8594;item, purchase_price **NN**, quantity **NN**) |
| R14                | advertisement(<ins>advertisement_id</ins>, title **NN UK**, begin_date **DF** Today, end_date **CK** end_date > begin_date, photo_id&#8594;photo) |
| R15                | item_photo(<ins>photo_id</ins>&#8594;photo, item_id&#8594;item) |
| R16                | cart(<ins>user_id</ins>&#8594;user, <ins>item_id</ins>&#8594;item, add_date **DF** Today, quantity **CK** quantity > 0) |
| R17                | wishlist(<ins>user_id</ins>&#8594;user, <ins>item_id</ins>&#8594;item, add_date **DF** Today) |
| R18                | discount(<ins>discount_id</ins>, percentage **CK** percentage > 0 && percentage < 100, begin_date **DF** Today, end_date **CK** end_date > begin_date) |
| R19                | notification(<ins>notification_id</ins>, user_id&#8594;user, item_id&#8594;item, discount_id&#8594;discount,date **DF** Today, is_seen **DF** False, type) |
| R20                | apply_discount(<ins>item_id</ins>&#8594;item, <ins>discount_id</ins>&#8594;discount) |
| R21                | item_detail(<ins>item_id</ins>&#8594;item, <ins>detail_id</ins>&#8594;detail, detail_info **NN**) |
| R22                | category_detail(<ins>category_id</ins>&#8594;category, <ins>detail_id</ins>&#8594;detail) |

All users' attributes must be not null when deleted is false but all but the id are null when deleted is true. Because of this, the attributes cannot have the flag not null.

### 2. Domains

| Domain Name | Domain Specification                               |
| ----------- | -------------------------------------------------- |
| Today       | DATE DEFAULT CURRENT_DATE                          |
| Status      | ENUM ('Processing', 'Delivered', 'Shipped','Lost') |

### 3. Functional Dependencies and schema validation

In this section, the functional dependencies and the normal form each table is in is presented

| **TABLE R01** | users             |
| --------------  | ---                |
| **Keys**        | { user_id } |
| **Functional Dependencies:** |       |
| FD0101          | { user_id } → { email, name, username, password, billing_addr, shipping_addr,photo_id,deleted} |
| **NORMAL FORM** | BCNF               |

| **TABLE R02**                | admin       |
| ---------------------------- | ----------- |
| **Keys**                     | { user_id } |
| **Functional Dependencies:** | None        |
| **NORMAL FORM**              | BCNF        |

| TABLE R03                    | authenticated             |
| ---------------------------- | ------------------------- |
| **Keys**                     | { user_id }               |
| **Functional Dependencies:** |                           |
| FD0301                       | { user_id } → { balance } |
| **NORMAL FORM**              | BCNF                      |

| **TABLE R0**4                | review                                             |
| :--------------------------- | :------------------------------------------------- |
| **Keys**                     | { review_id}                                       |
| **Functional Dependencies:** |                                                    |
| FD0401                       | { review_id } → { user_id, comment, date, rating } |
| **NORMAL FORM**              | BCNF                                               |

| **TABLE R05**                | category                  |
| ---------------------------- | ------------------------- |
| **Keys**                     | { category_id }           |
| **Functional Dependencies:** |                           |
| FD0501                       | { category_id} → { name } |
| **NORMAL FORM**              | BCNF                      |

| TABLE R06                    | detail                   |
| ---------------------------- | ------------------------ |
| **Keys**                     | { detail_id }            |
| **Functional Dependencies:** |                          |
| FD0601                       | { detail_id } → { name } |
| **NORMAL FORM**              | BCNF                     |

| **TABLE R07**                | item                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| **Keys**                     | { item_id }                                                  |
| **Functional Dependencies:** |                                                              |
| FD0701                       | { item_id } → { name, stock, description, price, brief_description, price, is_archived, category} |
| **NORMAL FORM**              | BCNF                                                         |

| **TABLE R08**                | ban                                      |
| ---------------------------- | ---------------------------------------- |
| **Keys**                     | { admin_id, user_id }                    |
| **Functional Dependencies:** |                                          |
| FD0801                       | { admin_id, user_id } → { date, reason } |
| **NORMAL FORM**              | BCNF                                     |

| **TABLE R09**                | country                   |
| ---------------------------- | ------------------------- |
| **Keys**                     | { country_id }            |
| **Functional Dependencies:** |                           |
| FD0901                       | { country_id } → { name } |
| **NORMAL FORM**              | BCNF                      |

| **TABLE R10**                | address                                              |
| ---------------------------- | ---------------------------------------------------- |
| **Keys**                     | { address_id }                                       |
| **Functional Dependencies:** |                                                      |
| FD1001                       | { address_id } → { city, street, zip_code, country } |
| **NORMAL FORM**              | BCNF                                                 |

| **TABLE R11**                | purchase                   |
| ---------------------------- | -------------------------- |
| **Keys**                     | { purchase_id }            |
| **Functional Dependencies:** |                            |
| FD1101                       | { purchase_id } → { date } |
| **NORMAL FORM**              | BCNF                       |

| **TABLE R12**                | purchase_item                                           |
| ---------------------------- | ------------------------------------------------------- |
| **Keys**                     | { purchase_id, item_id }                                |
| **Functional Dependencies:** |                                                         |
| FD1201                       | { purchase_id, item_id } → { purchase_price, quantity } |
| **NORMAL FORM**              | BCNF                                                    |

| **TABLE R13**                | photo                   |
| ---------------------------- | ----------------------- |
| **Keys**                     | { photo_id }            |
| **Functional Dependencies:** |                         |
| FD1301                       | { photo_id } → { path } |
| **NORMAL FORM**              | BCNF                    |

| TABLE R014                   | advertisement                                            |
| ---------------------------- | -------------------------------------------------------- |
| **Keys**                     | { advertisement_id }, { title }                          |
| **Functional Dependencies:** |                                                          |
| FD1401                       | { advertisement_id} → { title, begin_date,  end_date }   |
| FD1402                       | { title } -> { advertisement_id, begin_date,  end_date } |
| **NORMAL FORM**              | BCNF                                                     |

| TABLE R015                   | item_photo                 |
| ---------------------------- | -------------------------- |
| **Keys**                     | { photo_id }               |
| **Functional Dependencies:** |                            |
| FD1501                       | { photo_id } → { item_id } |
| **NORMAL FORM**              | BCNF                       |

| TABLE R016                   | cart                                               |
| ---------------------------- | -------------------------------------------------- |
| **Keys**                     | { user_id, item_id }                               |
| **Functional Dependencies:** |                                                    |
| FD1601                       | { user_id, item_id } → { add_date, is_seen, type } |
| **NORMAL FORM**              | BCNF                                               |

| TABLE R017                   | wishlist                            |
| ---------------------------- | ----------------------------------- |
| **Keys**                     | { user_id, item_id }                |
| **Functional Dependencies:** |                                     |
| FD1701                       | { user_id, item_id } → { add_date } |
| **NORMAL FORM**              | BCNF                                |

| TABLE R018                   | notification                                                 |
| ---------------------------- | ------------------------------------------------------------ |
| **Keys**                     | { user_id, item_id }                                         |
| **Functional Dependencies:** |                                                              |
| FD1801                       | { user_id, item_id } → {item_id, discount_id,date, is_seen, type } |
| **NORMAL FORM**              | BCNF                                                         |

| TABLE R019                   | discount                                      |
| ---------------------------- | --------------------------------------------- |
| **Keys**                     | { id }                                        |
| **Functional Dependencies:** |                                               |
| FD1901                       | { id } → { percentage, begin_date, end_date } |
| **NORMAL FORM**              | BCNF                                          |

| TABLE R020                   | apply_discount           |
| ---------------------------- | ------------------------ |
| **Keys**                     | { item_id, discount_id } |
| **Functional Dependencies:** |                          |
| (none)                       |                          |
| **NORMAL FORM**              | BCNF                     |

| TABLE R021                   | item_detail                               |
| ---------------------------- | ----------------------------------------- |
| **Keys**                     | { item_id, detail_id }                    |
| **Functional Dependencies:** |                                           |
| FD2101                       | { item_id, detail_id } -> { detail_info } |
| **NORMAL FORM**              | BCNF                                      |

| TABLE R022                   | category_detail                           |
| ---------------------------- | ----------------------------------------- |
| **Keys**                     | { category_id, detail_id }                |
| **Functional Dependencies:** |                                           |
| FD2101                       | { item_id, detail_id } -> { detail_info } |
| **NORMAL FORM**              | BCNF                                      |



### 4. SQL Code

This SQL script is responsible for creating our website's database using postgreSQL
```sql
DROP TABLE IF EXISTS country;
CREATE TABLE country (
    country_id SERIAL PRIMARY KEY,
    name text NOT NULL CONSTRAINT country_name_uk UNIQUE
); 

DROP TABLE IF EXISTS photo;
CREATE TABLE photo (
    photo_id SERIAL PRIMARY KEY,
    path text NOT NULL 
);

DROP TABLE IF EXISTS address;
CREATE TABLE address (
    address_id SERIAL PRIMARY KEY,
    city text NOT NULL,
    street text NOT NULL,
    zip_code text NOT NULL,
    country_id INTEGER REFERENCES country(country_id) ON UPDATE CASCADE
);

DROP TABLE IF EXISTS users;
CREATE TABLE users (
    user_id SERIAL PRIMARY KEY,
    username text NOT NULL CONSTRAINT username_uk UNIQUE,
    email text NOT NULL CONSTRAINT user_email_uk UNIQUE,
    first_name text NOT NULL,
    last_name text NOT NULL,
    password text NOT NULL,
    deleted BOOLEAN DEFAULT FALSE,
    img INTEGER REFERENCES photo(photoID) ON UPDATE CASCADE,
    billingAddress INTEGER REFERENCES address(addressID) ON UPDATE CASCADE,
    shippingAddress INTEGER REFERENCES address(addressID) ON UPDATE CASCADE
);

DROP TABLE IF EXISTS admin;
CREATE TABLE admin (
    admin_id INTEGER REFERENCES users(user_id) ON UPDATE CASCADE PRIMARY KEY
);

DROP TABLE IF EXISTS authenticated;
CREATE TABLE authenticated (
    authenticated_id INTEGER REFERENCES user(userID) ON UPDATE CASCADE PRIMARY KEY,
    balance money DEFAULT 0 NOT NULL
);
 
DROP TABLE IF EXISTS review;
CREATE TABLE review (
    review_id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES authenticated(authenticated_id) ON UPDATE CASCADE,
    comment text,
    "date" TIMESTAMP WITH TIME zone DEFAULT now() NOT NULL,
    rating INTEGER NOT NULL CONSTRAINT rating_ck CHECK (((rating > 0) AND (rating <= 5)))
);

DROP TABLE IF EXISTS category;
CREATE TABLE category (
    category_id SERIAL PRIMARY KEY,
    name text NOT NULL UNIQUE
);
 
DROP TABLE IF EXISTS details;
CREATE TABLE detail (
    detail_id SERIAL PRIMARY KEY,
    name text NOT NULL UNIQUE
);

DROP TABLE IF EXISTS item;
CREATE TABLE item (
    item_id SERIAL PRIMARY KEY,
    name text NOT NULL,
    stock INTEGER NOT NULL CONSTRAINT pos_stock CHECK (stock >= 0),
    brief_description text,
    description text NOT NULL,
    price MONEY NOT NULL CONSTRAINT pos_price CHECK (price >= 0::MONEY),
    is_archived BOOLEAN NOT NULL DEFAULT false,
    category_id INTEGER REFERENCES category (category_id) ON UPDATE CASCADE
);
 
DROP TABLE IF EXISTS ban;
CREATE TABLE ban (
    admin_id INTEGER NOT NULL REFERENCES admin(admin_id) ON UPDATE CASCADE,
    user_id INTEGER NOT NULL REFERENCES user (user_id) ON UPDATE CASCADE,
    "date" TIMESTAMP WITH TIME zone DEFAULT now() NOT NULL,
    reason text NOT NULL,
    PRIMARY KEY (adminID, userID)
);

DROP TABLE IF EXISTS purchase;
CREATE TABLE purchase (
    purchase_id SERIAL PRIMARY KEY,
    userID INTEGER REFERENCES authenticated (authenticated_id) ON UPDATE CASCADE,
    "date" TIMESTAMP WITH TIME zone DEFAULT now() NOT NULL
);
 
DROP TABLE IF EXISTS purchase_item;
CREATE TABLE purchase_item (
    purchase_id INTEGER NOT NULL REFERENCES purchase (purchase_id) ON UPDATE CASCADE,
    itemID INTEGER NOT NULL REFERENCES item (item_id) ON UPDATE CASCADE,
    price MONEY NOT NULL,
    quantity INTEGER NOT NULL CONSTRAINT quantity_more_zero CHECK (quantity > 0),
    PRIMARY KEY (purchase_id, item_id)
);

DROP TABLE IF EXISTS advertisement;
CREATE TABLE advertisement (
    advertisement_id INTEGER PRIMARY KEY,
    title text NOT NULL,
    begin_date TIMESTAMP WITH TIME zone DEFAULT now() NOT NULL,
    end_date TIMESTAMP WITH TIME zone NOT NULL,
    photo_id INTEGER REFERENCES photo (photo_id) ON UPDATE CASCADE,
    CONSTRAINT ad_dates_ck CHECK (begin_date < end_date)
);

DROP TABLE IF EXISTS item_photo;
CREATE TABLE item_photo (
    photo_id INTEGER NOT NULL REFERENCES photo (photo_id) ON UPDATE CASCADE PRIMARY KEY,
    item_id INTEGER NOT NULL REFERENCES item (item_id) ON UPDATE CASCADE

);
 
DROP TABLE IF EXISTS cart;
CREATE TABLE cart (
    user_id INTEGER REFERENCES authenticated (authenticated_id) ON UPDATE CASCADE,
    item_id INTEGER NOT NULL REFERENCES item (item_id) ON UPDATE CASCADE,
    add_date TIMESTAMP WITH TIME zone DEFAULT now() NOT NULL,
    quantity INTEGER NOT NULL CONSTRAINT quantity_more_zero CHECK (quantity > 0),
    PRIMARY KEY (user_id, item_id)
);
 
DROP TABLE IF EXISTS wishlist;
CREATE TABLE wishlist (
    user_id INTEGER REFERENCES authenticated (authenticated_id) ON UPDATE CASCADE,
    item_id INTEGER NOT NULL REFERENCES item (item_id) ON UPDATE CASCADE,
    add_date TIMESTAMP WITH TIME zone DEFAULT now() NOT NULL,
    PRIMARY KEY (userID, itemID)
);

DROP TABLE IF EXISTS discount;
CREATE TABLE discount (
    discount_id SERIAL PRIMARY KEY,
    "percentage" INTEGER NOT NULL CONSTRAINT valid_percentage CHECK ((("percentage" > 0) AND ("percentage" <= 100))),
    begin_date TIMESTAMP WITH TIME zone DEFAULT now() NOT NULL,
    end_date TIMESTAMP WITH TIME zone NOT NULL,
    CONSTRAINT ad_dates_ck CHECK (beginDate < endDate)
);

DROP TABLE IF EXISTS "notification";
CREATE TABLE "notification" (
    notification_id SERIAL PRIMARY KEY
    
);

DROP TABLE IF EXISTS discount_notification;
CREATE TABLE discount_notification (
    notification_id INTEGER NOT NULL REFERENCES discount (discount_id) ON UPDATE CASCADE PRIMARY KEY,
    discount_id INTEGER NOT NULL REFERENCES discount (discount_id) ON UPDATE CASCADE
);

DROP TABLE IF EXISTS stock_notification;
CREATE TABLE stock_notification (
    notification_id SERIAL PRIMARY KEY
);

DROP TABLE IF EXISTS apply_discount;
CREATE TABLE apply_discount (
    item_id INTEGER NOT NULL REFERENCES item (item_id) ON UPDATE CASCADE,
    discount_id INTEGER NOT NULL REFERENCES discount (discount_id) ON UPDATE CASCADE,
    PRIMARY KEY (itemID, discountID)
);

DROP TABLE IF EXISTS item_detail;
CREATE TABLE itemDetail (
    item_id INTEGER NOT NULL REFERENCES item (item_id) ON UPDATE CASCADE,
    detail_id INTEGER NOT NULL REFERENCES detail (detail_id) ON UPDATE CASCADE,
    detail_info text NOT NULL,
    PRIMARY KEY (detail_id, item_id)
);

DROP TABLE IF EXISTS category_detail;
CREATE TABLE category_detail (
    category_id INTEGER NOT NULL REFERENCES category (category_id) ON UPDATE CASCADE,
    detail_id INTEGER NOT NULL REFERENCES detail (detail_id) ON UPDATE CASCADE,
    PRIMARY KEY (category_id, detail_id)
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
| **Description** | Update user information |
| **Frequency**   | hundred per month                     |
```sql 
UPDATE "user"
    SET first_name = $first_name, last_name = $last_name, email = $email, 
    password = $password, billingAddress = $billingAddress, 
    shippingAddress = $shippingAddress, photoID = $photoID
    WHERE userID = $userID
```              

| **Query**       | UPDATE02                             |
| ---             | ---                                    |
| **Description** | Update item information |
| **Frequency**   | hundred per month                     |
```sql 
UPDATE "item"
    SET stock = $stock, brief_description = $brief_description, description = $description,
    price = $price, isArchived = $isArchived, category = $category
    WHERE itemID = $itemID
```                

| **Query**       | UPDATE03                             |
| ---             | ---                                    |
| **Description** | Update cart information |
| **Frequency**   | hundred per month                     |
```sql 
UPDATE "cart"
    SET addDate = $addDate, quantity = $quantity
    WHERE userID = $userID AND itemID = $itemID
```              

| **Query**       | INSERT01                           |
| ---             | ---                                    |
| **Description** | New user registered |
| **Frequency**   | dozens per day                     |
```sql 
INSERT INTO "user" (first_name,last_name,username,email,password)
    VALUES($first_name,$last_name,$username,$email,$password)
```          

| **Query**       | INSERT02                           |
| ---             | ---                                    |
| **Description** | New item for sale |
| **Frequency**   | hundreds per month                     |
```sql 
INSERT INTO "item" (name,stock,brief_description,description,price,category)
    VALUES ($name,$stock,$brief_description,$description,$price,$category)
```        

| **Query**       | INSERT03                           |
| ---             | ---                                    |
| **Description** | Create new review |
| **Frequency**   | hundreds per month                     |
```sql 
INSERT INTO "review" (userID,comment,date,rating)
    VALUES ($userID,$comment,$date,$rating)
```             

| **Query**       | INSERT04                           |
| ---             | ---                                    |
| **Description** | Create new address |
| **Frequency**   | hundreds per month                     |
```sql 
INSERT INTO "address" (city,street,zip_code,country)
    VALUES ($city,$street,$zip_code,$country)
```             

| **Query**       | INSERT05                           |
| ---             | ---                                    |
| **Description** | Ban user |
| **Frequency**   | dozens per month                     |
```sql 
INSERT INTO "ban" (adminID,userID,date,reason)
    VALUES ($adminID,$userID,$date,$reason)
```   

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

| T01 | Add to Cart, update stock                                    |
| --------------- | ----------------------------------- |
| Justification   | When adding an item to the cart, the stock must be decreased, but if more than one user adds the same item simultaneously, an error can occur and so the transaction is necessary.  Repeatable Read isolation is used to avoid dirty and nonrepeatable reads, while allowing new rows to be inserted in items. |
| Isolation level | Repeatable Read |

```sql
BEGIN TRANSACTION;
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ

DO
$do$
BEGIN
    IF (SELECT stock FROM item WHERE item_id = $item_id) > 0 THEN
		UPDATE item SET stock = stock - 1 WHERE item_id = $item_id 
    END IF;
END
$do$

COMMIT;
```



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