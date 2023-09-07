# Term Project: Disease Database
In our term project of the course "Introduction to Database Management System", we shall design a database and implement a practical application of the subject. We will provide a description of the database tables below. Firstly, we shall create a relational database, and then we will write and execute queries that will extract and update some data from the database. 

## Physical Database
Firstly, we construct a physical database according to the given schema. To create the physical database, it is required to use a database management system. We will use the free DBMS tool: PostgreSQL.
The schema is given as follows,
* **DiseaseType**(`id`: integer, `description`: varchar(140))
* **Country**(`cname`: varchar(50), `population`: bigint)
* **Disease**(`disease_code`: varchar(50), `pathogen`: varchar(20), `description`: varchar(140), `id`: integer)
  * References: **DiseaseType**(`id`)
* **Discover**(`cname`: varchar(50), `disease_code`: varchar(50), `first_enc_date`: date)
  * References: **Disease**(`disease code`), **Country**(`cname`)
* **Users**(`email`: varchar(60), `name`: varchar(30), `surname`: varchar(40), `salary`: integer, `phone`: varchar(20), `cname`: varchar(50))
  * References: **Country**(`cname`)
* **PublicServant**(`email`: varchar(60), `department`: varchar(50))
  * References: **Users**(`email`)
* **Doctor**(`email`: varchar(60), `degree`: varchar(20))
  * References: **Users**(`email`)
* Specialize(`id`: integer, `email`: varchar(60))
  * References: **DiseaseType**(`id`), **Doctor**(`email`)
* Record(`email`: varchar(60), `cname`: varchar(50), `disease_code`: varchar(50), `total_deaths`: integer, `total_patients`: integer)
  * References: **Disease**(`disease code`), **Country**(`cname`), **PublicServant**(`email`)

After constructing the database model, we will create tables and insert some example data instances on the tables (at least 10 instances for each table). Here, we will provide the instances in a specific way that the result set of the example queries from the next part of the project should be non-empty.

## Connect the Database
After constructing the physical database, we are going to connect to our PostgreSQL database and execute some queries and updates from the user interface. We are asked to use Python3 and SQLAlchemy library to connect and interact with the database. Also, we need to design a user interface. For this purpose, we use [tkinter](https://docs.python.org/3/library/tkinter.html) library. The user interface that we are going to construct will be able to perform basic CRUD functionalities.

## Example Queries
Finally, we are going to add some pre-defined queries to perform on the database by using the user interface. The queries are given as follows,
1. List the `disease_code` and the `description` of diseases that are caused by “bacteria” (`pathogen`) and were discovered before 1990.
2. List the name, `surname` and `degree` of doctors who did not specialize in “infectious diseases”.
3. List the name, `surname` and `degree` of doctors who specialized in more than 2 disease types.
4. For each country list the `cname` and `average_salary` of doctors who specialized in “virology”.
5. List the `departments` of public servants who report “COVID-19” cases in more than one country and the number of such public servants who work in these departments. (i.e. “Dept1 3” means that in the “Dept1” department there are 3 such employees.)
6. Double the `salary` of public servants who have recorded COVID-19 patients more than 3 times.
7. Delete the users whose `surname` contains the substring “alp” (e.g. Alp, Alper, Alperen, Eralp)
8. Create an `index` namely “idx pathogen” on the “pathogen” field.
9. List the `email`, `name`, and `department` of public servants who have created records where the number of patients is between 100000 and 999999.
10. List the top 5 `counties` with the highest number of total `patients` recorded.
11. Group the `diseases` by `disease-type` and the total number of `patients` treated.
