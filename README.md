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

## UC-5: Retrieve Data from Table
```
select salary from employee_payroll where name='bill';
select * from employee_payroll where start between cast('2018-01-01' as date) and date(now());
```
## UC-6: Edit Data from Table
```
alter table employee_payroll add gender CHAR(1) after name;
update employee_payroll set gender='F' where name='terisa';
update employee_payroll set gender='M' where name='bill' or name='mark';
```
## UC-7: Sum, Average, Maximum, Minimum and Number of Male and Female Employees
```
select sum(salary) from employee_payroll where gender='F' group by gender;
select sum(salary) from employee_payroll where gender='M' group by gender;
select avg(salary) from employee_payroll where gender='M' group by gender;
select gender, min(salary) from employee_payroll group by gender;
select gender, max(salary) from employee_payroll group by gender;
select gender, count(name) from employee_payroll group by gender;
```

## UC_8: Extend table to add Employee Information
```
alter table employee_payroll add phone_number VARCHAR(250) after name;
alter table employee_payroll add address VARCHAR(250) after phone_number;
alter table employee_payroll add department VARCHAR(250) NOT NULL after address;
alter table employee_payroll alter adress set default 'TBD';
update employee_payroll set phone_number = 9416029025, set address = 'sector-13' where name = 'bill';
update employee_payroll set phone_number = 9416029026, set address = 'sector-15' where name = 'terisa';
update employee_payroll set phone_number = 9412345433, set address = 'sector-6' where name = 'mark'; 
select * from employee_payroll;
```

## UC_9: Extend table to have basic pay, deductions, taxable, income tax, and net pay
```
alter table employee_payroll rename colum salary to basic_pay;
alter table employee_payroll add deductions Double NOT NULL after basic_pay;
alter table employee_payroll add taxable_pay Double NOT NULL after deductions;
alter table employee_payroll add tax Double NOT NULL after taxable_pay;
alter table employee_payroll add net_pay Double NOT NULL after tax;
```
## UC_10: Make terisa as a part of sales and marketing department
```
update employee_payroll set department='Sales' where name='terisa';
insert into employee_payroll (name, department, gender, basic_pay, deductions, taxable_pay, tax, net_pay, start)
VALUES('terisa', 'Marketing', 'F', 3000000, 100000, 2000000, 500000, 1500000, '2019-11-13');
```
## UC_11: ER Diagram

#Adding Table Company
```
 create table Company(
     company_id int not null,
     company_name varchar(50) not null,
     primary key(company_id));
```
#Adding Department Table
``` 
create table Department (
     department_id int not null,
     department_name varchar(50) not null,
     primary key(dept_id));
```
#Adding Employee Table
``` 
create table employee(
     employee_id int unsigned not null auto_increment primary key,
     company_id int not null,
     department_id int not null,
     first_name varchar(50) not null,
     last_name varchar(50) not null,
     address varchar(50) not null,
     phone_number int(10) not null,
     gender char(1) not null,
     foreign key(company_id) references company(company_id),
     foreign key(department_id) references department(department_id));
```
#Adding Table Payroll
```
create table payroll(
     employee_id int not null auto_increment primary key,
     basic_pay double not null,
     deductions double not null,
     taxable_income double not null,
     income_tax double not null,
     net_pay double not null,
     foreign key (employee_id) references employee(employee_id));
```
## UC_12: Insering and Retrieving  Data
# Inserting Data
```
insert into Company(company_id, company_name) VALUES
(1,'CG');

insert into employee(first_name,last_name,company_id,employee_id,department_id,phone_number,address,gender) VALUES
('mark','goel',1,1,101,'989968543','karnal','M'),
('terisa','james',1,2,202,'9899765676','agra','F');

insert into payroll(employee_id,basic_pay,deductions,taxable_pay,tax,net_pay) VALUES
(1,50000,1000,20000,2000,30000),
(2,70000,2000,25000,5000,45000);

insert into department (department_id, department_name) VALUES
(101,'Sales'),
(202,'Marketing),
(303,'AI');

insert into employee_department (employee_id, departmentt_id) VALUES
(1,101),
(2,101),
(2,202);
```
#Retrieving Data from Table
```
select sum(p.net_pay), e.gender from employee_details e left join payroll p
on p.emp_id=e.emp_id group by e.gender;

select avg(p.net_pay), e.gender from employee_details e left join payroll p
on p.emp_id=e.emp_id group by e.gender;

select min(p.net_pay), e.gender from employee_details e left join payroll p
on p.emp_id=e.emp_id group by e.gender;

select max(p.net_pay), e.gender from employee_details e left join payroll p
on p.emp_id=e.emp_id group by e.gender;

select count(p.net_pay), e.gender from employee_details e left join payroll p
on p.emp_id=e.emp_id group by e.gender;
```
