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
