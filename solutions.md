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

a.(i) 
```sql
SELECT FIRST_NAME, LAST_NAME, TO_CHAR(HIRE_DATE,'ddth Month, YYYY')
FROM EMPLOYEES;
```

a.(ii)
```sql
SELECT FIRST_NAME, LAST_NAME, TO_CHAR(HIRE_DATE,'dd Month, YYYY')
FROM EMPLOYEES;
```




