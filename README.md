# Employee Database-SQL: A Mystery in Two Parts

**Submitted By:** Saloni Gupta\
_Date_: november, 22nd, 2020 

This repository discusses a research project on the employee database at Pewlett Hackard Corporation from the 1980s and 1990s. All that remains of the database of employees from that period is in six CSV files. <br/>

On this project, a table was created that holds employees data in the CSVs, import the CSVs into a SQL database, and the data exploration was conducted to answering the research questions, and discussed in the following parts: <br/>

1. Data Modeling <br/>
To model the employee data a basic data modeling technique called Entity-Relationship Diagrams (ERD) was used. By using this technique six employee database entities or tables are identified. These entities are employees, departments, salaries, titles, department managers, and department employees. The attribute or the data type of the entities also presented. At last, the ER diagram was drawn to visualize the relationships between entities/objects (primary key or foreign keys in a database). To read the detailed description of the employee database click the following link and download the PDF file. [Employees-Dept-Data-Modelling.pdf](./EmployeeSQL/Data_Modeling-ERD/Employees-Dept-Data-Modelling.pdf)
The ER diagram also looks as follows: </br>

![Equator image](./EmployeeSQL/Images/Employees-Dept-ERD.png)


2. Data Engineering
Using the ERD, a table schema for each of the six CSV files is created including the datatypes, primary keys, foreign keys, and other constraints.
The order of the table is based on the primary, and foreign arrangements. </br>

 Note to import each CSV file into the corresponding SQL table the order strictly should be followed to avoid errors. </br>

 Click the following link to see the actual schema file [Employees-Dept-Data-Modelling.sql](./EmployeeSQL/Data_Modeling-ERD/Employees-Dept-Data-Modelling-ERD_exportedfile.sql) 

3. Data Analysis
After completing the importing process, a Postgresql analysis was perfomed and you can find the full query in this file [Employee-Dept-Query.sql](./EmployeeSQL/Data_Analysis/Employee-Dept-Query.sql) </br>

The analysis query were performed, and cascaded. There were nine main “questions” to answer, the first eight being done through PostgreSQL. </br>

For the first query, find the employee number, last name, first name, gender, and salary of every employee. The information needed was available in two tables, employees and   salaries, selected the appropriate columns and then joined those tables with an inner join on emp_no, which both tables had. </br>
 
![Query1](./EmployeeSQL/Images/Query1.PNG) </br>

For the second query, list all employees who were hired in 1986. Selected the first_name, last_name, and hire_date columns from the employees table and then used the WHERE     clause to set the date of hire condition. </br>
 
![Query2](./EmployeeSQL/Images/Query2.PNG) </br>

The third query looked into managers, listing the department number and name, and the managers’ name, employee number, and employment dates. The relevant information was stored in four separate tables this time, which required three inner joins. As before, selected the relevant columns and then joined the dept_manager table with the employees table, and the employees table with the dept_emp table, both on emp_no. I joined the dept_emp table with the departments table on dept_no. </br>

![Query3](./EmployeeSQL/Images/Query3.PNG) </br>

For the fourth query, list the departments of every employee along with their full name and employee number. The information I needed was stored on two tables, employees and departments. However, the tables did not share any primary/foreign keys. Therefore, used a third table (dept_emp) to join the other two together. First joined employees to dept_emp on the shared emp_no, and then dept_emp to departments on the shared dept_no. Through these joins, displayed the department name of each employee along with their name and employee number. </br>
![Query4](./EmployeeSQL/Images/Query4.PNG) </br>

For the fifth query, list all employees whose first name is "Hercules" and last names begin with "B." To do this, set two conditions joined by the AND clause, and made use of the SQL wildcard character % to search for last names beginning with “B”. </br>
![Query5](./EmployeeSQL/Images/Query5.PNG) </br>

The sixth query was much like the fourth, except to list information only for employees in the Sales department. Instead of repeating the fourth query, I created a view of it, named emp_info, and queried that, setting the condition of the department name being “Sales”. </br>
![Query6](./EmployeeSQL/Images/Query6.PNG) </br>

The seventh query was like the sixth, used the same query as in the sixth, but for the condition to look into Development department as well, used a subquery to search for the department name being “Sales” or “Development”. </br>
![Query7](./EmployeeSQL/Images/Query7.PNG) </br>

For the eighth query, count how many employees shared the same last name. To do this, selected the last_name column from the employees table and then also used the COUNT() function on the same column. Further grouped the data by last names and ordered the data by the count of last names in descending order to see the last names that were most shared among employees. </br>
![Query8](./EmployeeSQL/Images/Query8.PNG) </br>

4. Data Testing and Validation (Python)
In order to test, and validate the dataset, a python code is created on jupyter notebook by using SQL Alchemy to import the database into Pandas. The code generated a visualization of the data, wich proved the reliablity of the database. In order to import the SQL database in to Pandas without importing the CSV, but just by sourcing from SQL database use the following code.Input your postgresql username and password in the config.py file, and make sure your pgAdmin host, port, and database adjusted correctly.To look the python code vsit the following jupyter viewer page.

# Dependencies
from sqlalchemy import create_engine </br>
from config import username, password </br>
import pandas as pd </br>
import matplotlib.pyplot as plt </br>
import numpy as n </br>

engine = create_engine(f'postgresql://{username}:{password}@localhost:5432/Employees_db') </br>
connection = engine.connect() </br>
Consult [SQLAlchemy documentation](https://docs.sqlalchemy.org/en/14/core/engines.html#postgresql) for more information. </br>

After connecting to the database and creating an engine, imported emp_no and salary from the salaries table and emp_no and title from the titles table. Performed an inner join on the two tables on the shared emp_no before grouping the data by title.Took the mean of the salaries per title and rounded by two decimal points. Finally, plot the data in a bar chart to find that there was not much variance in salary amounts between each employee title. </br>

- A histogram to visualize the most common salary ranges for employees. </br>

![Histogram](./EmployeeSQL/Images/employee_salary_distribution.png)

- A bar chart of average salary by title. </br>

![Bar_Chart](./EmployeeSQL/Images/average_salary_by_title.png)

- Epilogue(Searching someone ID by using ID number) </br>
In this part, provide an evidence for anyone who asked to "Search an Id" from the database, for example let search employee ID number '499942' and the search result looks as follows in pandas.

 Who is fool ? 😄
![April_Fools](./EmployeeSQL/Images/April_Fools.png)
 
