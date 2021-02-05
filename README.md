# Predicting Blood Pressure Based on Diet
By: [Kelly Wu](https://www.linkedin.com/in/kelly-wu-nj/)

## Table of Contents: 
- [Problem Statement](#Problem-Statement)
- [Executive Summary](#Executive-Summary)
- [Conclusion](#Conclusion)
- [Recommendations](#Recommendations)
- [Sources](#Sources)

## Problem Statement

We have all gone to the doctor at least once in our life and went through the basic health checks: height, weight, temperature, and blood pressure. We're all familiar with the process of having our arm squeezed tightly by a cuff while our doctor listens in with his or her stethoscope and watches the little monitor intently. Then we all hope to never hear that we have high blood pressure. High blood pressure, also known as a "silent killer," normally doesn't induce any health symptoms, but can lead to a heart attack or stroke. What's worse is that hypertension is so common that it is a leading risk for death and disability worldwide (Dr. Paul Whelton, an expert in hypertension and kidney disease at Tulane University). So what could help us determine if we're at risk or not? 

Food is essential to life, but majority of the population simply eat what they deem tasty to them or what's convenient. There aren't many people who actually go through the trouble of calculating the necessary macronutrients (and micronutrients) needed on a daily basis. Culture is another factor that affects diet where certain foods, for instance, such as rice is the primary carbohydrate versus pasta in another culture. With such differences in diet and it being a factor that affects blood pressure, can we predict blood pressure simply based on what we eat? Maybe our predictions will cause us to rethink what we eat or put more consideration into eating more variety. 

After our regression modeling, we can refer to our $R^2$ and Root Mean Squared Error (RMSE) scores to determine model accuracy. Once we can determine any relationships and correlations between diet and basic health knowledge such as height and weight and blood pressure. Our goal is to help nutritionists better assist their clients as well as allow the typical layman to determine their risk for high blood pressure without the hassle of going to a physician or spending money to purchase at at home blood pressure machine. 

## Executive Summary

We initially begin by gathering public data from The National Health and Nurtition Examination Survey (NHANES) from 2013 - 2014. Luckily, [Kaggle](https://www.kaggle.com/cdc/national-health-and-nutrition-examination-survey#diet.csv) organized the data for us into simple `.csv` files. After reading in our data, we intiated the cleaning process by isolating the columns of interest, handling null values, and creating a master data frame. Upon finalizing our master data frame, we had the following data with their corresponding units of measurement: 

|Water|Caffeine|Alcohol|Calcium|Carbs|Fiber|Protein|Potassium|Sodium|Sugar|Fat|Diastolic|Systolic|Height|Weight|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|mL|mg|g|mg|g|g|g|mg|mg|g|g|mm Hg|mm Hg|cm|kg|

Once we get our working data frame, we move onto our exploratory data analysis where we look for any standout values that may need an explanation. In order to determine whether certain values stand out or not, we researched what the recommended daily intakes of the dietary features are below. 

|Water|Caffeine|Alcohol|Calcium|Carbs|Cholesterol|Fiber|Protein|Potassium|Sodium|Sugar|Fat|
|---|---|---|---|---|---|---|---|---|---|---|---|
|2,000-2,500 mL|< 400 mg|< 42 g|1,000 mg|225-325 g|300 mg|25-30 g|0.8g * kg|3,500-4,700 mg|< 2.3k mg|25-37.5 g|44-77 g|

We noticed interesting relationships where solid substances played a lesser role than liquids from our exploratory data analysis alone. However, we also discovered other relationships based on each individual such as height and weight. Upon our visualizations, we realized that the relationship with diastolic pressure and systolic pressure is different where some relationships were similar, while a few showed almost mirrored relationships. 

Afterwards, we dived into the modeling component where we had to work with 6 variables since we needed to predict for systolic and diastolic pressure. This led us to run each type of model twice with the corresponding variables for what we wanted to analyze. Overall, we saw that the model always tended to perform better with systolic readings than diastolic readings. 

At the end of our findings, we realized that there could be a classification method in determining the class of someone's blood pressure and risk for hypertension. Unfortunately, given our data set we didn't have the minimum number of two classes to utilize the classification approach as all our individuals had normal blood pressures. 

Similarly, while the model is overfit, this model yields like results to our Gradient Boost as we can see from the $R^2$ scores, 61.91% of the variance can be explained by the model regarding the training set and 38.19% of the variance for the testing set. In addition, from the RMSE scores it also proves to be better than our baseline and other models. 

## Conclusion

|_Diastolic_ Model|Training $R^2$ Score|Testing $R^2$ Score|Training RMSE Score|Testing RMSE Score|
|---|---|---|---|---|
|Linear|20.93|21.89|11.96|12.49|
|Lasso|20.89|21.8|11.96|12.5|
|Ridge|20.93|21.89|11.96|12.49|
|Elastic Net|20.85|21.75|11.96|12.50|
|Decision Tree|1.0|-0.34|0.0|16.36|
|Bagged Decision Tree|85.7|21.19|5.08|12.55|
|Random Forest|85.56|20.95|5.11|12.57|
|Adaptive Boost|22.06|20.00|11.87|12.64|
|Gradient Boost|41.15|30.13|10.31|11.82|
|Voting Regressor|52.98|30.02|9.22|11.83|

|_Systolic_ Model|Training $R^2$ Score|Testing $R^2$ Score|Training RMSE Score|Testing RMSE Score|
|---|---|---|---|---|
|Linear|38.49|36.02|13.39|13.84|
|Lasso|38.32|36.01|13.41|13.84|
|Ridge|38.49|36.03|13.39|13.84|
|Elastic Net|38.45|36.04|13.39|13.84|
|Decision Tree|1.0|-0.29|0.0|19.68|
|Bagged Decision Tree|87.89|32.23|5.94|14.24|
|Random Forest|87.95|31.45|5.93|14.33|
|Adaptive Boost|32.91|24.53|13.99|15.03|
|Gradient Boost|51.15|37.68|11.94|13.66|
|Voting Regressor|61.91|38.19|10.54|13.6|

Through our various models and based on our metrics, our best model turned out to be the Voting Regressor model. While the testing scores were very similar to the Gradient Boosting model, we determined the Voting Regressor to be our best choice as it is constructed with the Gradient Boost and other models as well. It was better fit on our training data and still managed to produce very similar results on our testing data. For our diastolic predictions, the Voting Regressor model had 52.98% of variance explained by the model for the training set, and 30.02% of variance explained by model based on the $R^2$ scores. In addition, the RMSE scores prove to be significantly better than our baseline and other models as well at 9.22 for our training set and 11.83 for our testing set. Furthermore, we can see from our systolic predictions that the Voting Regressor also performs the best. Overall, while diet may not be our best predictor in determining blood pressure, there could be other factors that better our model's accuracy. 

## Recommendations 

There are quite a few limitations to our data set and models. Since we are using regression models, they tend to be unbounded so the factor of creating boundaries is one thing. In addition, given how it could be difficult to predict diastolic and systolic readings accurately based on one's nutritional daily intake, proved that a classification model could've been a better approach. There could've been a class column where we simply determine whether or not someone is in the normal range, the elevated range, the stage 1 hypertension range, etc. Another aspect could be gather more information and utilizing more features beyond diet. While the goal was to provide something that didn't require much health information, it may prove to be beneficial to have those records be a factor. For instance, whether someone was a smoker could've been a feature to include. Lastly, the aspect of quantity. While quality over quantity is the saying, quantity also plays a major role. After our cleaning, we ended up with a little over 6,000 rows from the original 10,000. In the future, just having more participants or pushing (not forcing) individuals to answer all questions would allow for data sets to be much more manageable. 


## Sources

- [Blood Pressure Matters](https://newsinhealth.nih.gov/2016/01/blood-pressure-matters)
- [Dietary Data](https://wwwn.cdc.gov/nchs/nhanes/Search/DataPage.aspx?Component=Dietary&CycleBeginYear=2013)
- [Dietary Variable List](https://wwwn.cdc.gov/Nchs/Nhanes/Search/variablelist.aspx?Component=Dietary&CycleBeginYear=2013)
- [Examination Data](https://wwwn.cdc.gov/Nchs/Nhanes/Search/DataPage.aspx?Component=Examination&CycleBeginYear=2013)
- [Examination Variable List](https://wwwn.cdc.gov/Nchs/Nhanes/Search/variablelist.aspx?Component=Examination&CycleBeginYear=2013)
- [Demographics Data](https://wwwn.cdc.gov/nchs/nhanes/Search/DataPage.aspx?Component=Demographics&CycleBeginYear=2013)
- [Demographics Variable List](https://wwwn.cdc.gov/nchs/nhanes/Search/variablelist.aspx?Component=Demographics&CycleBeginYear=2013)
- [NHANES Datasets](https://www.kaggle.com/cdc/national-health-and-nutrition-examination-survey#diet.csv)
- [BMI Calculation](https://www.cdc.gov/healthyweight/assessing/bmi/childrens_bmi/childrens_bmi_formula.html)
- [About BMI](https://www.nhs.uk/common-health-questions/lifestyle/what-is-the-body-mass-index-bmi/)
- [Child and Teen BMI Breakdown](https://www.researchgate.net/figure/Body-mass-index-mean-SD-and-percentiles-by-age-and-gender-among-the-study-population_tbl10_7616717)
- [Diastolic Zero Reading](https://www.quora.com/It-is-possible-to-have-a-diastolic-pressure-of-zero)
- [Diastolic and Systolic Reading Ranges](https://www.healthline.com/health/high-blood-pressure-hypertension/blood-pressure-reading-explained)
