## Preparation and Overview (3 points total)

[2 points] Explain the task and what business-case or use-case it is designed to solve (or designed to investigate). Detail exactly what the classification task is and what parties would be interested in the results. For example, would the model be deployed or used mostly for offline analysis? As in previous labs, also detail how good the classifier needs to perform in order to be useful. 

The task involves performing classification on a dataset containing features of mobile phones and the last column being the price range of each phone. The goal is to build a model that can accurately predict the class or price range of a mobile phone based on its features.

Here are a few use cases for our model:

Pricing Strategy: Mobile phone manufacturers or retailers could use the model to estimate the price range of new or upcoming models based on their features. This could help in setting profitable price for their products.

Customer Recommendations: E-commerce platforms or mobile carriers can use the model to recommend mobile phones to customers based on their budget and desired features. Or, the customer himself can see which phone is the best for them.

Fraud Detection: In cases where mobile phones are sold through online stores, the model can help in detecting fraudulent listings by flagging phones with features that don't match with their reported price range.

Parties interested in the results could include:
Mobile phone manufacturers
Retailers
E-commerce platforms
Fraud detection agencies
Someone who wants to buy a phone

This can be used as an offline model for Mobile Manufacturers and retailers.
And can work online for E-commerce platforms, and fraud detection.


[.5 points] (mostly the same processes as from previous labs) Define and prepare your class variables. Use proper variable representations (int, float, one-hot, etc.). Use pre-processing methods (as needed) for dimensionality reduction, scaling, etc. Remove variables that are not needed/useful for the analysis (give reasoning). Describe the final dataset that is used for classification/regression (include a description of any newly formed variables you created). Provide a breakdown of the variables after preprocessing (such as the mean, std, etc. for all variables, including numeric and categorical). 
<mark> it mentions scaling, do we add the code that co pilot gave the thing that greatly increased our performance? </mark>

We made a feature correlation plot to determine which features have the most positive trend with our classification. And we selected <mark> RAM, px_height...... the rest is in code</mark>


[.5 points] Divide your data into training and testing splits using an 80% training and 20% testing split. Use the cross validation modules that are part of scikit-learn. Argue "for" or "against" splitting your data using an 80/20 split. That is, why is the 80/20 split appropriate (or not) for your dataset?  

Since the dataset is clean, there's less need for extensive validation or tuning. With a clean dataset, models are less likely to encounter unexpected challenges during training, making an 80/20 split suitable for efficient model development.

A larger validation set could enhance its ability to classify unseen data in the future. So if it is smaller than 20%, generally there is a less chance for over fitting.

if there are plans to scale the dataset or tackle more complex problems in the future, using a larger validation(even more than 20%) set now could help future-proof the model

<mark> ours it a large dataset, so we could probably use a 90/10 split. Use copilot to explain </mark> i personally (can be wrong) think this is not a good idea, becuase there is a chance for it to overfit

<mark> Did we use cross validation?</mark>

## Modeling (5 points total)

The implementation of logistic regression must be written only from the examples given to you by the instructor. No credit will be assigned to teams that copy implementations from another source, regardless of if the code is properly cited. 

[2 points] Create a custom, one-versus-all logistic regression classifier using numpy and scipy to optimize. Use object oriented conventions identical to scikit-learn. You should start with the template developed by the instructor in the course. You should add the following functionality to the logistic regression classifier:

Ability to choose optimization technique when class is instantiated: either steepest ascent, stochastic gradient ascent, and Newton's method. It is recommended to call this the "solver" input for the class.

Update the gradient calculation to include a customizable regularization term (either using no regularization, L1 regularization, L2 regularization, or both L1 and L2 regularization). Associate a cost with the regularization term, "C", that can be adjusted when the class is instantiated.  

[1.5 points] Train your classifier to achieve good generalization performance. That is, adjust the optimization technique and the value of the regularization term(s) "C" to achieve the best performance on your test set. Visualize the performance of the classifier versus the parameters you investigated.

Is your method of selecting parameters justified? That is, do you think there is any "data snooping" involved with this method of selecting parameters?

<mark> because we are Brute Forcing all possibilities to find the best accuracy, </mark>

[1.5 points] Compare the performance of your "best" logistic regression optimization procedure to the procedure used in scikit-learn. Visualize the performance differences in terms of training time and classification performance. Discuss the results. 



## Deployment (1 points total)

Which implementation of logistic regression would you advise be used in a deployed machine learning model, your implementation or scikit-learn (or other third party implementation)? Why?

Our implementation gives an accurancy of 0.99 when doing one versus all with Hessian Binary Logistic Regression with L1&L2 [(L1 + L2) = |w| + w^2 = c + 2cw] regularisation.



## Exceptional Work (1 points total)

 Implement an optimization technique for logistic regression using mean square error as your objective function (instead of maximum likelihood). 

Derive the gradient updates for the Hessian and use Newton's method to update the values of "w".

Then answer, which process do you prefer: maximum likelihood OR minimum mean-squared error?



L1 regularization  is |wsub1|
L2 is 2cw (derivative of w^2)
L1 and L2 is summing them (L1 + L2) = |w| + w^2 = c + 2cw