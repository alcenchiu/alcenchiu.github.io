## Introduction <img align="right" width="220" height="220" src="/assets/IMG/template_logo.png">

The gender pay gap has been a longstanding issue in the United States. In 2022, women earned roughly 82% of what men earned. This is similar to 2002, when women made roughly 80% of what men earned, showing that the gender pay gap has persisted at a similar rate over the past 20 years (Aragão 2023). This machine learning model is motivated by this fact, and looks to see whether the gender of an individual plays a significant role in predicting an individual’s wage income.

This project utilizes the 2021 American Community Survey, an annual demographic survey conducted by the U.S. Census Bureau. This survey provided numerous characteristics of individuals in the U.S., including but not limited to the gender characteristics that were incorporated into the machine learning models in the project.  

The machine learning models I chose to use for this project were the SciKit Learn’s Random Forest Classifier and Random Forest Regressor, and Scikit Learn’s Ridge Regression. The results of these models showed that while gender ranks highly on the feature importance measure in the Random Forest Regressor model and is above 50% accuracy for the Random Forest Classifier model, it does not pair well with the Random Forest model to create a successful model for predicting wage income. 

***

## Data

Data on the 2021 American Community Survey was obtained from the Integrated Public Use Microdata Series (IPUMS), the world’s largest individual-level population database. I selected a 0.1% sample size of the 2021 American Community Survey dataset and included the individual characteristics of age, gender, race, cognitive difficulty status, ambulatory difficulty status, 
citizenship status, English proficiency, area of residence, number of children, recency of childbirth, and wage income.

While the focus of this project was the effect of gender on wage income, I selected a variety of variables that either had potential to affect an individual’s wage income, or had been thoroughly researched in the past and proven to have correlation to wage income, to measure against the effects of gender. 

First, thorough processing of the dataset was necessary to make it usable for analysis. In the IPUMS database format, the values for each variable either represented a numerical value, or a numerical value that represented a categorical value that was noted in the dataset’s description upon download. For categorical variables, I transformed all numerical values into categorical descriptors in order to accurately represent their meaning. Certain numerical values also represented instances of illegibility, inapplicability to the individual, or missing answers, and had to be removed from the dataset. Particularly for the wage income variable, although the variable was numerical, the 999999 and 999998 values did not actually indicate the wage income earned by an individual, but instead represented missing values and inapplicability for an individual, and had to be removed. The wage income variable was also chosen over the total income variable because the total income variable included negative values, and when running a logistic regression model, values must be greater than zero for a logarithm to be taken. Additionally, a very small non-zero value (0.000001) had to be added to all wage income values because this variable included values of 0, and logarithms of 0 cannot be taken as well. 

***

## First-Look at Key Variables

Only individuals aged 16-49 were included in our analysis based on findings presented below, revealing that the age of peak income in the 2021 American Community Survey occurred at 49 years old. Beyond this age, income demonstrated a consistent decline. Individuals under the age of 16 were not included because minors under the age of 16 can only work limited hours, and would naturally have wage income limits because of this. 
[![screenshot][1]][1]

[1]: /assets/IMG/Figure1.png

I examine the wage income distribution by gender, as this is the primary variable being studied in the project. Figure 2 shows that there is a clear difference in average wage income for men and women. I also acknowledge that gender is not binary, however, for this project, gender is defined only as man and woman because of the constraints of the data. In the American Community Survey, gender is not differentiated from sex, and therefore only two options are available for an individual to choose when answering the survey - male or female. Therefore, for the purposes of this project, gender is defined as man or woman. 
[![screenshot][2]][2]

[2]: /assets/IMG/Figure2.png

I also examined the distribution of wage income upon educational attainment. Educational attainment encompassed high school completion, undergraduate degree completion, and advanced degree completion. The figure below illustrates a marked increase in wage income as years of schooling, and therefore completion of more advanced degrees, increases. This is important to note because while the main focus of this project was to examine the effects of gender on wage income, education has been widely studied as a mechanism of increased wages. The U.S. Bureau of Labor Statistics reported in 2020 that median usual weekly earnings increase and rates of unemployment decrease as level of degree attainment increases (U.S. Bureau of Labor Statistics).
[![screenshot][3]][3]

