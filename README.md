# project_etl
Project ETL
Team 4: Joe Adams, Michelle Lucio, Ben Farniok, and Jessica Schmitz.

SUMMARY:
 The project will deliver a database containing IMBD movie data. This data ranges from ratings, cast and crew information, year released, and much more. We began with six data sets, however we determined that one of the six data sets wasn’t useful due to duplicative data and lots of unnecessary details, so dropped it from our project (title.akas.tsv).  
We then started to clean up the remaining 5 dataframes. When looking through our different dataframes, we found that the titles_basics_df included inappropriate content (adult films), so we removed it from our dataframe. In the remaining dataframes we began renaming column to be consistent across our dataframes, removing columns that held content we didn’t find useful, removing null values, and last merging two dataframe.
 At first we ended with three dataframes from the original six that we would insert into MongoDB. However, after attempting to insert the “principle” dataframe, we found that it was too large of a dataframe, as it would error out and/or crash before it could be inserted fully. To solve for this issue, we split the data into 4 separate dataframes, ending with a total of 6 dataframes that we would insert into MongoDB. We decided on using MongoDB rather than PostgreSQL due to some of the columns containing lists of data that we believed were important to contain in our final database. 

Here is a visual representation of how we completed the project: 
 

INITIAL DATA SETS

Here are links to the original IMDB data sets. Please note: We did not include these in our repositories due to the large amount of data they contain. You will need to download them into a “Resources” folder at the same level as the repo folder, in order to get the script to run. 

https://datasets.imdbws.com/title.akas.tsv.gz

https://datasets.imdbws.com/name.basics.tsv.gz

https://datasets.imdbws.com/title.basics.tsv.gz

https://datasets.imdbws.com/title.ratings.tsv.gz

https://datasets.imdbws.com/title.principals.tsv.gz


CLEANING THE DATA

•	https://datasets.imdbws.com/title.akas.tsv.gz
o	Decided that this data wasn’t useful and ended up not using it 
•	https://datasets.imdbws.com/title.basics.tsv.gz
o	Removed inappropriate content (adult films “isAdult” column indicates this content)
	Once adult films are removed from the database, we then removed the column “isAdult” as it wasn’t necessary since the remaining values are all not adult content
o	Renamed columns 
	ttconst to titleID
	titleType to Type
o	Replace \N to N/A
o	Final data frame title: title_basics_clean
•	https://datasets.imdbws.com/title.principals.tsv.gz
o	Removed columns
	Ordering
	job
o	Renamed columns
	ttconst to titleID
	nconst to nameID
o	Replace \N to N/A
o	After attempting to insert this database into MongoDB, it would error out due to the size of the data set. To cut this data down to a more manageable dataframe.
o	Final data frame title: title_principals_df_1, title_principals_df_2, title_principals_df_3, andtitle_principals_df_4
•	https://datasets.imdbws.com/title.ratings.tsv.gz
o	Renamed columns
	ttconst to titleID
o	Final data frame title: title_ratings_df
•	https://datasets.imdbws.com/name.basics.tsv.gz
o	Removed columns:	
	birth year
	death year 
o	Replace 
	Replaced \N with N/A then dropped N/A values in “assocTitleID” column
o	Renamed columns
	nconst to nameID
	knowforTitles to assocTitleID
o	Final data frame title: name_basics_df
•	Merged the separate data 
o	Created new data set by merging title_basics_clean and title_ratings_df
o	Final data frame title: merge_title_df
•	Final list of data frames: 
o	merge_title_df
o	name_basics_df
o	title_principals_df_1
o	title_principals_df_2
o	title_principals_df_3
o	title_principals_df_4


CREATING THE DATA BASE ON MONGODB

•	Set up MongoDB connection
•	Used Pandas data frame to insert to MongoDB for each data frame:
o	merge_title_df as titles – took approximately 3 minutes
o	name_basics_df as names – took approximately 5 minutes
o	title_principals_df_1 as principals – took approximately 5 minutes
o	title_principals_df_2 as principals – took approximately 5 minutes
o	title_principals_df_3 as principals – took approximately 5 minutes
o	title_principals_df_4 as principals – took approximately 5 minutes


