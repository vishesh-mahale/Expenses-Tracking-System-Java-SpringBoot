# Expenses-Tracking-System

REST API for tracking expenses.

A RESTful API created using Spring Boot. We have used PostgreSQL as the relational database and JdbcTemplate to interact with that.
Apart from this, we have used JSON Web Token (JWT) to add authentication. Using JWT, we can protect certain endpoints and ensure that user must be logged-in to access those.

## Setup and Installation

1. **Clone the repo from GitHub**
   ```sh
   git clone https://github.com/vishesh-mahale/Expenses-Tracking-System.git
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

![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/670e2cf9-874e-403f-b30c-d35d50b61b9f)

![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/e72c1c25-7dd0-499f-bb3b-2b2fd292d513)

![image](https://github.com/vishesh-mahale/Expenses-Tracking-System/assets/55619589/4c759777-c327-4183-925d-8a3178a3d1c3)


## Postman Setup to use the APIs:

1. Goto the POSTMAN folder present inside the  Expenses-Tracking-System folder.
2. Open the Postman Software.
3. Inside postman goto Collections Tab and import the below file from Expenses-Tracking-System folder.
```
Expenses-Tracking-System.postman_collection 
```
4. Inside postman goto Environments Tab and import the below file from Expenses-Tracking-System folder.

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