[3]: /assets/IMG/Figure3.png

I also examined the distribution of wage income upon the state an individual is residing in. Although wage income by state naturally varies based on type of work prevalent in the state, and individual state economies, it is interesting to note that Washington, D.C., denoted by State FIP code 11 in Figure 3, has a much higher average wage income compared to all other states, each of which are denoted by a specific state FIP code. It is also clear that average wage income can vary greatly by state, with variations of over $20,000 excluding Washington, D.C., and variations of over $40,000, including Washington, D.C. Given the wide variation in average wage income by state, I chose to include state as one of the predictors of the project’s models. 
[![screenshot][4]][4]

[4]: assets/IMG/Figure4.png

***

## Modeling

After cleaning the dataset, I chose to run three models. Given my dataset, with labeled data, it was appropriate to run supervised learning models, which all three models below are. All data was also split into training and testing data to properly test the models. Additionally, for all models, many of my predictor variables were categorical, and therefore had to be turned into dummy variables for the model.

The first model I ran was a Ridge Regression, using wage income as the target variable.  The predictor variables were metropolitan status, childbirth in the last year, race, citizenship, english speaking ability, ambulatory difficulty status, physical difficulty status, number of children, age, educational attainment, gender, and state. I chose to use the Ridge Regression model because this is a linear regression model that adds a penalty term to the sum of squared coefficients and therefore makes sure that predictors that are redundant or less impactful will not have as large of an impact on the model. Given that I am choosing 12 predictor variables, and many will be turned into dummy variables, and I am unsure of how meaningful certain predictors are, I wanted to make sure that I was not adding too many predictors to the model that may not actually be useful. The data for this model was also scaled

The second model I ran was a Random Forest Regression model with 100 estimators and a max depth of 6. This shallower depth ensures that the model will not encounter overfitting. I used the same predictor and target variables as in the Ridge Regression model. Rather than a linear regression with a penalty term, this model uses groups of decision trees to come to a final prediction. Given that I was unsure of the exact relationship between the predictor and target variable, I wanted to use this model to see whether a more complex and nonlinear model would be more appropriate for the data. 

The third model I ran was a Random Forest Classifier model. Differing from the first two models, this model uses a categorical target variable. Therefore, instead of using income wage as the target variable, I chose to use gender. By doing this, I am looking to see whether age, educational attainment, state, and income wage can accurately predict the gender of the individual. I chose to only include these predictor variables, and not the wider range included in the previous two models because I wanted to focus on the impact of average wage income, as well the variables discussed in the Data Section that have clear relationships with wage income. Another motivation for training this model was that I acknowledge that predicting specific wage income is complex, and therefore wanted to attempt a simpler prediction, between only two output options - male, or female. 

***

## Results

The first model, the Ridge Regression model, did not perform well. As shown in Figure 5, the accuracy of the model was poor. The R-squared on the testing data of this model was 0.11, while the RMSE was 10.26. This indicates that this model was not appropriate for the data. 
[![screenshot][5]][5]

[5]: assets/IMG/Figure5.png

While Ridge Regression does not have feature ranking, the coefficients for each variable can also be interpreted. Gender has the largest coefficient, meaning that in this model, gender plays a significant role in predicting wage income. 
[![screenshot][6]][6]

[6]: assets/IMG/Figure6.png

Figure 7 shows the accuracy of the Random Forest Regression model, and clearly indicates that this model was not successful in predicting the wage income of an individual. The R-squared on the testing data of this model was 0.15, while the RMSE was 10.03. These are both not good indicators for the model, and demonstrate that this was not an appropriate model for this data. 
[![screenshot][7]][7]

[7]: assets/IMG/Figure7.png

