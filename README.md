# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Predicting Home Prices in Ames, IA (Kaggle challenge)

### Contents:
- [Background](#Background)
- [Data](#Data)
- [Summary](#Summary)
- [Conclusions and Recommendations](#Conclusions-and-Recommendations)

## Background

We will examine a housing data set consisting of ~80 variables related to home price in Ames, Iowa. As a member of realty company, we will be helping families get their homes ready to sell. 
The main question we have been tasked with answering is: **What characteristics of a home are most likely to increase the sale price, and what changes can be made to increase sale price before putting a home on the market?** We will try to answer these questions by building a Lasso linear regression model that will allow us to evaluate the strength of different home features on home price.

Additionally, as part of this project we will also use the data set to create a regression model that most accurately predicts the price of houses in Ames, IA and submit our results to a class Kaggle competition.

### Data

This project will analyze the Ames Housing data set compiled by Dean De Cock. This data set, and a description of all 82 features, can be found [`here`](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt). In addition to these features, two other features have been created from the data:
- Total square feet: The sum of the 1st, 2nd, and basement areas.
- Total baths: The total amount of full and half baths in the home.

We will explore if these features have any noticeable affects home prices in Ames, IA. All of these data sets have been cleaned and further detail on the cleaning process can be found in the accompanying iPython Notebooks. 

## Summary

From the raw data alone we can already get a good sense of what features matter most to the price of a home: 

# ![](https://git.generalassemb.ly/jserigano4/project_2/blob/main/figures/corr.png)

The heat map above shows the correlation between Sale Price of a home and all numeric features included in the data set. Overall quality and features related to home size show the strongest correlation to home sale price. 

Notebook 01 includes more details on the extensive data cleaning process involved with this data set. This includes rectifying null values, handling outliers, creating new variables, determining features that exhibit multicollinearity, and (for the Kaggle competition data only) log-transforming certain features in order to input more normally distributed data into our model. 

To address our problem statement, we want to get a sense of the effect that certain characteristics/variables of a house have on the overall sale price. In order to do this, we must standardize the variables in order to  more easily compare the relative strength of the effect they have on sale price.

Since we are interested in what changes can be made to a home to increase sale price, we will only be looking at variables that are capable of being changed by the homeowner. For example, we will not be comparing neighborhoods since the homeowner will not be able to move their house to a different location. Instead, we will be looking at other factors such as the quality of the home, the number of bathrooms, the overall size of the home, etc. The features included in our model are: 'Overall Qual', 'Overall Cond', 'Roof Matl', 'Exter Qual', 'Exter Cond', 'Bsmt Cond', 'BsmtFin Type 1', 'Heating', 'Heating QC', 'Central Air', 'Gr Liv Area', 'Bedroom AbvGr', 'Kitchen Qual', 'Fireplaces', 'Fireplace Qu', 'Garage Finish',  'Garage Area', 'Garage Qual', 'Paved Drive', 'Wood Deck SF', 'Open Porch SF', 'Enclosed Porch','3Ssn Porch', 'Screen Porch', 'Pool Area', 'Pool QC', 'Fence', 'Misc Val', 'Mo Sold','Total Bath', 'Total SF', and 'SalePrice' (our y-value).

To tackle this problem we use a Lasso linear regression model. This is advantageous because a Lasso model adds a penalty term that minimizes the coefficients of some parameters. In lasso regression, the penalty term has the ability to zero out some coefficients, essentially performing feature selection for us. Thus, this is a desirable model to use when we have many different variables.

In the end, our model does a pretty good job at fitting the data. 87.2% of the variance/variability in home sale price in our test data can be explained by the features in our model. Additionally, our model passes the LINEM assumptions associated with linear regression models.

# ![](https://git.generalassemb.ly/jserigano4/project_2/blob/main/figures/resids_scatter.png)

# ![](https://git.generalassemb.ly/jserigano4/project_2/blob/main/figures/resids_hist.png)


## Conclusions and Recommendations

# ![](https://git.generalassemb.ly/jserigano4/project_2/blob/main/figures/coefs.png)

The figure above shows the 20 most important features for home price. We can conclude from our model that the overall size and quality of material and finish of the house are the most important features affecting home price. Three out of the top five strongest correlations to home price relate to the size of the home: Total square feet, total garage area, and ground floor living area. The amount of bathrooms and fireplaces also have a strong affect on home price, with an increase in the number of either feature having a roughly equal effect on home price. 

Additionally, there are some categorical variables in the top 20 features that must be interpreted in the context of what ordinal value was dropped from that feature's list. For both the quality of the material on the home's exterior and the quality of the home's kitchen, the 'Excellent' value was dropped. We can see that having your home listed as anything below 'Excellent' has a very negative impact on home sale price. As seen on the figure, the two features with the strongest negative correlation are when a home's exterior material quality is deemed 'Typical/Average' and when a home's exterior material quality is deemed 'Good' instead of 'Excellent'. Similarly for kitchen quality, 'Typical/Average' and 'Good' ratings have strong negative correlations to price in comparison to a similar home rated as 'Excellent'. 

In conclusion, below are recommended steps that potential home sellers can follow to increase the sale value of their Ames, IA home before placing it on the market:
- Increase total square footage of your home, especially through ground level living space or garage expansion.
- Add more bathrooms or fireplaces to your home. A new bathroom could also increase square footage!
- Increase the quality of your home's exterior. A home with excellent quality exterior material significantly outperforms a home of lesser exterior quality.
- Similarly, increase the quality of your home's kitchen. A home with a kitchen of excellent quality significantly outperforms a home with a kitchen of lower quality. 