# Project 3

### Question 1: Download the dataset charleston_ask.csv and import it into your PyCharm project workspace. Specify and train a model the designates the asking price as your target variable and beds, baths and area (in square feet) as your features. Train and test your target and features using a linear regression model. Describe how your model performed. What were the training and testing scores you produced? How many folds did you assign when partitioning your training and testing data? Interpret and assess your output.

To perform K-fold validation, I will be using the `DoKFold` function defined in class: 
```
def DoKFold(model, X, y, k, standardize=False, random_state=146):
    from sklearn.model_selection import KFold
    if standardize:
        from sklearn.preprocessing import StandardScaler as SS
        ss = SS()

    kf = KFold(n_splits=k, shuffle=True, random_state=random_state)
    # kf = KFold(n_splits=k, shuffle=True)

    train_scores = []
    test_scores = []

    for idxTrain, idxTest in kf.split(X):
        Xtrain = X[idxTrain, :]
        Xtest = X[idxTest, :]
        ytrain = y[idxTrain]
        ytest = y[idxTest]

        if standardize:
            Xtrain = ss.fit_transform(Xtrain)
            Xtest = ss.transform(Xtest)

        model.fit(Xtrain, ytrain)

        train_scores.append(model.score(Xtrain, ytrain))
        test_scores.append(model.score(Xtest, ytest))
    return train_scores, test_scores
```
The model performed very poorly. The training score that I produced was on average 0.019 and the testing score was on average 0.023. I assigned 10 folds. This low number could possibly be attributed to the fact that while beds and baths are on similar scale while area is measured in square feet which is a completely different scale. We may be able to see a better training score. Another reason why the model may not be performing so well could be because the area and the number of bedrooms and bathrooms are simply not the strongest predictors of price. Variables such as geographical area could be better predictors, and we will be examining the possible improvements in the following problems. 

### Question 2: Now standardize your features (again beds, baths and area) prior to training and testing with a linear regression model (also again with asking price as your target). Now how did your model perform? What were the training and testing scores you produced? How many folds did you assign when partitioning your training and testing data? Interpret and assess your output.

Even after standardizing the features, the model still performed poorly. The resulting values were almost identical, with the training score being around 0.019 on average and the testing score somewhere around -0.010. I still assigned the same amount of folds so as to confirm that the improvements in the model performance came only from the standarization of the targets and not a combination of factors. 

### Question 3: Then train your dataset with the asking price as your target using a ridge regression model. Now how did your model perform? What were the training and testing scores you produced? Did you standardize the data? Interpret and assess your output.

The code for running ridge regression is as follows: 
```
a_range = np.linspace(0, 100, 100)
# a_range = np.linspace(5, 15, 100)
# a_range = np.linspace(7, 8, 100)
k = 10
avg_tr_score=[]
avg_te_score=[]
for a in a_range:
    rid_reg = Ridge(alpha=a)
    train_scores,test_scores = DoKFold(rid_reg,X,y,k,standardize=True)
    avg_tr_score.append(np.mean(train_scores))
    avg_te_score.append(np.mean(test_scores))
```

The model did not improve. Again, the results seemed to be largely identical to the two previous tests. The scores were on average 0.020 interally and -0.034 externally. I standardized the data using the `standardize = TRUE` argument in the `DoKFold` function that we examined in class. Since we have taken pretty much all the measures (that we looked at in class) to improve the training and testing scores, it is highly likely that the reason the models were unsuccessful is due to the fact that beds, baths, and area are not the best predictors of the asking price of houses in Charleston. 

### Question 4: Next, go back, train and test each of the three previous model types/specifications, but this time use the dataset charleston_act.csv (actual sale prices). How did each of these three models perform after using the dataset that replaced asking price with the actual sale price? What were the training and testing scores you produced? Interpret and assess your output.

With the charleston_act.csv, the model did not perform any better. In fact, the training score decreased. K Fold validation without standardization yielded a training score of 0.004 and a testing score of -0.062. With standardization, the training score was again 0.004 and the testing score -0.062. Running the ridge regression, the result did not improve, with a training score of 0.004 and a testing score of -0.055. This probably indicates that these metrics are not the greatest predictors of price of house prices in Charlottesville.  

### Question 5: Go back and also add the variables that indicate the zip code where each individual home is located within Charleston County, South Carolina. Train and test each of the three previous model types/specifications. What was the predictive power of each model? Interpret and assess your output.

Adding zip codes to the model greatly improved the model. 
K-fold validation without standardization:
Training: 0.339
Testing: 0.208

K-fold validation with standardization:
Training: 0.339
Testing: -566352630955906917466112.000

Ridge Regression:
Training: 0.333
Testing: 0.219

The training scores for all three versions of the model improved significantly. However, while K-fold validation without standardization and ridge regression had an increased testing value, K-fold validation with standardization performed very poorly. My initial thought was that this may be due to the zip codes being stored as binary data, and standardizing it will turn it into non-binary values and therefore may negatively infuence the predictability.  

Nonetheless, including the zip code greatly improved the predictive power of the models in general. This makes sense since housing prices greatly depend on the location. A small apartment in the middle of Manhattan will probably cost more than living in a larger house in South Dakota. Therefore we can expect to see an increase in model performance when zip code is taken into consideration.

### Question 6: Finally, consider the model that produced the best results. Would you estimate this model as being overfit or underfit? If you were working for Zillow as their chief data scientist, what action would you recommend in order to improve the predictive power of the model that produced your best results from the approximately 700 observations (716 asking / 660 actual)?

It appeared that adding in the zip code data produced the best results. The best model that produced the highest testing score was ridge regression with zip codes. The model is slightly overfit, since the training score is marginally higher than the testing score. To improve the predictive power of this model, we may consider adding more detailed metrics related to geogrpahical area, since region seemed to be the biggest boost to the testing/training scores. Although zip code is a good measure of geographical area and the prices of homes may be relatively homogenous, there may be further divisions within area covered by a zip code that may differ in housing price. 





