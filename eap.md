# EAP: Architecture Specification and Prototype

Our website aims to help customers get what then need when they need it during these troubling times with an enjoyable browsing experience.

## A7: High-level architecture. Privileges. Web resources specification

This artifact intends to document the catalogue of resources and the properties of each resource available to all users. The artifact contains operations over data such as: create, delete, update and read.

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

Link to the Swagger generated documentation (https://app.swaggerhub.com/apis/LBAW-FEUP-11/lbaw-fneuc_web_api/1.0).
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
- url: http://lbaw-prod.fe.up.pt
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
                  
  /users/{id}/edit:
  
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
                  value: '/users/{id}'
                302Failure:
                  description: 'Failed edit. Redirect to user profile.'
                  value: '/users/{id}'                
                  
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
                  description: 'Successful credential recovery. Redirect to signin.'
                  value: '/signin'
                  
  /users/{id}:
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
          
  /users/{id}/billing_address:
    post:
      operationId: R111
      summary: 'R111: Update billing address'
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
                  
  /users/{id}/shipping_address:
    post:
      operationId: R112
      summary: 'R112: Update shipping address'
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
                
  /users/{id}/purchase_history:
    get:
      operationId: R113
      summary: 'R113: View user''s purchase history'
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
                    details: [["18+", "Age restriction"], ["01-10-2020", "Release Date"], ["CDPR", "Developer"]]
  /products/{id}:
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
        
  /products/{id}/review:
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

    patch:
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
                review_id:
                  type: integer
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
                  id:
                    type: integer
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
    
  
  /admin:
    get:
      operationId: R301
      summary: 'R301: View administration page'
      description: "Show administration area. Acess: ADM"

      tags:
        - 'M03: Management'

      responses:
        '200':
          description: 'Ok. Show [UI06](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui06-admin-main-page)'
  
  /admin/usermanagement:
    get:
      operationId: R302
      summary: 'R302: View user administration page'
      description: "Show user administration area. Acess: ADM"

      tags:
        - 'M03: Management'

      responses:
        '200':
          description: 'Ok. Show [UI14](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui14-user-administration)'
  
  /admin/addproduct:
    get:
      operationId: R303
      summary: 'R303: Add product Form'
      description: 'Provide add product form. Access: ADM'
      tags:
        - 'M03: Management'
      responses:
        '200':
          description: 'Ok. Show [UI05](https://git.fe.up.pt/lbaw/lbaw2021/lbaw2111/-/wikis/er#ui05-add-a-new-item)'
    put:
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
          
  /admin/usermanagement/ban/{id}:  
    parameters:
        - in: path
          name: id
          schema:
            type: integer
          required: true

    post:
      operationId: R305
      summary: 'R305: Ban user Action'
      description: 'Processes the ban user operation. Access: ADM'
      tags:
        - 'M03: Management'

      requestBody:
        required: true
        content:
          application/x-www-form-urlencoded:
            schema:
              type: object
              properties:
                ban_reason:
                  type: string

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
                  value: '/admin/usermanagement'
                302Failure:
                  description: 'Failed ban. Redirect to user management.'
                  value: '/admin/usermanagement' 
  
  /admin/usermanagement/promote/{id}:  
    
    patch:
      operationId: R306
      summary: 'R306: Promote user Action'
      description: 'Processes the promote user operation. Access: ADM'
      tags:
        - 'M03: Management'
        
      parameters:
      - in: path
        name: id
        schema:
          type: integer
        required: true

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
                  value: '/admin/usermanagement'
                302Failure:
                  description: 'Failed promotion. Redirect to user management.'
                  value: '/admin/usermanagement'  
                  
  /products/{id}/deletecomment/{id2}:
    delete:
      operationId: R307
      summary: 'R307: Delete comment Action'
      description: 'Processes the delete comment operation. Access: ADM'

      tags:
        - 'M03: Management'

      parameters:
        - in: path
          name: id
          description: Product identifier
          schema:
            type: integer
          required: true
        - in: path
          name: id2
          description: Comment identifier
          schema:
            type: integer
          required: true

      responses:
        '302':
          description: 'Redirect after deleting the comment.'
          headers:
            Location:
              schema:
                type: string
              examples:
                302Success:
                  description: 'Successful comment deletion. Redirect to item page.'
                  value: '/product/{id}'
                302Failure:
                  description: 'Failed comment deletion. Redirect to item page.'
                  value: '/product/{id}'  
                  
  /admin/discount_product:
    post:
      operationId: R308
      summary: 'R308: Add product discount Action'
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
          
  /admin/discount_category:
    post:
      operationId: R309
      summary: 'R309: Add category discount Action'
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
          
  /admin/discounts:
    post:
      operationId: R310
      summary: 'R310: Remove product discounts Action'
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
          
  /admin/purchases/{id}/purchase_status:
    patch:
      operationId: R311
      summary: 'R311: Update purchase status Action'
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
                  
  /products/{id}/stock:
    post:
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
           
      responses:
        '200':
            description: 'Sucessfully added item to wishlist.'
        '401':
          description: 'Unauthorized user cannot edit product stock'
                  
                  
  /api/wishlist/{id}:
    parameters:
      - in: path
        name: id
        description: Product identifier
        schema:
          type: integer
        required: true
        
    post:
      operationId: R601
      summary: 'R601: Add item to wishlist API'
      description: 'AJAX request. Adds an item to the users wishlist. Access: OWN'
      tags:
        -  'M06: Wishlist and cart'
        
      responses:
        '200':
          description: 'Sucessfully added item to wishlist.'
        '401':
          description: 'The password does not correspond to the email.'
  
    delete:
      operationId: R602
      summary: 'R602: Remove item from wishlist'
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
   
  /users/{id}/cart:
    get:
      operationId: R603
      summary: 'R603: View user''s cart'
      description: 'Redirect to user''s cart page. Access: OWN'
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
          
  /api/cart/{id}:
    parameters:
      - in: path
        name: id
        description: product 
        schema:
          type: integer
        required: true
        
    post:
      operationId: R604
      summary: 'R604: Add item to cart'
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
                product_id:         
                  type: integer
                quantity:    
                  type: integer
              required:
              - product_id
              - quantity
                
      responses:
        '200':
          description: 'Sucessfully added item to cart.'
        '406':
          description: 'Item not available.'
  
    delete:
      operationId: R605
      summary: 'R605: Remove item from cart'
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
          
  /api/cart/{id}/{quantity}:
    parameters:
      - in: path
        name: id
        description: Product identifier 
        schema:
          type: integer
        required: true
      - in: path
        name: quantity
        description: Quantity 
        schema:
          type: integer
        required: true
        
    patch:
      operationId: R606
      summary: 'R606: Edit Product cart quantity'
      description: 'AJAX request. Updates the quantity of a product in the user''s cart. Access: OWN'
      tags:
        - 'M06: Wishlist and cart'


      responses:
        '200':
          description: 'Sucessfully updated item quantity.'
        '401':
          description: 'Unauthenticated user cannot update quantity in cart.'
        '406':
          description: 'Item not in the cart'
          
  /admin/announcement:
    post:
      operationId: R312
      summary: 'R312: Add announcement Action'
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
      operationId: R313
      summary: 'R313: Remove announcement Action'
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
GROUP2111, 26/04/2021

* Diogo Guimarães do Rosário, [up201806582@fe.up.pt](mailto:up201806582@fe.up.pt) (Editor)
* Henrique Melo Ribeiro, [up201806529@fe.up.pt](mailto:up201806529@fe.up.pt)
* Davide António Ferreira Castro, [up201806512@fe.up.pt](mailto:up201806512@fe.up.pt)
* João Alexandre Lobo Cardoso, [up201806531@fe.up.pt](mailto:up201806531@fe.up.pt)