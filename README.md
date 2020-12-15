# Project: Data Modeling with Cassandra
## Project Overview
A startup company wants to analyze the data they've been collecting on songs and user activity on their new music streaming app especilly interested in understanding what songs users are listening to. Currently, they have a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

This project is to create a Postgres database with tables designed to optimize queries on song play analysis from json files. First, create a database schema with Postgres  to define fact and dimension tables for a star schema for a particular analytic focus. Second , build an ETL pipeline using Python that transfers data from json files in two local directories into these tables in Postgres using Python and SQL.


### Datasets: event_data
event_data: The directory of CSV files partitioned by date. Here are examples of filepaths to two files in the dataset:
``code
event_data/2018-11-08-events.csv
event_data/2018-11-09-events.csv
``
The event_datafile_new.csv contains the following columns:  
* artist(text)
* firstName of user (text)
* gender of user(text)
* item number in session(int)
* last name of user(text)
* length of the song(float)
* level (paid or free song)(text)
* location of the user(text)
* sessionId(int)
* song title(text)
* userId(int)
The image below is a screenshot of what the denormalized data should appear like in the <font color=red>**event_datafile_new.csv**</font> after the code above is run:<br>
<img src="images/image_event_datafile_new.jpg">

### ETL pipeline sturucture 
* process the event_datafile_new.csv dataset to create a denormalized dataset
* model the data table to run queries to ask the following three questions of the data
    1. Give me the **artist, song title and song's length** in the **music app history** that was heard during *sessionId = 338, and itemInSession = 4* 
        table name: "musicapp_history_by_session_by_item"
        primary keys: session_id, item_in_session
    2. Give me only the following: **name of artist, song (sorted by itemInSession) and user (first and last name)** *for userid = 10, sessionid = 182*  
        table name: "musicapp_history_by_user_by_session"
        primary keys: user_id, session_id
    3. Give me every **user name (first and last)** in my **music app history** who listened to the **song** *'All Hands Against His Own* 
        table name: "musicapp_history_by_song"
        primary keys: song, first_name, last_name, user_id
* load the data into tables in Apache Cassandra and run queries

### Project Steps
* Apache Cassandra CREATE KEYSPACE and SET KEYSPACE statements
* CREATE statement for each of the tables to address each question
* Load the data with INSERT statement into relevant tables for each of the tables
* Include IF NOT EXISTS clauses in CREATE statements to create tables only if the tables do not already exist. 
* Test by running the proper select statements with the correct WHERE clause
* Test by running SELECT statements after running the queries on Cassandra database
* include DROP TABLE statement and shutdown session and cluster
