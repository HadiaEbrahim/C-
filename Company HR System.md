```
create database Company_HR_System;

create table department(
department_id int primary key identity(1,1),
name varchar(255) not null check(len(trim(name))>0)

);

create table Employee(
employee_id int primary key identity(1,1),
name varchar(255) check(len(trim(name))>0) not null,
email varchar(255) check(len(trim(email))>0) unique not null,
title varchar(255) check(len(trim(title))>0) not null,
age int not null check(age>=18),
address varchar(255) check(len(trim(address))>0) not null,
phone varchar(255) check(len(trim(phone))=11) not null,
photo varchar(255) ,
salary int not null check(salary>0),
national_id varchar(255) check(len(trim(national_id))=14) not null unique,
Fingerprint varbinary(MAX) not null,
department_id int not null,
foreign key (department_id) references department(department_id)
);


create table project(
project_id int primary key identity(1,1),
name varchar(255) not null check(len(trim(name))>0),
department_id int not null,
foreign key (department_id) references department(department_id)
);

create table task(
task_id int primary key identity(1,1),
name varchar(255) not null check(len(trim(name))>0),
project_id int not null,
employee_id int not null,
foreign key (project_id) references project(project_id),
foreign key (employee_id) references Employee(employee_id)
);

create table employee_projects(
employee_projects_id int primary key identity(1,1),
project_id int not null,
employee_id int not null,
foreign key (project_id) references project(project_id),
foreign key (employee_id) references Employee(employee_id)
);

INSERT INTO department (name) VALUES 
('Software Development'),
('Human Resources'),
('Quality Assurance');

insert into Employee 
(name, email, title, age, address, phone, photo, salary, national_id, Fingerprint, department_id) 
VALUES 
('Ahmed Ali', 'ahmed.ali@company.com', 'Senior Backend Developer', 28, '12 Cairo St, Cairo', '01012345678', 'uploads/photos/ahmed.jpg', 18000, '29501011234567', 0x89504E470D0A1A0A, 1),
('Sara Mohamed', 'sara.mohamed@company.com', 'HR Specialist', 25, '45 Nasr City, Cairo', '01123456789', 'uploads/photos/sara.jpg', 10000, '29805151234568', 0xFFD8FFE000104A46, 2),
('Omar Hassan', 'omar.hassan@company.com', 'QA Engineer', 26, '8 Giza Sq, Giza', '01234567890', 'uploads/photos/omar.jpg', 12000, '29709201234569', 0x4749463839610100, 3),
('Mona Ibrahim', 'mona.ibrahim@company.com', 'Junior DotNet Developer', 23, '19 Maadi, Cairo', '01545678901', NULL, 8500, '30102101234570', 0x504B030414000000, 1);

INSERT INTO project (name, department_id) VALUES 
('E-Commerce Platform', 1),
('HR Management System', 1),
('Employee Onboarding 2026', 2),
('Security & Performance Audit', 3);

INSERT INTO task (name, project_id, employee_id) VALUES 
('Design Database Schema', 2, 2),
('Implement Auth JWT Middleware', 2, 2),
('Create User Profile ViewModels', 2, 4),
('Conduct Technical Interviews', 3, 2),
('Automate API Stress Tests', 4, 3);

INSERT INTO employee_projects (project_id, employee_id) VALUES 
(2, 2), 
(2, 4), 
(2, 2), 
(3, 2), 
(4, 3);

SELECT * FROM department;
SELECT * FROM Employee;
SELECT * FROM project;

SELECT * FROM task;
--Retrieve employee names and titles where age > 30
select name ,title from Employee 
where age>30;
--Retrieve employees from a specific department.
select* from Employee e,department d
where e.department_id=d.department_id and d.name='Software Development';
--Find the minimum salary.
select min(salary) from Employee ;
--Find employees whose names start with A.
select name from Employee where name like('A%');
--Find employees whose email contains Gmail.
select* from Employee where email like('%Gmail%');
--Find employees without a phone number.
select* from Employee where phone is null;
--Sort employees by age.
select* from Employee order by age;
--Classify employees by age group.
select 
name,
age,
case
when age<30 then'Junior.'
when age between 30 and 40 then'Mid Level'
else 'Senior'
end as Classify_employees
from Employee;
```
