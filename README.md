# Predict Book Ratings 📚: Project Overview

Created a tool that can estimate the book ratings **(Mean Absolute Error - 0.21)** to help bibliophiles to predict the average book ratings when it comes to picking the next book to read.

Pulled over **11123 books** from Kaggle using pandas and opendatasets libraries in python.

Applied **Linear Regression** and **Random Forest Regression** and optimized using **RandomGridSearchCV** to find the best model.

Built a client-facing API using **flask.**

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

* Pulled years from publication_date column and created publication_year column.
* Calculated age of each book by substracting the publication year by 2022 (the current year we are in).
* Dropped ISBN column since we have the isbn13 column.
* Changed language codes with their full name and merged English-based ones (e.g. en-ca, en-us, etc.) to English.


## Exploratory Data Analysis

Visualized the cleaned data to see the trends and correlation between attributes and check if there is any outliers.

* Created *Bar graphs, Box plots, Scatter plot, and Heat map * for **numerical** variables.
![alt text](https://github.com/cerenkasap/book_ratings/blob/master/images/ratings.png "Number of books each rating received")
![alt text](https://github.com/cerenkasap/book_ratings/blob/master/images/num_pages.png "Number of Pages")
![alt text](https://github.com/cerenkasap/book_ratings/blob/master/images/coef.png "Heat map for numerical variables ")

* Created *Pie Chart and WordCloud* for **categorical** variables.
![alt text](https://github.com/cerenkasap/book_ratings/blob/master/images/languages_piechart.png "Pie chart for languagues")
![alt text](https://github.com/cerenkasap/book_ratings/blob/master/images/wordcloud.png "Word Cloud for authors")
## Model Building

Categorical variables were transformed: 
* **language** variable transformed to a dummy variable.
* **authors, title, and publisher** variables were encoded.

Data were split into **train (80%)** and **test (20%)** sets.

I used two models *(Linear Regression and Random Forest Regression)* to predict book ratings and evaluated them by using *MAE (Mean Absolute Error)*.

![alt text](https://github.com/cerenkasap/book_ratings/blob/master/images/Linear_Reg_Model.png "Linear Regression Model")
![alt text](https://github.com/cerenkasap/book_ratings/blob/master/images/Linear_Reg.png "Linear Regression Model")

![alt text](https://github.com/cerenkasap/book_ratings/blob/master/images/Random_Forest_Model.png "Random Forest Regression Model")
![alt text](https://github.com/cerenkasap/book_ratings/blob/master/images/Random_Forest.png "Random Forest Regression Model")

## Model Performance Evaluation
The Random Forest Regression model performed better than the Linear Regression model in this project.

|Linear Regression |Train  |Test |                      
| -------------    |:-----:| ---:|                      
|MSE               |0.122  |0.098|
|R^2               |0.042  |0.008|
|MAE               |0.228  |0.223|
|RMSE              |0.350  |0.313|

|Random Forest Regression |Train  |Test  |
| -------------           |:-----:| ----:|
|MSE                      |0.014  |0.101 |
|R^2                      |0.888  |-0.019|
|MAE                      |0.079  |0.210 |
|RMSE                     |0.120  |0.318 |


## Productionization
The flask API endpoint was built and hosted on a local server (web), it takes in a request and predicts a book rating. 

### Notes
My model was over 100 MB which GitHub doesn't support any file over 100MB. 
I tried [this method](https://stackoverflow.com/a/70765999) and it worked for me, attaching for future reference.

Thanks :) 


