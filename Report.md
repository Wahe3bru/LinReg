# Linear Regression Report

### Intro
[lorem ipsum hoo haa]
______

### Data
Using Company fundamentals, futures prices, history of stock prices, interest rates, CPI, GDP, SA Debt and unemployment we **created additional features** to improve the model.  


The data was merged into one dataframe, saving as a csv file in the format ready for modelling.<br>
__ie__ each observation is a row, each feature/independent variable is a column.
the label or Dependant variable is `target_return` column.

The features are (data_all.columns (_33 columns_) __list of columns__

Using backwards elimination with a significance level of 0.05% <br>
we whittled down the features till only the most significant features remained
data_signif.columns (9 columns?) __list of columns__

The data was Standardised using sklearn’s StandardScaler
- reason we chose standard scaler over Normalization
- - normalization would squash all features to fit between 0 and 1. <br>
  if there are outliers a lot of valuable      information will be lost.
- standardScaler keeps the information while scaling all the features, so as not to bias any one feature


data then divided into Train and  Test, using these paramters __[ test_size=0.3, random_state=101]__

We then built 4 Models:
- linear regression
- ridge regression
- lasso regression
- elastic net regression
- ~~polynomial regression~~

The data was trained on two sets of data.<br>
the data with all the  features - *data_all* <br>
the data with only the  significant features - *data_signif*

___
### Results of models on data_all


##### models settings
- lm = LinearRegression()
- ridge = Ridge(alpha=1)
- lasso = Lasso(alpha=0.001)
- enet = ElasticNet(alpha=0.001,l1_ratio=0.8)


##### comparing intercept

Regression | Intercept
---|---
Linear |0.026327
Ridge	|0.023940
Lasso	|0.025472
ElasticNet	|0.025054



##### comparing coef_s
- note on how Lasso weights the coefs compared to Ridge and linear

coef | Linear	| Ridge	| Lasso |	ElasticNet
---|---|---|---
current_price	|-0.173379	|-0.030485	|-0.007082	|-0.008359
momentum	|0.013896	|0.005502	|0.003563	|0.003810
moving_average	|0.162553	|0.016215	|-0.000000	|-0.000000
moving_volatility	|0.032811	|0.023150	|0.015220	|0.016882


##### comparing R^2 (train)  and R^2 (Test)

model |Adjusted R-SQUARED SCORES (train) |Adjusted R-SQUARED SCORES (train)
---|---|---
Linear:    |  0.08199521051827285 | 1.2050198401335255
Ridge:     |  0.011024112279151344  | 0.34845869704466637
Lasso:     |  -0.009716076528737627 | 0.16353392615205586
ElasticNet:|  -0.005899508330628134 | 0.17892115191240965

comparing adjusted R^2 (train)  and adjusted R^2 (Test)
- comment on R^2 vs adjusted R^2 between models

##### comparing MSE (train)  and MSE (Test)
- comment on bias vs variance

Model | MSE (train) | MSE (test)
---|---|---                            
Linear:      | 0.01338626315815241   | 0.026150708502340535
Ridge:       | 0.014421157320511111  | 0.015992214524348968
Lasso:       | 0.01472358888569816   | 0.013799076081575625
ElasticNet:  | 0.01466793603198073   | 0.013981562809447583



**Notes:** Lasso performed the best. This demonstrates the feature selection strength of Lasso

                     _______________________________________________


### Results of models on data_signif

#### models settings (alphas, L1, etc)
- lm = LinearRegression()
- ridge = Ridge(alpha=1)
- lasso = Lasso(alpha=0.001)
- enet = ElasticNet(alpha=0.001,l1_ratio=0.6)


##### comparing R^2 (train)  and R^2 (Test)

Model |Adjusted R-SQUARED SCORES (Train) | Adjusted R-SQUARED SCORES (Test)
---|---|
Linear:      |0.10861831434112834 | 0.056709941424155974
Ridge:       |0.05514041862950381 | 0.04964065476310464
Lasso:      | 0.04738614822449938 | 0.05639666565877155
ElasticNet: | 0.050732849018022885 | 0.05892363152723756

comparing adjusted R^2 (train)  and adjusted R^2 (Test)
- comment on R^2 vs adjusted R^2 between models

##### comparing MSE (train)  and MSE (Test)

Model |MSE (train) |MSE (test) 
---|---|---|
Linear:      |0.013918263205177094   |0.01430007776421342
Ridge:       |0.014753280841447275  |0.014207866918323007
Lasso:       |0.0148743580165759  |0.013827493612571065
ElasticNet:  |0.01482210176848078  |0.013928592149042488

- comment on bias vs variance
- each model performed much better with better data!

##### comparing MSE train (data_all)  and MSE train (data_signif)
Model |MSE (train) |MSE (test)
---|---|---
Linear:| 0.026150708502340535 | 0.013642763896953482
Ridge: |0.015992214524348968 | 0.013745006688510317
Lasso: |0.013799076081575625 | 0.013647294790990708
ElasticNet:|0.013981562809447583 | 0.013610747391380462




Notes: When the data has been processed and the best features selected for modelling, then Lasso doesn’t outperform linear regression as well. Elastic Net performs the best using the best of both Lasso and Ridge.
