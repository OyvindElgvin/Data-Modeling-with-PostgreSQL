
### Project: Data Modeling with Postgres

(Will try to make a better readme next time, describing how to run and an explanation of the files.)



##### 1. 

The purpose of this database is to make it easier to analyze the data Sparkify is generating, and further to maximize growth and revenue. The unorderly data from a Song Dataset and a Log Dataset are converted into a star schema database, which makes it possible to analyze the data much more deeply and intuitively. I would think that the new schema will also make it applicable to predictive analyses like machine learning to, for instance, find good next song suggestions. 


##### 2.

This schema makes it fast and easy to make queries. It is normalized to 3. degree, I think, which makes it use atomic values, all columns rely on the Primary Key, and the tables have no transitive dependencies. 

The ETL pipeline is set up so that all the create table queries are in a create_tables-py file, while the other queries are in a sql_queries.py file. The etl.py imports the queries from sql_queries.py and has a main function that sets up the connection to the database and runs the queries for the song dataset and the log dataset. 

![Image of Schema](https://imgur.com/a/pb1adpc)



##### 3.


I tried to make a SELECT query in the test.ipynb. The query was supposed to sum the duration listened for each user and order them DESC with the user listening the most on top. Maybe it will work with the whole dataset? 

%sql SELECT u.user_id, u.first_name, u.last_name, u.gender, u.level, SUM(so.duration) total_duration_listened FROM users u JOIN songplays sp ON u.user_id = sp.user_id JOIN songs so ON so.song_id = sp.song_id GROUP BY 1, 2, 3, 4, 5 ORDER BY 6 DESC LIMIT 10;

postgresql://student:@127.0.0.1/sparkifydb
0 rows affected.
user_id	first_name	last_name	gender	level	total_duration_listened
