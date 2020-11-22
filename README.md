# Employee Database-SQL: A Mystery in Two Parts

This repository discusses a research project on the employee database at Pewlett Hackard Corporation from the 1980s and 1990s. All that remains of the database of employees from that period is in six CSV files.

On this project, a table was created that holds employees data in the CSVs, import the CSVs into a SQL database, and the data exploration was conducted to answering the research questions, and discussed in the following parts:

1. Data Modeling
To model the employee data a basic data modeling technique called Entity-Relationship Diagrams (ERD) was used. By using this technique six employee database entities or tables are identified. These entities are employees, departments, salaries, titles, department managers, and department employees. The attribute or the data type of the entities also presented. At last, the ER diagram was drawn to visualize the relationships between entities/objects (primary key or foreign keys in a database). To read the detailed description of the employee database click the following link and download the PDF file. Employees_db_modeling.pdf

The ER diagram also looks as follows:


2. Data Engineering
Using the ERD, a table schema for each of the six CSV files is created including the datatypes, primary keys, foreign keys, and other constraints.
The order of the table is based on the primary, and foreign arrangements.

Note to import each CSV file into the corresponding SQL table the order strictly should be followed to avoid errors.

Click the following link to see the actual schema file Employees_db_schema.sql

3. Data Analysis
After completing the importing process a Postgresql analysiss was perfomed and you can find the full query in this file Employees_db_Query.sql

The analysis query were performed, and cascaded.
There were nine main “questions” I wanted to answer, the first eight being done through PostgreSQL.

For the first query, I have to find the employee number, last name, first name, gender, and salary of every employee. The information I needed was available in two tables, employees and salaries, so I selected the appropriate columns and then joined those tables with an inner join on emp_no, which both tables had.

For the second query, I have to list all employees who were hired in 1986. I selected the first_name, last_name, and hire_date columns from the employees table and then used the WHERE clause to set the date of hire condition.

The third query looked into managers, listing the department number and name, and the managers’ name, employee number, and employment dates. The relevant information was stored in four separate tables this time, which required three inner joins. As before, I selected the relevant columns and then joined the dept_manager table with the employees table, and the employees table with the dept_emp table, both on emp_no. I joined the dept_emp table with the departments table on dept_no.

For the fourth query, I wanted to list the departments of every employee along with their full name and employee number. The information I needed was stored on two tables, employees and departments. However, the tables did not share any primary/foreign keys. I therefore, had to use a third table (dept_emp) to join the other to together. I first joined employees to dept_emp on the shared emp_no, and then dept_emp to departments on the shared dept_no. Through these joins, I was able to display the department name of each employee along with their name and employee number.

For the fifth query, I wanted to list all employees whose first name is "Hercules" and last names begin with "B." To do this, I set two conditions joined by the AND clause, and made use of the SQL wildcard character % to search for last names beginning with “B”.

The sixth query was much like the fourth, except I wanted to list information only for employees in the Sales department. Instead of repeating the fourth query, I created a view of it, named emp_info, and queried that, setting the condition of the department name being “Sales”.

The seventh query was like the sixth, but looked into employees in the Development department as well. Here, I used the same query as in the sixth, but for the condition, I used a subquery to search for the department name being “Sales” or “Development”.

For the eighth query, I wanted to count how many employees shared the same last name. To do this, I selected the last_name column from the employees table and then also used the COUNT() function on the same column. I then grouped the data by last names and ordered the data by the count of last names in descending order to see the last names that were most shared among employees.

4. Data Testing and Validation (Python)
In order to test, and validate the dataset in this part a python code created on jupyter notebook. The code generate a visualization of the data, wich proves the reliablity of the database. In order to import the SQL database in to Pandas without importing the CSV, but just by sourcing from SQL database use the following code.Input your postgresql username and password in the config.py file, and malke sure your pgAdmin host, port, and database adjusted correctly.To look the python code vsit the following jupyter viewer page.

Finally, I wanted to determine the average salary for each position in the company and graph my findings. To accomplish this, I made use of SQL Alchemy to import the database into Pandas. After connecting to the database and creating an engine, I imported emp_no and salary from the salaries table and emp_no and title from the titles table. I then performed an inner join of the two tables on the shared emp_no before grouping the data by title. I then took the mean of the salaries per title and rounded by two decimal points. I then plot the data in a bar chart to find that there was not much variance in salary amounts between each employee title.



# Dependencies
from sqlalchemy import create_engine
from config import username, password
import pandas as pd
import matplotlib.pyplot as plt
import numpy as n
import seaborn as sns

engine = create_engine(f'postgresql://{username}:{password}@localhost:5432/Employees_db')
connection = engine.connect()
Consult SQLAlchemy documentation for more information.
- A histogram to visualize the most common salary ranges for employees.
- A bar chart of average salary by title

Epilogue(Searching somone ID by using ID number)
In this part I provide an evidence for any one who asked to "Search an Id" from the database, for example let seacrh employee ID number 499942 and It looks as follows the search result in pandas.

😄 Who is fool ? 😆
emp_no	emp_title_id	birth_date	first_name	last_name	sex	hire_date
0	499942	e0004	1963-01-10	April	Foolsday	F	1997-02-10
 
