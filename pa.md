# PA: Product and Presentation

Our website aims to help customers get what then need when they need it during these troubling times with an enjoyable browsing experience.

## A9: Product

> Brief presentation of the product developed.  

### 1. Installation

> Link to the release with the final version of the source code in the group's git repository.  
> Full Docker command to test the group's Docker Hub image using the DBM database.  

### 2. Usage

> URL to the product: http://lbaw21gg.lbaw-prod.fe.up.pt  

#### 2.1. Administration Credentials

> Administration URL: URL  

| Username | Password |
| -------- | -------- |
| admin    | password |

#### 2.2. User Credentials

| Type          | Username  | Password |
| ------------- | --------- | -------- |
| basic account | user 1    | password |
| news editor   | user 1    | password |

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
| US01  | Access Home  | Module 2 | Mandatory | **Henrique Ribeiro**, Davide Castro | 100% | 
| US02  | Access About Page | Module 4  | Important | **Henrique Ribeiro**, Davide Castro  | 100% | 
| US03  | See Contacts | Module 4 | Important | **Henrique Ribeiro**, Davide Castro  | 100% | 
| US04  | Search items | Module 2 | Mandatory | **Henrique Ribeiro**, Davide Castro  | 100% |
| US05  | Filter items | Module 2 | Mandatory | **João Cardoso**, Davide Castro  | 25% |
| US06  | View items | Module 2 | Mandatory | **Henrique Ribeiro**, Davide Castro  | 100% |
| US07  | Delete account | Module 1 | Mandatory | **Diogo Rosário**, Henrique Ribeiro | 0% |
| US11       | Sign-up                    | Module 1 | Mandatory | **Henrique Ribeiro** | 100% |
| US12       | Sign-in                    | Module 1 | Mandatory | **Henrique Ribeiro** | 100% |
| US13       | Administrator Sign-in      | Module 1 | Mandatory | **Henrique Ribeiro** | 100% |
| US14       | Sign-up using external API | Module 1 | Optional | **Diogo Rosário**, Henrique Ribeiro | 0% |
| US15       | Sign-in using external API | Module 1 | Optional | **Diogo Rosário**, Henrique Ribeiro | 0% |
| US21       | View purchase history  | Module 1 | Important | **Davide Castro**, Henrique Ribeiro | 100% |
| US22      | Rate item             | Module 2 | Important | **Davide Castro**, Henrique Ribeiro | 100% |
| US23      | Comment item         | Module 2 | Important | **Davide Castro**, Henrique Ribeiro | 100% |
| US24    | Remove comment      | Module 2 | Important | **Davide Castro**, Henrique Ribeiro | 100% |
| US25      | Add to cart          | Module 6 | Mandatory | **Davide Castro**, Henrique Ribeiro | 100% |
| US26      | Remove from cart          | Module 6 | Mandatory | **Davide Castro**, Henrique Ribeiro | 100% |
| US27      | Checkout cart          | Module 6 | Mandatory | **Davide Castro**, Diogo Rosário | 0% |
| US28 | Logout | Module 1 | Important | **Henrique Ribeiro** | 100% |
| US29      | Edit profile     | Module 1 | Important | **João Cardoso**, Davide Castro | 0% |
| US210      | Recharge account balance     | Module 1 | Mandatory | **Davide Castro**, Henrique Ribeiro | 0% |
| US211 | View Cart | Module 6 | Mandatory | **Henrique Ribeiro** | 100% |
| US212     | View product recommendations | Module 1 | Important | **Henrique Ribeiro** | 100% |
| US213     | View notifications | medium | As an *Authenticated*, I would like to have notifications when my comment is answered, a product in my wishlist is re-stocked or put on sale, so that I can be on time to make the best purchases |
| US214 | View wish list | medium | As an *Authenticated*, I want to see my wish list, so that I can decide if I want to purchase the items in it |
| US215     | Add to wish list        | medium   | As an *Authenticated*, I want to add items to my wish list, so that I can purchase them easily in the future                          |
| US216     | Remove from wish list      | medium   | As an *Authenticated*, I want to remove an item from my wish list, so that I can forget the item                                      |
| US31  | Create items  | high  | As an *Administrator*, I want to create item listings, so that I can sell new items |
| US32  | Remove items  | high  | As an *Administrator*, I want to remove item listings, so that I can prevent users from buying certain items |
| US33  | Edit items  | high  | As an *Administrator*, I want to edit item listings, so that I change the items I am selling |
| US34  | Create admin accounts  | high  | As an *Administrator*, I want to create administrator accounts, so that others can have administrator permissions  |
| US35  | Remove comments  | high  | As an *Administrator*, I want to remove comments, so that I can filter inappropriate language|
| US36  | View notifications of items without stock | high | As an *Administrator*, I want to have a notification alert me when an item is out of stock, so that I can re-stock them as soon as possible|
| US37  | Logout | high | As an *Administrator*, I want to be able to log out from my account, so that I can exit my account|
| US38 | View all unbanned users | high | As an *Administrator*, I want to be able to see a list of all unbanned users, so that I can manage them with ease |
| US39 | Put item on sale | medium | As an *Administrator*, I want to have the ability to put items on sale, so that I can get attract uses to buy products that are not selling as well|
| US310 | View statistics of sold items | medium | As an *Administrator*, I want to have easy access to statistics of items filtered by different categories of users, so that I can have a better overview of what items sell better|
| US311 | Ban user accounts | medium | As an *Administrator*, I want to be able to ban users, so that I'm able to remove problematic users|
| US312 | Unban user accounts | medium | As an *Administrator*, I want to be able to unban users, so that I'm able to forgive certain users or correct a mistake I have made |
| US313 | View  users profile | medium | As an *Administrator*, I want to be able to view all users profile, so that I can get check their information|
| US314 | View users buy history | low | As an *Administrator*, I want to be able to view customer's purchase history, so that I can get a better understanding of what users look for the most|


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