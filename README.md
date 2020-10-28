### Employee_Payroll_Database

## UC-1: Create Database and Display

```
create database payroll_service;
show databases;
use payroll_service; 
```
## UC-2: Create Table in Database
```
create table employee_payroll
(
id          INT unsigned NOT NULL AUTO_INCREMENT,
name        VARCHAR(150) NOT NULL,
salary      Double NOT NULL,
start_date       DATE NOT NULL,
PRIMARY KEY (id)
);
```

