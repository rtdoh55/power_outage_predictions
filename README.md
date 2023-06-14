### By: Jerry Wu and Ryan Doh
# Framing the Problem
Our prediction problem will be a Regression problem, We are going to create a model that will predict the Outage Duration (in minutes) of each major power outage. We chose outage duration because we want to see if we could create a model that can accurately predict the length of each major power outage without using time and based solely on other factors related to the outage. The metric that we are using to evaluate our model is Root Mean Squared Error (RMSE) and we chose this over Mean Squared Error (MSE) and R^2 because R^2 can be artificially increased due to overfitting, whereas RMSE is less likely to be increased. The RMSE also takes the square root of the the mean squared error and creates more interpretable error and is less susceptible to outliers. The columns that we decide that we would know at the time of prediction 'MONTH', 'U.S._STATE', 'NERC.REGION', 'CLIMATE.REGION', 'CLIMATE.CATEGORY', 'POPDEN_URBAN', 'POPDEN_RURAL' because all of these can be known before the outage even occurs.
# Baseline Model
For our baseline model, we dropped all the rows with NAN, because our model needs to assume that there are no NANs. We split our data into a testing size of .25 and for our baseline model, we chose the features of MONTH, POPDEN_URBAN, and POPDEN_RURAL. Month was a nominal feature and we enocded it with OneHotEncoder, we did this because it was nominal and not ordinal and therefore ordinal encoding wouldn't produce a correct regression. Population density for both Rural and Urban were both quantitative features and we decided that it would be best in our baseline model to just use these features without any transformation. Our baseline model's Root Mean Squared Error was 7067.1617337894195 which is terrible                                        

# Final Model


# Fairness Analysis
