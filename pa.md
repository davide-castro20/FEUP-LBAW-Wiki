# PA: Product and Presentation

Our website aims to help customers get what then need when they need it during these troubling times with an enjoyable browsing experience.

## A9: Product

> Brief presentation of the product developed.  

### 1. Installation

> Link to the release with the final version of the source code in the group's git repository.  
> Full Docker command to test the group's Docker Hub image using the DBM database.  

### 2. Usage

URL to the product: http://lbaw2111.lbaw-prod.fe.up.pt  

#### 2.1. Administration Credentials

> Administration URL: URL 

 URL to the product's management page: http://lbaw2111.lbaw-prod.fe.up.pt/management 

| Email                 | Password   |
| --------------------- | ---------- |
| normallogin@gmail.com | normaluser |

#### 2.2. User Credentials

| Type          | Email               | Password  |
| ------------- | ------------------- | --------- |
| basic account | lbawAdmin@gmail.com | lbawAdmin |

### 3. Application Help

> Describe where help has been implemented, pointing to working examples.  

### 4. Input Validation

> Describe how input data was validated, and provide examples to scenarios using HTML validation and server-side validation.  

### 5. Check Accessibility and Usability

> Provide the results of accessibility and usability tests (as PDF files included in the submitted ZIP file on Moodle), using respectively the following checklists:  
> https://ux.sapo.pt/checklists/acessibilidade/  
> https://ux.sapo.pt/checklists/usabilidade/  

### 6. HTML & CSS Validation

> Provide the results (as PDF files included in the submitted ZIP file on Moodle) of the validation of the HTML and CSS code using the following tools:  
> HTML: https://validator.w3.org/nu/  
> CSS: https://jigsaw.w3.org/css-validator/  

### 7. Revisions to the Project

> Describe the revisions made to the project since the requirements specification stage.  

### 8. Implementation Details

#### 8.1. Libraries Used

> Include reference to all the libraries and frameworks used in the product.  
> Include library name and reference, description of the use, and link to the example where it's used in the product.  

#### 8.2 User Stories

> This subsection should include all high and medium priority user stories, sorted by order of implementation. Implementation should be sequential according to the order identified below. 

> If there are new user stories, also include them in this table. 
> The owner of the user story should have the name in **bold**.
> This table should be updated when a user story is completed and another one started. 

