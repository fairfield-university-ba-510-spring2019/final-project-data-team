## Data Team Final Project

For our Final Project we created a relational database and data warehouse containing information relating to the courses offered at Fairfield University.
The information was provided by Dr. Huntley where he scraped the information into .csv files and we were tasked with populating the database and data warehouse
that we created.

## Steps Taken

1. Created an ERD outlining the tables we intended to create in our CourseData.db database
2. Imported the necessary packages to read in .csv files and connect to the database
3. Read in the .csv files into pandas dataframes and converted them to SQL
4. Created tables from ERD and inserted the data from the .csv files to corresponding tables
5. Tested the integrity of our database with a variety of SQL queries
6. Created an ERD outlining the tables we intended to create in our CourseDataWarehouseFinal.db data warehouse
7. Imported the necessary packages to connect to data warehouse
8. Created the tables from ERD and inserted the data from the information contained in our CourseData.db database
9. Tested the integrity of our data warehouse with a variety of SQL queries
10. Created ReadmeFinal.md and DataDictionary.md

## Step 1

Our first step taken was to create an ERD based on the .csv files Dr. Huntley scraped for us.  The ERD was created to show our tables
that we planned on creating and how they connected/related to the other tables.  

## Step 2

In order to read in the .csv files and connect to the database we planned on creating, we had to import the necessary packages to do so.
These imports included:
    - from sqlalchemy import create_engine: Used to connect to server and create database
    - import pandas as pd: All query results are returned as Pandas DataFrames
    - import glob, os: Used for importing .csv's
    - %load_ext sql: Needed for sql Magic
    - import sqlite3

## Step 3

We then read in all of the .csv files provided to us.  We used pd.read_csv to read the course catalog csv's in and glob and os to read in the
courses and course meetings .csv's.  Glob was used to find all the pathnames in the SourceData file that matched course_meetings.csv and
courses.csv.  This allowed us to import all of the years beginning in 2014 at once.

We then wanted to get the .csv files into SQL.  We used .to_sql to do this and used the engine we created earlier in the notebook.
This was easy for the course catalog and courses files but was much more difficult for the course meeting .csv's due to their size.
We had to import them into ten sepearte tables and then use a union later to combine them back together in order to insert them into the tables
we planned on createing.

## Step 4

We first wanted to create a course catalog table to hold all of the information contained in the .csv's.  To do this we once again used a
union when inserting the information into the table to capture both years information.  

We then wanted to create an overall course meetings table.  This is where we used a union on the ten tables we created earlier when getting the
.csv files into SQL.  This combined all of the information into one table for all of the years beginning in Fall 2014.  We noticed that the course
meeting .csv's had column with start and end times that also contained the dates the classes took place.  We decided to separate these facts into
separate columns using alter table adding a column for the date the class met, the time the class started and the time the class ended.

We then created an overall courses table and used a union to combine all of the .csv's beginning with Fall 2014.  We wanted to clean up the courses table
we created and since this can not be done very easily in SQL we created another dataframe to be able to clean it up easier.

We now created our tables based on our ERD.  We had 4 tables called Terms, Calendar, CRN and Course.
The Terms table contained information about the dates each term began and ended.
The calendar table had the specific date and the day of the week it fell on.
The CRN table contained information about the CRN, the term it fell in, the title of the course, the catalog_id of the course and the section of the course.
The Course table contained information about the capacity of the class, the actual amount of students in the class, the remaining seats in the class,
the instructor of the course, the crn and term of the course, and the start and end time of each course.

We populated these tables from the overarching tables we first created from the .csv files.

[CourseDataETL](../CourseDataETL.ipynb)

## Step 5

In order to test the domain, entity and relational integrity of the database we created and ran a variety of SQL queries to see if it held up.

[CourseDataTests](../CourseDataTests.ipynb)

## Step 6

We once again created an ERD for the data warehouse we planned on creating.  We used a star schema with our fact table in the middle and our dimensions
surrounding it.

## Step 7

In order to connect to the data warehouse we imported the necessary connection string.

## Step 8

Based on our ERD, we created tables and populated them from the information contained in the tables in our CourseData.db.
Our facts table contained four foreign keys connecting to our four dimension tables.

[CourseDataWarehouseDemo](../CourseDataWarehouseDemo.ipynb)

## Step 9

In order to test the domain, entity and relational integrity of the data warehouse we created and ran a variety of SQL queries to see if it held up.

[CourseDataWarehouseTest](../CourseDataWarehouseTest.ipynb)
