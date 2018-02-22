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
