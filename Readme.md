# Lab 7

## Student information

* Full name: Owen Sugiarto
* E-mail: osugi001@ucr.edu
* UCR NetID: osugi001
* Student ID: 8632296300

## Answers

Q1: What is the nesting level of this column root.entities.hashtags.element.text? 

root is at level 0.
.entities is at level 1.
.hashtags is at level 2.
.element indicates an array element but does not add to the nesting levels as specified.
.text is at level 3, following the instructions that element does not add to the nesting levels.


Q2: In Parquet, would this field be stored as a repeated column? Explain your answer.
Yes, this field would be stored as a repeated column in Parquet. The presence of element in the column path suggests that the hashtags field is an array. In Parquet's data model, columns that are part of a nested structure like an array are typically marked as REPEATED to accommodate multiple values per record under the same column path. Since hashtags can contain multiple text entries for each tweet (or whatever entity root represents), the text values within each hashtags array would be stored in a repeated column to capture this one-to-many relationship. Parquet efficiently handles such nested and repeated data structures through its complex type support, allowing for efficient storage and access patterns for nested arrays and structures.

Q3: Based on this schema answer the following:

How many fields does the place column contain?
How many fields does the user column contain?
What is the datatype of the time column?
What is the datatype of the hashtags column?


The place column contains 8 fields:
bounding_box
country
country_code
full_name
id
name
place_type
url


The user column contains 39 fields. This can be determined by counting the individual fields listed under the user struct.


The datatype of the time column is string.


The datatype of the hashtags column is array. More specifically, it is an array of structs (array<struct>), where each struct contains at least the indices and text fields.

Q4: Based on this new schema answer the following:

How many fields does the place column contain?

The place column contains 3 fields: country_code, name, and place_type.
How many fields does the user column contain?

The user column contains 3 fields: followers_count, statuses_count, and id.
What is the datatype of the time column?

The datatype of the time column is timestamp.
What is the datatype of the hashtags column?

The datatype of the hashtags column is an array of string.

Q5: What is the size of each folder? Explain the difference in size, knowing that the two folders tweets.json and tweets.parquet contain the exact same dataframe?
.json file have 2.85 GB, while .parquet have only 647MB
I think the reason why it is so different in size is because, Parquet's efficient use of compression, encoding, and its columnar storage format, which minimizes redundancy and reduces the storage footprint. These optimizations make Parquet highly suitable for storing and processing large datasets in distributed computing environments like Hadoop and Spark.

Q6: What is the error that you see? Why isn't Spark able to write this dataframe in the CSV format?
I think the error that i see is because of spark’s inability of handling complex datatype directly in csv file, 
“Exception in thread "main" org.apache.spark.sql.AnalysisException: [UNSUPPORTED_DATA_TYPE_FOR_DATASOURCE] The CSV datasource doesn't support the column `coordinates` of the type "STRUCT<coordinates: ARRAY<DOUBLE>, type: STRING>".”

indicates that the CSV format does not support the complex data type STRUCT<coordinates: ARRAY<DOUBLE>, type: STRING> for the coordinates column






