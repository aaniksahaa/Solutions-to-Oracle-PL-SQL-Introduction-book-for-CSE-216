## Solution Manual for 'Oracle-PL-SQL-A Brief Introduction'

# Introduction

First of all, my earnest tribute to the author of the book, **Prof. Sukarna Barua Sir** for such an amazing documentation with abundant exercises and practice problems.

These are my solutions to the exercise problems provided in the aforementioned book. **Please do care to star the repository if you find it helpful** :D

# Contents   

## [Chapter 1](#chapter-1-1)
## [Chapter 2](#chapter-2-1)
## [Chapter 3](#chapter-3-1)
## [Chapter 4](#chapter-4-1)
## [Chapter 5](#chapter-5-1)
## [Chapter 6](#chapter-6-1)
## [Chapter 7](#chapter-7-1)

# Chapter 1   

> No Practice Problems in this chapter...Cheers!<br>   

# Chapter 2

# Practice 2.1

>a. Write an SQL query to retrieve all country names.<br>
>b. Write an SQL query to retrieve all job titles.<br>
>c. Write an SQL query to retrieve all MANAGER_IDs.<br>
>d. Write an SQL query to retrieve all city names. Remove duplicate outputs.<br>
>e. Write an SQL query to retrieve LOCATION_ID, ADDRESS from LOCATIONS table.<br> 
>   The ADDRESS should print each location in the following format: STREET_ADDRESS, CITY,<br>
>   STATE_PROVINCE, POSTAL_CODE<br>

a. Write an SQL query to retrieve all country names.<br>
```sql
SELECT DISTINCT COUNTRY_NAME
FROM COUNTRIES;
```
b. Write an SQL query to retrieve all job titles.<br> 
```sql
SELECT DISTINCT JOB_TITLE
FROM JOBS ;
```
c. Write an SQL query to retrieve all MANAGER_IDs.<br> 
```sql
SELECT DISTINCT MANAGER_ID
FROM EMPLOYEES
WHERE MANAGER_ID IS NOT NULL;
```
d. Write an SQL query to retrieve all city names. Remove duplicate outputs.<br>
```sql
SELECT DISTINCT CITY 
FROM LOCATIONS;
```
e. Write an SQL query to retrieve LOCATION_ID, ADDRESS from LOCATIONS table. 
The ADDRESS should print each location in the following format: STREET_ADDRESS, CITY,STATE_PROVINCE, POSTAL_CODE<br>
```sql
SELECT LOCATION_ID, STREET_ADDRESS || ', ' || CITY || ', ' || STATE_PROVINCE || ', ' || POSTAL_CODE AS ADDRESS
FROM LOCATIONS;
```

# Practice 2.2

> a. Select names of all employees who have joined before January 01, 1998.<br>
> b. Select all locations in the following countries: Canada, Germany, United Kingdom.<br>
> c. Select first names of all employees who do not get any commission.<br>
> d. Select first names of employees whose last name starts with an 'a'.<br>
> e. Select first names of employees whose last name starts with an 's' and ends with an 'n'.<br>
> f. Select all department names whose MANAGER_ID is 100.<br>
> g. Select all names of employees whose job type is 'AD_PRES' and whose salary is at least 23000.<br>
> h. Select names of all employees whose last name do not contain the character 's'.<br>
> i. Select names and COMMISSION_PCT of all employees whose commission is at most 0.30.<br>
> j. Select names of all employees who have joined after January 01, 1998.<br>
> k. Select names of all employees who have joined in the year 1998.<br>

