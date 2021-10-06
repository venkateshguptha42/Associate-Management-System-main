# Associate-Management-System
# Project Description
This project is to manage the database of an  educational institute which provides the courses in various domain.
It consist of 4 tables:

1 Master table: It consist of all the records with all the details of the associates.
2 Demo table: It consist the list of students whose demo has been scheduled, demo done and demo not done.
3 Enroll table: It consist of list of all the students who have been enrolled in any of the course.
4 Account table: It consist of all the payment details of all the students who are enrolled in any of the course.

# Technologies Used
Hive
HDFS
Sqoop
SQL and MySQL
# Features
1. Dividing enrolled students into batches.
2. Including payment modes both online of offline, if online then using debit card, credit card, UPI or Internet Banking and if offline then by cash, cheque, demand draft, etc.
3. List of students who have dropped from the institution.
4. For the good execution purpose we can deploy this project on AWS
5. Joining and Demo available Weekdays as well as WEEKENDS.
6. Fees Due data facility available if student forgot the data.
7. Update all records from Master Table using ORC.
8. Create another Data Set for Payment table because it has more features

# It consists of 3 tables:
1. demo_table
2. enrolled
3. payment

# Getting Started
1. create the data base. 
        create database project1
        use database project1
        
        
2. create table temporary master in the format of textfile and load the data
          create table temp(id int, name string, mail string, mobile string, course string, age int, gender string, fee int, discount string, status1 string, status2 string)row format delimited fields terminated by ',' stored as             textfile;
          laod data local inpath '/home/Desktop/table_main.csv/' into table temp;
          
          
3. create a master table in ORC format and load data from temp to ORC main table
            create table Student_details(id int, name string, mail string, mobile string, course string, age int, gender string, fee int, discount string, status1 string, status2 string)stored as                                             orctblproperties('transactional'='true');
          insert into Student_details select * from temp;
          
          
4. create demo_table in ORC format
          create table demo_table(id int, name string, mail string, contact string, course string, demo_status1 string,demo_status2 string)stored as orc tblproperties('transactional'='true');

          insert into demo_table select id,name,mail,mobile,course,status1,status2 from Student_details where status1='DS' or status1='DM' or status1 = 'DD';
          
          
          
5. create enrolled table and load the data
       create table enrolled(id int, name string, mail string, contact string, course string, enroll_status1 string,enroll_status2 string)stored as orc tblproperties('transactional'='true');
       insert into enrolled select id,name,mail,mobile,course,status1,status2 from Student_details where status1='J';          
         

          
# Contributors
Developer : Anand
Database Admin : Kavya
Quality Manager : Akhil
Data Analyst : Venkatesh

