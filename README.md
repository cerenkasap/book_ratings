# Predict Book Ratings 📚: Project Overview

Created a tool that can estimate the book ratings **(Mean Absolute Error - 0.21)** to help bibliophiles to predict the average book ratings when it comes to pick next book to read.

Pulled over **11123 books** from Kaggle using pandas and opendatasets libraries in python.

Applied **Linear Regression** and **Random Forest Regression** and optimized using **RandomGridSearchCV** to find the best model.

Built a client facing API using **flask.**

### Code Used

Python version: *Python 3.7.11* 

Packages: *pandas, opendatasets, seaborn, matplotlib, numpy, nltk, wordcloud, pickle, flask, json*

For Web Framework Requirements: *pip install -r requirements.txt*


### Resources Used

[The dataset from Kaggle](https://www.kaggle.com/jealousleopard/goodreadsbooks)

[How to download Kaggle datasets to Jupyter notebook guide](https://www.analyticsvidhya.com/blog/2021/04/how-to-download-kaggle-datasets-using-jupyter-notebook/)

[Language code table](https://iso639-3.sil.org/code_tables/639/data)

[Flask productionization](https://towardsdatascience.com/productionize-a-machine-learning-model-with-flask-and-heroku-8201260503d2)

[Instructions for Git LFS](https://git-lfs.github.com)

[Cheatsheet for Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)


## Data Collection
Used Kaggle to pull the datasets 11123 books with 12 columns:
* bookID              
* title                
* authors             
* average_rating      
* isbn                
* isbn13              
* language_code      
* num_pages         
* ratings_count      
* text_reviews_count  
* publication_date    
* publisher 


## Data Cleaning

After pulling the data, I cleaned up the dataset to be ready to use for the model. The changes were made follows:

Pulled years from publication_date column and created publication_year column.
Calculated age of each book by substracting the publication year by 2022 (current year we are in).
Dropped isbn column since we have isbn13 column.
Changed language codes with their full name and merged English based ones (e.g. en-ca, en-us etc.) to English.


## Exploratory Data Analysis

Visualized the cleaned data to see the trends and correlation between attributes and check if there is any outliers.

Created *Bar graphs, Box plots, Scatter plot, and Heat map * for **numerical** variables.
![alt text](https://github.com/cerenkasap/book_ratings/blob/master/images/ratings.png "Number of books each rating received")
data:image/png;base64,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
![alt text](https://github.com/cerenkasap/book_ratings/blob/master/images/num_pages.png "Number of Pages")

![alt text](https://github.com/cerenkasap/book_ratings/blob/master/images/coef.png "Heat map for numerical variables ")

Created *Pie Chart and WordCloud* for **categorical** variables.
![alt text](https://github.com/cerenkasap/book_ratings/blob/master/images/languages_piechart.png "Pie chart for languagues")
![alt text](https://github.com/cerenkasap/book_ratings/blob/master/images/wordcloud.png "Word Cloud for authors")

## Model Building

## Model Performance Evalution

## Productionization

### Notes



