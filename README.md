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
## UC-3: Insert Data in Table
```
insert into employee_payroll (name,salary,start_date) VALUES
('mark', 50000, '2020-01-02'),
('bill', 50000, '2018-01-03'),
('terisa', 200000, '2019-11-13');
```
## UC-4: Display Data in Table
```
select * from employee_payroll;
```
## UC-5: Retrieve Data from Table
```
select salary from employee_payroll where name='bill';
select * from employee_payroll where start between cast('2018-01-01' as date) and date(now());
```

