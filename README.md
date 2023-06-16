### By: Jerry Wu and Ryan Doh
# Framing the Problem
Our prediction problem will be a Regression problem, We are going to create a model that will predict the Outage Duration (in minutes) of each major power outage. We chose outage duration because we want to see if we could create a model that can accurately predict the length of each major power outage without using time and based solely on other factors related to the outage. The metric that we are using to evaluate our model is Root Mean Squared Error (RMSE) and we chose this over Mean Squared Error (MSE) and R^2 because R^2 can be artificially increased due to overfitting, whereas RMSE is less likely to be increased. The RMSE also takes the square root of the the mean squared error and creates more interpretable error and is less susceptible to outliers. The columns that we decide that we would know at the time of prediction 'MONTH', 'U.S._STATE', 'NERC.REGION', 'CLIMATE.REGION', 'CLIMATE.CATEGORY', 'AREAPCT_URBAN', 'AREAPCT_UC', POPDEN_URBAN, POPDEN_RURAL because all of these can be known before the outage even occurs.
# Baseline Model
For our baseline model, we dropped all the rows with NAN, because our model needs to assume that there are no NANs. We split our data into a testing size of .25 and for our baseline model, we chose the features of MONTH, POPDEN_URBAN, and POPDEN_RURAL. Month was a nominal feature and we enocded it with OneHotEncoder, we did this because it was nominal and not ordinal and therefore ordinal encoding wouldn't produce a correct regression. Population density for both Rural and Urban were both quantitative features and we decided that it would be best in our baseline model to just use these features without any transformation. Our baseline model's Root Mean Squared Error was 7067.1617337894195 which is terrible The actual model is not predicting well, the constant that minimizes our RMSE is the mean and that would lead to our RMSE being the standard deviation. the standard deviation is 5954.499907910649 which is way better than our model. The reason we believe this is the case is because outage duration is very unpredictable.                              
# Final Model
For our final model we decide on using a lasso model, and to tune the hyperparameters we used GridSearchCV, we were able to find out that the best hyperparameter for alpha was 10 and the best hyperparameter for tol was .0001. We changed the One Hot Encoding to these columns 'CLIMATE.REGION', 'CLIMATE.CATEGORY', 'NERC.REGION' and made our month column Ordinal Encoded while we standardized 'AREAPCT_URBAN' and square rooted 'AREAPCT_UC'. We thought that Month would be better off as ordinal encoded because the length of the outage duration can be affected by each month differently with certain months having probably a higher chance of leading to a longer outage which we thought could correlate better with ordinal encoding. Our Climate and geographical features are one hot encoded because they provide information about the region, but they are not better or worse in our opinion, and therefore cannot be ordinal encoded. Finally, we chose AREAPCT_URBAN' to standard scale and 'AREAPCT_UC' to square root, this is because we thought that percentage Urban would benefit from standardization and area percentage under the curve would benefit from square root because the perecentage needed to be minimized somehow and we thought that square rooting would help minimize it. It is definitely an improvement from the baseline model because the baseline model doesn't have any transformations and we thought that would be sufficient but it had some serious flaws and also the columns of this model are better thought out. lasso is better optimized with hyperparamters so we used lasso instead of linear regression our RMSE for this model was 6850.581854784288 compared to 7036.036549331963 which was an improvement.
# Fairness Analysis
Our fairness analysis was performed on the CLIMATE.CATEGORY column and our group X was cold and our group y was not cold. Our reasoning was that in power outages, cold temperature may have a greater effect on the linear regression and so it might perform bettter on cold data because it is better tailored to the cold data. Our Null hypothesis is that cold and not cold are treated the same by the regression model and that there is no bias towards one or the other. Our Alternative hypothesis is that there was a difference in cold and not cold regions in our regression model. We chose .1 as our significance level and our test statistic was the absolute difference in group RMSE for the cold and not cold regions, we performed a permutation test and found that we had a p-value of much greater than .1 and so we failed to reject the null.
<iframe src="assets/thing.html" width=800 height=600 frameBorder=0 style = "position: relative; right: 30%" >
