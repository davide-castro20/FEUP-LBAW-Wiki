# EAP: Architecture Specification and Prototype

Our website aims to help customers get what then need when they need it during these troubling times with an enjoyable browsing experience.

## A7: High-level architecture. Privileges. Web resources specification

> Brief presentation of the product.  
> Brief presentation of the artefact goals.

### 1. Overview

|   |   |
|---|---|
| M01: Authentication and profile  | Web resources associated with user authentication and profile management. Includes the following system features: login/logout, registration, credential recovery, view and edit personal profile information.  |
| M02: Products and categories  | Web resources associated with the searching, filtering and listing of all products and categories available to the user.  |
| M03: Management  | Web resources associated with website management, such as: promote and ban users, add, view, edit and remove item listings, delete user comments. |
| M04: Static pages  | Web resources associated with static pages, such as: FAQ, About and Contacts.  |
| M05: Products and reviews  | Web resources associated with products and reviews. Includes system features: Add to cart and wishlist, add, edit and remove reviews. |
| M06: Wishlist and cart | Web resources associated with cart and wishlist actions. Includes system features such as: View, delete and checkout cart and view, add to cart and delete from wishlist |

### 2. Permissions

|   |   |   |
|---|---|---|
| PUB  | Public | Group of users without privileges |
| USR  | User | Authenticated user |
| OWN  | Owner | Group of users who own something (e.g. own profile) |
| ADM  | Administrator | Group of administrators |



### 3. Modules

> Web resources organized by module  
> Document and describe the web resources associated with each module, indicating the URL, HTTP method, request parameters and response.  
> Follow the RESTful resource naming  
> At the end of this page is presented some usual descriptors to document the web resources.

#### 3.1 Module 1

##### R105: Register Action

|   |   |   |
|---|---|---|
| **URL**          | `/register` ||
| **Description**  | This web resource... ||
| **Method**       | POST ||
| **Request Body** | +name: string | Name  |
|   | +email: string | Email  |
|   | +password: string | Password  |
|   | ?picture: file | Profile picture  |
| **Redirects**    | [R106](#r106) | Success |
|   | [R104](#r104) | Error |
| **AJAX Calls** | [R110](#r110) ||
| **Permissions** | PUB ||

#### 3.2 Module 2

### 4. JSON/XML Types

> Document the JSON or XML responses that will be used by the web resources.  

### Web resources descriptors (Note: **NOT to be included on the final artefact**)

* URL - Resource identifier, following the RESTful resource naming conventions 
* Description - Describe the resource, when it's used and why
* UI - Reference to the A3 user interface used by the resource
* SUBMIT - Reference to the actions/requests integrated with the resource
* Method - HTTP request Method
* Parameters - Information that is sent through the URL, by a query string or path
* Request Body - Data associated and transmitted with each request
* Returns - HTTP code returned from a request
* Response Body - Data sent from the server, in response to a given request
* Permissions - Required permissions to access the resource


---


## A8: Vertical prototype

> Brief presentation of the product.  
> Brief presentation of the artefact goals.

### 1. Implemented Features

#### 1.1. Implemented User Stories

> Identify the user stories that were implemented in the prototype.  

| User Story reference | Name                   | Priority                   | Description                   |
| -------------------- | ---------------------- | -------------------------- | ----------------------------- |
| US01                 | Name of the user story | Priority of the user story | Description of the user story |

...

#### 1.2. Implemented Web Resources

> Identify the web resources that were implemented in the prototype.  

> Module M01: Module Name  

| Web Resource Reference | URL                            |
| ---------------------- | ------------------------------ |
| R01: Web resource name | URL to access the web resource |

...

> Module M02: Module Name  

...

### 2. Prototype

> URL of the prototype plus user credentials necessary to test all features.  
> Link to the prototype source code in the group's git repository.  


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