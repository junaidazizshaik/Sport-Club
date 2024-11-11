# Sport-Club

Database management system of the Sport Club

-- a new database will be created first named "SCMS" by suing the create database statement --
Create database SCMS;

-- need to select the databse named "SCMS" in order to perform queries inside it --
Use SCMS;

-- need to create four tables using the create table statement --
-- creating table for member --
Create table Member_Details (
	memNumber int(5) primary key,
    firstName varchar(40) not null,
    lastName varchar(40) not null,
    address varchar(50),
    phoneNumber int(11) not null,
    email varchar(30) not null,
    dob date not null,
    healthCondition varchar(30) null
    );

-- creating table for staff --  
Create table Staff_Details (
	staffCode int(5) primary key,
    firstName varchar(40) not null,
    lastName varchar(40) not null,
    staffRole varchar(40) not null,
    phoneNumber int(11) not null
    );
    
-- creating table for sportsclass --    
create table SportsClass_Details (
	classID varchar(5) primary key,
    classTitle varchar(40) not null,
    sportDay varchar(30) not null,
    sportTime varchar(20) not null,
    staffCode int(5),
    Foreign key (staffCode) references Staff_Details (staffCode)
    );
    
-- creating table for booking --
Create table Booking_Details (
	bookingCode int(5) primary key,
    classDate date not null,
    classTimeSlot varchar(20) not null,
    classAttendance varchar(20) not null,
    memNumber int(5),
    classID varchar(5),
    Foreign key (memNumber) references Member_Details (memNumber),
    foreign key (classID) references SportsClass_Details (classID)
    );

Select m.firstname, m.lastname, b.bookingcode, b.classDate, b.classtimeSlot,c.classtitle 
from Member_Details m 
inner join booking_details b on b.memnumber=m.memnumber 
inner join SportsClass_details c on c.classid=b.classid;










-- need to insert the values to the created tables in order to perform operations --
    
insert into member_details values (101, 'Barry', 'Allen', '7th Avenue', 654785487,'barry@mail.com', '1995-10-21',null);
insert into member_details values (102, 'John', 'Jonathan', 'Kings Road', 325658987,'jonathan@mail.com', '1998-03-19','Diabetes');
insert into member_details values (103, 'Nina', 'Williams', '6th Mile', 365236986,'nina@mail.com', '1992-10-15',null);
insert into member_details values (104, 'Beve', 'Jane', 'George Road', 546987854,'jane@mail.com', '1991-10-05',null);
insert into member_details values (105, 'Harry', 'Potter', '1/2 Mile', 785487548,'harry@mail.com', '1992-05-20','Asthama');
insert into member_details values (106, 'Christie', 'Winslet', '18th Avenue', 965878547,'christie@mail.com', '1996-11-17',null);
    
Insert into Staff_Details values (100, 'Jonny', 'Wilson', 'Instructor',785487854);
Insert into Staff_Details values (102, 'Jack', 'Mathew', 'Instructor',546854787);
Insert into Staff_Details values (101, 'Shein', 'Johnson', 'Receptionist',658458745);
Insert into Staff_Details values (103, 'Sam', 'Markson', 'Trainer',698565898);
 
Insert into SportsClass_Details values ('c12', 'Swimming','Mon-Wed', '09:00 AM to 11:00 AM', 100);
Insert into SportsClass_Details values ('c11', 'Football','Mon-Fri', '03:00 PM to 05:00 PM', 102);
Insert into SportsClass_Details values ('c13', 'Rock Climbing','Thu', '09:00 AM to 11:00 AM', 102);
Insert into SportsClass_Details values ('c14', 'Swimming','Mon-Wed', '11:00 AM to 01:00 PM', 100);
Insert into SportsClass_Details values ('c15', 'Cycling','Mon-Thu', '02:00 PM to 04:00 PM', 102);
    
Insert into Booking_Details Values (1, '2021-08-20', '02:00 PM to 04:00 PM','Present', 101, 'c15');
Insert into Booking_Details Values (2, '2021-08-21', '09:00 AM to 11:00 AM','Present', 102, 'c13');
Insert into Booking_Details Values (3, '2021-08-22', '03:00 PM to 05:00 PM','Present', 103, 'c11');
Insert into Booking_Details Values (4, '2021-08-15', '09:00 AM to 11:00 AM','Present', 104, 'c12');
Insert into Booking_Details Values (5, '2021-08-17', '02:00 PM to 04:00 PM','Present', 101, 'c15');
Insert into Booking_Details Values (6, '2021-08-20', '11:00 AM to 01:00 PM','Present', 102, 'c14');
Insert into Booking_Details Values (7, '2021-08-17', '11:00 AM to 01:00 PM','Absent', 103, 'c14');


Select B.bookingcode, c.classtitle as Current_Activities, b.classtimeSlot 
from booking_details b 
inner join SportsClass_details c on c.classid=b.classid 
where b.classdate>=sysdate()+7;

