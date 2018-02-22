# Modeling and Prediction of Credit Scores

## Introduction

## Description of dataset

The dataset credit.csv consists of a number of numeric and categorical variables relevant to a person’s credit score.

The numeric variables are:

1. Income: in thousands of dollars
2. Rating: the Credit score rating
3. Balance: Average credit card debt for a number of individuals
4. Education: Years of education
5. Limit: Credit Card Limit
6. Cards: Number of credit cards owned

The categorical variables are:

1. Gender {Male, Female}
2. Married {Yes, No}
3. Ethnicity {African American, Asian, Caucasian}
4. Student {Yes, No}

## Background information of dataset

This dataset is available as part of the book “An Introduction to Statistical Learning, with applications in R” (Springer, 2013) and can be downloaded from http://www-bcf.usc.edu/~gareth/ISL/Credit.csv

## Motivation

A credit score in the United States is a number representing the creditworthiness of a person, the likelihood that person will pay his or her debts. Lenders, such as banks and credit card companies, use credit scores to evaluate the potential risk posed by lending money to consumers. Widespread use of credit scores has made credit more widely available and less expensive for many consumers

The FICO score was first introduced in 1989 by FICO, then called Fair, Isaac, and Company. The FICO model is used by the vast majority of banks and credit grantors, and is based on consumer credit files of the three national credit bureaus: Experian, Equifax, and TransUnion.

Banks and Lenders are always interested in models that can accurately predict the credit score rating. It is natural to assume a linear relationship between the predictor variable balance and the response variable rating. However, other variables such as limit (credit card limit), income, marital status and education may have some interaction with balance.

In this study, we would like to explore the following:

- Multiple regression models between the response variable rating and the other variables in the dataset
- Which variables are more important than others and can lead to a good prediction of a person’s credit card score
- Which categorical variables interact with the numeric variables?
- Which model choice is acceptable? Provide enough justification
- Use the chosen model to explain relationships and predict observations.

## Methods

### Modification of Dataset

The original dataset contains numeric variables Limit and Balance. In determining the credit score or rating of an individual, How FICO scores looks at credit card limits, the credit limit by itself is not considered directly. Instead, the FICO score considers your credit limit when determining your “credit utilization rate.” Utilization means the amount of your available credit that you are using at the time your score is calculated. It is calculated by dividing an account’s outstanding balance by its credit limit. Credit utilization rate has proven to be extremely predictive of future repayment risk. So it is often an important factor in a person’s score. Generally speaking, the higher your utilization rate is, the greater is the risk that you will default on a credit account within the next two years.

As a result, the dataset has been modified by eliminating the variables Limit and Balance and instead replacing it by a new variable CreditUtilization which is the ratio of Balance to Limit

### Significance of Regression Tests for Linear Regression

The significance of regression test between 2 models is based on the F-statistic. The p-values when we test for significance using the ANOVA test between a pair of models are as follows:

- SLR based on Income vs. MLR based on Income and Credit Utilization: **8.95076e-117**
- SLR based on Credit Utilization vs. MLR based on Income and Credit Utilization: **4.049131e-160**
- MLR based on Income and Credit Utilization vs. MLR based on Income, Credit Utilization and Student: **7.083355e-91**
- MLR based on Income, Credit Utilization and Student vs. MLR based on all predictors: **0.026**

Based on the above, for a significance level less than or equal to 2%, the multi regression model based on Income, Credit Utilization and Student is significant amongst all the models including the additive model based on all predictor variables.

### Goodness of fit based on the coefficient of determination (R2)

The coefficient of determination is interpreted as the proportion of observed variation in the response that can be explained by the linear regression model. It is a statistical measure of how close the data are to the fitted regression.

Below is the R-squared metric for different regression models

- SLR based on Income: **0.6263**
- SLR based on Credit Utilization: **0.3823**
- MLR based on Income and Credit Utilization: **0.9012**
- MLR based on Income, Credit Utilization and Student: **0.9649**
- MLR based on all predictors: **0.9662**

