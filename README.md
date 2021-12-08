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
For our logistic regression to predict the winner of a given season, we decided to primarily use the Kaggle data. Since this data was separated into 4 sets ('Bachelor' leads, 'Bachelorette' leads, 'Bachelor' contestants, & 'Bachelorette' contestants. We needed to do a good amount of data preprocessing to fill in missing values & get all the data sets into a consistent format to be able to be joined into one complete data frame. Due to the nature of this data, we were able to do our own research to identify correct values for missing data rather than using imputation methods that might undermine the validity of our model. The steps taken in our data preprocessing are described & can be followed in the Final Rose Project.ipynb file. <br />

**Data Understanding and Exploration** <br /> 

All datasets use the same explanatory variables to predict the likeliness of a certain contestant being a winner. The variables in our datasets can be seen in the dictionary below.

*Name* - The name column refers to the Contestant Name <br />
*Age* - Age refers to the age of the contestant <br />
*Occupation* - Occupation is what the individual contestant's report as their occupations when they join the show <br />
*City* - Hometown city for contestants <br />
*State* - Hometown state for contestants <br />
*Region* - Hometown region based on the US Census Bureau <br />
*Elim Week* - The week of elimination for each contestant. If the value is null, that contestant won <br />
*Season ID* - The combination of the name of the show (either Bachelor or Bachelorette) and season number <br />
*Lead Name* - Name of the Bachelor/Bachelorette <br />
*Lead Age* - Bachelor/Bachelorette age at the time of filming <br />
*Lead Occupation* - Occupation of the lead as reported by the lead at the beginning of the season <br />
*Lead City* - Hometown city for the Bachelor/Bachelorette <br />
*Lead State* - Hometown state for the Bachelor/Bachelorette <br />
*Lead Region* - Lead's hometown region based on the US Census Bureau <br />
*Age Difference* - The absolute value of the difference between the lead's and individual contestant's ages <br />
*Same Region* - Dummy variable to determine if the lead and the contestant are from the same region - 0 if different, 1 if same <br />
*Target* - The predictor variable - 0 if eliminated, 1 if winner <br />

We have also completed exploratory data analysis on both our inital data sources prior to transformation & our combined data set. Our EDA process & data visualizations can be seen in the Final Rose Project.ipynb file. <br />

-----
The density curves below show the age distributions of contestants on The Bachelor (pink graph) and The Bachelorette (blue graph). The distribution of contestant ages on both shows appear to follow roughly the same curve with a right skew, but the Bachelorette contestant curve is centered approximately 3 years higher than the Bachelor contestant curve. <br />

<img width="299" alt="image" src="https://user-images.githubusercontent.com/89612682/142284922-fc0329d6-cd49-4f13-b4a8-32889da2a829.png">

-----
The plot below shows the ages of each lead of The Bachelor (blue dots) and The Bachelorette (pink dots). The ages of the female Bachelorette leads are pretty closely clustered on the low end (ranging from about 25-30) while the ages of the male Bachelor leads are more spread out and reaching higher (26-38 years of age). Based on the differences that we observed in the ages of leads & contestants of both shows, we felt even more strongly about using the absolute value of age difference between contestant & lead in our model rather than the raw age values. <br />

<img width="347" alt="image" src="https://user-images.githubusercontent.com/89612682/142284968-9b5ee5a5-6dc8-4af9-8b83-c14511f6d703.png">

-----
The below map displays the density of hometowns for all Bachelor contestants. We can see that a majority of contestants come from California and Texas. 

<img width = '352' alt = 'image' src='https://user-images.githubusercontent.com/89612584/145270681-97c5b986-7d5c-48ba-8a47-0a5c62196ac7.png'>

-----
Since we plan to do text mining on the occupation attribute of our contestants, we created the word cloud shown below to get some preliminary insights into what common groupings & categories may exist within this data. A few possible categories that jump out from this word cloud include business, education, and sales. 

<img width="332" alt="image" src="https://user-images.githubusercontent.com/89612682/142285139-82e874e6-92af-4406-b0f5-ea8612c9e4f0.png">

-----

**Data Preparation for Modeling** <br /> 
Once we built our complete data set, we had to create some calculated columns to be used in our model. <br />
These new variables included:

* Age difference between contestant & lead   
* Dummy variables for whether contestant & lead hometowns are in same region  
* Dummy variable for whether or not a contestant was the winner of their season  

We also plan to perform text mining on occupation variable to create groupings of jobs and some measure of similarity between contestant & lead occupations <br />

**Modeling** <br /> 
To predict the likeliness of a given contestant winning a season, we used a logistic regression algorithm trained with previous seasons, tested on season 17, and deployed on season 18, the most recent season. The independent variables used were age, age difference, same region, and an interaction term between age and gender. 

**Evaluation** <br /> 

**Results** <br /> 

**Future Work** <br /> 
The next steps include finishing our data preparation for modeling by text mining our occupation data and then moving into the modeling stage of the CRISP-DM process. The primary analysis that we are planning to complete is a logistic regression to predict the likelihood of a given contestant being the winner with age difference between contestant & lead being our primary predictor of interest. If we have time though, we may also conduct a linear regression to predict the number of weeks each contestant will remain on the show before elimination.
