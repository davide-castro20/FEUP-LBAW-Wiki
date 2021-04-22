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
| M05: Products and reviews  | Web resources associated with products and reviews. Includes system features: Add, edit and remove reviews, and see product rating. |
| M06: Wishlist and cart | Web resources associated with cart and wishlist actions. Includes system features such as: View, delete and checkout cart and view, add and delete to cart and wishlist |

### 2. Permissions

|   |   |   |
|---|---|---|
| PUB  | Public | Group of users without privileges |
| USR  | User | Authenticated user |
| OWN  | Owner | Group of users who own something (e.g. own profile) |
| ADM  | Administrator | Group of administrators |



### 3. OpenAPI Specification

OpenAPI specification in YAML format to describe the web application's web resources.

Link to the `.yaml` file in the group's repository.

Link to the Swagger generated documentation (https://app.swaggerhub.com/apis/Diogogrosario/LBAW-FNEUC/1.0#/M02%3A%20Products%20and%20categories/R201).
```yaml
openapi: 3.0.0

info:
  version: '1.0'
  title: 'LBAW FNEUC Web API'
  description: 'Web Resources Specification (A7) for FNEUC'

servers:
# Added by API Auto Mocking Plugin
- description: SwaggerHub API Auto Mocking
  url: https://virtserver.swaggerhub.com/Diogogrosario/LBAW-FNEUC/1.0
- url: http://lbaw-prod.fe.up.pt
  description: Production server

externalDocs:
  description: Find more info here.
  url: https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/home

tags:
  - name: 'M01: Authentication and profile'
  - name: 'M02: Products and categories'
  - name: 'M03: Management'
  - name: 'M04: Static pages'
  - name: 'M05: Products and reviews'
  - name: 'M06: Wishlist and cart'

paths:
  /signin:
    get:
      operationId: R101
      summary: 'R101: Signin Form'
      description: 'Provide signin form. Access: PUB'
      tags:
        - 'M01: Authentication and profile'
      responses:
        '200':
          description: 'Ok. Show [UI11](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui11-sign-in)'
    post:
      operationId: R102
      summary: 'R102: Signin Action'
      description: 'Processes the signin form submission. Access: PUB'
      tags:
        - 'M01: Authentication and profile'
 
      requestBody:
        required: true
        content:
          application/x-www-form-urlencoded:
            schema:
              type: object
              properties:
                username:          # <!--- form field name
                  type: string
                password:    # <!--- form field name
                  type: string
              required:
                - username
                - password
 
      responses:
        '302':
          description: 'Redirect after processing the signin credentials.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful authentication. Redirect to mainpage.'
                  value: '/mainpage'
                302Error:
                  description: 'Failed authentication. Redirect to signin form.'
                  value: '/signin'
  
  /signout:
    post:
      operationId: R103
      summary: 'R103: Signout Action'
      description: 'Signout the current authenticated used. Access: USR, ADM'
      tags:
        - 'M01: Authentication and profile'
      responses:
        '302':
          description: 'Redirect after processing signout.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful signout. Redirect to mainpage.'
                  value: '/mainpage'                 
  
  /signup:
    get:
      operationId: R104
      summary: 'R104: Signup Form'
      description: 'Provide new user signup form. Access: PUB'
      tags:
        - 'M01: Authentication and profile'
      responses:
        '200':
          description: 'Ok. Show [UI12](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui12-sign-up)'

    post:
      operationId: R105
      summary: 'R105: Signup Action'
      description: 'Processes the new user signup form submission. Access: PUB'
      tags:
        - 'M01: Authentication and profile'

      requestBody:
        required: true
        content:
          application/x-www-form-urlencoded:
            schema:
              type: object
              properties:
                username:
                  type: string
                email:
                  type: string
                firstName:
                  type: string
                lastName:
                  type: string
                password:
                  type: string
                passwordConfirmation:
                  type: string
              required:
                - username
                - email
                - firstName
                - lastName
                - password
                - passwordConfirmation

      responses:
        '302':
          description: 'Redirect after processing the new user information.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful registration. Redirect to mainpage.'
                  value: '/mainpage'
                302Failure:
                  description: 'Failed signup. Redirect to signup form.'
                  value: '/signup'                          
                  
  /credentialRecovery:
    get:
      operationId: R106
      summary: 'R106: Credential Recovery Form'
      description: 'Provide credential recovery form. Access: PUB'
      tags:
        - 'M01: Authentication and profile'
      responses:
        '200':
          description: 'NOT YET DONE!!!!!!!!!!!'

    post:
      operationId: R107
      summary: 'R107: Credential Recovery Action'
      description: 'Processes the credential recovery form submission. Access: PUB'
      tags:
        - 'M01: Authentication and profile'

      requestBody:
        required: true
        content:
          application/x-www-form-urlencoded:
            schema:
              type: object
              properties:
                email:
                  type: string
              required:
                - email

      responses:
        '302':
          description: 'Redirect after processing the credential recovery information.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful credential recovery. Redirect to signin.'
                  value: '/signin'
                  
  /users/{id}:
    get:
      operationId: R108
      summary: 'R108: View user profile'
      description: 'Show the individual user profile. Access: USR, ADM'
      tags:
        - 'M01: Authentication and profile'

      parameters:
        - in: path
          name: id
          schema:
            type: integer
          required: true

      responses:
        '200':
          description: 'Ok. Show [UI13](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui13-user-profile)'
          
  /api/products:
    get:
      operationId: R201
      summary: 'R201: Search products API'
      description: 'Searches for products and returns the results as JSON. Access: PUB.'

      tags: 
        - 'M02: Products and categories'

      parameters:
        - in: query
          name: query
          description: String to use for full-text search
          schema:
            type: string
          required: false
        - in: query
          name: item
          description: Category of the products
          schema:
            type: string
          required: false
        - in: query
          name: priceRange
          description: Integer with the maximum price of the product
          schema:
            type: integer
          required: false
        - in: query
          name: review
          description: Integer with the minimum review of the product
          schema:
            type: integer
          required: false
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                type: array
                items:
                  type: object
                  properties:
                    id:
                      type: string
                    name:
                      type: string
                    price:
                      type: integer
                    category:
                      type: string
                    description:
                      type: string
                    inStock:
                      type: boolean
                    details:
                      type: array
                      items:
                        type: array
                        items: 
                          type: string
                example:
                  - id: 1
                    name: Asus Computer
                    price: 300
                    category: Computers
                    description: This asus computer is the best for its price
                    inStock: true
                    details: [["16GB","RAM"], ["i7-7000K","Processor"], ["512GB","HDD"]]
                  - id: 2
                    name: Cyber Punk
                    price: 59
                    category: Video Games
                    description: Cyber Punk is a futuristic RPG that will blow you away with stunning graphics
                    inStock: false
                    details: ["18+"]

...
```


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