# Amazon_Vine_Analysis

## Overview of Project 

### Purpose

The purpose of this project is to analyze Amazon reviews for a product (chosen from a dataset), some of which may have been given by members of the paid Amazon Vine program.\
This is performed by choosing a dataset from AWS's S3, and exctracting it in PySpark. A table/dataframe of the reviews is created, called vine_df. This dataset is then analyzed to determine if any bias exists towards favorable reviews from Vine members in the dataset chosen.

### Resources used
- Data : https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Books_v1_02.tsv.gz

- Software : Google Colab, Spark 3.1.2

## Results
The dataset chosen were reviews of books. The dataset was extracted into a Google Colab notebook named Vine_Review_Analysis.\
The vine_table dataframe was created with the following columns:\
review_id\
star_rating\
helpful_votes\
total_votes\
vine\
verified_purchase

The above table was then filtered to only contain rows that had reviews that got 20 or more number of total_votes, so as to have a higher likelihood of picking helpful reviews.\
This table was further refined to only contain rows where the helpful_votes make up at least 50% of the total_votes.\
This refined table was then divided into two more tables as defined below,\
vine_paid -> table that contains reviews written as part of the paid Vine program.\
vine_unpaid -> table that contains reviews not part of the Vine program.

Analysis was then performed to answer the following questions: 

#### How many Vine reviews and non_Vine reviews were there?

For this particular dataset, observe that all the reviews from refined dataframe (where helpful votes were made up at least half of the total votes) are from non-members of the Vine program.

![paid_reviews](https://user-images.githubusercontent.com/71800628/128531886-3ba8750e-9da7-4591-8970-544d105ed2e8.png)

The picture above shows that there is no data in the table filtered to have reviews from only Vine-members.

![unpaid_reviews](https://user-images.githubusercontent.com/71800628/128531988-a355f381-ba89-434e-a005-c4118db67653.png)

The picture above shows the reviews from non-members of Vine, or unpaid users.

#### How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?

The following analysis was performed, as shown in the picture below:

![unpaid-5-star-reviews](https://user-images.githubusercontent.com/71800628/128532099-826589ff-6ee7-4e6d-9d8f-55a0cc693510.png)

Observe that the total number of reviews of the refined dataframe (403,807) is equal to the total number of non-Vine reviews, confirming again that this particular dataset did not contain any reviews from Vine-members that may be considered helpful.

From the total number of non-Vine reviews (403, 807), about 242,889 reviews were 5-stars.\
There obviously are no 5-stars Vine reviews.

#### What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?

The 5-stars non-Vine reviews comprised 60.1% of the total reviews.\
The non-Vine reviews comprised 0% of the total reviews. 

## Summary
As this dataset contains helpful reviews from only users that are not members of the Vine program, it can be confidently stated that there is no positivity bias here for reviews from the Vine program.\
This could be because most of the books reviewed here may not have been sent to Amazon Vine members.

#### Provide one additional analysis that you could do with the dataset to support your statement.

An additional analysis was performed to support the above statement. The original dataset, as downloaded from the webite was filtered for reviews from Vine members (as seen in the pictures below) to see how many of the books were actually reviewed by Vine members.

![original_df](https://user-images.githubusercontent.com/71800628/128532154-24229a48-eca3-480d-bb94-463044c0f24e.png)

The above is the first 20 rows of the dataframe created from the dataset originally obtained from amazon cloud services.

![check_for_vine_reviews](https://user-images.githubusercontent.com/71800628/128532206-64e149d1-a87b-4c3a-b847-0ff2f2415fc6.png)

The above gives the total number of reviews from Vine-members.

We note that there are only two reviews from Vine-members in the whole dataset. Moreover these two reviews had very low total votes (3 and 6), and therefore they were eliminated in the beginning when the dataset to be analysed was filtered to contain only those reviews that had 20 or more votes. 

### Note:
The dataset used in the above analysis is the one that was transformed into DataFrames, and loaded into tables in pgAdmin. I chose not to pick any other data set after analysis showed that it contained no helpful reviews from Amazon Vine members because one should be able to address any general question given any real world dataset in contrast to choosing datasets that align with the questions asked i.e. pick a dataset ,and then ask questions about it, rather than pick the questions, and then choose the datasets later.\
However, if there were reviews from Amazon Vine members present here, then the process to determine presence of bias towards favorable reviews would be to calculate the number, and percentage of 5-star reviews from Amazon Vine members. Then compare this with the percentage of 5-star reviews from the non-members of the Vine program.\
A further analysis would be to calculate the number, and percentage of bad reviews ( 2-stars or less) from members, and non-members of the Vine program, and check if they are  lower for Vine-members.

 


