# EAP: Architecture Specification and Prototype

Our website aims to help customers get what then need when they need it during these troubling times with an enjoyable browsing experience.

## A7: High-level architecture. Privileges. Web resources specification

This artifact intends to document the catalogue of resources and the properties of each resource available to all users. The artifact contains operations over data such as: create, delete, update and read.

### 1. Overview

| Module Name | Module Description |
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

Link to the Swagger generated documentation (https://app.swaggerhub.com/apis/LBAW-FEUP-11/lbaw-fneuc_web_api/1.0).  
Link to the OpenAPI specification file in the repository: [a7_openapi](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/blob/master/a7_openapi.yaml).
```yaml
openapi: 3.0.0

info:
  version: '1.0'
  title: 'LBAW FNEUC Web API'
  description: 'Web Resources Specification (A7) for FNEUC'

servers:
# Added by API Auto Mocking Plugin
- description: SwaggerHub API Auto Mocking
  url: https://virtserver.swaggerhub.com/LBAW-FEUP-11/LBAW-FNEUC/1.0
- url: http://lbaw2111.lbaw-prod.fe.up.pt/
  description: Production server

externalDocs:
  description: Find more info here.
  url: https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/home

tags:
  - name: 'M01: Authentication and profile'
  - name: 'M02: Products and categories'
  - name: 'M03: Management'
  - name: 'M04: Static Pages'
  - name: 'M05: Products and reviews'
  - name: 'M06: Wishlist and cart'

paths:
  /login:
    get:
      operationId: R101
      summary: 'R101: Login Form'
      description: 'Provide Login form. Access: PUB'
      tags:
        - 'M01: Authentication and profile'
      responses:
        '200':
          description: 'Ok. Show [UI11](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui11-sign-in)'
    post:
      operationId: R102
      summary: 'R102: Login Action'
      description: 'Processes the Login form submission. Access: PUB'
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
          description: 'Redirect after processing the login credentials.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful authentication. Redirect to mainpage.'
                  value: '/mainpage'
                302Error:
                  description: 'Failed authentication. Redirect to login form.'
                  value: '/login'
  
  /logout:
    post:
      operationId: R103
      summary: 'R103: Logout Action'
      description: 'Logout the current authenticated used. Access: USR, ADM'
      tags:
        - 'M01: Authentication and profile'
      responses:
        '302':
          description: 'Redirect after processing logout.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful logout. Redirect to mainpage.'
                  value: '/mainpage'                 
  
  /register:
    get:
      operationId: R104
      summary: 'R104: Register Form'
      description: 'Provide new user register form. Access: PUB'
      tags:
        - 'M01: Authentication and profile'
      responses:
        '200':
          description: 'Ok. Show [UI12](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui12-sign-up)'

    post:
      operationId: R105
      summary: 'R105: Register Action'
      description: 'Processes the new user register form submission. Access: PUB'
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
                  
  /userProfile/{id}/edit:
  
    parameters:
        - in: path
          name: id
          schema:
            type: integer
          required: true
    
    get:
      operationId: R106
      summary: 'R106: Edit Profile Form'
      description: 'Provide edit profile form. Access: USR'
      tags:
        - 'M01: Authentication and profile'
      responses:
        '200':
          description: 'Ok. Show [UI13](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui13-user-profile)'

    patch:
      operationId: R107
      summary: 'R107: Edit Profile Action'
      description: 'Processes the edit profile form submission. Access: USR'
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
                picture:
                  type: string
                  format: binary
                address:
                  type: object
                  properties:
                    zip-code:
                      type: string
                    street:
                      type: string
                    city: 
                      type: string
                    country:
                      type: string

      responses:
        '302':
          description: 'Redirect after processing the new user information.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful edit. Redirect to user profile.'
                  value: '/userProfile/{id}'
                302Failure:
                  description: 'Failed edit. Redirect to user profile.'
                  value: '/userProfile/{id}'                
                  
  /credentialRecovery:
    get:
      operationId: R108
      summary: 'R108: Credential Recovery Form'
      description: 'Provide credential recovery form. Access: PUB'
      tags:
        - 'M01: Authentication and profile'
      responses:
        '200':
          description: 'NOT YET DONE!!!!!!!!!!!'

    post:
      operationId: R109
      summary: 'R109: Credential Recovery Action'
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
                  description: 'Successful credential recovery. Redirect to login.'
                  value: '/login'
                  
  /userProfile/{id}:
    get:
      operationId: R110
      summary: 'R110: View user profile'
      description: 'Show the individual user profile. Access: OWN, ADM'
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
          
    delete:
      operationId: R111
      summary: 'R111: Delete account Action'
      description: 'Processes the delete account action. Access: OWN'
      tags:
        - 'M01: Authentication and profile'
 
      parameters:
        - in: path
          name: id
          description: User identifier
          schema:
            type: integer
          required: true
           
      responses:
        '302':
          description: 'Redirect after processing the account deletion.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful deletion. Redirect to main page.'
                  value: '/mainpage'
                302Error:
                  description: 'Failed deletion. Redirect to user profile page.'
                  value: '/userProfile/{id}'
          
  /userProfile/{id}/billingAddress:
    post:
      operationId: R112
      summary: 'R112: Update billing address'
      description: 'AJAX request. Update the user''s billing address. Access: OWN'
      tags:
        - 'M01: Authentication and profile'

      parameters:
        - in: path
          name: id
          description: User identifier
          schema:
            type: integer
          required: true
      
      requestBody:
        required: true
        content:
          application/x-www-form-urlencoded:
            schema:
              type: object
              properties:
                street:
                  type: string
                country:
                  type: string
                zip_code:
                  type: string
                city:
                  type: string
                  
      responses:
          '200':
            description: 'Address updated successfuly.'
            content:
              application/json:
                schema:
                  type: object
                  properties:
                    street:
                      type: string
                    country:
                      type: string
                    zip_code:
                      type: string
                    city:
                      type: string
                      
                example:
                  street: 'Washington Avenue'
                  county: 'USA'
                  zip_code: '124231'
                  city: 'Washington DC'
                  
  /userProfile/{id}/shippingAddress:
    post:
      operationId: R113
      summary: 'R113: Update shipping address'
      description: 'AJAX request. Update the user''s shipping address. Access: OWN'
      tags:
        - 'M01: Authentication and profile'

      parameters:
        - in: path
          name: id
          description: User identifier
          schema:
            type: integer
          required: true
      
      requestBody:
        required: true
        content:
          application/x-www-form-urlencoded:
            schema:
              type: object
              properties:
                street:
                  type: string
                country:
                  type: string
                zip_code:
                  type: string
                city:
                  type: string

      responses:
        '200':
          description: 'Address updated successfuly.'
          content:
            application/json:
              schema:
                type: object
                properties:
                  street:
                    type: string
                  country:
                    type: string
                  zip_code:
                    type: string
                  city:
                    type: string
                    
              example:
                street: 'Washington Avenue'
                county: 'USA'
                zip_code: '124231'
                city: 'Washington DC'
                
  /userProfile/{id}/purchaseHistory:
    get:
      operationId: R114
      summary: 'R114: View user''s purchase history'
      description: 'Show the individual user purchase history. Access: OWN, ADM'
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
          description: 'Ok. Show [UI09](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui09-purchase-history)'
          
  /api/items:
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
          name: category
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
                    details: [["18+", "Age restriction"], ["01-10-2020", "Release Date"], ["CDPR", "Developer"]]
  /item/{id}:
    parameters:
      - in: path
        name: id
        description: Product Identifier
        schema:
          type: integer
        required: true
        
    get:
      operationId: R202
      summary: 'R202: View product page'
      description: "Show a product's page containing all its information. Access: PUB"

      tags:
        - 'M02: Products and categories'

      responses:
        '200':
          description: 'Ok. Show [UI08](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui08-item)'
        '404':
          description: 'Product not found!'
        
  /item/{id}/review:
    parameters:
      - in: path
        name: id
        description: Product Identifier
        schema:
          type: integer
        required: true
        
    post:
      operationId: R501
      summary: 'R501: Submit product review'
      description: "AJAX request. Submits a review with rating to a product. Access: USR"
      tags:
        - 'M05: Products and reviews'

      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                review_text:
                  type: string
                rating:
                  type: integer
              required:
                - rating

      responses:
        '201':
          description: "Review added successfully."
          content:
            application/json:
              schema:
                type: object
                properties:
                  id:
                    type: integer
                  text:
                    type: string
                  rating:
                    type: integer

              example:
                id: 1
                text: "Amazing product"
                rating: 5
        '401':
          description: "Unauthenticated user cannot review product."
        '403':
          description: "User already reviewed this product / invalid review."

  /review/{reviewId}:
    parameters:
      - in: path
        name: reviewId
        description: Review Identifier
        schema:
          type: integer
        required: true
      
    put:
      operationId: R502
      summary: 'R502: Edit product review'
      description: "AJAX request. Updates a user review of the product. Access: OWN"
      tags:
        - 'M05: Products and reviews'

      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                review_text:
                  type: string
                rating:
                  type: integer
              required:
                - review_id
                - rating

      responses:
        '200':
          description: "Review edited successfully."
          content:
            application/json:
              schema:
                type: object
                properties:
                  text:
                    type: string
                  rating:
                    type: integer

              example:
                id: 1
                text: "Not amazing anymore"
                rating: 3
        '401':
          description: "Unauthenticated user cannot edit review."
        '406':
          description: "Invalid review. Update failed."
    delete:
      operationId: R503
      summary: 'R503: Delete product review'
      description: "AJAX that deletes a user review of the product. Access: OWN, ADM"
      tags:
        - 'M05: Products and reviews'

      responses:
        '200':
          description: "Review deleted successfully."
        '401':
          description: "Unauthenticated user cannot delete reviews."
        '406':
          description: "Invalid review. Deletion failed."

  /about:
    get:
      operationId: R401
      summary: 'R401: View About page'
      description: 'Get the About page. Access: PUB'
      tags:
        - 'M04: Static Pages'

      responses:
        '200':
          description: 'Ok. Show [UI02](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui02-about)'

  /faq:
    get:
      operationId: R402
      summary: 'R402: View FAQ page'
      description: 'Get the FAQ page. Access: PUB'
      tags:
        - 'M04: Static Pages'

      responses:
        '200':
          description: 'Ok. Show [UI03](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui03-faq)'

  /contacts:
    get:
      operationId: R403
      summary: 'R403: View Contacts page'
      description: 'Get the Contacts page. Access: PUB'
      tags:
        - 'M04: Static Pages'

      responses:
        '200':
          description: 'Ok. Show [UI04](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui04-contacts)'
    
  
  /management:
    get:
      operationId: R301
      summary: 'R301: View administration page'
      description: "Show administration area. Acess: ADM"

      tags:
        - 'M03: Management'

      responses:
        '200':
          description: 'Ok. Show [UI06](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui06-admin-main-page)'
  
  /management/manageUsers:
    get:
      operationId: R302
      summary: 'R302: View user administration page'
      description: "Show user administration area. Acess: ADM"

      tags:
        - 'M03: Management'

      responses:
        '200':
          description: 'Ok. Show [UI14](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui14-user-administration)'
  
  /management/item:
    get:
      operationId: R303
      summary: 'R303: Add product Form'
      description: 'Provide add product form. Access: ADM'
      tags:
        - 'M03: Management'
      responses:
        '200':
          description: 'Ok. Show [UI05](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui05-add-a-new-item)'
    post:
      operationId: R304
      summary: 'R304: Add product Action'
      description: 'Processes the add product form submission. Access: ADM'
      tags:
        - 'M03: Management'
 
      requestBody:
        required: true
        content:
          application/x-www-form-urlencoded:
            schema:
              type: object
              properties:
                name:          # <!--- form field name
                  type: string
                price:    # <!--- form field name
                  type: integer
                category:          # <!--- form field name
                  type: string
                pictures:
                  type: array
                  items:
                    type: string
                    format: binary
                details:
                      type: array
                      items:
                        type: array
                        items: 
                          type: string
                brief_description:          # <!--- form field name
                  type: string
                description:          # <!--- form field name
                  type: string
              required:
                - name
                - price
                - category
                - pictures
                - brief_description
                - description
                - details
 
      responses:
        '302':
          description: 'Redirect after processing the product addition fields.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful addition. Redirect to item page.'
                  value: '/products/{id}'
                302Error:
                  description: 'Failed authentication. Redirect to add product form.'
                  value: '/admin/addproduct'
                  
  /management/item/{id}:
    parameters:
      - in: path
        name: id
        description: Product identifier
        schema:
          type: integer
        required: true
        
    put:
      operationId: R305
      summary: 'R305: Edit product Action'
      description: 'Processes edit product form submission. Access: ADM'
      tags:
        - 'M03: Management'
 
      requestBody:
        required: true
        content:
          application/x-www-form-urlencoded:
            schema:
              type: object
              properties:
                name:          
                  type: string
                price:   
                  type: integer
                category:          
                  type: string
                pictures:
                  type: array
                  items:
                    type: string
                    format: binary
                details:
                      type: array
                      items:
                        type: array
                        items: 
                          type: string
                brief_description:          # <!--- form field name
                  type: string
                description:          # <!--- form field name
                  type: string
              required:
                - name
                - price
                - category
                - pictures
                - brief_description
                - description
                - details
 
      responses:
        '302':
          description: 'Redirect after processing the product addition fields.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful addition. Redirect to item page.'
                  value: '/products/{id}'
                302Error:
                  description: 'Failed authentication. Redirect to add product form.'
                  value: '/admin/addproduct'      
  /admin/userManagement/ban:  

    post:
      operationId: R306
      summary: 'R306: Ban user Action'
      description: 'Processes the ban user operation. Access: ADM'
      tags:
        - 'M03: Management'

      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                user_id:
                  type: integer

      responses:
        '302':
          description: 'Redirect after processing the user ban.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful ban. Redirect to user management.'
                  value: '/admin/userManagement'
                302Failure:
                  description: 'Failed ban. Redirect to user management.'
                  value: '/admin/userManagement' 
  
  /admin/userManagement/promote:  
    
    patch:
      operationId: R307
      summary: 'R307: Promote user Action'
      description: 'Processes the promote user operation. Access: ADM'
      tags:
        - 'M03: Management'
        
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                user_id:
                  type: integer

      responses:
        '302':
          description: 'Redirect after processing the user promotion.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful promotion. Redirect to user management.'
                  value: '/admin/userManagement'
                302Failure:
                  description: 'Failed promotion. Redirect to user management.'
                  value: '/admin/userManagement'  
                  
  /admin/discountProduct:
    post:
      operationId: R309
      summary: 'R309: Add product discount Action'
      description: 'AJAX request. Add a discount to a chosen product. Access: ADM'
      tags:
        - 'M03: Management'
 
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                product_id:
                  type: integer
                percentage:
                  type: integer
                begin_date:
                  type: string
                end_date:
                  type: string      
                
      responses:
        '200':
          description: 'Discount added to product successfuly.'
          
  /admin/discountCategory:
    post:
      operationId: R310
      summary: 'R310: Add category discount Action'
      description: 'AJAX request. Add a discount to all products of a chosen category. Access: ADM'
      tags:
        - 'M03: Management'
 
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                category_id:
                  type: integer
                percentage:
                  type: integer
                begin_date:
                  type: string
                end_date:
                  type: string      
                
      responses:
        '200':
          description: 'Discount added to product successfuly.'
        '401':
          description: 'Product not found'
          
  /admin/discounts:
    post:
      operationId: R311
      summary: 'R311: Remove product discounts Action'
      description: 'AJAX request. Removes current discounts on a product. Access: ADM'
      tags:
        - 'M03: Management'
 
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                product_id:
                  type: integer
                
      responses:
        '200':
          description: 'Discounts removed from product successfuly.'
        '401':
          description: 'Item or discount not found'
          headers:
            Location:
              schema:
                type: string
              examples:
                401Item:
                  description: 'Item not found'
                401Discount:
                  description: 'Discount not found'
              
              
          
  /admin/purchases/{id}/purchaseStatus:
    patch:
      operationId: R312
      summary: 'R312: Update purchase status Action'
      description: 'AJAX request. Update the status of a purchase. Access: ADM'
      tags:
        - 'M03: Management'
        
      parameters:
        - in: path
          name: id
          description: Purchase identifier
          schema:
            type: integer
          required: true
      
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: integer   # <!--- status type
                
      responses:
        '200':
          description: 'Discounts removed from product successfuly.'

    post:
      operationId: R203
      summary: 'R203: Edit product Action'
      description: 'Processes the edit product form submission. Access: ADM'
      tags:
        - 'M02: Products and categories'
 
      parameters:
        - in: path
          name: id
          description: Product identifier
          schema:
            type: integer
          required: true
          
      requestBody:
        required: true
        content:
          application/x-www-form-urlencoded:
            schema:
              type: object
              properties:
                name:          # <!--- form field name
                  type: string
                price:    # <!--- form field name
                  type: integer
                category:          # <!--- form field name
                  type: string
                pictures:
                  type: array
                  items:
                    type: string
                    format: binary
                brief_description:          # <!--- form field name
                  type: string
                details:
                      type: array
                      items:
                        type: array
                        items: 
                          type: string
                description:          # <!--- form field name
                  type: string        
      responses:
        '302':
          description: 'Redirect after processing the edit product form fields.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful edit. Redirect to item page.'
                  value: '/products/{id}'
                302Error:
                  description: 'Failed edit. Redirect to item page.'
                  value: '/products/{id}'
                  
    delete:
      operationId: R204
      summary: 'R204: Delete product Action'
      description: 'Processes the delete product action. Access: ADM'
      tags:
        - 'M02: Products and categories'
 
      parameters:
        - in: path
          name: id
          description: Product identifier
          schema:
            type: integer
          required: true
           
      responses:
        '302':
          description: 'Redirect after processing the product deletion.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful deletion. Redirect to main page.'
                  value: '/mainpage'
                302Error:
                  description: 'Failed deletion. Redirect to main page.'
                  value: '/mainpage'
                  
  /item/{id}/stock:
    patch:
      operationId: R205
      summary: 'R205: Update product stock Action'
      description: 'AJAX request. Update the current stock of a product. Access: ADM'
      tags:
        - 'M02: Products and categories'
  
      parameters:
        - in: path
          name: id
          description: Product identifier
          schema:
            type: integer
          required: true
          
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                stock:
                  type: integer
           
      responses:
        '200':
            description: 'Sucessfully added item to wishlist.'
        '401':
          description: 'Unauthorized user cannot edit product stock'
                  
                  
  /user/{id}/wishlist:
    parameters:
      - in: path
        name: id
        description: User identifier
        schema:
          type: integer
        required: true
      
    get:
      operationId: R601
      summary: 'R601: View user''s wishlist'
      description: 'Redirect to user''s wishlist page. Access: OWN, ADM'
      tags:
        - 'M06: Wishlist and cart'
      responses:
        '200':
          description: 'Ok. Show [UI07](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui07-cart)'
  
  /wishlist:
    post:
      operationId: R602
      summary: 'R602: Add item to wishlist API'
      description: 'AJAX request. Adds an item to the users wishlist. Access: OWN'
      tags:
        -  'M06: Wishlist and cart'
        
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                productID:
                  type: integer  
                  
      responses:
        '200':
          description: 'Sucessfully added item to wishlist.'
        '401':
          description: 'The password does not correspond to the email.'

  /wishlist/{id}:
    parameters:
      - in: path
        name: id
        description: Product identifier
        schema:
          type: integer
        required: true
        
    delete:
      operationId: R603
      summary: 'R603: Remove item from wishlist'
      description: 'AJAX request. Removes an item from the user''s wishlist. Access: OWN'
      tags:
        -  'M06: Wishlist and cart'
                
      responses:
        '200':
          description: 'Sucessfully removed item from wishlist.'
        '401':
          description: 'Unauthenticated user cannot remove item from wishlist.'
        '406':
          description: 'Item not in the wishlist'
   
  /user/{id}/cart:
    get:
      operationId: R604
      summary: 'R604: View user''s cart'
      description: 'Redirect to user''s cart page. Access: OWN, ADM'
      tags:
        - 'M06: Wishlist and cart'
        
      parameters:
      - in: path
        name: id
        description: id of the user that has the correponding cart
        schema:
          type: integer
        required: true
        
      responses:
        '200':
          description: 'Ok. Show [UI07](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui07-cart)'
          
  /cart/{id}:
    parameters:
      - in: path
        name: id
        description: product 
        schema:
          type: integer
        required: true
  
    delete:
      operationId: R606
      summary: 'R606: Remove item from cart'
      description: 'AJAX request. Removes an item from the user''s cart. Access: OWN'
      tags:
        -  'M06: Wishlist and cart'

                
      responses:
        '200':
          description: 'Sucessfully removed item from cart.'
        '401':
          description: 'Unauthenticated user cannot remove item from cart.'
        '406':
          description: 'Item not in the cart'
        
  /cart:
    post:
      operationId: R605
      summary: 'R605: Add item to cart'
      description: 'AJAX request. Adds an item with chosen quantity to the users cart. Access: OWN'
      tags:
        -  'M06: Wishlist and cart'
      
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                productID:
                  type: integer 
                quantity:
                  type: integer
                  
      responses:
        '200':
          description: 'Sucessfully added item to cart.'
        '406':
          description: 'Item not available.'
        
    patch:
      operationId: R607
      summary: 'R607: Edit Product cart quantity'
      description: 'AJAX request. Updates the quantity of a product in the user''s cart. Access: OWN'
      tags:
        - 'M06: Wishlist and cart'

      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                productID:
                  type: integer 
                quantity:
                  type: integer
      
      responses:
        '200':
          description: 'Sucessfully updated item quantity.'
        '401':
          description: 'Unauthenticated user cannot update quantity in cart.'
        '406':
          description: 'Item not in the cart'
          
  /admin/announcement:
    post:
      operationId: R313
      summary: 'R313: Add announcement Action'
      description: 'AJAX request. Add an announcement. Access: ADM'
      tags:
        - 'M03: Management'
 
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                picture:
                  type: string
                  format: binary   
                
      responses:
        '200':
          description: 'Announcement added successfuly.'
          
  /admin/announcement/{id}:
    parameters:
      - in: path
        name: id
        description: Announcement identifier 
        schema:
          type: integer
        required: true
        
    post:
      operationId: R314
      summary: 'R314: Remove announcement Action'
      description: 'AJAX request. Remove an announcement. Access: ADM'
      tags:
        - 'M03: Management'
 
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                announcement_id:
                  type: integer
                
      responses:
        '200':
          description: 'Announcement removed successfuly.'
          
  /checkout:
    get:
      operationId: R608
      summary: 'R608: Checkout Form'
      description: 'Provide checkout form. Access: USR'
      tags:
        - 'M06: Wishlist and cart'
      responses:
        '200':
          description: 'Ok. "NOT YET IMPLEMENTED'

    post:
      operationId: R609
      summary: 'R609: Checkout Action'
      description: 'Processes the checkout form submission. Access: PUB'
      tags:
        - 'M06: Wishlist and cart'

      requestBody:
        required: true
        content:
          application/x-www-form-urlencoded:
            schema:
              type: object
              properties:
                address:
                  type: object
                  properties:
                    zip-code:
                      type: string
                    street:
                      type: string
                    city: 
                      type: string
                    country:
                      type: string
                shipping:
                  type: string
                payment_method:
                  type: string
              required:
                - address
                - shipping
                - payment_method

      responses:
        '302':
          description: 'Redirect after processing the checkout information.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful checkout. Redirect to mainpage.'
                  value: '/mainpage'
                302Failure:
                  description: 'Failed checkout. Redirect to checkout.'
                  value: '/checkout'
```


## A8: Vertical prototype

The vertical prototype includes the implementation of some of the user stories described in the er artifacts and aims to validate our product. Our main focus was the item page and some of it's interactions, but we also implemented all user interfaces as well as the authentication system (such as login, register and logout), some policies and middlewares.

### 1. Implemented Features

#### 1.1. Implemented User Stories

| User Story reference | Name        | Priority | Description                                                  |
| -------------------- | ----------- | -------- | ------------------------------------------------------------ |
| US01                 | Access Home | high     | As a *User*, I want to access the website's homepage, so that I can know its general-purpose |
| US02 | Access About Page | high | As a *User*, I want to access the 'About' page, so that I can see a complete and detailed description of the website |
| US03 | See Contacts      | high | As a *User*, I want to consult the website's contacts, so that I know how to contact the team if needed |
| US04 | Search items      | high | As a *User*, I want to search for an item's name, so that I can get more information about it |
| US06 | View items | high | As a *User*, I want to view all the items, so that I can see all the products available |
| US11 | Sign-up               | high | As a *Visitor*, I want to be able to create a new account so that I'm able to authenticate myself |
| US12 | Sign-in               | high | As a *Visitor*, I want to be able to authenticate myself so that I'm able to buy products |
| US13 | Administrator Sign-in | high | As a *Visitor*, I want to be able to sign-in as an administrator if I'm permitted to do so |
| US21 | View purchase history | high | As an *Authenticated*, I want to see my purchasing history, so that I can see the products I have bought |
| US22 | Rate item | high | As an *Authenticated*, I would like to attribute a score to an item, so that other users can know my basic opinion of the item |
| US23 | Comment item | high | As an *Authenticated*, I would like to attach a comment to an item, so that other users can know my more complete opinion of the item |
| US24 | Remove comment | high | As an *Authenticated*, I want to be able to be able to delete my own comments so that I'm able to remove comments that I don't find useful |
| US25 | Add to cart | high | As an *Authenticated*, I want to add an item to my cart, so that I am able to purchase it |
| US26 | Remove from cart | high | As an *Authenticated*, I want to remove an item from my cart, so that I can reconsider my purchase before I finalize it |
| US28 | Logout | high | As an *Authenticated*, I want to be able to log out from my account, so that I can exit my account |
| US211 | View Cart | high | As an *Authenticated*, I want to see my car, so that I can make sure i added the correct items to it |
| US212 | View product recommendations | medium | As an *Authenticated*, I would like to have a list of recommended items according to my history of products, so that I can easily find products that may be of my interest |
| US213 | View notifications | medium | As an *Authenticated*, I would like to have notifications when my comment is answered, a product in my wishlist is re-stocked or put on sale, so that I can be on time to make the best purchases |
| US214 | View wish list | medium | As an *Authenticated*, I want to see my wish list, so that I can decide if I want to purchase the items in it |
| US37 | Logout | high | As an *Administrator*, I want to be able to log out from my account, so that I can exit my account |
| US312 | View  users profile | medium | As an *Administrator*, I want to be able to view all users profile, so that I can get check their information |
| US38 | View all unbanned users | high | As an *Administrator*, I want to be able to see a list of all unbanned users, so that I can manage them with ease |
| US314 | View users buy history | low | As an *Administrator*, I want to be able to view customer's purchase history, so that I can get a better understanding of what users look for the most |

#### 1.2. Implemented Web Resources

Module M01: Authentication and profile

| Web Resource Reference             | URL                               |
| ---------------------------------- | --------------------------------- |
| R101: Login Form                   | /login                            |
| R102: Login Action                 | POST /login                       |
| R103: Logout Action                | POST /logout                      |
| R104: Register Form                | /register                         |
| R105: Register Action              | POST /register                    |
| R110: View user profile            | /userProfile/{id}                 |
| R114: View user's purchase history | /userProfile/{id}/purchaseHistory |



Module M02: Products and categories

| Web Resource Reference    | URL        |
| ------------------------- | ---------- |
| R201: Search products API | /api/items |
| R202: View product page   | /item/{id} |



Module M03: Management

| Web Resource Reference              | URL                     |
| ----------------------------------- | ----------------------- |
| R301: View administration page      | /management             |
| R302: View user administration page | /management/manageUsers |
| R303: Add product Form              | /management/addItem     |



Module M04: Static Pages

| Web Resource Reference   | URL       |
| ------------------------ | --------- |
| R401: View About page    | /about    |
| R402: View FAQ page      | /faq      |
| R403: View Contacts page | /contacts |



Module M05: Products and reviews

| Web Resource Reference      | URL                                 |
| --------------------------- | ----------------------------------- |
| R501: Submit product review | POST item/{id}/review               |
| R502: Edit product review   | PUT review/{reviewId}               |
| R503: Delete product review | DELETE /item/{id}/review/{reviewId} |



Module M06: Wishlist and cart

| Web Resource Reference      | URL                            |
| --------------------------- | ------------------------------ |
| R601: View user's wishlist  | /userProfile/{id1}/wishlist    |
| R604: View user's cart      | /userProfile/{id}/cart         |
| R605: Add item to cart      | POST /api/cart/{id}/{quantity} |
| R606: Remove item from cart | DELETE /api/cart/{id}          |
| R608: Checkout Form         | /checkout                      |



### 2. Prototype

Prototype: http://lbaw2111.lbaw-prod.fe.up.pt/

Credentials:

​		Admin: 

​					Email: lbawAdmin@gmail.com

​					Password: lbawadmin

​		User: 

​					Email: normallogin@gmail.com

​					Password: normaluser



Source code: https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/


---


## Revision history

Changes made to the first submission:
1. Item 1
1. ..

***
GROUP2111, 26/04/2021

* Diogo Guimarães do Rosário, [up201806582@fe.up.pt](mailto:up201806582@fe.up.pt) (Editor)
* Henrique Melo Ribeiro, [up201806529@fe.up.pt](mailto:up201806529@fe.up.pt)
* Davide António Ferreira Castro, [up201806512@fe.up.pt](mailto:up201806512@fe.up.pt)
* João Alexandre Lobo Cardoso, [up201806531@fe.up.pt](mailto:up201806531@fe.up.pt)