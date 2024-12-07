# playoff-chances
In this project, my goal was to predict the chance of a team making the playoffs in both the current year and the following year. If given a dataset of  player stats, accolades, and various team records, could I predict if a certain team makes the playoffs? Likewise, if given historical data of a team, can I predict if they'll make the playoffs the following year, where I have no knowledge of that year's data?

Methodology:

Download HTML: This is the first file in the project. Since I wanted data from the past 20 years for multiple categories, multiple websites sensed that I was "spam" as I had sent numerous requests. To avoid this, I decided on downloading the webpage's HTML into a folder and then scraping the files in the folder instead. This way, I would not get restricted from sites by sending multiple requests. In 'DownloadHTML', I used Selenium Webdriver to download the website HTML into its respective folders. There are 8 total folders, each containing HTML of the websites for the various stats for the 2000-2022 seasons (passingstats, rushingstats, receivingstats, defense, probowl, playoffs, standings, all-pro)

Scrape_Awards: This file was where I scraped all the awards to use as predictor variables (MVP, Offensive Player of the Year, Defensive Player of the Year, Rookie of the Year, All Pro, Pro Bowl). For this, I used Beautiful Soup to scrape the website "Pro Football Reference". Unlike the other variables I discussed in "Download HTML", I was able to scrape the awards directly from the site because it was only one page of awards, instead of 20+ pages as above. Once I scraped the data, I saved each award into a csv file.

Awards_Records: Once the awards from "Scrape_Awards" were converted into a csv file, I imported them into a new notebook called "Awards_Records". In this file, I created a function that dropped unwanted columns, filtered the 'year' column to be greater than 1999, and uses a dictionary to abbreviate the team name (for example, the row value containing 'Green Bay Packers' gets changed to 'GNB'). Once the individual awards were finalized, I merged them into one dataset which I simply called 'awards'. This merged dataset allowed me to use Seaborn and Matplotlib to perform exploratory data analysis, such as visualizing teams with most MVPs since 2000, most Powbowls per team since 2000, and most AllPros since 2000. The next step was to find the win-loss record and playoff performance for every team. For this, I used the same process of using Beautiful Soup to scrape table data on websites such as ProFootballReference and Wikipedia. 

NFL read rosters: The purpose of this file was to find the starting offensive lineups for each team.

NFL Playoffs player stats: This file was the most important as it is where I created "overall" ratings for a team's quarterback, running backs, wide receivers, and entire defense. To do this, I once again used Beautiful Soup to scrape the HTML from the folders I created earlier. After cleaning the data for all datasets, I created a function called "overall" which accepted a dataframe and particular columns, and found the quantile that particular column was in. This way, I was able to compare players from their respective position and year to other players from those positions and years and quantify how good a player was for a particular season. I chose to do this instead of scraping offensive statistics for a team because in the NFL, individual players can affect the game a lot, especially the quarterback. Team statistics would not be able to quantify how good a particular running back group is as many positions can obtain rushing yards. 

Playoff Prediction This Year: I conducted a Grid Search to optimize the hyperparameters of Random Forest, Gradient Boosting, and XGBoost classifiers to predict the probability of a team making the playoffs this year, based on features such as team accolades, records, and other relevant data. Using the optimized Random Forest model, I achieved a 93% accuracy rate.

Playoff Prediction Next Year: I conducted a Grid Search to optimize the hyperparameters of Random Forest, Gradient Boosting, and XGBoost classifiers to predict the probability of a team making the playoffs in the following year. The prediction was based on features such as the team's previous year's win-loss percentage, player statistics, projected player performance, awards, and playoff performance. Using the optimized XGBoost model, I achieved a 58.6% accuracy rate.

What variables could I not account for?: Firstly, there are 14 total teams that make the playoffs as of 2023, with 7 from each conference. There are 2 conferences in the NFL, with 4 divisions per conference. In each conference, the team with the highest W-L% in each division makes the playoffs, and the remaining 3 'wild-card' teams are those with the highest W-L% from the remaining 12 teams. I was not able to account for this in my model which I believe would have made a significant difference as my model treats all teams as if they are in the same Conference/Division. To improve my accuracy, this is an important aspect to take into account. Furthermore, there were no datasets available to find the Offensive Line rankings. Offensive Lines play an important role in a team's success, and that would have certainly improved my accuracy. Although I hoped for a better prediction for predicting next year's playoffs than 68.8%, we must recognize that aside from the variables I discussed above that were not accounted for, injuries are impossible to account for which significantly affects our model. For example, the Los Angeles Rams won the SuperBowl in 2021, and were highly expected to reach the playoffs again in 2022. However, they suffered many injuries from key players which derailed their season.
