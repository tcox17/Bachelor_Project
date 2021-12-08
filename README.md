# Final Rose Project
**Team Members:** <br /> 
1. Taylor Cox <br /> 
2. Connor Derrick <br />

**Team Name** : Team Final Rose <br />

**Introduction to Problem or Opportunity** <br /> 
The Bachelor Franchise is one of the largest TV franchises across the globe with over 5 million viewers every week. This has created a community of those who watch the Bachelor, Bachelorette, and Bachelor in Paradise who enjoy exploring the data surrounding people on the show, their growing popularity, and applying predictive analytics to foresee the winners of each season and how the public will react. So, what exactly impacts the winner of a custom engagement ring, $250,000, and popularity among pop culture. To win the above rewards, you must go through 10 weeks of dating the Bachelor/Bachelorette, receive a rose each week to continue the relationship, and receive one ‘Final Rose’ from the lead. While descriptive analytics of the show have taken off in recent years, few have gone so far as to use predictive modeling to forecast winners of the show and that is what we plan to do in this prjoect.

**Research Question(s)** <br /> 

*Main Research Question:* <br />
What is the difference in probability of a given contestant being the final rose recipient of a season of The Bachelor or The Bachelorette considering age difference between the given contestant and the season's lead? Using logistic regression on past seasons' data, we will predict the most likely winners of the upcoming season of The Bachelorette, ranking each contestant by their probability of being the winner, and comparing weekly eliminations to our predictions. <br />

*Questions to consider for future research:* <br />
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
*Sex* - Dummy variable indicating sex - 0 if female, 1 if male (essentially a binary differentiatior between Bachelor & Bachelorette contestants) <br />
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
*Age Sex Interaction* - Product of Age & Sex variables <br />
*Target* - The predictor variable - 0 if eliminated, 1 if winner <br />

We have also completed exploratory data analysis on both our inital data sources prior to transformation & our combined data set. Our EDA process & data visualizations can be seen in the Final Rose Project.ipynb file. <br />

-----
The density curves below show the age distributions of contestants on The Bachelor (pink graph) and The Bachelorette (blue graph). The distribution of contestant ages on both shows appear to follow roughly the same curve with a right skew, but the Bachelorette contestant curve is centered approximately 3 years higher than the Bachelor contestant curve. <br />

<img width="299" alt="image" src="https://user-images.githubusercontent.com/89612682/142284922-fc0329d6-cd49-4f13-b4a8-32889da2a829.png">

-----
The plot below shows the ages of each lead of The Bachelor (blue dots) and The Bachelorette (pink dots). The ages of the female Bachelorette leads are pretty closely clustered on the low end (ranging from about 25-30) while the ages of the male Bachelor leads are more spread out and reaching higher (26-38 years of age). Based on the differences that we observed in the ages of leads & contestants of both shows, we felt even more strongly about using the absolute value of age difference between contestant & lead in our model rather than the raw age values. <br />

<img width="347" alt="image" src="https://user-images.githubusercontent.com/89612682/142284968-9b5ee5a5-6dc8-4af9-8b83-c14511f6d703.png">

-----
The below map displays the density of hometowns for all Bachelor contestants. We can see that a majority of contestants come from California and Texas. We will use location as a variable in relation to US regions and how distance may effect winners.

<img height = '250' alt = 'image' src='https://user-images.githubusercontent.com/89612584/145270681-97c5b986-7d5c-48ba-8a47-0a5c62196ac7.png'>

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
* Dummy variable for sex of contestant
* Interaction term between age & sex of contestant <br />

**Modeling** <br /> 
To predict the likeliness of a given contestant winning a season, we used a logistic regression algorithm trained with season 1,2,5 & 9-21 of The Bachelor & seasons 1-12 of The Bachelorette. Due to the nature of our target variable (predicting the lone winner out of approximately 30 contestants each season), we also needed to rebalance our training data in order to best prepare our model. We tested the process on multiple levels of rebalancing from 25% positive values up to a 50/50 split and ultimately decided on rebalancing the data to have 30% of our training data be positive target results. <br />

While working through the best parameters for our model, we tested its performance on season 17 which is the most recent, fully completed season. The final set of independent variables used in our model included contestant age, age difference, same region, & an interaction term between age & sex. Finally, we deployed the model on season 18, which is actively airing. Though we do not know the official winner yet, it will be interesting to see how well our model applies to this season. 

**Evaluation** <br /> 


**Conclusion** <br /> 


*Future Work* <br /> 
While we did not achieve great success in predicting the winner of the Bachelor or Bachelorette based entirely on information that is available prior to the start of the season, there are multiple opportunities for our project to be improved & expanded upon. Due to our limited experience with text analytics, we were not able to extract any usuable information out of the occupation attribute (which is typically available prior to the airing of the show). However, it would be an interesting project to write some sort of algorithm to categorize the occupation data and/or be able to analyze the level of similarity between the contestants' occupations & that of the lead. <br />

Another approach would be to not put so much emphasis on predicting the winner from the very first week, but create an algorithm that could be updated each week with the probability of each remaining contestant being the winner. Possible attributes to include in this model include a measure of quality time spent with the lead based on the number of dates attended & the number of other contestants on each of those dates and some variable regarding the order in which the roses were handed out each week.

One other variable that we did not include due to a lack of historical data and ethical concerns was race of the contestants & leads. This has been a hot topic within the Bachelor community recently due to a significant underrepresentation of minorities in both contestant & lead roles. However, the show has made efforts to be more inclusive and it will be interesting to see how this progresses in years to come. <br />

*Instructions for Use:* <br />
1. Download the 'bachelors.csv', 'bachelorettes.csv', 'bachelor-contestants.csv', & 'bachelorette-contestants.csv' files from the Original Datasets folder.
2. Download 'Final Rose Project.ipynb' from the code folder. 
3. Make sure all documents are in the same directory in order to successfully run the Python notebook.
