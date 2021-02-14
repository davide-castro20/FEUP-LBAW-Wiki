# ER: Requirements Specification Component

Our website aims to help customers get what they need when they need it during these troubling times with an enjoyable browsing experience.

## A1: Online Shop
This project intends to specify, develop and promote an information system available through the web for the management of an online store, in which users can buy products.  

We have a group of products to sell and we feel that a physical storefront wouldn't be enough to sell them. In addition, because of current circumstances, the physical contact required to sell our products in such a way has been heavily discouraged, to say the least. Because of this, we are creating an online website to facilitate the transactions and increase the scope of potential buyers. We aim to create a platform with a responsive design, to give our uses the best browsing experience available in the market, allowing users to search through various categories, filter items, search them by name or choose from a recommended list.

Users are separated into three different types: system administrators, buyers who have to register and log into the system, and guests.

Buyers can acquire products. Additionally, the admins have full access and modification privileges, including removing ongoing sales and assign users as admins. In addition, all users except guests, can have a list of their favorite products and be able to see their history of products.



---


## A2: Actors and User stories
> Brief presentation of the product.  
> Brief presentation of the artefact goals.


### 1. Actors

| Identifier    | Description                                                                                                                                                  | Example  |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| Guest         | Unauthenticated user that can register himself or log into the website                                                                                                                   | n/a      |
| User          | Generic user that has access to public information                                                                                                           | n/a      |
| Buyer         | Authenticated user that can browse items, make purchases, add items to their favourites list, charge their account's balance and rate and comment item posts | lbaw2021 |
| Administrator | Authenticated user that can browse items, add/remove/edit items, manage comments and users, create new administrator accounts                                | lbaw2021 |


### 2. User Stories

#### 2.1 **Guest**
| Identifier | Name                       | Priority | Description                                                                                  |
|------------|----------------------------|----------|----------------------------------------------------------------------------------------------|
| US01       | Sign-up                    | high     | As a *Guest*, I want to be able to create a new account so that I'm able to authenticate myself |
| US02       | Sign-in                    | high     | As a *Guest*, I want to be able to authenticate myself so that I'm able to buy products         |
| US03       | Administrator Sign-in      | high     | As a *Guest*, I want to be able to sign-in as an administrator if I'm permitted to do so  |
| US04       | Sign-up using external API | low      | As a *Guest*, I want to be able to create a new account using my existent Google account        |
| US05       | Sign-in using external API | low      | As a *Guest*, I want to be able to sign-in using my Google account                              |

#### 2.2 **User**
| Identifier  | Name  | Priority  | Description  |
|---|---|---|---|
| US11  | Access Home  | high  | As a *User*, I want to access the website's homepage, so that I can know its general-purpose  |
| US12  | Access About Page  | high  | As a *User*, I want to access the 'About' page, so that I can see a complete and detailed description of the website  |
| US13  | See Contacts  | high  | As a *User*, I want to consult the website's contacts, so that I know how to contact the team if needed  |
| US14  | Search | high | As a *User*, I want to search for public information, like categories, items and prices, so that I can be informed about the platform's content |

#### 2.3 **Buyer**

| Identifier | Name                 | Priority | Description                                                                                                                 |
|------------|----------------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| US21       | See purchase history  | high     | As a *Buyer*, I want to see my purchasing history, so that I can see the products I have bought                              |
| US22       | See wish list        | medium   | As a *Buyer*, I want to see my wish list, so that I can decide if I want to purchase them                                    |
| US23       | Add to wish list        | medium   | As a *Buyer*, I want to add items to my wish list, so that I can purchase them easily in the future                          |
| US24       | Remove from wish list      | medium   | As a *Buyer*, I want to remove an item from my wish list, so that I can forget the item                                      |
| US25       | Buy item             | high     | As a *Buyer*, I would like to purchase an item, so that I can use it                                                        |
| US26       | Rate item             | high     | As a *Buyer*, I would like to attribute a score to an item, so that other users can know my basic opinion of the item        |
| US27       | Comment item         | high     | As a *Buyer*, I would like to attach a comment to an item, so that other users can know my more complete opinion of the item |

#### 2.4 **Administrator**

| Identifier  | Name  | Priority  | Description  |
|---|---|---|---|
| US31  | Manage products  | high  | As an *Administrator*, I want to manage product listings, so that I can create, remove and edit items|
| US32  | Create admin accounts  | high  | As an *Administrator*, I want to create administrator accounts, so that others can have administrator permissions  |
| US33  | Remove comments  | high  | As an *Administrator*, I want to remove comments, so that I can filter inappropriate language|
| US34  | View Buyer's History | medium | As an *Administrator*, I want to be able to view customer's purchase history in order to get a better understanding of what buyers look for the most|
| US35  | Statistics of sold items | medium | As an *Administrator*, I want to have easy access to statistics of items filtered by different categories of users|


### 3. Supplementary Requirements

> Annex including business rules, technical requirements, and restrictions.  
> For each subsection, a table containing identifiers, names, and descriptions for each requirement.

#### 3.1. Business rules

#### 3.2. Technical requirements

#### 3.3. Restrictions


---


## A3: User Interface Prototype

> Brief presentation of the product.  
> Brief presentation of the artefact goals.


### 1. Interface and common features

> Screenshots highlighting the main elements of the interface, for desktop and mobile.


### 2. Sitemap

> Sitemap presenting the overall structure of the web application.  
> Each screen must be identified in the sitemap.  
> Multiple pages of the same screen (e.g. student profile in SIGARRA) are presented as page stacks.


### 3. Storyboards

> Storyboards for the main use cases of the system.  
> Do not include trivial use cases.


### 4. Interfaces

> Screenshots, structured in subsections, including a reference, a description and a URL to the working version.

#### UI01: Home

#### UI02: About


### 4. Hand-made materials

> Include digitization of the hand-made materials, particularly the wireflows. 


---


## Revision history

Changes made to the first submission:
1. Item 1
1. ...

***
GROUP21gg, DD/MM/2021

* Group member 1 name, email (Editor)
* Group member 2 name, email
* ...