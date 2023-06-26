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
WHERE HIRE_DATE < '01-JAN-2007'
```
b. Select all locations in the following countries: Canada, Germany, United Kingdom.<br>


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
WHERE LOWER(LAST_NAME) LIKE 'a%'
```
e. Select first names of employees whose last name starts with an 's' and ends with an 'n'.<br>
```sql
SELECT FIRST_NAME
FROM EMPLOYEES 
WHERE LOWER(LAST_NAME) LIKE 's%n'
```
f. Select all department names whose MANAGER_ID is 100.<br>
```sql
SELECT DISTINCT DEPARTMENT_ID
FROM EMPLOYEES
WHERE MANAGER_ID = 100
```
g. Select all names of employees whose job type is 'AD_PRES' and whose salary is at least 23000.<br>
```sql
SELECT (FIRST_NAME || ' ' || LAST_NAME) NAME
FROM EMPLOYEES 
WHERE JOB_ID = 'AD_PRES' AND SALARY >= 23000
```
h. Select names of all employees whose last name do not contain the character 's'.<br>
```sql
SELECT (FIRST_NAME || ' ' || LAST_NAME) NAME
FROM EMPLOYEES 
WHERE LOWER(LAST_NAME) NOT LIKE '%s%'
```
i. Select names and COMMISSION_PCT of all employees whose commission is at most 0.30.<br>
```sql
SELECT FIRST_NAME, LAST_NAME, COMMISSION_PCT 
FROM EMPLOYEES 
WHERE COMMISSION_PCT <= 0.30
```
j. Select names of all employees who have joined after January 01, 1998.<br>
```sql
SELECT FIRST_NAME, LAST_NAME 
FROM EMPLOYEES 
WHERE HIRE_DATE > '01-JAN-1998'
```
k. Select names of all employees who have joined in the year 1998.<br>
```sql
SELECT FIRST_NAME, LAST_NAME, HIRE_DATE 
FROM EMPLOYEES 
WHERE TO_CHAR(HIRE_DATE, 'YYYY') = '1998'
```

