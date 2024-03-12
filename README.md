# Data Modeling with Apache Cassandra

Thie project is a data warehouse by Paulina R and is a part od Data Engineering Nanodegree with Udacity.<br>
The Sparkify startup is seeking to analyze the data they have gathered from their new music streaming app. The analysis team's main focus is understanding user listening habits and the songs they prefer. However, the current data storage, consisting of CSV files in a directory, lacks an efficient querying method to generate the desired results.
To address this issue, Sparkify is looking for a data engineer to develop an Apache Cassandra database. This database should enable the execution of queries on song play data, allowing the analytics team to obtain the necessary insights. 

# Data Processing
![Cassandra_NoSQL_data_processing](https://github.com/paulinaruda/no_sql_data_modeling_apache_cassandra/assets/84568114/7e174b38-4789-49b5-ac69-4850045a5c15)

# Implementation

### Part I: Files Pre-Processing
The first step imports the necessary Python packages and creates a list of file paths to process the original event CSV data files. The files are located in the event_data directory. The pipeline involves reading the CSV files, extracting relevant data, and storing it in a new CSV file called event_datafile_new.csv.

### Part II: Apache Cassandra Implementation
Since Apache Cassandra is an OLTP (Online Transaction Processing) databases, the queries are modelled to be denormalized and are created to the specific questions that need to be answered. 
The create table statements are designed to answer the following questions using Apache Cassandra:<br>
1. Give me the artist, song title and song's length in the music app history that was heard during sessionId = 338, and itemInSession = 4<br>
2. Give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182<br>
3. Give me every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'<br>

#### Query 1: Artist, Song Title, and Song Length by Session and Item
A table named artist_song_length is created to answer the first query. The primary key consists of sessionId and itemInSession, as they together provide a unique value per session and item. The relevant data is inserted into this table, and a SELECT statement is used to retrieve the artist, song title, and song length for a specific sessionId and itemInSession.

#### Query 2: Artist, Song, and User by User ID and Session ID
The second query requires the name of the artist, song (sorted by itemInSession), and user (first and last name) for a given userId and sessionId. To answer this query, a table named artist_song_user is created. The primary key consists of userId, sessionId, and itemInSession to ensure uniqueness and allow sorting by itemInSession.

#### Query 3: Users who Listened to a Specific Song
The third query aims to identify every user who listened to a particular song, 'All Hands Against His Own'. A table named user_by_song is created with the song as the partition key and userId as the clustering column. This table allows for retrieving the user's first and last name based on the song they listened to.

### Conclusion
Thanks to creating the Apache Cassandra database, Sparkify can now efficiently query the data to gain valuable insights into user behavior and song preferences. The project demonstrates the importance of data modeling and the use of appropriate primary keys and clustering columns to optimize query performance.

