# Predict_SP500_Returns\
# 1. Main Question and Hypothesis\
Attempts to predict stock market returns or the equity premium have been a long tradition in finance. Our main purpose for this project is to test whether stock returns can be predicted. More specifically, we would like to forecast S&P 500 index excess returns. So, our hypothesis is that past indicators can predict future market excess returns. We are looking forward to explore some feasible methods to make it come true, even though as we all know, it is pretty hard. \
To realize this, we first take a look at the characteristics of variables like mean, standard deviation and correlation among them, and most importantly, we study several machine learning methods of predicting future stock returns, such as the ElasticNet regression, PLS, Random Forests and Multi-layer Perception(MLP). Finally, we evaluate our models’ performance and analyze the results so that we can reach our conclusions.\
# 2. Model Construction and Results Analysis\
#    2.1 ElasticNet Regression\
First of all, we start with a basic model. The first model we choose is a penalized linear model called ElasticNet. The reason why we choose it is that we want to avoid the overfitting problem. With enough variables, we do not need to worry about the problem of under-fitting. ElasticNet is a combination of Lasso and Ridge regression, which can be deemed as a combination of L1 and L2 regularization. Ridge have the ability to reduce the model’s fit of noise while preserving its fit of the signal. \
One of the most parameters in ElasticNet is Alpha, which decide the choice between Lasso and Ridge regression. We run a loop on Alpha to see which perform better in test data. Here, we split the whole data into 30% of test data and 70% of training data. One more thing we need to take care of is to keep all the predictors in the same scale. As a result, we standardize them before running the model.\
#    2.2 PLS Regression\
Our second model is PLS regression, which is a technique that reduces the predictors to a smaller set of uncorrelated components and performs least squares regression on these components, instead of on the original data. PLS regression is especially useful when the predictors are highly collinear, or when you have more predictors than observations and ordinary least-squares regression either produces coefficients with high standard errors or fails completely.\
So, in our case, we don’t think that we should worry OLS doesn’t work because we have 348 observations and 14 predictors. However, as we analyzed before, there indeed exists some variables highly correlated with each other. In this sense, we are able to take full advantage of PLS regression.\
The PLS algorithm returns us altogether 14 principal components. We would like to study the model performance when increasing the number of PCs which we throw into the regression in steps of 2 until we hit 11 and choose the best PLS model fitting our sample data. \
#    2.3 Random Forests\
Our third model is the random forest model. Decision tree is one of the widely used models for classification and regression. It breaks complicated situation down to easier-to-understand scenarios. Random forest consists of a large number of individual decision trees that operate as an ensemble. For decision trees, they are sensitive to the data that they are trained on. Any small changes to the data would lead to a significant difference on the decision trees. However, for random forest, it could allow each individual tree to randomly sample from the dataset with replacement to form different trees. Because a large number of relatively uncorrected trees operating as an ensemble and they could protect each other from their individual errors, hence the random forest definitely outperforms any of individual trees.\
Here, we want to dig deep and do some analysis on under-learning versus over-learning and ensemble model in random forest.The first step is to look at the problem of overlearning. Here, we assume a forest of 100 trees while the depth of the tree varies from 5 to 30. \
The second step is to investigate on the effect of ensemble model. Here, we assume a forest of 5 depths while the number of the tree varies from 10 to 10000.\
#    2.4 Multi-layer Perception(MLP)\
Our last model is MLP. Since MLP is a class of feedforward artificial neural network (ANN), we are especially looking forwards to the model’s performance in predicting market excess return. It is different from logistic regression, in that between the input and the output layer, there can be one or more non-linear layers, called hidden layers. As we mentioned in Random Forests about the issue of overlearning, when constructing the MLP model, we pay attention to the setting of the number of the hidden layers. Similarly, adding too many hidden layers may cause overfitting and significantly cost more time. Hence, we just set the number of hidden layers to two. On the other hand, notice that we use stochastic gradient-based optimizer(‘adam’) as our weight optimization function. Therefore, we should be careful about the learning rate. It controls the step-size in updating the weights. The network with a crazy small alpha didn't hardly converge.  This is because we make the weight updates so small that they hardly changed anything. And with a larger alpha, we would find that the error increases instead of decreasing. This is an example of divergence. So, after we tune this learning rate parameter, we finally choose 0.001 which yields the best model performance. \
# 3. Conclusion\
After we fit our data into four different machine learning models, we find that it is pretty difficult to predict market excess return even if we have already employed several advanced algorithms. In general, even though our model contributes to forecasting returns, the R2 is pretty low. And this is something typical of a predictive model. We just have to live with this. This is a statistical fact that whenever you try to predict the market return, you usually get very low R2 especially if the frequency of the data is higher like daily or weekly. In this sense, our MLP model is the best among our trials. \
Therefore, our recommendation is to use low frequency data like annual data. It is likely that the model performance would be more ideal. Furthermore, we think if we use machine learning classification models to predict stock movement(e.g., up, down and not change), the accuracy would be higher and we could use this movement as a signal to help us construct a marketing timing strategy. For example, if the model predicts market return to go up, we will hold the market this month; Otherwise we will hold the risk-free asset. We could also study whether the market timing strategy beat the strategy of holding the market at all times in terms of cumulative return.\
Finally, our findings help justify the growing role of machine learning throughout the architecture of the burgeoning fintech industry.\