a. Select names of all employees who have joined before January 01, 1998.<br>
```sql
SELECT (FIRST_NAME || ' ' || LAST_NAME) NAME, TO_CHAR(HIRE_DATE,'DD-MON-YYYY') HIRE_DATE
FROM EMPLOYEES
WHERE HIRE_DATE < '01-JAN-2007';
```
b. Select all locations in the following countries: Canada, Germany, United Kingdom.<br>
```sql
SELECT *
FROM LOCATIONS
WHERE COUNTRY_ID IN ('CA','DE','UK');
```
c. Select first names of all employees who do not get any commission.<br>
```sql
SELECT FIRST_NAME
FROM EMPLOYEES 
WHERE COMMISSION_PCT IS NULL;
```
d. Select first names of employees whose last name starts with an 'a'.<br>
```sql
SELECT FIRST_NAME 
FROM EMPLOYEES 
WHERE LOWER(LAST_NAME) LIKE 'a%';
```
e. Select first names of employees whose last name starts with an 's' and ends with an 'n'.<br>
```sql
SELECT FIRST_NAME
FROM EMPLOYEES 
WHERE LOWER(LAST_NAME) LIKE 's%n';
```
f. Select all department names whose MANAGER_ID is 100.<br>
```sql
SELECT DISTINCT DEPARTMENT_ID
FROM EMPLOYEES
WHERE MANAGER_ID = 100;
```
g. Select all names of employees whose job type is 'AD_PRES' and whose salary is at least 23000.<br>
```sql
SELECT (FIRST_NAME || ' ' || LAST_NAME) NAME
FROM EMPLOYEES 
WHERE JOB_ID = 'AD_PRES' AND SALARY >= 23000;
```
h. Select names of all employees whose last name do not contain the character 's'.<br>
```sql
SELECT (FIRST_NAME || ' ' || LAST_NAME) NAME
FROM EMPLOYEES 
WHERE LOWER(LAST_NAME) NOT LIKE '%s%';
```
i. Select names and COMMISSION_PCT of all employees whose commission is at most 0.30.<br>
```sql
SELECT FIRST_NAME, LAST_NAME, COMMISSION_PCT 
FROM EMPLOYEES 
WHERE COMMISSION_PCT <= 0.30;
```
j. Select names of all employees who have joined after January 01, 1998.<br>
```sql
SELECT FIRST_NAME, LAST_NAME 
FROM EMPLOYEES 
WHERE HIRE_DATE > '01-JAN-1998';
```
k. Select names of all employees who have joined in the year 1998.<br>
```sql
SELECT FIRST_NAME, LAST_NAME, HIRE_DATE 
FROM EMPLOYEES 
WHERE TO_CHAR(HIRE_DATE, 'YYYY') = '1998';
```

# Practice 2.3
> a. Select names, salary, and commissions of all employees of job type 'AD_PRES'. Sort the
>    result in ascending order of commission and then descending order of salary.<br>
> b. Retrieve all country names in lexicographical ascending order.<br>

a. Select names, salary, and commissions of all employees of job type 'AD_PRES'. Sort the
result in ascending order of commission and then descending order of salary.<br>
```sql
SELECT FIRST_NAME, LAST_NAME, SALARY, COMMISSION_PCT
FROM EMPLOYEES
WHERE JOB_ID = 'AD_PRES'
ORDER BY COMMISSION_PCT ASC, SALARY DESC;
```
b. Retrieve all country names in lexicographical ascending order.<br>
```sql
SELECT COUNTRY_NAME
FROM COUNTRIES
ORDER BY COUNTRY_NAME;
```

# Chapter 3

# Practice 3.1

> a. Print the first three characters and last three characters of all country names. Print in capital letters.<br>
> b. Print all employee full names (first name followed by a space then followed by last name).<br>
All names should be printed in width of 60 characters and left padded with '*' symbol for 
names less than 60 characters<br>
> c. Print all job titles that contain the text 'manager'<br>

a. Print the first three characters and last three characters of all country names. Print in capital letters.<br>
```sql
SELECT UPPER(SUBSTR(COUNTRY_NAME,1,3)) AS FIRST3, UPPER(SUBSTR(COUNTRY_NAME,LENGTH(COUNTRY_NAME)-2,3))
FROM COUNTRIES
```
b. Print all employee full names (first name followed by a space then followed by last name).
All names should be printed in width of 60 characters and left padded with '*' symbol for 
names less than 60 characters<br>
```sql
SELECT LPAD((FIRST_NAME || ' ' || LAST_NAME),60,'*') AS NAME
FROM EMPLOYEES
```
c. Print all job titles that contain the text 'manager'.
```sql
SELECT JOB_TITLE
FROM JOBS 
WHERE INSTR(UPPER(JOB_TITLE),'MANAGER') > 0
```

# Practice 3.2

> a. Print employee last name and number of days employed. Print the second information 
rounded up to 2 decimal places.<br>
> b. Print employee last name and number of years employed. Print the second information 
truncated up to 3 decimal place.<br>

