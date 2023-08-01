# Boston_Crime_Analysis

This project will look at crime data from Boston from 2022 to investigate what factors are predicting factors to whether a crime committed involved a shooting or not. This project will analyze if the location, time, month, district, and day a crime is committed in have an effect on whether the crime involved a shooting or not. The data used for this project comes from the Boston police department database where data on other years can be found as well. This investigation will help understand what the most significant predictors for whether crimes involve shootings or not are. This is important with the increasing number of shootings in the US and more insights are always helpful in understanding patterns in shooting crimes as well as suggesting proactive solutions to the problem of gun related crimes in America (more specifically in Boston). Analysis of similar data from Boston PD for crimes in 2018 by Pankaj Shah found that:

- The most affected districts in Boston are Dorchester, South-End (D-4), Roxbury (B-2).
- It can be noted that the highest number of the crimes were reported during summer months of July and August.
- Motor-Vehicle accident response were the highest number of report registered with the Boston Police.

The data contains crimes that occurred in Boston in 2022. The resulting clean data has 70007 observations and 14 variables. Important variables are: OFFENSE_CODE which is an assigned code to a crime type, OFFENSE_DESCRIPTION which is the specific crime the offense code/crime type is, DISTRICT is the district the crime was committed in, SHOOTING which is whether the crime involved a shooting or not; YEAR, MONTH, DAY_OF_WEEK, HOUR which respectively contain the year, month, day of the week, and hour a crime was committed on; Lat and Long which are the latitude and longitude where the crime is committed.

The data exploration shows that of the 70007 crimes that occurred in Boston in 2022, 69291 did not involve a shooting while 716 did. When viewing the crimes by their latitude and longitude, it is clear that regions closer to the center have more crimes that have involved a shooting that regions closer to the edges of the city. This is moreover demonstrated by the fact that Districts B2, B3, and C11 which are closer to the center of Boston (Zimmerman and Douglas, 2020). Furthermore, although there is little fluctuation in the frequency of shootings over months, there are clear variations throughout the day where times around midnight have significantly higher shootings while early morning has significantly fewer shootings.

- Bar chart of the number of crimes that did and did not involve shootings in Boston in 2022. 69291 crimes did not involve shootings while only 716 involved a shooting.
- The scatter plot of the crimes in boston in 2022 accounting for shootings shows that there are regions with more shootings than others, especially between longitude -70.05 and -71.1 and latitude 42.25 and 42.35. These are where districts B2, B3, and C11 are found (Zimmerman and Douglas, 2020). The center of the city has more crimes involving shootings than places near the outside. This suggests that a KNN classifier model is a natural choice for models. This implies that the Latitude and Longitude could be potential predictors for whether a crime committed in Boston involved a shooting.
- The barchart of the shooting frequency by districts in Boston in 2022 shows that districts B2, B3, and C11 have a significantly higher number of shootings compared to other districts. Districts A1 and A15 have the lowest shooting frequency. This implies that the district a crime occurred in can be used as a predictor for whether it involved a shooting or not.

The variance inflation factor shows that Lat, Long, District_E18, and District_E5 have significant multicorrelation. It makes sense that Latitude and Longitude are highly correlated to each other (with scores of 17396348.0 and 17436869.0 respectively) and the district data since they all denote location. District_B3 has a VIF score of 9 which implies higher multicorrelation. Other variables have insignificant multicorrelation. The correlation martrix also shows that Districts D14, E5, E18, A7, and B3 have high correlation with Lat and Long of magnitudes above 0.3. Furthermore, Lat and Long have a correlation of 0.376 as well.

For all models, a random sample of crimes that did not involve shootings of size 716 is taken with all 716 crimes that involved shootings for training and testing. Otherwise, all models will be skewed to only predicting/classifying crimes as not involving shootings as it results in an accuracy of approximately 69291/70007= 0.9898.

Because of the high multicorrelation that latitude and longitude have, the first model that will be considered is a logistic regression with lasso to investigate the relationship between crimes involving shootings and month, day, hour, and location. A logistic regression with lasso is chosen because:

- The response variable is binary (a crime involves a shooting or not),
- There are multiple predictors and lasso will aid in feature selection and identifying the most signficant predictors,
- Lasso will help mitigate the identified multicorrelation.

Finally, a kNN classifier will be used to classify crime as involving a shooting or not depending on all the predictors in the lasso logistic regression model because of the low predictive performance of the logistic lasso regression. The predictors for the model are standardized since there are multiple which are not on the same scale.

# Conclusion

Given the performance of the models, it is clear that the kNN model is a better option than the logistic lasso regression in predicting whether a crime in Boston in 2022 involved a shooting. The kNN classifier has the advantage of being more in depth as it accounts for all predictors which have been seen to be related to shooting frequency in the data exploration. However, the logistic lasso regression helps make sure that only the most significant predictors are included in the model. Although the model does not perform well, it provides insight into the fact that location and time of the day are the most important predictors of whether a crime committed in Boston in 2022 involved a shooting. Additionally, all models show that location is an important predictor in whether a crime committed in Boston in 2022 involved a shooting or not. This is similar to Pankaj Shah's observation that in 2018 certain districts have higher crime rates. District B2 is still a district with worse crime rates (especially involving shootings in this observation). Expanding this investigation to other ranges of years can provide insight into shooting patterns over the years.

# Bibliography

https://data.boston.gov/dataset/crime-incident-reports-august-2015-to-date-source-new-system

https://rstudio-pubs-static.s3.amazonaws.com/453629_6be32e64d25b4e7189bc3bbe6968bcaf.html#data-preparation

https://www.researchgate.net/figure/Boston-Police-Department-districts-included-in-BWC-evaluation_fig1_336674159
