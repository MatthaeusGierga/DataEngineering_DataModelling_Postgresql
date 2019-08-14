# Introduction

The startup Sparkify wants to analyze the data they have been collecting on songs and user activity on their new music streaming app. They are particularly interested in understanding what songs users are listening to. Currently, they do not have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

Possible analytical use cases could be:
* what song would a user of Sparkify like to hear next based on his song history (what he was listening to)
* what kind of songs would a user of Sparkify like to listen to depending on the time of the day or region
* do the payed and free user behave differently regarding songs and artists?
* a lot of more business cases... 

# Approach
Instead of using JSON-Files to store the data, it is recomended to create a database to store the data and to be able to process analytical querys. An efficiant way to do it is the STAR schema. The STAR schema consists of one fact table and multiple dimension tables, which are connected to the fact table. 

In this specific szenario we created the following tables:

### Fact table: 
**songplays**
consists the keys to each dimension table and facts 

### Dimension tables:
**user**, **songs**, **artists**, **time**
each dimension table consist of one primary key which is linked to the fact table and attributes that discribe the data of the specific table - for example all the necessary data of an song like name, artist and year.


### ETL pipeline
1. sql_queries.py
consists of all the necessary functions and sql-querys of the project. Dimension tabeles and insert querys are defined in this file.

2. create_tables.py
basic python file for creating the database, drop tables and create new tables that are defined in the 'sql_queries.py'. No changes in this file done.

3. etl.ipynb
hands on file with detailed instructions of the etl process. It loads the data from a single file from 'song_data' and 'load_data' into the created tables of the database. 

4. test.ipynb
test file to check if the data was correctly loaded to the database after running 'etl.ipynb' or 'etl.py'. It displays the first few records of the specific table. 

5. etl.py
loads all data from all **song_data** and **load_data** and loads them into the database. 

Important functions in this file:

**process_song_file:** Is used to read the song files and insert the specific data to the tables **songs** and **artists**.

**process_log_file:**  Is used to read the log files and insetr the specific data to the tables into **time**, **user** and **songplays**. 

**process_data:** Loops through all the **song files** and **log files**.

**main:** is used to call the **process_data** function and call the **process_song_file** and **process_log_file** for each of the files within the loop. 

6. run.ipynd
final python file to call the **create_tables.py**, **sql_queries.py** and **etl.py**