a. Print employee last name and number of days employed. Print the second information 
rounded up to 2 decimal places.<br>
```sql
SELECT LAST_NAME, ROUND((TO_DATE(SYSDATE) - HIRE_DATE),2) AS "DAYS EMPLOYED"
FROM EMPLOYEES
```
b. Print employee last name and number of years employed. Print the second information 
truncated up to 3 decimal place.<br>
```sql
SELECT LAST_NAME, TRUNC((TO_DATE(SYSDATE) - HIRE_DATE)/365,3) AS "YEARS EMPLOYED"
FROM EMPLOYEES
```

# Practice 3.3

> a. For all employees, find the number of years employed. Print first names and number of years 
employed for each employee.<br>
> b. Suppose you need to find the number of days each employee worked during the first month 
of his joining. Write an SQL query to find this information for all employees.<br>

a. For all employees, find the number of years employed. Print first names and number of years 
employed for each employee.<br>
```sql
SELECT FIRST_NAME, ROUND((TO_DATE(SYSDATE)-HIRE_DATE)/365,2)
FROM EMPLOYEES
```
b. Suppose you need to find the number of days each employee worked during the first month 
of his joining. Write an SQL query to find this information for all employees.<br>
```sql
SELECT FIRST_NAME, LAST_NAME, HIRE_DATE, ADD_MONTHS(TRUNC(HIRE_DATE, 'MONTH'),1) - HIRE_DATE AS "FIRST MONTH WORKED"
FROM EMPLOYEES
```

# Practice 3.4

> a. Print the commission_pct values of all employees whose commission is at least 20%. Use 
NVL function.<br>
> b. Print the total salary of an employee for 5 years and 6 months period. Print all employee last 
names along with this salary information. Use NVL function assuming that salary may 
contain NULL values.<br>


a. Print the commission_pct values of all employees whose commission is at least 20%. Use 
NVL function.<br>
```sql
SELECT FIRST_NAME, LAST_NAME, COMMISSION_PCT
FROM EMPLOYEES
WHERE NVL(COMMISSION_PCT,0) >= 0.2
```
b. Print the total salary of an employee for 5 years and 6 months period. Print all employee last 
names along with this salary information. Use NVL function assuming that salary may 
contain NULL values.<br>
```sql
SELECT LAST_NAME, NVL(SALARY,0)*66*(1+NVL(COMMISSION_PCT,0)) SAL
FROM EMPLOYEES
```
# Practice 3.5

> a. Print hire dates of all employees in the following formats: <br>
(i) 13th February, 1998 (ii) 13 February, 1998.<br>

a.(i) 13th February, 1998
```sql
SELECT FIRST_NAME, LAST_NAME, TO_CHAR(HIRE_DATE,'ddth Month, YYYY')
FROM EMPLOYEES;
```

a.(ii) 13 February, 1998
```sql
SELECT FIRST_NAME, LAST_NAME, TO_CHAR(HIRE_DATE,'dd Month, YYYY')
FROM EMPLOYEES;
```
# Chapter 4

# Practice 4.1

> a. For all managers, find the number of employees he/she manages.
> Print the MANAGER_ID and total number of such employees.<br>
> b. For all departments, find the number of employees who get more than 30k salary. Print the 
DEPARTMENT_ID and total number of such employees.<br>
> c. Find the minimum, maximum, and average salary of all departments except 
DEPARTMENT_ID 80. Print DEPARTMENT_ID, minimum, maximum, and average salary. <br>
Sort the results in descending order of average salary first, then maximum salary, then 
minimum salary. Use column alias to rename column names in output for better display.<br>


a. For all managers, find the number of employees he/she manages.
Print the MANAGER_ID and total number of such employees.<br>
```sql
SELECT MANAGER_ID, COUNT(*)
FROM EMPLOYEES
WHERE MANAGER_ID IS NOT NULL
GROUP BY MANAGER_ID;
```
b. For all departments, find the number of employees who get more than 30k salary. Print the 
DEPARTMENT_ID and total number of such employees.<br>
```sql
SELECT DEPARTMENT_ID, COUNT(*)
FROM EMPLOYEES
WHERE SALARY > 10000
GROUP BY DEPARTMENT_ID;
```
c. Find the minimum, maximum, and average salary of all departments except 
DEPARTMENT_ID 80. Print DEPARTMENT_ID, minimum, maximum, and average salary. <br>
Sort the results in descending order of average salary first, then maximum salary, then 
minimum salary. Use column alias to rename column names in output for better display.<br>
```sql
SELECT DEPARTMENT_ID, MIN(SALARY) MIN_SALARY, MAX(SALARY) MAX_SALARY, ROUND(AVG(SALARY),4) AVG_SALARY 
FROM EMPLOYEES
WHERE DEPARTMENT_ID <> 80 AND DEPARTMENT_ID IS NOT NULL 
GROUP BY DEPARTMENT_ID
ORDER BY AVG_SALARY DESC, MAX_SALARY DESC, MIN_SALARY DESC;
```

