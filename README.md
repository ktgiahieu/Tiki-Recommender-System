# Tiki-Recommender-System

_Author: Hieu Khuong_

-------
### Table of Contents
[Web Scraping Notebook](TikiScraper.ipynb)  
[Data Cleaning Notebook](TikiDataCleaning.ipynb)  
[Feature Engineering & Recommender Model](TikiRecommender.ipynb)

## Executive Summary

**Problem Statement**

The world of retail is changing at a rapid pace.  Many brick and mortar locations are closing and being replaced by online stores.  However, while the breadth of assortment that comes with shopping online is something that drives customers to a website, a lot of eCommerce platforms fail to sell through a high percent of their merchandise.  This is often due to a poor user browsing experience. Customers can spend hours scrolling through hundreds, sometimes thousands of items of merchandise never finding an item they want to buy.  

#### Project Goal
This goal of this project is to create both content-based and collaborative user- and item-based recommender systems, that will help solve this problem. Customers should be provided suggestions based on their likes and needs in order to create a better shopping environment that boosts sales and increases their time spent on a website. 

#### Data Source

Since TIKI does not granted permission to its OpenAPI (except for sellers and co-operator), I have to scrape all the most relevant data on the web page [tiki.vn](https://tiki.vn). Details can be found in [this notebook](TikiScraper.ipynb)  

#### Data Cleaning
[Data Cleaning Notebook](TikiDataCleaning.ipynb)  
The data consists of many unrelevant information and NaNs. Therefore, I have drop multiple columns and only keep useful features.
For the products' info dataset, I have extracted the whole description using BeautifulSoup and then tokenizing it with PyVi for Vietnamese language.
For the products' review dataset, I have extracted the user's info using BeautifulSoup, including their full names, purchase time, comment time, etc.
All timestamp provided are converted into Datetime format for further investigation.

#### Modeling
[Feature Engineering & Recommender Model](TikiRecommender.ipynb)
4 different learning regressors (Linear Regression, SVM, Random Forest, and Gradient Boosting) were tested, and I have achieved the best prediction performance using SVM. Therefore, the recommender system are going to use Support Vector Machine for recommendation for each user using their IDs.

The best prediction performance was achieved with a SVM, using part of the features in the dataset, and resulted in the following metrics:

* Mean Absolute Error (MAE): 0.552
* Root mean squared error (RMSE): 1.103

#### Conclusion
I have created a model using data scraped from TIKI website with the help of BeautifulSoup to train, deploy the final model. The deployment of the model is in development.

