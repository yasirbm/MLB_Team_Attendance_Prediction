Orioles Attendance Prediction – Model Card
Basic Information
•	Persons involved in developing model: Yasir Mohammad - yasir@gwu.edu
•	Model date: November, 2021
•	Model version: 1.0
•	License: MIT License
•	Model implementation code:
o	Python Model: Please click here
Intended Use
•	Primary intended uses: This model is intended to predict attendance for 2022 home games played by the Baltimore Orioles
Data Source & Data Dictionary:
•	Please click here
•	How training data was split: 80% training, 20% test
Model Details
•	Columns used as inputs in the final model:
#	Independent Variable	Variable from original dataset?	Description of Variable
1	Jun	Yes	Game played in June (Y/N)
2	Day.1_Mon	No	Game played on a Monday (Y/N)
3	Day.1_Tue	No	Game played on a Tuesday (Y/N)
4	Day.1_Wed	No	Game played on a Wednesday (Y/N)
5	Day.1_Thu	No	Game played on a Thursday (Y/N)
6	SAT.	Yes	Game played on a Saturday (Y/N)
7	Day.1_Sun	No	Game played on a Sunday (Y/N)
8	NIGHT	Yes	Game played after 6pm (Y/N)
9	Opening Day	Yes	Opening day of the season (Y/N)
10	Holiday (Memorial Day/4th of July)	Yes	Game played on a holiday (Y/N)
11	Promo_yn	No	Promotion for the game (Y/N)
12	Bobblehead	Yes	Promotion was a bobblehead (Y/N)
13	NYY	Yes	Game was against Yankees (Y/N)
14	WSH	Yes	Game was against Nationals (Y/N)
15	BOS	Yes	Game was against Boston Red Sox (Y/N)
16	Interleague	Yes	Game was an interleague game (Y/N)

•	Columns used as targets in the final model: ATTENDANCE
•	Type of Model: Multiple Regression
•	Software used to train the Model: Python v3.8.8
•	Metrics used to evaluate the model and final figures:
o	R Squared: 0.923
o	Adjusted R Squared: 0.919
Part A1: Initial Model 
Data Exploration:
After importing the data on Python, I ran a few basic functions to get a better understanding of the data, data-types, null values etc. I found that a few things would need to be tackled before I was able to run an initial model for Part A1. These included:
•	Turning time into a numerical variable
•	Turning day of the week into multiple categorical variables
•	Extracting temperature from the ‘weather’ variable
Data Visualizations:
After cleaning the data and getting it in a shape where its ready for further analysis, I ran some basic visualizations. Some were on Python, and some on Tableau.
Independent Variable Histograms (Python): 
 







Correlation Heatmap (Python):
 
The above plot gives us a good base to understand which factors correlate more strongly with attendance, so we know which to focus on for the model
 
We compare the distribution of attendance for games against the Yankees, Red Sox and the Nationals. We see that Yankees are the most popular from the 3 in terms of the mean, although Red Sox have a higher ‘maximum’ value. 
 
As we can see from the plot above, whilst Saturday’s are the most popular games in terms of attendance, Fridays and Sundays are not too far behind. Hence, we should account for these days in our model too (not just Saturdays). 
Initial Model:
After splitting the data into training and testing data (80:20 split), I ran the initial model and got an R Squared score of 0.480. The table can be found below. This score can certainly be improved, which will be the focus of Part A2. 
 
Part A2: Improving the Model
Omitting variables with high p values and with multicollinearity:
I first calculated the Variance Inflation Factor (VIF) scores for all of the independent variables to detect which of these variables are exhibiting high levels of multicollinearity. The VIF scores can be seen below: 
 
With the general rule being a VIF score above 4 generally indicates multicollinearity, I removed a few variables (timenum, temp and Day.1_Sat). Some of these also happen to have had high p-values. After removing them, all VIF scores were below 4 and all p values were below 0.05.
After re-running the model, with these changes, the R Squared score improved to 0.866.
 
 Removing Outliers:
I tested for any outliers and found that there were no instances of data points being outside 3 standard deviations. In fact, there weren’t even any instances outside 2.5 standard deviations. Hence, I decided not to remove any instances that may be considered ‘moderate outliers’. 
Adding Variables:
I added 2 new variables to the model:
1.	promo_yn: a variable that indicates whether there was a promotion on or not for a given game)
2.	bad_weather_yn: a variable that indicates whether the weather conditions of that game were ‘bad’ (amongst the lowest 10 weather condition types in terms of attendance)
After rerunning the model with these new variables also added, the r squared improved to 0.923.
 
Considering the use of only recent data:
I created a time series plot using Tableau to analyze the relation between year and attendance. 
 
As we can see from the plot, average attendance has been on a decline since 2001. Because of this, we can expect the model to be stronger if we consider more recent years.
I found that as we restrict the number of years used in the model, the R Squared score increases more and more. The R Squared scores when we filtered by each year were as follows:

Years Included	R Squared score	Change from R Squared score using all years (0.923)
2014 onwards	0.923	0.00
2015 onwards	0.926	0.00
2016 onwards	0.925	0.00
2017 onwards	0.934	0.01
2018 onwards	0.954	0.03
2019 onwards	0.973	0.05
•	We observe that as we make the data more and more recent, the r squared score becomes higher and higher. When we use only 2019 data, our r squared score is actually 0.973!
•	However, this is likely due to overfitting. We don't want to restrict the data too much so we will restrict just from 2014 onwards rather than choosing to filter even more recent years. We choose 2014 onwards so that we have more data for the model to predict from, even at the cost of a few r squared points
Final Model:
Therefore, when filtering only 2014 onwards, and including all the changes described previously, the final model is as follows:
 
Testing the final model on ‘test’ data:
I used this model to test on the 20% of data we had split initially. The blue line on the graph (from Python) below represents a perfect prediction, whilst the green dots are the actual predictions. As we can see, the predictions are far from perfect but are following a similar trend:
 
Part B: Predictions
Before making the predictions, I found that the model would have to be altered slightly as not all the data was available in the prediction file (i.e. – temperature data, whether the game was a make-up game or not etc.).
Hence, I removed those 2 variables which decreased the R Squared score slightly from 0.923 to 0.895. The final model was as follows:
 

Final Predictions:
The final predictions can be found here. 
Data Visualizations: 
I compared a histogram of the attendances from historical data to a histogram of the forecasted data. Here were the results:
 
 
Of course, the sample size from the predictions histogram is only 80, therefore the results will be significantly better. However, we can see a resemblance in terms of trend in both histograms.