# Practice 4.2

> a. Find for each department, the average salary of the department. Print only those 
DEPARTMENT_ID and average salary whose average salary is at most 50k.<br>

a. Find for each department, the average salary of the department. Print only those 
DEPARTMENT_ID and average salary whose average salary is at most 50k.<br>
```sql
SELECT DEPARTMENT_ID, ROUND(AVG(SALARY),2)
FROM EMPLOYEES
GROUP BY DEPARTMENT_ID
HAVING AVG(SALARY) <= 50000 AND DEPARTMENT_ID IS NOT NULL
```

# Practice 4.3

> a. Find number of employees in each salary group. Salary groups are considered as follows. 
Group 1: 0k to <5K, Group 2: 5k to <10k, Group 3: 10k to <15k, and so on.<br>
> b. Find the number of employees that were hired in each year in each job type. Print year, job id, 
and total employees hired.<br>

a. Find number of employees in each salary group. Salary groups are considered as follows. 
Group 1: 0k to <5K, Group 2: 5k to <10k, Group 3: 10k to <15k, and so on.<br>
```sql
SELECT TRUNC(SALARY/5000,0) + 1 SALARY_GROUP, COUNT(*)
FROM EMPLOYEES
GROUP BY TRUNC(SALARY/5000,0)
ORDER BY SALARY_GROUP;
```
b. Find the number of employees that were hired in each year in each job type. Print year, job id, 
and total employees hired.<br>
```sql
SELECT TO_CHAR(HIRE_DATE, 'YYYY') YEAR, JOB_ID, COUNT(*)
FROM EMPLOYEES
GROUP BY TO_CHAR(HIRE_DATE, 'YYYY'), JOB_ID
ORDER BY YEAR, JOB_ID;
```

# Chapter 5

# Practice 5.1

> a. For each employee print last name, salary, and job title.<br>
> b. For each department, print department name and country name it is situated in.<br>
> c. For each country, finds total number of departments situated in the country.<br>
> d. For each employee, finds the number of job switches of the employee.<br>
> e. For each department and job types, find the total number of employees working. Print 
department names, job titles, and total employees working.<br>
> f. For each employee, finds the total number of employees those were hired before him/her. 
Print employee last name and total employees.<br>
> g. For each employee, finds the total number of employees those were hired before him/her and 
those were hired after him/her. Print employee last name, total employees hired before him, 
and total employees hired after him.<br>
> h. Find the employees having salaries greater than at least three other employees.<br> 
> i. For each employee, find his rank, i.e., position with respect to salary. The highest salaried 
employee should get rank 1 and lowest salaried employee should get the last rank. Employees 
with same salary should get same rank value. Print employee last names and his/he rank.<br>
> j. Finds the names of employees and their salaries for the top three highest salaried employees. 
The number of employees in your output should be more than three if there are employees 
with same salary.<br>

