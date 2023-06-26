# Chapter 1
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
