## AOS C111 Final Project by Alcen Chiu <img align="right" width="220" height="220" src="/assets/IMG/template_logo.png">

**Introduction**

The gender pay gap has been a longstanding issue in the United States. In 2022, women earned roughly 82% of what men earned. This is similar to 2002, when women made roughly 80% of what men earned, showing that the gender pay gap has persisted at a similar rate over the past 20 years (Pew Research Center 2023). This machine learning model is motivated by this fact, and looks to see whether the gender of an individual plays a significant role in predicting an individual’s wage income.

This project utilizes the 2021 American Community Survey, an annual demographic survey conducted by the U.S. Census Bureau. This survey provided numerous characteristics of individuals in the U.S., including but not limited to the gender characteristics that were incorporated into the machine learning models in the project.  

The machine learning models I chose to use for this project were the SciKit Learn’s Random Forest Classifier and Random Forest Regressor, and Scikit Learn’s Ridge Regression. The results of these models showed that while gender ranks highly on the feature importance measure in the Random Forest Regressor model and is above 50% accuracy for the Random Forest Classifier model, it does not pair well with the Random Forest model to create a successful model for predicting wage income. 

**Data**

Data on the 2021 American Community Survey was obtained from the Integrated Public Use Microdata Series (IPUMS), the world’s largest individual-level population database. I selected a 0.1% sample size of the 2021 American Community Survey dataset and included the individual characteristics of age, gender, race, cognitive difficulty status, ambulatory difficulty status, 
citizenship status, English proficiency, area of residence, number of children, recency of childbirth, and wage income.

While the focus of this project was the effect of gender on wage income, I selected a variety of variables that either had potential to affect an individual’s wage income, or had been thoroughly researched in the past and proven to have correlation to wage income, to measure against the effects of gender. 

First, thorough processing of the dataset was necessary to make it usable for analysis. In the IPUMS database format, the values for each variable either represented a numerical value, or a numerical value that represented a categorical value that was noted in the dataset’s description upon download. For categorical variables, I transformed all numerical values into categorical descriptors in order to accurately represent their meaning. Certain numerical values also represented instances of illegibility, inapplicability to the individual, or missing answers, and had to be removed from the dataset. Particularly for the wage income variable, although the variable was numerical, the 999999 and 999998 values did not actually indicate the wage income earned by an individual, but instead represented missing values and inapplicability for an individual, and had to be removed. The wage income variable was also chosen over the total income variable because the total income variable included negative values, and when running a logistic regression model, values must be greater than zero for a logarithm to be taken. Additionally, a very small non-zero value (0.000001) had to be added to all wage income values because this variable included values of 0, and logarithms of 0 cannot be taken as well. 

**First-Look at Key Variables**

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

**Modeling**
1.	You can choose any theme [listed on this page](https://pages.github.com/themes/), though some do not work as well on mobile devices.
2.	From GitHub, edit `_config.yml` and replace the `theme:` line with `theme: jekyll-theme-name` where `name` is the name of the theme from the above list. **For the `minima` theme, use a shortened preface like so `theme: minima`**, the others seem to need the whole preface `theme: jekyll-theme-`. You can check the *Actions* tab (as in step 6. above) to make sure the site is building successfully.

### How to change your site logo (optional)
1. Some themes, such as `jekyll-theme-minimal`, show a logo. In your repository, upload a logo or profile picture to the `assets/IMG/` directory
2. Open `_config.yml` and modify the line `logo: /assets/IMG/template_logo.png` to point to your new image

***

## Guide to Adding Content
* Your repository's `README.md` file (the file you are reading now) acts like a home page. Replace its contents with whatever you want the world to see by editing the file on GitHub.
* If you want to turn this page into a CV or blog, etc., it may be useful to refer to a [guide for writing Markdown](https://www.markdownguide.org/basic-syntax/).
* You can create other markdown files (.md) in your repository and navigate to them from this page using links, i.e.: [here is a link to another file, `project.md`](project.md)
* When editing a markdown file on GitHub, it is useful to wrap text by selecting the *Soft wrap* option as shown: ![screenshot](/assets/IMG/instr_wrap.png)
* If you want to get even more technical, you can also write HTML in your .md files, and GitHub Pages will render it. For example, the image below is displayed by writing the following (edit this file to see!): `<img align="right" width="200" height="200" src="/assets/IMG/template_frog.png">`
<img align="right" width="337" height="200" src="/assets/IMG/template_frog.png"> 

***

## Delivering your Project

Your final project has three components: a dataset, a report, and your code.

### Dataset

A link to the dataset you used must be submitted on BruinLearn so that your course instructor can use it to run your code. To do this, it might be easiest to upload the dataset to Google Drive, then share a link (click *Share* then *Copy link*). If your dataset is too big to upload, try to find a way to reduce its size, or speak with your instructor if this is not possible.

### Report

Your report should be **delivered via your website**. Submit a link to your website on BruinLearn so that your instructor can browse it to find your report. 

To make this simple, you can write the report using a word processor or Latex, then export it as a .pdf file and upload it to the `assets` directory. You can then link to it [like so](/assets/project_demo.pdf). However, you can also type the report directly onto the website using another markdown page - [here is](/project.md) a template for that.

### Code

A link to your code must be submitted on BruinLearn, and the course instructor must be able to download and run your code using the dataset. The code could be in a Google Colab notebook (make sure to *share* the notebook so access is set to **Anyone with the link**), or you could upload the code into a separate GitHub repository, or you could upload the code into the `assets` directory of your website and link to it. 
