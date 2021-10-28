# Final Rose Project
**Team Members:** <br /> 
1. Taylor Cox <br /> 
2. Connor Derrick <br />

**Team Name** : Team Final Rose <br />

**Introduction to Problem or Opportunity** <br /> 
The Bachelor Franchise is one of the largest TV franchises across the globe with over 5 million viewers every week. This has created a community of those who watch the Bachelor, Bachelorette, and Bachelor in Paradise who enjoy exploring the data surrounding people on the show, their growing popularity, and applying predictive analytics to foresee the winners of each season and how the public will react. So, what exactly impacts the winner of a custom engagement ring, $250,000, and popularity among pop culture. To win the above rewards, you must go through 10 weeks of dating the Bachelor/Bachelorette, receive a rose each week to continue the relationship, and receive one ‘Final Rose’ from the lead. While descriptive analytics of the show have taken off in recent years, few have gone so far as to use predictive modeling to forecast winners of the show and that is what we plan to do in this prjoect.

**Research Question(s)** <br /> 

**Main Research Question:** What is the difference in probability of a given contestant being the final rose recipient of a season of The Bachelor or The Bachelorette considering age difference between the given contestant and the season's lead? Using logistic regression on past seasons' data, we will predict the most likely winners of the upcoming season of The Bachelorette, ranking each contestant by their probability of being the winner, and comparing weekly eliminations to our predictions. <br />

Can we predict the likelihood of a given contestant receiving the season’s final rose based on their amount of time spent with the lead calculated by a weighted point system based on the number of dates attended and the number of contestants on each date? <br />

How do factors such as age difference, distance between hometowns, and similarity of occupations between contestants & the lead impact the number of weeks a contestant spends on the show? <br />

**Data Resources** <br /> 
We have obtained datasets from FiveThirtyEight and Kaggle containing contestant information from past seasons of "The Bachelor" and "The Bachelorette". The FiveThirtyEight dataset contains contestant names, weekly elimination/rose data, and weekly date data for seasons 1-13 of "The Bachelorette" and seasons 1-21 of "The Bachelor". The Kaggle dataset contains contestant names, ages, hometowns & weeks of elimination for seasons 1-12 of "The Bachelorette" and seasons 1, 2, 5 & 9-21 of "The Bachelor". The Kaggle dataset also contains the name, age & hometown of show leads for those same seasons. We will webscrape data from the most recent seasons of the shows as well as the one that begins airing this month to utilize as testing set for our model. <br />
FiveThirtyEight Data: https://github.com/fivethirtyeight/data/tree/master/bachelorette <br />
Kaggle Data: https://www.kaggle.com/brianbgonz/the-bachelorette-contestants?select=bachelors.csv <br />

**Data Preprocessing** <br /> 
For our logistic regression to predict the winner of a given season, we decided to primarily use the Kaggle data. Since this data was separated into 4 sets ('Bachelor' leads, 'Bachelorette' leads, 'Bachelor' contestants, & 'Bachelorette' contestants. We needed to do a good amount of data preprocessing to fill in missing values & get all the data sets into a consistent format to be able to be joined into one complete data frame. Due to the nature of this data, we were able to do our own research to identify correct values for missing data rather than using imputation methods that might undermine the validity of our model. <br />

**Data Understanding and Exploration** <br /> 

**Data Preparation for Modeling** <br /> 
Once we built our complete data set, we had to create some calculated columns to be used in our model. <br />
These new variables included: <br />
-Age difference between contestant & lead <br />
-Dummy variables for whether contestant & lead hometowns are in same region <br />
-Dummy variable for whether or not a contestant was the winner of their season <br />

We also plan to perform text mining on occupation variable to create groupings of jobs and some measure of similarity between contestant & lead occupations <br />

**Modeling** <br /> 

**Evaluation** <br /> 

**Results** <br /> 

**Future Work** <br /> 
The next steps include finishing our data preparation for modeling by text mining our occupation data and then moving into the modeling stage of the CRISP-DM process. The primary analysis that we are planning to complete is a logistic regression to predict the likelihood of a given contestant being the winner with age difference between contestant & lead being our primary predictor of interest. If we have time though, we may also conduct a linear regression to predict the number of weeks each contestant will remain on the show before elimination.
