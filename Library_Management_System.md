```
create database Library_Management_System;

create table Members(
Member_id int primary key identity(1,1),
Name varchar(255) check(len(Trim (Name))>0),
Email varchar(255)  unique check(len(Trim (Email))>0),
);

create table MemberProfile(   --1:1
Member_id int primary key,
Photo nvarchar(255),
foreign key (Member_id) references Members(Member_id)
);

create table Author(
Author_id int primary key identity(1,1),
Name varchar(255) check(len(Trim (Name))>0)
);

create table Books(  --1:N
Book_id int primary key identity(1,1),
Name varchar(255) check(len(Trim (Name))>0),
price int not null check(price>0),
quantity int not null check(quantity>=0),
Author_id int not null,
foreign key (Author_id) references Author(Author_id)
);

create table Borrow(
Borrowing_id int primary key identity(1,1),
Member_id int not null,
Book_id int not null,
Borrowing_Date date default Getdate() not null,
NDays int not null check(NDays>0),
foreign key (Member_id) references Members(Member_id),
foreign key (Book_id) references Books(Book_id)
);

create table Categories(
CategoryID int primary key identity(1,1),
Name varchar(255) check(len(Trim (Name))>0)
);

create table BookCategories(
BookCategories_id int primary key identity(1,1),
CategoryID int not null,
Book_id int not null,
foreign key (CategoryID) references Categories(CategoryID),
foreign key (Book_id) references Books(Book_id)
);
```