As seen above, based on R-squared metric alone, a good model choice would be the one based on Income, Credit Utilization and Student, since it uses only 4 coefficients and it is very close in value to the additive model based on all predictors.

So, we see that based on both a) Significant tests and b) R-squared criteria, the additive model based on Income, Credit Utilization and Student is a good model choice.

### Reduction in Std. Deviation of Error

The standard deviation of error of the observed samples Rating corresponds to a very simple model Yi=β+ϵi resulting in the Rating estimator to be the sample mean y^=y¯. In other words, in the absence of applying a regression model, we assume the null hypothesis i.e. none of the predictors are useful.

On the other hand, if we apply a regression model, the estimate of Rating has a much lower standard deviation of error compared to the simple model that assumes no regression (null hypothesis).

- sy=154.7241426 gives us an estimate of the variability of Rating. Specifically how the observed Rating data varies about its mean. (We could think of this as an estimate for how the observations vary in the model Yi=β0+ϵi.) This estimate does not use the predictors in any way.
- The standard error se gives us an estimate of the variability of the residuals of the model, specifically how the observed Rating data varies about the fitted regression. This estimate does take into account the predictors.

In the following, we evaluate the standard error se for the following regression models:

- SLR based on Income: **94.706**
- SLR based on Credit Utilization: **121.754**
- MLR based on Income, Credit Utilization and Student: **29.117**
- MLR based on all predictors: **28.789**

As seen above, while the variability of the estimate of the response variable Rating around the fiited regression reduces for the simple regression models based on Income as well as Credit Utilization, there is a drastic reduction in variability due to MLR based on Income, Credit Utilization and Student. Furthermore, this variability is very close to that observed for the MLR based on all predictors which happens to be the lowest amongst all.

### Analysis of Model Coefficients:

#### Multiple Linear Regression model based on Income, Credit Utilization and Student

#### Estimated coefficients βi^

- β0^=95.203 is the estimated Rating for a an income of $0, a credit utilization rate of 0, and an individual who is not a student
- β1^=3.149 is the estimated change in mean Rating for an increase of $1 in income for a certain credit utilization and student type
- β2^=1468.494 is the estimated change in mean Rating for an increase of 1 in credit utilization for a certain income and student type
- β3^=−142.205 is the estimated change in mean Rating for a student with a certain income and credit utilization.

#### Confidence interval estimates of coefficients βi^

The 90% confidence interval estimate of the linear regression coefficients βi^ is given as

|  | 5% | 95% |
| :---:         |     :---:      |          :---: |
 (Intercept)|   90.360584|  100.046257|
 Income|         3.080547|    3.218063|
 CreditUtil|  1429.274898| 1507.712362|
 StudentYes|  -150.962338| -133.448192|

## Results

### Exploring Explanation Models

In the following, we explore reasonably “small” models that are good at explaining the relationship between the response and the predictors.

## Adding Interactions

Using the additive model based on Income, Credit Utilization and Student as a starting point, we investigate further the effect of two-way and three-way interactions between these variables.

### Significance of Regression

We now test for significance between the two hypotheses:

- H0: Rating is a linear estimate of Income, Credit Utilization and Student predictor variables
- H1: Rating is a linear estimate of Income, Credit Utilization, Student and the interaction terms between these predictor variables

Since the p-value(**2.799674e-33**) is incredibly low, we reject the null hypothesis and accept the alternate hypothesis.

### Improvement in coefficient of determination (R2)

We also investigate the improvement in the coefficient of determination due to interactions. Compared to the value **0.9649** obtained for the additive model based on Income, Credit Utilization and Student, if we include the interaction terms, the R2 value improves to **0.9765**.

Given the high value R2 and the low number of coefficients (length(coef(mlr_rating_inc_credit_util_stud_inter))) in this model, we conclude that this model serves as a good explanation model.

