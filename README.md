# Expenses-Tracking-System

REST API for tracking expenses.

A RESTful API created using Spring Boot. We have used PostgreSQL as the relational database and JdbcTemplate to interact with that.
Apart from this, we have used JSON Web Token (JWT) to add authentication. Using JWT, we can protect certain endpoints and ensure that user must be logged-in to access those.

## Setup and Installation

1. **Clone the repo from GitHub**
   ```sh
   git clone https://github.com/vishesh-mahale/Expenses-Tracking-System-Java-SpringBoot.git
   cd Expenses-Tracking-System
   ```
2. **Spin-up PostgreSQL database instance**

   You can use either of the below 2 options:

   - one way is to download from [here](https://www.postgresql.org/download) and install locally on the machine
   - another option is by running a postgres docker container:
     ```sh
     docker container run --name postgresdb -e POSTGRES_PASSWORD=admin -d -p 5432:5432 postgres
     ```

3. **Create database objects**

   In the root application directory (expense-tracker-api), SQL script file (expensetracker_db.sql) is present for creating all database objects

   - if using docker (else skip this step), first copy this file to the running container using below command and then exec into the running container:
     ```
     docker container cp expensetracker_db.sql postgresdb:/
     docker container exec -it postgresdb bash
     ```
   - run the script using psql client:
     ```
     psql -U postgres --file expensetracker_db.sql
     ```

4. **(Optional) Update database configurations in application.properties**

   If your database is hosted at some cloud platform or if you have modified the SQL script file with some different username and password, update the src/main/resources/application.properties file accordingly:

   ```properties
   spring.datasource.url=jdbc:postgresql://localhost:5432/expensetrackerdb
   spring.datasource.username=expensetracker
   spring.datasource.password=password
   ```

5. **Run the spring boot application**
   ```sh
   ./mvnw spring-boot:run
   ```
   this runs at port 8080 and hence all enpoints can be accessed starting from http://localhost:8080

6. **Run the APIs using Postman**
     
    Please scroll to the last section to see how to use the APIs. 

## Goal

The project mainly aimed to put into practice knowledge of Java, SpringBoot, JWT, PostgreSQL, CRUD, REST APIs.

## Tech Stack

	1. Spring Boot
	2. REST APIs 
	3. JWT
	4. PostgreSQL
	5. VS Code 
	6. Chrome Browser
	7. Postman
	8. SQL Workbench
	9. Docker(Optional)


## Comments
The Expenses Tracking System can be reused in any Java SprinBoot  Project which needs JWT for Authentication and Authorization and require the CRUD functionality.



## Screenshots

**Creating a Database:**
![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/8af78ee1-8dd9-4f50-a77d-010323b0e6ff)

**Accessing the Database using SQL Workbench:**
![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/c3c8d442-fec2-4575-b4b8-e09e6917959a)

![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/2c68bebc-f245-4084-aa9f-de8087db0c75)

**Tables:**

![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/94062cc9-1d3f-4625-a725-a5be13e7eac0)



**et_users:**

![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/5cb7f464-973c-4d16-be67-ddffbd83d17e)


**et_categories:**

![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/81da423d-5ba6-4db6-b2ca-41ba09e78530)


**et_transactions:**

![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/5a2f18a9-c3aa-47d4-b49b-c8af19c4c404)


**et_categories_seq:**

![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/907cfb2f-1843-47ac-ad28-67f086d563ab)


**et_transactions_seq:**

![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/46342da5-0a0b-446e-b407-09d447928c4c)

**et_users_seq:**

![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/77795b0f-74a2-4d19-8fa9-da03cc5c567f)


**CODE STRUCTURE:**

![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/10675dd4-4717-40e8-8cdb-fda297c843d6)
![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/00ae377c-91f5-482a-8c21-0334c46477a9)

**POSTMAN APIs:**

![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/76812828-04f0-475f-b252-e72537a1f4e7)

![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/f2357b6f-f891-41f0-a6b9-b6046a92c47e)

![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/ca05b93d-11b8-441d-9abd-a8c1b46543c3)


## Postman Setup to use the APIs:

1. Goto the POSTMAN folder present inside the  Expenses-Tracking-System-Java-SpringBoot-main folder.
2. Open the Postman Software.
3. Inside postman goto Collections Tab and import the below file from Expenses-Tracking-System-Java-SpringBoot-main folder.
```
Expenses-Tracking-System.postman_collection 
```
4. Inside postman goto Environments Tab and import the below file from Expenses-Tracking-System-Java-SpringBoot-main folder.

```
Expenses Tracking System API Env  Vars.postman_environment  
```

To call this API, you will need to add the below environment variables.


**Environment Variables:**

`RootUrl` : http://localhost:8080  Project will run on port 8080 in you local system.  

`Token` : JWT Token will get generated after successful Registration or Login.

`CategoryId` : CategoryId will get generated after adding the Category.  

`TransactionId` : TransactionId will get generated after adding the Transaction to any particular Category.


## API Reference: 


#### **Login and Registration**

#### Register New User:

```http
  POST /api/users/register

  Payload
  {
    "firstName": "Jeevan",
    "lastName": "Daka",
    "email":  "Jeevandaka@gmail.com",
    "password": "Jeevan"
  }
```

#### Login:

```http
  POST /api/users/login

  Payload
  {
    "email":  "Jeevandaka@gmail.com",
    "password": "Jeevan"
  }
```

#### **CATEGORIES:**

NOTE: For all the APIs mentioned below you will need to pass the JWT Token as a part of the Authorization received after Successfully Login or Registration.


#### Add Category
```http
  POST /api/categories

  Payload
  {
    "title": "Shopping",
    "description": "Day to Day Shopping"
  }
```


#### GET Category By Category Id

```http
 GET /api/categories/{{CategoryId}}

```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `CategoryId` | `string` | **Required**. Your CategoryId |



#### GET All Category

```http
 GET /api/categories
```

#### UPDATE Category By Category Id
```http
 PUT /api/categories/{{CategoryId}}

  Payload
  {
    "title": "Shopping List",
    "description": "Day to Day Shopping List"
  }
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `CategoryId` | `string` | **Required**. Your CategoryId |


#### DELETE Category By Category Id
```http
 DELETE /api/categories/{{CategoryId}}
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `CategoryId` | `string` | **Required**. Your CategoryId |




#### **TRANSACTIONS:**

#### Add Transaction

```http
 POST /api/categories/{{CategoryId}}/transactions

  Payload
  {
    "amount": 100,
    "note": "Groceries",
    "transactionDate": 1577817000000
  }
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `CategoryId` | `string` | **Required**. Your CategoryId |


#### GET Transactions By Category and Transaction Id
```http
 GET /api/categories/{{CategoryId}}/transactions/{{TransactionId}}
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `CategoryId` | `string` | **Required**. Your CategoryId |
| `TransactionId` | `string` | **Required**. Your TransactionId |


#### GET All Transactions By Category Id
```http
 GET /api/categories/{{CategoryId}}/transactions
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `CategoryId` | `string` | **Required**. Your CategoryId |


#### UPDATE Transaction By Category and Transactions Id

```http
 PUT /api/categories/{{CategoryId}}/transactions/{{TransactionId}}

  Payload
  {
    "amount": 100,
    "note": "Groceries",
    "transactionDate": 1577817000000
  }
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `CategoryId` | `string` | **Required**. Your CategoryId |
| `TransactionId` | `string` | **Required**. Your TransactionId |


#### DELETE Transaction By Category and Transactions Id

```http
 DELETE /api/categories/{{CategoryId}}/transactions/{{TransactionId}}

```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `CategoryId` | `string` | **Required**. Your CategoryId |
| `TransactionId` | `string` | **Required**. Your TransactionId |


## SQL Queries

```SQL

USERS QUERIES:

SELECT * FROM et_users;
DELETE FROM et_users WHERE user_id=1;


CATEGORY QUERIES:

SELECT C.CATEGORY_ID, C.USER_ID, C.TITLE, C.DESCRIPTION, COALESCE(SUM(T.AMOUNT), 0) TOTAL_EXPENSE FROM ET_TRANSACTIONS T RIGHT OUTER JOIN ET_CATEGORIES C ON C.CATEGORY_ID = T.CATEGORY_ID WHERE C.USER_ID = 2 GROUP BY C.CATEGORY_ID;

SELECT C.CATEGORY_ID, C.USER_ID, C.TITLE, C.DESCRIPTION, COALESCE(SUM(T.AMOUNT), 0) TOTAL_EXPENSE FROM ET_TRANSACTIONS T RIGHT OUTER JOIN ET_CATEGORIES C ON C.CATEGORY_ID = T.CATEGORY_ID WHERE C.USER_ID = 2 AND C.CATEGORY_ID = 4 GROUP BY C.CATEGORY_ID;

/* Below CATEGORY_ID we are not passing*/
INSERT INTO ET_CATEGORIES (CATEGORY_ID, USER_ID, TITLE, DESCRIPTION) VALUES(NEXTVAL('ET_CATEGORIES_SEQ'), 2, 'title', 'desc');

UPDATE ET_CATEGORIES SET TITLE = 'title 1', DESCRIPTION = 'desc 2' WHERE USER_ID = 2 AND CATEGORY_ID = 4;

DELETE FROM ET_CATEGORIES WHERE USER_ID = 2 AND CATEGORY_ID = 4;

DELETE FROM ET_TRANSACTIONS WHERE CATEGORY_ID = 4;


TRANSACTIONS QUERIES:

SELECT * FROM et_transactions;

SELECT * FROM et_transactions WHERE USER_ID = 2 AND CATEGORY_ID = 3 AND TRANSACTION_ID = 1004;

UPDATE ET_TRANSACTIONS SET AMOUNT = 999, NOTE = 'new year 2222', TRANSACTION_DATE = 1577817000000 WHERE USER_ID = 2 AND CATEGORY_ID = 3 AND TRANSACTION_ID = 1004;

SELECT TRANSACTION_ID, CATEGORY_ID, USER_ID, AMOUNT, NOTE, TRANSACTION_DATE FROM ET_TRANSACTIONS WHERE USER_ID = 2 AND CATEGORY_ID = 3;

SELECT TRANSACTION_ID, CATEGORY_ID, USER_ID, AMOUNT, NOTE, TRANSACTION_DATE FROM ET_TRANSACTIONS WHERE USER_ID = 2 AND CATEGORY_ID = 3 AND TRANSACTION_ID = 1003;

/* Below TRANSACTION_ID we are not passing*/
INSERT INTO ET_TRANSACTIONS (TRANSACTION_ID, CATEGORY_ID, USER_ID, AMOUNT, NOTE, TRANSACTION_DATE) VALUES(NEXTVAL('ET_TRANSACTIONS_SEQ'), 6, 2, 4999, 'second' ,1577817000000 );

UPDATE ET_TRANSACTIONS SET AMOUNT = 1000, NOTE = 'new note', TRANSACTION_DATE = 1577817000000  WHERE USER_ID = 2 AND CATEGORY_ID = 6 AND TRANSACTION_ID = 1007;

DELETE FROM ET_TRANSACTIONS WHERE USER_ID = 2 AND CATEGORY_ID = 6 AND TRANSACTION_ID = 1007;

```
