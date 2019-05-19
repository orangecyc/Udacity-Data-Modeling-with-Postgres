### Files in the repository
The repository consists of the following files/folder:
1. **data** folder - contains the raw data of song and log data files
2. **create_tables.py** - drops and creates database tables, tables are reset by running this file.
3. **etl.py** - reads, processes and load data from song and log data files into database tables.
4. **test.ipynb** - displays the first few rows of each database table for checking the database, also with some **example queries and results of analysis**
5. **etl.ipynb** - detailed explanation on the ETL process for each of the database tables.
6. **sql_queries.py** - all the SQL queries required to support the actions on database.
7. **README.md** - this readme file.

### Procedure to run python script for setting up the database and performing ETL
1. Start a Python 3 Console
2. In the console, run create_tables.py
3. run etl.py

### Schema of database : **sparkifydb**
The database **sparkifydb** consist of 5 tables, and their columns are given below:
1.	**songplays** - records in log data associated with song plays
    - *songplay_id*, int, the id of song played
    - *start_time*, varchar, start time of song played
    - *user_id*, int, user id
    - *level*, varchar, level of user account (free or paid account)
    - *song_id*, varchar, song id
    - *artist_id*, varchar, artist id
    - *session_id*, int, session id
    - *location*, varchar, location of user
    - *user_agent*, varchar, user agent used by user
2.	**users** - users in the app
    - *user_id*, int, user id
    - *first_name*, varchar, first name of user
    - *last_name*, varchar, last name of user
    - *gender*, varchar, gender of user
    - *level*, varchar, level of user account (free or paid account)
3.	**songs** - songs in music database
    - *song_id*, varchar, song id
    - *title*, varchar, song title
    - *artist_id*, varchar, artist id
    - *year*, int, release year of song
    - *duration*, numeric, duration of song (in seconds)
4.	**artists** - artists in music database
    - *artist_id*, varchar, artist id 
    - *name*, varchar, artist name
    - *location*, varchar, location of artist
    - *latitude*, numeric, latitude of artist's location
    - *longitude*, numeric, longitude of artist's location
5.	**time** - timestamps of records in songplays broken down into specific units
    - *start_time*, varchar, timestamp of start time of song played
    - *hour*, int, hour in a day of *start_time*
    - *day*, int, day in a month of *start_time*
    - *week*, int, week in a year of *start_time*
    - *month*, int, month of *start_time*
    - *year*, int, year of *start_time*
    - *weekday*, int, weekday of *start_time*

### Purpose of database **sparkifydb**
For **Sparkify** as a start-up, it is essential to have the business growing rapidly in order to build a solid foundation (considering that 99% of start-up cannot sustain for 3 years) as well as to ensure that the company is profit-making. Knowing your customers well is important for a company to draw up better marketing plans and customer relations programmes. All of this can be driven by data analytics on users' behaviour.

The purpose of the database **sparkifydb** is to provide structured datasets that support the data analytics for the business. Given with a structured and timely-updated database covering different variables (songplayed, users, songs, artists, times), various kinds of analytics can be conveniently performed, such as multivariate analysis, identifying loyal customers, identifying customers that require our retention, customer segmentation by types of songs listened, favourite songs, etc.

### The database, schema design and ETL pipeline
The database is a relational database with star schema, with table **songplays** as fact table at the centre and other 4 as dimension tables that can draw relations with the fact table. We choose to use relational database because the raw data of songs and usage logs is standardised, thus can be framed in structured data model. Using different tables storing different aspects of information makes our data model intuitive, say when we wish to look for the information about songs, we simple query on songs table. Finally, using a star schema implies certain degree of normalisation, hence reducing data redundancy.

For the ETL pipeline, the raw data in JSON format is processed and loaded to relational database system using Python and SQL scripting. Logics for database management, data ETL, SQL queries and testing are stored in separated files. Different tiers within the ETL pipeline is modular and can be maintained independently. Data engineers, software developers and data scientists can all understand and manage the pipeline easily.

### Other remarks
1. Following the instruction for this project, the database table **users** will contains many duplicated records because it is directly extracted by merely column selection from log data, suggest to remove duplicates by including Python syntax: `user_df.drop_duplicates(subset = None, keep = 'first', inplace = True)`
2. In ths sample data of this project, seems all the song played in log_data cannot be found in the song_data, hence song_id and artist_id cannot be matched thus both columns in songplays table are all None in values.