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

URL to the product's management page: http://lbaw2111.lbaw-prod.fe.up.pt/management 

| Email               | Password  |
| ------------------- | --------- |
| lbawAdmin@gmail.com | lbawadmin |

#### 2.2. User Credentials

| Type                            | Email                                 | Password   |
| ------------------------------- | ------------------------------------- | ---------- |
| basic account                   | normallogin@gmail.com                 | normaluser |
| PayPal sandbox personal account | sb-i474td6133157@personal.example.com | e(c?W>y4   |
| PayPal sandbox business account | sb-6os6a6029158@business.example.com  | \|G)x+Z<1  |

### 3. Application Help

> Describe where help has been implemented, pointing to working examples.  

### 4. Input Validation

> Describe how input data was validated, and provide examples to scenarios using HTML validation and server-side validation.  

### 5. Check Accessibility and Usability

Checklists results for our product:

- [Accessibility checklist](./checklists/accessibility.pdf)
- [Usability checklist](./checklists/usability.pdf)

### 6. HTML & CSS Validation

Validation results for HTML (https://validator.w3.org/nu/) and CSS (https://jigsaw.w3.org/css-validator/):

- [HTML validation results](./validations/html)
- [CSS validation results](./validations/css)

### 7. Revisions to the Project

**ER - Requirements specification**:

- Added user story US212
- Added user story US38
- Updated Authenticated user stories numeration
- Administrators also have access to normal Authenticated users, such as make purchases and add items to their wishlist

Throughout the project we made minor changes to the project's specification and, as such, we updated ER to reflect those changes. 

**EBD - Database Specification Component**:

- Added ON DELETE SET NULL to users atributes
- Added an enum to show the purchase state
- Fixed a duplicate trigger issue
- Added notify_admin trigger and corresponding function; Changed "Trigger" to "Rule" in rule01
- Added update_stock_remove_from_cart trigger and function; Changed transaction 1 procedure's name from 'remove_stock' to 'add_to_cart'
- Added remember_token to user table and reset_password table for "forgot password" feature
- Removed update_stock_remove_from_cart as it is not needed anymore
- Updated Transaction 2 and purchase table to support shipping option, and added shipping options table.
- Fixed add_to_cart procedure for cases when item was already in cart.



### 8. Implementation Details

#### 8.1. Libraries Used

- **Laravel-PayPal** (https://github.com/srmklive/laravel-paypal) - Laravel plugin used to handle money transactions through use of the PayPal Orders API. This is used for the PayPal payment option on checkout and to recharge the user's account balance (User Page, Add balance - http://lbaw2111.lbaw-prod.fe.up.pt/userProfile). User is redirected to PayPal Sandbox website to pay.

#### 8.2 User Stories

| Identifier  | Name  | Module | Priority  | Team member | State |
|---|---|---|---|---|---|
| US11       | Sign-up                    | M1: Authentication and Profile | Mandatory | **Henrique Ribeiro** | 100% |
| US12       | Sign-in                    | M1: Authentication and Profile | Mandatory | **Henrique Ribeiro** | 100% |
| US13       | Administrator Sign-in      | M1: Authentication and Profile | Mandatory | **Henrique Ribeiro** | 100% |
| US37  | Logout | M1: Authentication and Profile | Mandatory | **Henrique Ribeiro**, Davide Castro | 100% |
| US313 | View  users profile | M1: Authentication and Profile | Mandatory | **Henrique Ribeiro**, Davide Castro | 100% |
| US314 | View users buy history | M1: Authentication and Profile | Mandatory | **Henrique Ribeiro**, Davide Castro | 100% |
| US210      | Recharge account balance     | M1: Authentication and Profile | Mandatory | **Davide Castro**, Henrique Ribeiro | 100% |
| US07  | Delete account | M1: Authentication and Profile | Mandatory | **Diogo Rosário**, Henrique Ribeiro | 100% |
| US01  | Access Home  | M2: Products and Categories | Mandatory | **Henrique Ribeiro**, Davide Castro | 100% |
| US04  | Search items | M2: Products and Categories | Mandatory | **Henrique Ribeiro**, Davide Castro  | 100% |
| US06  | View items | M2: Products and Categories | Mandatory | **Henrique Ribeiro**, Davide Castro  | 100% |
| US05  | Filter items | M2: Products and Categories | Mandatory | **João Cardoso**, Davide Castro  | 100% |
| US31  | Create items  | M3: Management | Mandatory | **Diogo Rosário**, Henrique Ribeiro | 100% |
| US32  | Remove items  | M3: Management | Mandatory | **Diogo Rosário**, Henrique Ribeiro | 100% |
| US33  | Edit items  | M3: Management | Mandatory | **Diogo Rosário**, Henrique Ribeiro | 100% |
| US34  | Create admin accounts  | M3: Management | Mandatory | **João Cardoso**, Davide Castro | 100% |
| US38 | View all unbanned users | M3: Management | Mandatory | **Henrique Ribeiro**, Davide Castro | 100% |
| US311 | Ban user accounts | M3: Management | Mandatory | **Davide Castro**, Diogo Rosário | 100% |
| US312 | Unban user accounts | M3: Management | Mandatory | **Diogo Rosário**, Davide Castro | 100% |
| US35  | Remove comments  | M5: Products and Reviews | Mandatory | **Henrique Ribeiro**, Davide Castro | 100% |
| US39 | Put item on sale | M5: Products and Reviews | Mandatory | **Diogo Rosário**, Davide Castro | 100% |
| US25      | Add to cart          | M6: Wishlist and Cart | Mandatory | **Davide Castro**, Henrique Ribeiro | 100% |
| US26      | Remove from cart          | M6: Wishlist and Cart | Mandatory | **Davide Castro**, Henrique Ribeiro | 100% |
| US27      | Checkout cart          | M6: Wishlist and Cart | Mandatory | **Davide Castro** | 100% |
| US211 | View Cart | M6: Wishlist and Cart | Mandatory | **Henrique Ribeiro** | 100% |
| US28 | Logout | M1: Authentication and Profile | Important | **Henrique Ribeiro** | 100% |
| US29      | Edit profile     | M1: Authentication and Profile | Important | **João Cardoso**, Davide Castro | 100% |
| US212     | View product recommendations | M1: Authentication and Profile | Important | **Henrique Ribeiro** | 100% |
| US213     | View notifications | M1: Authentication and Profile | Important | **Henrique Ribeiro**, Diogo Rosário | 100% |
| US21       | View purchase history  | M1: Authentication and Profile | Important | **Davide Castro**, Henrique Ribeiro | 100% |
| US22      | Rate item             | M2: Products and Categories | Important | **Davide Castro**, Henrique Ribeiro | 100% |
| US23      | Comment item         | M2: Products and Categories | Important | **Davide Castro**, Henrique Ribeiro | 100% |
| US24    | Remove comment      | M2: Products and Categories | Important | **Davide Castro**, Henrique Ribeiro | 100% |
| US36  | View notifications of items without stock | M3: Management | Important | **João Cardoso**, Davide Castro | 100% |
| US02  | Access About Page | M4: Static Pages | Important | **Henrique Ribeiro**, Davide Castro  | 100% |
| US03  | See Contacts | M4: Static Pages | Important | **Henrique Ribeiro**, Davide Castro  | 100% |
| US214 | View wish list | M6: Wishlist and Cart | Important | **Henrique Ribeiro** | 100% |
| US215     | Add to wish list        | M6: Wishlist and Cart | Important | **Davide Castro** | 100% |
| US216     | Remove from wish list      | M6: Wishlist and Cart | Important | **Davide Castro** | 100% |


---


## A10: Presentation

### 1. Product presentation

> Brief presentation of the product and its main features (2 paragraphs max).  

> URL to the product: http://lbaw21gg.lbaw-prod.fe.up.pt  
>
> Slides used during the presentation should be added, as a PDF file, to the group's repository and linked to here.

### 2. Video presentation

> Screenshot of the video plus the link to the lbaw20gg.mp4 file  

> - Upload the lbaw20gg.mp4 file to the video uploads' [Google folder](https://drive.google.com/drive/folders/1HDNOZ4y834m7pXgJ0XjNa_ZC26e9-Xge?usp=sharing "Videos folder")  
> - The video must not exceed 2 minutes.  
> - Include a link to the video on the Google Drive folder.


---


## Revision history

No revisions.

***
GROUP2111, 08/06/2021

* Diogo Guimarães do Rosário, [up201806582@edu.fe.up.pt](mailto:up201806582@fe.up.pt) 
* Henrique Melo Ribeiro, [up201806529@edu.fe.up.pt](mailto:up201806529@fe.up.pt)
* Davide António Ferreira Castro, [up201806512@edu.fe.up.pt](mailto:up201806512@fe.up.pt) (Editor)
* João Alexandre Lobo Cardoso, [up201806531@edu.fe.up.pt](mailto:up201806531@fe.up.pt)