a. For each employee print last name, salary, and job title.<br>
```sql
SELECT E.LAST_NAME, E.SALARY, J.JOB_TITLE
FROM EMPLOYEES E JOIN JOBS J
ON (E.JOB_ID = J.JOB_ID);
```
b. For each department, print department name and country name it is situated in.<br>
```sql
SELECT D.DEPARTMENT_NAME, C.COUNTRY_NAME
FROM DEPARTMENTS D JOIN LOCATIONS L 
ON (D.LOCATION_ID = L.LOCATION_ID)
JOIN COUNTRIES C
ON (L.COUNTRY_ID = C.COUNTRY_ID);
```
c. For each country, finds total number of departments situated in the country.<br>
```sql
SELECT C.COUNTRY_NAME, COUNT(*)
FROM DEPARTMENTS D JOIN LOCATIONS L
ON (D.LOCATION_ID = L.LOCATION_ID)
JOIN COUNTRIES C
ON (L.COUNTRY_ID = C.COUNTRY_ID)
GROUP BY C.COUNTRY_ID, C.COUNTRY_NAME;
```
d. For each employee, finds the number of job switches of the employee.<br>
```sql
SELECT E.LAST_NAME, COUNT(J.JOB_ID) JOB_SWITCHES
FROM EMPLOYEES E LEFT OUTER JOIN JOB_HISTORY J 
ON (E.EMPLOYEE_ID = J.EMPLOYEE_ID)
GROUP BY E.EMPLOYEE_ID, E.LAST_NAME;
```
e. For each department and job types, find the total number of employees working. Print 
department names, job titles, and total employees working.<br>
```sql
SELECT D.DEPARTMENT_NAME, J.JOB_TITLE, COUNT(*)
FROM EMPLOYEES E JOIN DEPARTMENTS D
ON (E.DEPARTMENT_ID = D.DEPARTMENT_ID)
JOIN JOBS J 
ON (E.JOB_ID = J.JOB_ID)
GROUP BY D.DEPARTMENT_ID, J.JOB_ID, D.DEPARTMENT_NAME, J.JOB_TITLE;
```
f. For each employee, finds the total number of employees those were hired before him/her. 
Print employee last name and total employees.<br>
```sql
SELECT E1.LAST_NAME, COUNT(E2.EMPLOYEE_ID) HIRED_BEFORE
FROM EMPLOYEES E1 LEFT OUTER JOIN EMPLOYEES E2 
ON (E2.HIRE_DATE < E1.HIRE_DATE)
GROUP BY E1.EMPLOYEE_ID, E1.LAST_NAME;
```
g. For each employee, finds the total number of employees those were hired before him/her and 
those were hired after him/her. Print employee last name, total employees hired before him, 
and total employees hired after him.<br>
```sql
SELECT E1.LAST_NAME, COUNT(DISTINCT E2.EMPLOYEE_ID) HIRED_BEFORE, COUNT(DISTINCT E3.EMPLOYEE_ID) HIRED_AFTER
FROM EMPLOYEES E1 LEFT OUTER JOIN EMPLOYEES E2
ON (E2.HIRE_DATE < E1.HIRE_DATE)
LEFT OUTER JOIN EMPLOYEES E3
ON (E3.HIRE_DATE > E1.HIRE_DATE)
GROUP BY E1.EMPLOYEE_ID, E1.LAST_NAME;
```
h. Find the employees having salaries greater than at least three other employees.<br> 
```sql
SELECT E1.LAST_NAME
FROM EMPLOYEES E1, EMPLOYEES E2 
WHERE E1.SALARY > E2.SALARY
GROUP BY E1.EMPLOYEE_ID, E1.LAST_NAME
HAVING COUNT(E2.EMPLOYEE_ID) >= 3;
```
i. For each employee, find his rank, i.e., position with respect to salary. The highest salaried 
employee should get rank 1 and lowest salaried employee should get the last rank. Employees 
with same salary should get same rank value. Print employee last names and his/he rank.<br>
```sql
SELECT E1.LAST_NAME, E1.SALARY, COUNT(DISTINCT E2.SALARY)+1 RANK 
FROM EMPLOYEES E1 LEFT OUTER JOIN EMPLOYEES E2 
ON (E1.SALARY < E2.SALARY)
GROUP BY E1.EMPLOYEE_ID, E1.LAST_NAME, E1.SALARY
ORDER BY RANK;
```
j. Finds the names of employees and their salaries for the top three highest salaried employees. 
The number of employees in your output should be more than three if there are employees 
with same salary.<br>
```sql
SELECT E1.LAST_NAME, E1.SALARY
FROM EMPLOYEES E1 LEFT OUTER JOIN EMPLOYEES E2 
ON (E1.SALARY < E2.SALARY)
GROUP BY E1.EMPLOYEE_ID, E1.LAST_NAME, E1.SALARY
HAVING COUNT(DISTINCT E2.SALARY) <=2
ORDER BY E1.SALARY DESC;
```

# Chapter 6

# Practice 6.1

> a. Find the last names of all employees that work in the SALES department.<br> 
> b. Find the last names and salaries of those employees who get higher salary than at least one 
employee of SALES department.<br>
> c. Find the last names and salaries of those employees whose salary is higher than all employees 
of SALES department.<br>
> d. Find the last names and salaries of those employees whose salary is within ± 5k of the 
average salary of SALES department.<br>

