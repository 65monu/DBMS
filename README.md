# DBMS
 
Create and use the following database schema to answer the given queries.
EMPLOYEE Schema
Field Type NULL KEY
DEFAULT
Eno Char(3) NO PRI NIL
Ename Varchar(50) NO NIL
Job_type Varchar(50) NO NIL
Manager Char(3) Yes FK NIL
Hire_date Date NO NIL
Dno Integer YES FK NIL
Commission Decimal(10,2) YES NIL
Salary Decimal(7,2) NO NIL
DEPARTMENT Schema
Field Type NULL KEY
DEFAULT
Dno Integer No PRI NULL
Dname Varchar(50) Yes NULL
Location Varchar(50) Yes New Delhi
                  Queries:
Create EMPLOYEE table:
CREATE TABLE EMPLOYEE (
Eno CHAR(3) NOT NULL PRIMARY KEY,
Ename VARCHAR(50) NOT NULL,
Job_type VARCHAR(50) NOT NULL,
Manager CHAR(3),
Hire_date DATE NOT NULL,
Dno INTEGER,
Commission DECIMAL(10,2),
Salary DECIMAL(7,2) NOT NULL,
FOREIGN KEY (Manager) REFERENCES EMPLOYEE(Eno),
FOREIGN KEY (Dno) REFERENCES DEPARTMENT(Dno)
);
Create DEPARTMENT table:
CREATE TABLE DEPARTMENT (
Dno INTEGER NOT NULL PRIMARY KEY,
Dname VARCHAR(50),
Location VARCHAR(50) DEFAULT 'New Delhi'
);
            
            1. Query to display Employee Name, Job, Hire Date, Employee Number; for each employee with the Employee Number appearing first.
        
  SELECT Eno AS "Employee Number", Ename AS "Employee Name", Job_type AS "Job", Hire_date AS "Hire Date" FROM EMPLOYEE ORDER BY Eno;
 
           2. Query to display unique Jobs from the Employee Table.
SELECT DISTINCT Job_type FROM EMPLOYEE;
 
           3. Query to display the Employee Name concatenated by a Job separated by a comma.
SELECT CONCAT(Ename, ', ', Job_type) AS "Employee and Job" FROM EMPLOYEE;
 

           4. Query to display all the data from the Employee Table. Separate each Column by a comma and name the said column as THE_OUTPUT.
SELECT CONCAT_WS(',', Eno, Ename, Job_type, SupervisonENO, Hire_date, Dno, Commission, Salary) AS "THE_OUTPUT" FROM EMPLOYEE;
 
            5. Query to display the Employee Name and Salary of all the employees earning more than $2850.
SELECT Ename, Salary FROM EMPLOYEE WHERE Salary > 2850;
 
            6. Query to display Employee Name and Department Number for the Employee No= 79.
SELECT Ename, Dno FROM EMPLOYEE WHERE Eno = '79';
Output: The table does not have an employee number as 79 so instead we use employee 019.
          
          7. Query to display Employee Name and Salary for all employees whose salary is not in the range of $1500 and $2850.
 SELECT Ename, Salary FROM EMPLOYEE WHERE Salary < 1500 OR Salary > 2850;
  
            8. Query to display Employee Name and Department No. of all the employees in Dept 10 and Dept 30 in the alphabetical order by name.
SELECT Ename, Dno FROM EMPLOYEE WHERE Dno IN (1,3) ORDER BY Ename ASC;
 
         9. Query to display Name and Hire Date of every Employee who was hired in 1981.
SELECT Ename, Hire_date FROM EMPLOYEE WHERE YEAR(Hire_date) = 2021;
   OUtput: Since the database don’t have the record for year 1981.
           
           10.Query to display Name and Job of all employees who have not assigned a supervisor. 
SELECT Ename, Job_type FROM EMPLOYEE WHERE SupervisonENO IS NULL;
Output:
           
           11. Query to display the Name, Salary and Commission for all the employees who earn commission.
SELECT Ename, Salary, Commission FROM EMPLOYEE WHERE Commission IS NOT NULL;
Output:
                 
           12. Sort the data in descending order of Salary and Commission.
SELECT * FROM EMPLOYEE WHERE Commission IS NOT NULL ORDER BY Salary DESC, Commission DESC;
Output:

         13. Query to display Name of all the employees where the third letter of their name is ‘A’.
SELECT Ename FROM EMPLOYEE WHERE SUBSTRING(Ename, 3, 1) = 'A';
Output:

       14. Query to display Name of all employees either have two ‘R’s or have two ‘A’s in their name and are either in Dept No = 30 or their Manger’s Employee No = 7788.