While the model did not perform well, it is still interesting to note that for feature importance, the age of the individual was most indicative of the wage income of the individual. The gender of the individual was the second most important feature, but significantly lower in importance than the age. 
[![screenshot][8]][8]

[8]: assets/IMG/Figure8.png

For the Random Forest Classifier Model, the model did not perform particularly well. The accuracy of the model was 56.22%, meaning that the model accurately predicted the gender of the individual a little over half of the time, given the set of predictors mentioned above. 
[![screenshot][9]][9]

[9]: assets/IMG/Figure9.png

The feature importance ranking for this model indicated that wage income was indeed the most important factor when predicting the gender of an individual, however, age and the state of the individual also had importance. 
[![screenshot][10]][10]

[10]: assets/IMG/Figure10.png

An additional metric was used to measure the Ridge and Random Forest Regression models. In Figure 11, the REC curves are shown for both models. This figure illustrates that the percentage of correct predictions is very low when tolerance is low. Even as tolerance rises up to 20, correction predictions do not reach 100%. This indicates that even with a large tolerance for error, the models are unable to correctly predict wage income.  Both models have very similar REC curves, demonstrating that despite a marginally higher R-squared for the Random Forest Regression model, both model do not predict wage income well. 
[![screenshot][11]][11]

[11]: assets/IMG/Figure11.png

***

## Discussion

As seen in the results portion of this website, none of the models performed well with this dataset.

Notably, the Random Forest regression model had a higher R-squared than the Ridge Regression model, indicating that the Random Forest model did marginally better than the Ridge Regression model, but still did not perform well. This could indicate that my dataset displays a more non-linear relationship because Random Forests are more well suited to dealing with complex, non-linear models, while Ridge Regressions are a form of linear regression. Figure 6 was also important to note in that the most important predictor variables for the Ridge Regression was gender. Therefore, while the model did not perform well, gender was still the most important predictor of wage income.

These two models may not have performed well because of the complexity of predicting the target variable. Wage income is subject to many factors, some of which may be under an individual’s control, but much of which is not. While certain relationships seem clear, such as in Figure 1, 2, 3, and 4, this does not mean creating a machine learning model for this data will yield meaningful results. The variables that I chose to predict wage income also may not have encompassed enough of the complexity of predicting wage income, and therefore the models would not be able to accurately predict wage income. 

The Random Forest Classifier model was also used to attempt to explore the relationship between gender and wage income from a different angle, but did not yield particularly good results as well, as seen in Figure 9. However, in this model, wage income did display the greatest feature importance in predicting gender, as seen in Figure 10. 

***

## Conclusion

In this project, three supervised machine learning models were used to try to predict the wage income of an individual based on a number of different characteristics drawn from the 2021 American Community Survey. 

The complexity of predicting the wage income of an individual rendered all the models unsuccessful. What can be taken away from this work however, is that gender does appear to have correlation with wage income, through examination of the feature importance and coefficients of predictors in the three models. 

In a future project, more research could be done on what factors could be influencing wage income, and therefore inform what variables should be chosen to include in a dataset for training a machine-learning model. 

***

### References

1. Aragão, C. (2023, March 1). Gender pay gap in U.S. hasn’t changed much in two decades. Pew Research Center. 
   https://www.pewresearch.org/short-reads/2023/03/01/gender-pay-gap-facts/
   
2. U.S. Bureau of Labor Statistics. (n.d.). Education pays, 2020 : Career outlook. U.S. Bureau of Labor Statistics.             
   https://www.bls.gov/careeroutlook/2021/data-on-display/education-pays.htm  

***

### Code

Here is a link to my Google Colab Notebook with the code for this project: 
https://colab.research.google.com/drive/1wMZWS4ghx-1ywyY0ZOI0fFVo2T7ofR5Q?usp=sharing 

Here is a link to the dataset used in my code:
https://drive.google.com/file/d/1BMZzHwad_tvnGtjP5FZmjOwL83CzFS0l/view?usp=sharing