a. Find the last names of all employees that work in the SALES department.<br> 
```sql
SELECT LAST_NAME
FROM EMPLOYEES
WHERE DEPARTMENT_ID = 
(
	SELECT DEPARTMENT_ID
	FROM DEPARTMENTS
	WHERE DEPARTMENT_NAME = 'Sales'
);
```
b. Find the last names and salaries of those employees who get higher salary than at least one 
employee of SALES department.<br>
```sql
SELECT LAST_NAME, SALARY
FROM EMPLOYEES
WHERE SALARY > ANY 
(
	SELECT SALARY
	FROM EMPLOYEES
	WHERE DEPARTMENT_ID = 
	(
		SELECT DEPARTMENT_ID
		FROM DEPARTMENTS
		WHERE DEPARTMENT_NAME = 'Sales'
	)
);
```
c. Find the last names and salaries of those employees whose salary is higher than all employees 
of SALES department.<br>
```sql
SELECT LAST_NAME, SALARY
FROM EMPLOYEES
WHERE SALARY > ALL 
(
	SELECT SALARY
	FROM EMPLOYEES
	WHERE DEPARTMENT_ID = 
	(
		SELECT DEPARTMENT_ID
		FROM DEPARTMENTS
		WHERE DEPARTMENT_NAME = 'Sales'
	)
);
```
d. Find the last names and salaries of those employees whose salary is within ± 5k of the 
average salary of SALES department.<br>
```sql
SELECT LAST_NAME, SALARY
FROM EMPLOYEES
WHERE ABS(SALARY - 
(
	SELECT AVG(SALARY)
	FROM EMPLOYEES
	WHERE DEPARTMENT_ID = 
	(
		SELECT DEPARTMENT_ID
		FROM DEPARTMENTS
		WHERE DEPARTMENT_NAME = 'Sales'
	)
)) <= 5000;
```
# Practice 6.2

> a. Find those employees whose salary is higher than at least three other employees. Print last 
names and salary of each employee. You cannot use join in the main query. Use sub-query in 
WHERE clause only. You can use join in the sub-queries.<br>
> b. Find those departments whose average salary is greater than the minimum salary of all other 
departments. Print department names. Use sub-query. You can use join in the sub-queries.<br>
> c. Find those department names which have the highest number of employees in service. Print 
department names. Use sub-query. You can use join in the sub-queries.<br>
> d. Find those employees who worked in more than one department in the company. Print 
employee last names. You cannot use join in the main query. Use sub-query. You can use join 
in the sub-queries.<br>
> e. For each employee, find the minimum and maximum salary of his/her department. Print 
employee last name, minimum salary, and maximum salary. Do not use sub-query in 
WHERE clause. Use sub-query in FROM clause.<br>
> f. For each job type, find the employee who gets the highest salary. Print job title and last name 
of the employee. Assume that there is one and only one such employee for every job type.<br>

