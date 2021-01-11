# <center>WeRateDogs Data Analysis Project Report</center>

## Data Gathering

This project contains three dataframes, **first** one is the `twitter-archive-enhanced.csv` file which was downloaded through the course resources.

**The second** dataframe is the `extra_archive` which was obtained with the twitter API `tweepy` by obtaining the authentication with the api tokens, the extra_archive dataframe contained the retweeted counts and the favourite counts. To obtain this file I gatherd all the necessary information and wrote this info to a **txt** file that contained a string dictionary. To read this string dictionary I used the _pd.read_json_ function to read the json file inside the txt file and specified the _lines_ parameter to true to read each line as a separate JSON file.

**The third** dataframe is the `image_predictions` dataframe which contained mainly top 3 predictions for the corresponding dog. This dataframe was obtained with the help of `request` library that requested to download the TSV of the URL that was specified in the function. To read the TSV we needed to specify the **sep** parameter to be _\t_

## Assessing

First of all the `twitter_archive` table, the table was assessed by checking the following: 
- Datatypes with the **info()** found some columns with inaccurate datatypes like timestamp.
- The duplicated rows with **duplicated()**, no duplicated values were found.
- Whether the ids are unique or not with **nunique()**, no duplicated ids were found.
- the NaN values of the in_reply_to_status_id column, i noticed that these rows are actually re-tweets.
- rating_denominator and rating_numerator, which had inconsistent values.
- name values, which had inaccurate values.

The `image_predictions` table, the table was assessed by checking the following:
- the false predictions, some rows had other than dog animals.
- Datatypes with the **info()**.
- The duplicated rows with **duplicated()**.
- the names of the breeds, which were inconsistent.

## Cleaning

`twitter_archive` table.
- the false names were mostly lowercase so names with lowercase were removed.
- ratings contained decimal numbers, the correct numbers were extracted with Regex and were corrected.
- rows with retweets were removed, which had a non-Nan value of retweeted_status_id.
- rating nominator that exceeded 14 were approximated to 14 and the denominator is considered to be 14.
- some columns had no use like  [in_reply_to_status_id, in_reply_to_user_id, retweeted_status_id, retweeted_status_user_id, retweeted_status_timestamp, source] which were dropped.
- expanded_url column which had NaN value were dropped.
- Timestamp datatype was converted to datetime.
- type of dog was merged in one column instead of 4 different columns.


`image_predictions` table.
- rows which had all False prediction were droppped.
- most accurately predicted dog column was extracted and created.
- dog names were corrected by removing the underscore from the names.
- column names need to be edited to indicated description.
