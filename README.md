# Udacity_Data_Science_Project1
My solution to the first project of the Udacity data science Nanodegree

![figure0](https://user-images.githubusercontent.com/65665840/112819315-c29bb800-9084-11eb-84e6-4814f39b6fdf.jpeg)
(Image by IFATCA)

This repository contains a jupyter notebook that was created to navigate through the first project of the Uadacity data science Nanodegree program. It contains the code used to answer three questions regarding a dataset containing COVID-19 related data from https://github.com/owid/covid-19-data/tree/master/public/data

This repository includes the following relevant files:
- Project_1_solution.ipynb: This Jupyter notebook contains all the code and the analysis for the project. The notebook uses Python 3 and the Pandas, the Numpy, the sklearn and the matplot library.
- owid-covid-data.csv: The data file for the Jupyter notebook.

Three results were concluded from the project:

1) different approaches to the vaccination process result in big differences in the amount of time required to reach herd immunity. In the two example cases, it may take half a year to reach herd immunity in contrast to about two years.

![figure1](https://user-images.githubusercontent.com/65665840/112819550-fecf1880-9084-11eb-8878-b46440050209.png)

2) when using a linear regression approach, no satisfying model can be crated to investigate the relation between the number of people fully vaccinated and other parameters although the human development index is the driving factor for the training data when all features are used.

![figure3](https://user-images.githubusercontent.com/65665840/112819605-0bec0780-9085-11eb-8e37-6f2af60e48b6.png)

3) two of the main contributing factors to a high COVID-19 death rate are the (inverse) human development index (a lower index gives a higher death rate) and the reproduction rate.

![figure4](https://user-images.githubusercontent.com/65665840/112819634-14444280-9085-11eb-8ebf-a927abb400b5.png)

Acknowledgment 
This repository uses data from https://github.com/owid/covid-19-data/tree/master/public/data. In addition the first presented image is taken from IFATCA. Some of the funtions used in the notebook are taken from the Udacity course and adopted for the pupose of creating this project.

Detailed description

Business Understanding

This project aims at using the CRISP-DM process. In particular, I analysed data with regard to COVID-19 to answer the following questions:
-When will herd immunity will be reached?
-What factors from the data contribute to a high COVID-19 vaccination rate?
-What factors from the data contribute to a high COVID-19 death rate?

Data Understanding

This repository uses data from https://github.com/owid/covid-19-data/tree/master/public/data. The datafile contains entries for every day and a lot of countries since March 2020. In the columns, specific data is some form related to COVID-a9 are stored. For instance, the total number of COVID-19 cases, the number of people vaccinated and the total number of deaths in a given country. In addition, the data contains smoothed data and data per a certain number of inhabitants (i.e. number of deaths per million). Furthermore, the data contains some parameters describing the environment in a given country (i.e. human development index, mean age of the population, population and more). A description of each colum is provided in https://github.com/owid/covid-19-data/tree/master/public/data. I wanted to find out, how the vaccination process is going and how the different factors in the data contribute to vaccination rates and number of deaths.

Prepare Data

In this step, the data was cleaned. Generally, I dropped all the rows that did not contain data for the colum that was relevant for the respective question. For example, for the number of people fully vaccinated in the first question, I dropped all rows that did not contain data in that column. Most of the data did not contain an entry for dated before the start of the vaccination process, so they were irrelevant. Sometimes a value was missing for a day or two but imputing those values did not make too much sense before the modeling of the data. Any imputed value would have biased the data, especially when using all conties to impute the data because the countries differ too much.

The same is true for the two other questions. I dropped the rows that did not contain data for the column in question. Then, I selected one (most recent) date with the biggest number of entries. I dropped all other dates because if you are using all datesm the data will get biased by the multiple entries for each country. I also dropped the "absolute" colums becase I was interested in the normalized data (per hundred, thousand, million). Furthermore, I dropped colums that did not contain values. As discussed, imputing values doeas not make sense due to the vast differences in the individual countries.

Data Modeling

In this step, I created models for the three questions above. For the first question, I used data from Germany and the USA to model a prediction for the number of people vaccinated over time. I wanted to find out, when 80% of the respective popuation is fully vaccinated. I fitted a linear regression model with a 2nd degree polynomial to the data and predicted the numbers for the future.

For the second question, I tried to fit a linear regression model in order to find our what contributing factors are in the data to a high vaccination rate. I searched for an optimal model variying the number of features used for the model.

For the third question I did the same thing, trying to find out what factors contribute to the death rate for a given country.

Evaluate the Results

For question 1, I came up with the following graph:

![figure1](https://user-images.githubusercontent.com/65665840/112831269-00540d00-9094-11eb-938f-ce05a50f43d3.png)

The figue shows, that different approaches to the vaccination process result in big differences in the amount of time required to reach herd immunity. In the two example cases, it may take half a year to reach herd immunity in contrast to about two years. The model r2 scores are above 0.99, so the confidence is pretty high.

R2 score of training data for USA:
0.9986557935849394
R2 score of test data for USA:
0.998835952712302
R2 score of training data for GER:
0.9979308836409566
R2 score of test data for GER:
0.9965484114016288

For question 2, I tried to fit a model with the data but the results were not too good. 

R2 score training data
0.7769935296683523
R2 score test data
-2.403775037423565

I looked at the coefficients for the model and came up with this inconclusive result:

![figure2](https://user-images.githubusercontent.com/65665840/112831385-25488000-9094-11eb-8e63-43e6961d7d81.png)

When using all features the score gets even worse:

R2 score training data
0.7175317467906196
R2 score test data
-7.449719019824565

Looking at the coefficients yiels following table:

![figure3](https://user-images.githubusercontent.com/65665840/112833103-8cffca80-9096-11eb-8fb5-d194c27a95e5.png)

It seems that human development index is a factor contributing to a high vaccination rate but the confidence in the model is rather low.

For the third question, I came up with the following table:

![figure4](https://user-images.githubusercontent.com/65665840/112833224-bc163c00-9096-11eb-83ff-ada480f75eaa.png)

The r2 scores are not too good for the test data:

R2 score training data
0.9733499625909201
R2 score test data
0.47448420343498887

How ever, some trnds are visible. It seems that two of the main contributing factors to a high COVID-19 death rate are the (inverse) human development index (a lower index gives a higher death rate) and the reproduction rate.