a. Find those employees whose salary is higher than at least three other employees. Print last 
names and salary of each employee. You cannot use join in the main query. Use sub-query in 
WHERE clause only. You can use join in the sub-queries.<br>
```sql
SELECT LAST_NAME, SALARY
FROM EMPLOYEES E1
WHERE 
(
	SELECT COUNT(*)
	FROM EMPLOYEES E2 
	WHERE E1.SALARY > E2.SALARY
) >= 3;
```
b. Find those departments whose average salary is greater than the minimum salary of all other 
departments. Print department names. Use sub-query. You can use join in the sub-queries.<br>
```sql
SELECT DEPARTMENT_ID, ( SELECT DEPARTMENT_NAME FROM DEPARTMENTS D WHERE E1.DEPARTMENT_ID = D.DEPARTMENT_ID ) DEPARTMENT_NAME , ROUND(AVG(SALARY),4)
FROM EMPLOYEES E1
GROUP BY DEPARTMENT_ID
HAVING AVG(SALARY) > ANY
(
	SELECT SALARY
	FROM EMPLOYEES E2 
	WHERE E2.DEPARTMENT_ID <> E1.DEPARTMENT_ID
);
```
c. Find those department names which have the highest number of employees in service. Print 
department names. Use sub-query. You can use join in the sub-queries.<br>
```sql
SELECT DEPARTMENT_ID, (SELECT DEPARTMENT_NAME FROM DEPARTMENTS D WHERE E1.DEPARTMENT_ID = D.DEPARTMENT_ID )
FROM EMPLOYEES E1
WHERE 
(
	SELECT COUNT(*)
	FROM EMPLOYEES E2
	WHERE E2.DEPARTMENT_ID = E1.DEPARTMENT_ID
) = 
(
	SELECT MAX(CNT)
	FROM (SELECT DEPARTMENT_ID, COUNT(*) CNT FROM EMPLOYEES GROUP BY DEPARTMENT_ID) D_COUNT
)
GROUP BY E1.DEPARTMENT_ID;
```
d. Find those employees who worked in more than one department in the company. Print 
employee last names. You cannot use join in the main query. Use sub-query. You can use join 
in the sub-queries.<br>
```sql
SELECT EMPLOYEE_ID
FROM JOB_HISTORY J1
WHERE 
(
	SELECT COUNT(DISTINCT DEPARTMENT_ID)
	FROM JOB_HISTORY J2
	WHERE J1.EMPLOYEE_ID = J2.EMPLOYEE_ID
) > 1;
```
e. For each employee, find the minimum and maximum salary of his/her department. Print 
employee last name, minimum salary, and maximum salary. Do not use sub-query in 
WHERE clause. Use sub-query in FROM clause.<br>
```sql
SELECT E.LAST_NAME, D.MAXSAL, D.MINSAL
FROM EMPLOYEES E, ( SELECT DEPARTMENT_ID, MAX(SALARY) MAXSAL, MIN(SALARY) MINSAL FROM EMPLOYEES GROUP BY DEPARTMENT_ID ) D
WHERE E.DEPARTMENT_ID = D.DEPARTMENT_ID;
```
f. For each job type, find the employee who gets the highest salary. Print job title and last name 
of the employee. Assume that there is one and only one such employee for every job type.<br>


# Chapter 7

# Practice 7.1

> a. Find EMPLOYEE_ID of those employees who are not managers. Use minus operator to perform this.<br>
> b. Find last names of those employees who are not managers. Use minus operator to perform this.<br>
> c. Find the LOCATION_ID of those locations having no departments.<br>

a. Find EMPLOYEE_ID of those employees who are not managers. Use minus operator to perform this.<br>
```sql
SELECT EMPLOYEE_ID
FROM EMPLOYEES
MINUS
SELECT MANAGER_ID
FROM EMPLOYEES;
```
b. Find last names of those employees who are not managers. Use minus operator to perform this.<br>
```sql
SELECT LAST_NAME
FROM EMPLOYEES
WHERE EMPLOYEE_ID IN
(
	SELECT EMPLOYEE_ID FROM EMPLOYEES
	MINUS
	SELECT MANAGER_ID FROM EMPLOYEES
);
```
c. Find the LOCATION_ID of those locations having no departments.<br>
```sql
SELECT LOCATION_ID
FROM LOCATIONS
MINUS
SELECT LOCATION_ID
FROM DEPARTMENTS;
```

# Chapter 11

# Practice 11.1

>a. Write a PL/SQL block that will print ‘Happy Anniversary X’ for each employee X whose<br> 
>   hiring date is today. Use cursor FOR loop for the task.<br>

a. Write a PL/SQL block that will print ‘Happy Anniversary X’ for each employee X whose 
hiring date is today. Use cursor FOR loop for the task.<br>
```sql
DECLARE 
	
	JDATE DATE;
	
BEGIN 
	
	FOR R IN (SELECT * FROM EMPLOYEES)
	LOOP 
	
		JDATE := R.HIRE_DATE;
		
		IF TO_CHAR(JDATE,'DD-MM') = TO_CHAR(TO_DATE(SYSDATE),'DD-MM') THEN 
		
			DBMS_OUTPUT.PUT_LINE('Happy Anniversary ' || R.FIRST_NAME || ' ' || R.LAST_NAME);
			
		END IF;
	
		
	END LOOP;
	
END;
/
```
# Practice 11.2

>a. Extend the above block by handing the following exception: TOO_MANY_ROWS.
>   Print an appropriate message when such an exception occurs.<br>
>b. Write an example PL/SQL block that inserts a new arbitrary row to the COUNTRIES table.
>   The block should handle the exception DUP_VAL_ON_INDEX and OTHERS.
>   Run the block for different COUNTRY_ID and observe the cases when above exception occurs.