| Identifier  | Name  | Module | Priority  | Team member | State |
|---|---|---|---|---|---|
| US11       | Sign-up                    | M1: Authentication and Profile | Mandatory | **Henrique Ribeiro** | 100% |
| US12       | Sign-in                    | M1: Authentication and Profile | Mandatory | **Henrique Ribeiro** | 100% |
| US13       | Administrator Sign-in      | M1: Authentication and Profile | Mandatory | **Henrique Ribeiro** | 100% |
| US37  | Logout | M1: Authentication and Profile | Mandatory | **Henrique Ribeiro**, Davide Castro | 100% |
| US313 | View  users profile | M1: Authentication and Profile | Mandatory | **Henrique Ribeiro**, Davide Castro | 100% |
| US314 | View users buy history | M1: Authentication and Profile | Mandatory | **Henrique Ribeiro**, Davide Castro | 100% |
| US01  | Access Home  | M2: Products and Categories | Mandatory | **Henrique Ribeiro**, Davide Castro | 100% |
| US04  | Search items | M2: Products and Categories | Mandatory | **Henrique Ribeiro**, Davide Castro  | 100% |
| US06  | View items | M2: Products and Categories | Mandatory | **Henrique Ribeiro**, Davide Castro  | 100% |
| US38 | View all unbanned users | M3: Management | Mandatory | **Henrique Ribeiro**, Davide Castro | 100% |
| US35  | Remove comments  | M5: Products and Reviews | Mandatory | **Henrique Ribeiro**, Davide Castro | 100% |
| US25      | Add to cart          | M6: Wishlist and Cart | Mandatory | **Davide Castro**, Henrique Ribeiro | 100% |
| US26      | Remove from cart          | M6: Wishlist and Cart | Mandatory | **Davide Castro**, Henrique Ribeiro | 100% |
| US211 | View Cart | M6: Wishlist and Cart | Mandatory | **Henrique Ribeiro** | 100% |
| US21       | View purchase history  | M1: Authentication and Profile | Important | **Davide Castro**, Henrique Ribeiro | 100% |
| US28 | Logout | M1: Authentication and Profile | Important | **Henrique Ribeiro** | 100% |
| US212     | View product recommendations | M1: Authentication and Profile | Important | **Henrique Ribeiro** | 100% |
| US22      | Rate item             | M2: Products and Categories | Important | **Davide Castro**, Henrique Ribeiro | 100% |
| US23      | Comment item         | M2: Products and Categories | Important | **Davide Castro**, Henrique Ribeiro | 100% |
| US24    | Remove comment      | M2: Products and Categories | Important | **Davide Castro**, Henrique Ribeiro | 100% |
| US02  | Access About Page | M4: Static Pages | Important | **Henrique Ribeiro**, Davide Castro  | 100% |
| US03  | See Contacts | M4: Static Pages | Important | **Henrique Ribeiro**, Davide Castro  | 100% |
| US214 | View wish list | M6: Wishlist and Cart | Important | **Henrique Ribeiro** | 100% |
| US213     | View notifications | M1: Authentication and Profile | Important | **Henrique Ribeiro**, Diogo Rosário | 50% |
| US05  | Filter items | M2: Products and Categories | Mandatory | **João Cardoso**, Davide Castro  | 25% |
| US27      | Checkout cart          | M6: Wishlist and Cart | Mandatory | **Davide Castro**, Diogo Rosário | 0% |
| US07  | Delete account | M1: Authentication and Profile | Mandatory | **Diogo Rosário**, Henrique Ribeiro | 0% |
| US210      | Recharge account balance     | M1: Authentication and Profile | Mandatory | **Davide Castro**, Henrique Ribeiro | 0% |
| US31  | Create items  | M3: Management | Mandatory | **Diogo Rosário**, Henrique Ribeiro | 0% |
| US32  | Remove items  | M3: Management | Mandatory | **Diogo Rosário**, Henrique Ribeiro | 0% |
| US33  | Edit items  | M3: Management | Mandatory | **Diogo Rosário**, Henrique Ribeiro | 0% |
| US34  | Create admin accounts  | M3: Management | Mandatory | **João Cardoso**, Davide Castro | 0% |
| US311 | Ban user accounts | M3: Management | Mandatory | **Davide Castro**, Diogo Rosário | 0% |
| US312 | Unban user accounts | M3: Management | Mandatory | **Diogo Rosário**, Davide Castro | 0% |
| US39 | Put item on sale | M5: Products and Reviews | Mandatory | **Diogo Rosário**, Davide Castro | 0% |
| US29      | Edit profile     | M1: Authentication and Profile | Important | **João Cardoso**, Davide Castro | 0% |
| US36  | View notifications of items without stock | M3: Management | Important | **João Cardoso**, Davide Castro | 0% |
| US215     | Add to wish list        | M6: Wishlist and Cart | Important | **Davide Castro** | 0% |
| US216     | Remove from wish list      | M6: Wishlist and Cart | Important | **Davide Castro** | 0% |
| US15       | Sign-in using external API | M1: Authentication and Profile | Optional | **Diogo Rosário**, Henrique Ribeiro | 0% |
| US14       | Sign-up using external API | M1: Authentication and Profile | Optional | **Diogo Rosário**, Henrique Ribeiro | 0% |
| US310 | View statistics of sold items | M1: Authentication and Profile | Optional | **Henrique Ribeiro**, Davide Castro | 0% |


---


## A10: Presentation

> This artefact (A10 - Product Presentation) must be submitted as a PDF on Moodle.

### 1. Product presentation

> Brief presentation of the product and its main features (2 paragraphs max).  

> URL to the product: http://lbaw21gg.lbaw-prod.fe.up.pt  

### 2. Video presentation

> Screenshot of the video plus the link to the lbaw20gg.mp4 file  

> - Upload the lbaw20gg.mp4 file to the video uploads' [Google folder](https://drive.google.com/open?id=1C8ZAcqh6HRPsQEVpTRDeNNPwzKWXLPh4 "Videos folder")  
> - The video must not exceed 2 minutes.  

### 4. Overall Group Self-Evaluation

> Group members that have quit should not be included in the list below.
>
> Keep the text below in your final delivery, it works as a statement from all group members.

All group members have worked in all the components.

The individual contribution of each member to the LBAW project, and considering all artefacts, is expressed in the following list:

* Group member 1 name, _contribution level_ [A to F]
* Group member 2 name, _contribution level_ [A to F]
* ...


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