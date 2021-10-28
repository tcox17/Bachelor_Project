## Testing Dataset

The testing data was created by web scraping for all necessary data on Season 17 and 18; the two most recent season.

* **Season 17** stars Katie Thurston and ran from June 7, 2021 - August 9, 2021. This season will allow us to test our model with a full testing set using the most recent data from the most recent season. We will be able to run our full model and guage accuracy on a full season.

* **Season 18** stars Michelle Young and premiered on October 19, 2021. This season is expected to run through January of 2022, so we will not be able to complete a full model during the project window. This data allows our model to have a live, week by week prediction and improvement techniques in real time.

Following the CRISP-DM process, we will evaluate our model on Katie's season and deploy the model on Michelle's season.

### Files in this Folder

1. *Season 17 (Test Data Full) and Season17.csv*

     This file is the creation of the season 17 dataset. The original CSV was derived from the Web Scraping notebook. Here, we created the variables 'Region', 'Age Difference', and created all columns for lead information. From here, I exported the dataframe to the final CSV file.     

2. *Season 18 (Test Data) and Season18.csv*

     This notebook contains all information relation to season 18 of the Bachelorette. Here, I used a different technique in manually webscraping the information since there was no good format for Python to pull the data. This was done by creating lists of all data and combining into a final dataframe. I then added all lead information, region, and age difference. This turned into the final CSV dataset.     
     
3. *Web Scraping*
     
     The Web Scraping notebook used BeautifulSoup and Requests to pull all contestant data from an online table and create a dataframe with those values. From here, manual cleaning and updating was done to create the working csv for season 17.
