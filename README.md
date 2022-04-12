## The purpose of the database
This database contains four dimension tables for users, songs, artist, time and a fact table for songplays.
As a relational database, it permits for a wide range of queries and analysis: about users, songs and artists, we can querie about the most listened songs, the most poplar artists, what every users listens the most whitch can help for recommending similar content and inderstanding the trends of listenings.

## How to run the Python scripts:

We first need to run the "create_tables.py" script. It creates the database and create the tables (the queries for tables dropping and creation are implemented in the "sql_queries.py"). 
Then we just need to run the "etl.py" script that extracts the data from the json files (logs and song data) and the inserts it properly into the tables.

Inside a terminal run this commands:

> python create_tables.py
> python etl.py

## Files of the porject:

* sql_queries.py: contains the sql queries for tables creation, deletion and insertion. It contains also a sql query to get the song and artist id
* create_tables.py: create an empty database and creates the tables. It uses the queries from the sql_queries.py script
* etl.py: extracts the data from the songs and logs files, transforms them in the proper shape to load it then into the database
* etl.ipynb: a notebook to extract and load data from one json file (one song file and one log file) it helps inderstand and make sure the etl process works correctly before running it on the whole data.
* test.ipynb: a notebook to show some rows from each table in order to see the result after the etl process. It contains also sanity checks to make sure of some properties of the tables (data types, primary keys, ...)

# Schema:

The schema of our database is a star schema. It consist of a fact table "songplays" that references four dimension tables: "artists", "users", "songs", "time". It allows to simplifie querries and makes aggregations fast.

# ETL:

The process is rather simple, we extract the data from the json files and put them into pandas dataframe where we can keep the columns that we want and drop the rest. We also perform timestamps transformation to datetime. The only non straight forward transformation is the one for the songplays table, where we needed to querie the dataset about song_id and artist_id (instead of keeping names) ids are better foreign keys.