Q7.1: What do you see in the output? Copy it here.
tweets_1m.json
![Q1-What-is-the-nesting-level-of-this-column-root-Google-Docs](https://github.com/osugi001/CS152/assets/102548267/349c8f5b-1499-4d95-a3d8-2e4578b8c79d)

tweets.json
same with different runtime
tweets.parquet
same with different runtime
(runtime shown below)




Q7.2: What do you observe in terms of run time for each file? Which file is slowest and which is the fastest? Explain your observation?.
tweets_1m.json: 18.8 seconds
tweets.json: 17.38 seconds
tweets.parquet: 7.2 seconds
Observation:

The Parquet file format is the fastest to process.
The JSON files (tweets_1m.json and tweets.json) take longer, with tweets_1m.json being the slowest.
Explanation:

Parquet is a columnar storage format, which makes reading, processing, and querying data much more efficient, especially for analytical queries that only need a subset of columns. This efficiency significantly reduces the processing time.
JSON is a row-based format and stores data in text form. Processing JSON requires parsing the text into a data structure, which is more compute-intensive than reading from a columnar format like Parquet. This makes JSON files slower to process compared to Parquet.
The slight difference in run times between the two JSON files could be due to their size or structure complexity, but they both inherently suffer from the inefficiencies of row-based, text-heavy processing.
In summary, Parquet's design for efficient data storage and access results in faster processing times compared to the text-based JSON format.

Q8.1: What are the top languages that you see? Copy the output here
tweets_1m.json 12.2 seconds
![Q1-What-is-the-nesting-level-of-this-column-root-Google-Docs (1)](https://github.com/osugi001/CS152/assets/102548267/9b6be5ef-aeab-41db-a19b-c8d9a6360378)
tweets.json 10.4 seconds
tweets.parquet 5.6 seconds
again both same values but different run time


Q8.2: Do you also observe the same performance for the different file formats?

Yes same performance.










Q9: After step B.3.2, how did the schema change? What was the effect of the explode function?
Tweets_1m.json

![Q1-What-is-the-nesting-level-of-this-column-root-Google-Docs (1)](https://github.com/osugi001/CS152/assets/102548267/602ca5fe-cb1d-4975-8f89-4b6b022295c8)


| Country | Tweet Count | Lang | Lang Percent |
|---------|-------------|------|--------------|
| US      | 196,740     | en   | 85.95%       |
| US      | 196,740     | und  | 8.66%        |
| US      | 196,740     | es   | 1.4%         |
| US      | 196,740     | tl   | 0.68%        |
| US      | 196,740     | ja   | 0.43%        |
| JP      | 133,690     | ja   | 95.13%       |
| JP      | 133,690     | und  | 1.67%        |
| JP      | 133,690     | en   | 1.56%        |
| JP      | 133,690     | in   | 0.5%         |
| JP      | 133,690     | th   | 0.2%         |
| GB      | 65,130      | en   | 89.22%       |
| GB      | 65,130      | und  | 7.03%        |
| GB      | 65,130      | es   | 0.46%        |
| GB      | 65,130      | fr   | 0.45%        |
| GB      | 65,130      | ar   | 0.4%         |
| PH      | 57,320      | tl   | 50.87%       |
| PH      | 57,320      | en   | 34.91%       |
| PH      | 57,320      | und  | 6.86%        |
| PH      | 57,320      | in   | 2.81%        |
| PH      | 57,320      | es   | 0.82%        |
| BR      | 44,570      | pt   | 87.61%       |
| BR      | 44,570      | und  | 4.71%        |
| BR      | 44,570      | en   | 3.01%        |
| BR      | 44,570      | es   | 2.15%        |
| BR      | 44,570      | it   | 0.52%        |


Operation top-country-with-lang on file './Tweets_1m.json' finished in 20.238104999 seconds

Tweets.json
Schema after step B.3.1:
root
|-- country: string (nullable = true)
|-- tweet_count: long (nullable = false)
|-- top_langs: array (nullable = true)
| |-- element: struct (containsNull = true)
| | |-- _1: string (nullable = true)
| | |-- _2: integer (nullable = false)

Schema after step B.3.2:
root
|-- country: string (nullable = true)
|-- tweet_count: long (nullable = false)
|-- top_langs: struct (nullable = true)
| |-- _1: string (nullable = true)
| |-- _2: integer (nullable = false)

Schema after step B.3.3:
root
|-- country: string (nullable = true)
|-- tweet_count: long (nullable = false)
|-- lang: string (nullable = true)
|-- lang_percent: double (nullable = true)```


| Country | Tweet Count | Lang | Lang Percent |
|---------|-------------|------|--------------|
| US      | 196740      | en   | 85.95        |
| US      | 196740      | und  | 8.66         |
| US      | 196740      | es   | 1.4          |
| US      | 196740      | tl   | 0.68         |
| US      | 196740      | ja   | 0.43         |
| JP      | 133690      | ja   | 95.13        |
| JP      | 133690      | und  | 1.67         |
| JP      | 133690      | en   | 1.56         |
| JP      | 133690      | in   | 0.5          |
| JP      | 133690      | th   | 0.2          |
| GB      | 65130       | en   | 89.22        |
| GB      | 65130       | und  | 7.03         |
| GB      | 65130       | es   | 0.46         |
| GB      | 65130       | fr   | 0.45         |
| GB      | 65130       | ar   | 0.4          |
| PH      | 57320       | tl   | 50.87        |
| PH      | 57320       | en   | 34.91        |
| PH      | 57320       | und  | 6.86         |
| PH      | 57320       | in   | 2.81         |
| PH      | 57320       | es   | 0.82         |
| BR      | 44570       | pt   | 87.61        |
| BR      | 44570       | und  | 4.71         |
| BR      | 44570       | en   | 3.01         |
| BR      | 44570       | es   | 2.15         |
| BR      | 44570       | it   | 0.52         |


Operation top-country-with-lang on file './tweets.json' finished in 27.036789300000002 seconds


lab7-1.0-SNAPSHOT.jar top-country-with-lang ./tweets.parquet
Using Spark master 'local[*]'
Schema after step B.3.1:
Schema after step B.3.1:
root
|-- country: string (nullable = true)
|-- tweet_count: long (nullable = false)
|-- top_langs: array (nullable = true)
| |-- element: struct (containsNull = true)
| | |-- _1: string (nullable = true)
| | |-- _2: integer (nullable = false)

Schema after step B.3.2:
root
|-- country: string (nullable = true)
|-- tweet_count: long (nullable = false)
|-- top_langs: struct (nullable = true)
| |-- _1: string (nullable = true)
| |-- _2: integer (nullable = false)

Schema after step B.3.3:
root
|-- country: string (nullable = true)
|-- tweet_count: long (nullable = false)
|-- lang: string (nullable = true)
|-- lang_percent: double (nullable = true)

| Country | Tweet Count | Lang | Lang Percent |
|---------|-------------|------|--------------|
| US      | 196740      | en   | 85.95        |
| US      | 196740      | und  | 8.66         |
| US      | 196740      | es   | 1.4          |
| US      | 196740      | tl   | 0.68         |
| US      | 196740      | ja   | 0.43         |
| JP      | 133690      | ja   | 95.13        |
| JP      | 133690      | und  | 1.67         |
| JP      | 133690      | en   | 1.56         |
| JP      | 133690      | in   | 0.5          |
| JP      | 133690      | th   | 0.2          |
| GB      | 65130       | en   | 89.22        |
| GB      | 65130       | und  | 7.03         |
| GB      | 65130       | es   | 0.46         |
| GB      | 65130       | fr   | 0.45         |
| GB      | 65130       | ar   | 0.4          |
| PH      | 57320       | tl   | 50.87        |
| PH      | 57320       | en   | 34.91        |
| PH      | 57320       | und  | 6.86         |
| PH      | 57320       | in   | 2.81         |
| PH      | 57320       | es   | 0.82         |
| BR      | 44570       | pt   | 87.61        |
| BR      | 44570       | und  | 4.71         |
| BR      | 44570       | en   | 3.01         |
| BR      | 44570       | es   | 2.15         |
| BR      | 44570       | it   | 0.52         |


Operation top-country-with-lang on file './tweets.parquet' finished in 10.391 seconds

Q10: For the country with the most tweets, what is the fifth most used language? Also, copy the entire output table here.

Look at Q9

Q11: Does the observed statistical value show a strong correlation between the two columns? Note: a value close to 1 or -1 means there is high correlation, but a value that is close to 0 means there is no correlation.

The observed statistical value for the correlation between a user's statuses_count and their followers_count is approximately 0.66. This value indicates a moderate positive correlation between the number of statuses a user posts and the number of followers they have.

Q12.1: What are the top 10 hashtags? Copy paste your output here.
![Q1-What-is-the-nesting-level-of-this-column-root-Google-Docs (2)](https://github.com/osugi001/CS152/assets/102548267/1137a098-9d43-43a6-a6d3-2ef94b9eb181)
runtime 28.4 seconds
for tweets.parquet is 12.5 seconds.

Q12.2: For this operation, do you observe difference in performance when comparing the two different input files tweets.json and tweets.parquet?
Yes the first was slower while the second one was faster 2x

table = 
| Command               | Tweets_1m.json | tweets.json | tweets.parquet |
|-----------------------|----------------|-------------|----------------|
| top-country           | 18.8           | 17.3        | 7.2            |
| top-lang              | 12.2           | 10.4        | 5.6            |
| top-country-with-lang | 20.2           | 27.0        | 10.4           |
| corr                  | 9.2            | 9.1         | 7.5            |
| top-hashtags          | N/A            | 28.4        | 12.5           |


Run.sh = 
spark-submit --master "local[*]" --class edu.ucr.cs.cs167.osugi001.PreprocessTweets ./target/osugi001_lab7-1.0-SNAPSHOT.jar ./Tweets_1m.json

spark-submit --master "local[*]" --class edu.ucr.cs.cs167.osugi001.AnalyzeTweets ./target/osugi001_lab7-1.0-SNAPSHOT.jar top-lang ./Tweets_1m.json
spark-submit --master "local[*]" --class edu.ucr.cs.cs167.osugi001.AnalyzeTweets ./target/osugi001_lab7-1.0-SNAPSHOT.jar top-lang ./tweets.json
spark-submit --master "local[*]" --class edu.ucr.cs.cs167.osugi001.AnalyzeTweets ./target/osugi001_lab7-1.0-SNAPSHOT.jar top-lang ./tweets.parquet


spark-submit --master "local[*]" --class edu.ucr.cs.cs167.osugi001.AnalyzeTweets ./target/osugi001_lab7-1.0-SNAPSHOT.jar top-country-with-lang ./Tweets_1m.json
spark-submit --master "local[*]" --class edu.ucr.cs.cs167.osugi001.AnalyzeTweets ./target/osugi001_lab7-1.0-SNAPSHOT.jar top-country-with-lang ./tweets.json
spark-submit --master "local[*]" --class edu.ucr.cs.cs167.osugi001.AnalyzeTweets ./target/osugi001_lab7-1.0-SNAPSHOT.jar top-country-with-lang ./tweets.parquet


spark-submit --master "local[*]" --class edu.ucr.cs.cs167.osugi001.AnalyzeTweets ./target/osugi001_lab7-1.0-SNAPSHOT.jar top-country-with-lang ./Tweets_1m.json
spark-submit --master "local[*]" --class edu.ucr.cs.cs167.osugi001.AnalyzeTweets ./target/osugi001_lab7-1.0-SNAPSHOT.jar top-country-with-lang ./tweets.json
spark-submit --master "local[*]" --class edu.ucr.cs.cs167.osugi001.AnalyzeTweets ./target/osugi001_lab7-1.0-SNAPSHOT.jar top-country-with-lang ./tweets.parquet


spark-submit --master "local[*]" --class edu.ucr.cs.cs167.osugi001.AnalyzeTweets ./target/osugi001_lab7-1.0-SNAPSHOT.jar corr ./Tweets_1m.json
spark-submit --master "local[*]" --class edu.ucr.cs.cs167.osugi001.AnalyzeTweets ./target/osugi001_lab7-1.0-SNAPSHOT.jar corr ./tweets.json
spark-submit --master "local[*]" --class edu.ucr.cs.cs167.osugi001.AnalyzeTweets ./target/osugi001_lab7-1.0-SNAPSHOT.jar corr ./tweets.parquet


spark-submit --master "local[*]" --class edu.ucr.cs.cs167.osugi001.AnalyzeTweets ./target/osugi001_lab7-1.0-SNAPSHOT.jar top-hashtags ./tweets.json
spark-submit --master "local[*]" --class edu.ucr.cs.cs167.osugi001.AnalyzeTweets ./target/osugi001_lab7-1.0-SNAPSHOT.jar top-hashtags ./tweets.parquet