a. Extend the above block by handing the following exception: TOO_MANY_ROWS. Print an appropriate message when such an exception occurs.<br>
```sql
DECLARE

 JDATE DATE ;
 YEARS NUMBER ;
 
BEGIN

 SELECT HIRE_DATE INTO JDATE
 FROM EMPLOYEES
 WHERE EMPLOYEE_ID > 101 ;
 
 YEARS := (MONTHS_BETWEEN(SYSDATE, JDATE) / 12) ;
 
 IF YEARS >= 10 THEN 
 
	DBMS_OUTPUT.PUT_LINE('The employee worked 10 years or more') ;
	
 ELSE
 
	DBMS_OUTPUT.PUT_LINE('The employee worked less than 10 years') ;
	
 END IF ;
 
EXCEPTION

	WHEN NO_DATA_FOUND THEN
	
		DBMS_OUTPUT.PUT_LINE('data nai') ;
	
	WHEN TOO_MANY_ROWS THEN
	
		DBMS_OUTPUT.PUT_LINE('Onek row select korsen Sorry') ;
	
	WHEN OTHERS THEN
	
		DBMS_OUTPUT.PUT_LINE('Kijani bhai ki hoise!') ;
	
END ;
/
```
b. Write an example PL/SQL block that inserts a new arbitrary row to the COUNTRIES table.  The block should handle the exception DUP_VAL_ON_INDEX and OTHERS. Run the block for different COUNTRY_ID and observe the cases when above exception occurs.
```sql
DECLARE 
	
	
	
BEGIN 
	
	INSERT INTO COUNTRIES(COUNTRY_ID,COUNTRY_NAME,REGION_ID)
	VALUES('AR','Argentina_Best',2);
	
EXCEPTION 

	WHEN DUP_VAL_ON_INDEX THEN

		DBMS_OUTPUT.PUT_LINE('Sorry, Duplicate values cannot be stored in Unique declared columns');
				
	WHEN OTHERS THEN

		DBMS_OUTPUT.PUT_LINE('Unknown Error occurred');
	
END;
/
```
# Practice on Functions ( Page - 102 )

>a. In Oracle, there is a function TO_NUMBER that converts a VARCHAR2 value to a numeric value.
>   If the input to this function is not a valid number, then this function throws an exception.
>   This is a problem in a SQL query because the whole query would not produce any result
>   if one row generates an exception. So, your job is to write a PL/SQL function ISNUMBER that
>   receives an input VARCHAR2 value and checks whether the input can be converted to a valid number.
>   If the input can be converted to a valid number than ISNUMBER should return ‘YES’,
>   otherwise ISNUMBER should return ‘NO’.<br>

a. In Oracle, there is a function TO_NUMBER that converts a VARCHAR2 value to a numeric value. If the input to this function is not a valid number, then this function throws an exception. This is a problem in a SQL query because the whole query would not produce any result if one row generates an exception. So, your job is to write a PL/SQL function ISNUMBER that receives an input VARCHAR2 value and checks whether the input can be converted to a valid number. If the input can be converted to a valid number than ISNUMBER should return ‘YES’, otherwise ISNUMBER should return ‘NO’.<br>
```sql
CREATE OR REPLACE FUNCTION ISNUMBER(STR IN VARCHAR2)
RETURN VARCHAR2 IS
	
	DUMMY NUMBER;
	MSG VARCHAR2(100);
	
BEGIN 
	
	DUMMY := TO_NUMBER(STR);
	MSG := 'YES';
	RETURN MSG;
	
EXCEPTION 
	
	WHEN INVALID_NUMBER THEN
	
		MSG := 'NO';
		RETURN MSG;
		
	WHEN VALUE_ERROR THEN
	
		MSG := 'NO';
		RETURN MSG;
		
	WHEN OTHERS THEN
	
		MSG := 'Unknown Error Occured';
		RETURN MSG;
	
END;
/

DECLARE 
	
	MESSAGE VARCHAR2(100);
	
BEGIN 
	
	MESSAGE := ISNUMBER('23b4');
	DBMS_OUTPUT.PUT_LINE(MESSAGE);
	MESSAGE := ISNUMBER('234');
	DBMS_OUTPUT.PUT_LINE(MESSAGE);
	
END;
/
```