## Exploring Predictive Models

Here, we explore models that have small errors and hence are good for making predictions. To find models for prediction, we use the selection criterion that implicitly penalizes larger models, such as the leave-one-out cross-validated RMSE (LOOCV RMSE). So long as the model does not over-fit, we do not actually care how large the model becomes. Explaining the relationship between the variables is not our goal here and we don’t need to worry about model assumptions.

For each of the following models we perform a step search to obtain the best model based on the AIC and BIC criteria:

1. An additive model that includes all the predictor variables.
2. A model based on all possible 2-way interactions of the predictor variables.
3. A model based on all possible 3-way interactions of the predictor variables
4. A model based on 3rd order polynomial terms of the Income and CreditUtil variables
5. A model based on all possible 2-way interactions and 3rd order polynomial terms of the Income and CreditUtil variables

In the case of model 2, two variants of step search were performed:

- In the first variant, no scope argument was provided.
- In the second variant, a single formula was provided in the scope argument that represented the 9-way interaction between all the predictor variables: **Income, Cards, Age, Education, Gender, Student, Married, Ethnicity and CreditUtil**

Table 1 provides a summary of the LOOCV RMSE achieved and the number of regression coefficients for each of the models considered. As seen in the Table, the step-wise search based on the 2-way interaction and third order polynomial terms of the Income and Credit Utilization predictor variables achieves the lowest LOOCV RMSE.


**Table 1: Comparing LOOCV RMSE for different fitted models**

|MODEL| LOOCV RMSE| Number of Coefficients|
| :---:         |     :---:      |          :---: |
Additive (BIC)|	29.2856157|	8
Two-way interaction (BIC)|	24.3232235|	9
Two-way interaction w/ scope (AIC)|	23.146347|	66
Three-way interaction (AIC)|	24.6682874|	99
Third order polynomial (AIC)|	29.4252018|	12
Two-way interaction & Third order polynomial(AIC)|	21.9256914|	30

## Discussion

In this study, we investigated the problem of modeling and prediction of a person’s credit score as a function of multiple variables such as a person’s income, credit card limit, outstanding balance, etc. An elementary statistical analysis was performed on each of these variables to determine the distribution (histograms, boxplots) of these variables and metrics (estimation coefficients, mean and variance of residuals ) related to simple linear regression. Several techniques studied throughout STAT420 as appropriate were applied here in this study.

The dataset was slightly modified to introduce a new predictor variable related to credit utilization rate as a function of balance and credit limit as this variable is directly used in determining a person’s credit score. A key finding upfront was that credit score can be well explained by a linear combination of three important predictor variables (Income, Credit Utilization rate and whether the person is a student or not). In fact, it was shown that such a model is a significant when compared to a model based on all predictors for levels of significance less than or equal to 2%. An analysis of βi^ coefficients and confidence interval estimates was also obtained for this model.

Next, explanation models were explored from the point of view of maximizing R2 and using as few coefficients as possible. Towards this objective, a model based on 2-way and 3-way interaction between the Income, Credit Utlization and Student predictor variables was obtained leading to **R2 = 0.9765 and utilization of 8 coefficients**.

Further checks were performed on the explanation model assumptions for linearity, constant variance and normality. An exercise was also performed to identify subsets of the data that led to a favorable decision on the constant variance assumption via the Breusch-Pagan test. Also, an outlier analysis was performed on this model to assess the sensitivity of regression coefficients to influential observations and the prediction of Rating estimate had we used a model that was trained on data without these influential observations.

Finally we also explored a few candidate models to determine the best predictive model using LOOCV RMSE as a metric. Methods based on step-wise search using the AIC and BIC criteria were used for this purpose. Amongst the candidates considered here, a model derived based on 2-way interactions and third order terms using **30 coefficients was shown to achieve the lowest LOOCV RMSE (21.926 )**