SELECT Ename FROM EMPLOYEE WHERE (Ename LIKE '%R%R%' OR Ename LIKE '%A%A%') AND (Dno = 3 OR SupervisonENO = '7788');
Output:
        
       15. Query to display Name, Salary and Commission for all employees whose Commission amount is 14 greater than their Salary increased by 5%.
SELECT Ename, Salary, Commission FROM EMPLOYEE WHERE Commission = Salary * 1.05 + 14;
Output:

      16. Query to display the Current Date along with the day name.
SELECT DATE_FORMAT(NOW(), '%W, %M %e, %Y') AS 'Current Date';
Output:

     17. Query to display Name, Hire Date and Salary Review Date which is the 1st Monday after six months of employment.
SELECT Ename AS Name, Hire_date AS "Hire Date", DATE_ADD(Hire_date, INTERVAL 6 MONTH) AS "Salary Review Date" FROM Employee WHERE WEEKDAY(DATE_ADD(Hire_date, INTERVAL 26 MONTH)) = 0;
Output: as the data is old, so i use 26 months instead of 6.

     18. Query to display Name and calculate the number of months between today and the date on which employee was hired of department ‘Purchase’.
SELECT E.Ename, DATEDIFF(NOW(), E.Hire_date)/30 AS Months_Worked FROM EMPLOYEE E INNER JOIN DEPARTMENT D ON E.Dno = D.Dno WHERE D.Dname = 'Sales';
Output:
19. Query to display the following for each employee earns < Salary> monthly but wants
< 3 * Current Salary >. Label the Column as Dream Salary.
SELECT Ename, Salary, (Salary * 3) AS Dream_Salary
FROM EMPLOYEE;
Output:

20. Query to display Name with the 1st letter capitalized and all other letter lower case
and length of their name of all the employees whose name starts with ‘J’, ’A’ and ‘M’.
SELECT CONCAT(UCASE(LEFT(Ename, 1)), LCASE(SUBSTRING(Ename, 2))) AS
Name,
LENGTH(Ename) AS Name_Length
FROM EMPLOYEE
WHERE Ename LIKE 'J%' OR Ename LIKE 'A%' OR Ename LIKE 'M%';
Output:
21. Query to display Name, Hire Date and Day of the week on which the employee
started.
SELECT Ename, Hire_date, DATE_FORMAT(Hire_date,'%W') AS Start_day_of_week
FROM EMPLOYEE
WHERE Hire_date IS NOT NULL;
Output:
22. Query to display Name, Department Name and Department No for all the
employees.
SELECT
e.Ename AS Name,
d.Dname AS Department_Name,
e.Dno AS Department_No
FROM
EMPLOYEE e
JOIN DEPARTMENT d ON e.Dno = d.Dno;
Output:
23. Query to display Unique Listing of all Jobs that are in Department # 30.
SELECT DISTINCT
e.Job_type AS Job
FROM
EMPLOYEE e
JOIN DEPARTMENT d ON e.Dno = d.Dno
WHERE
d.Dno = 3;
Output:
24. Query to display Name, Dept Name of all employees who have an ‘A’ in their name.
SELECT e.Ename AS Name, d.Dname AS Dept_Name
FROM
EMPLOYEE e
JOIN DEPARTMENT d ON e.Dno = d.Dno
WHERE
e.Ename LIKE '%A%';
Output:
25. Query to display Name, Job, Department No. And Department Name for all the
employees working at the Dallas location.
SELECT e.Ename as Name, e.Job_type as Job, e.Dno as Department_No, d.Dname as
Department_Name
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.Dno = d.Dno
WHERE d.Location = 'Kolkata';
Output:
26. Query to display Name and Employee no. Along with their Manger’s Name and the
Manager’s employee no; along with the Employees’ Name who do not have a Manager.
SELECT
e1.Ename AS "Employee Name",
e1.Eno AS "Employee Number",
COALESCE(e2.Ename, 'No Manager') AS "Manager Name",
COALESCE(e2.Eno, 0) AS "Manager Number"
FROM
EMPLOYEE e1
LEFT JOIN
EMPLOYEE e2 ON e1.SupervisonENO = e2.Eno
ORDER BY
"Employee Name";
Output:
27. Query to display Name, Dept No. And Salary of any employee whose department
No. and salary matches both the department no. And the salary of any employee who
earns a commission.
SELECT e1.Ename AS Name, e1.Dno AS Dept_No, e1.Salary, e1.Commission
FROM Employee e1
INNER JOIN Employee e2 ON e1.Dno = e2.Dno AND e1.Salary = e2.Salary
WHERE e2.Commission IS NOT NULL;
Output:
28. Query to display Name and Salaries represented by asterisks, where each asterisk
(*) signifies $100.
SELECT Ename, CONCAT(REPEAT('*', (Salary/100)), ' $', Salary) AS Salary_Asterisks
FROM EMPLOYEE;
Output:
29. Query to display the Highest, Lowest, Sum and Average Salaries of all the
employees.
SELECT MAX(salary) AS "Highest Salary",
MIN(salary) AS "Lowest Salary",
SUM(salary) AS "Total Salary",
AVG(salary) AS "Average Salary"
FROM EMPLOYEE;
Output:
30. Query to display the number of employees performing the same Job type functions.
SELECT Job_type, COUNT(*) AS NumberOfEmployees
FROM Employee
GROUP BY Job_type;
Output:
31. Query to display the no. of supervisors without listing their names
SELECT COUNT(DISTINCT SupervisonENO) as "No. of Supervisors"
FROM EMPLOYEE
WHERE SupervisonENO IS NOT NULL;
Output:
32. Query to display the Department Name, Location Name, No. of Employees and the
average salary for all employees in that department.
SELECT d.Dname, d.Location, COUNT(e.Ename) AS No_of_Employees,
AVG(e.Salary) AS Average_Salary
FROM DEPARTMENT d
INNER JOIN EMPLOYEE e ON d.Dno = e.Dno
GROUP BY d.Dname, d.Location;
Output:
33. Query to display Name and Hire Date for all employees in the same dept. as Blake
SELECT e2.Ename, e2.Hire_date
FROM EMPLOYEE e1, EMPLOYEE e2
WHERE e1.Ename = 'Alice Lee' AND e1.Dno = e2.Dno;
Output:
34. Query to display the Employee No. And Name for all employees who earn more
than the average salary
SELECT Eno, Ename
FROM EMPLOYEE
WHERE Salary > (SELECT AVG(Salary) FROM EMPLOYEE);
Output:
35. Query to display Employee Number and Name for all employees who work in a
department with any employee whose name contains a ‘T’.
SELECT e.Eno, e.Ename
FROM EMPLOYEE e
WHERE e.Dno IN (
SELECT DISTINCT e2.Dno
FROM EMPLOYEE e2
WHERE e2.Ename LIKE '%T%'
);
Output:
36. Query to display the names and salaries of all employees who report to King.
SELECT e.Ename, e.Salary
FROM EMPLOYEE e
JOIN EMPLOYEE m ON e.SupervisonENO = m.Eno
WHERE m.Ename = 'KING';
Output:
37. Query to display the department no, name and job for all employees in the Sales
department .
SELECT d.Dno, d.Dname, e.Job_type
FROM EMPLOYEE e
INNER JOIN DEPARTMENT d ON e.Dno = d.Dno
WHERE d.Dname = 'SALES';
Output:
38. Display names of employees along with their department name who have more than
20 years experience
SELECT E.Ename, D.Dname
FROM EMPLOYEE E
INNER JOIN DEPARTMENT D
ON E.Dno = D.Dno
WHERE DATEDIFF(CURDATE(), E.Hire_date)/365 >= 20;
Output:
39. Display total number of departments at each location
Output:
40. Find the department name in which at least 20 employees work in.
SELECT d.Dname
FROM DEPARTMENT d
JOIN EMPLOYEE e ON d.Dno = e.Dno
GROUP BY d.Dname
HAVING COUNT(*) >= 2;
Output:
41. Query to find the employee’ name who is not supervisor and name of supervisor
supervising more than 5 employees.
SELECT e1.Ename as Employee_Name
FROM EMPLOYEE e1
WHERE e1.SupervisonENO IS NULL
AND EXISTS (
SELECT COUNT(*)
FROM EMPLOYEE e2
WHERE e2.SupervisonENO= e1.Eno
GROUP BY e2.SupervisonENO
HAVING COUNT(*) > 5
)
42. Query to display the job type with maximum and minimum employees
(SELECT Job_type
FROM EMPLOYEE
GROUP BY Job_type
ORDER BY COUNT(*) DESC LIMIT 1)
UNION ALL (SELECT Job_type
FROM EMPLOYEE
GROUP BY Job_type
ORDER BY COUNT(*) ASC LIMIT 1);
Output:
