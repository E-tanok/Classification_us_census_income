This project is an assesment provided by the "Dataiku" software company.
![alt text](https://github.com/E-tanok/projects_pictures/blob/master/Classification/AssessmentDataiku/logo_dataiku.png)

# The project

This project aim is to study social census data in order to understand income levels of two populations.
We have also to put in place methods that make it possible to classify the populations.

Its data was extracted from the census bureau database found at http://www.census.gov/ftp/pub/DES/www/welcome.html
Donor: Terran Lane and Ronny Kohavi
Data Mining and Visualization
Silicon Graphics.
e-mail: terran@ecn.purdue.edu, ronnyk@sgi.com for questions.

The data was split into train/test in approximately 2/3, 1/3 proportions using MineSet's MIndUtil mineset-to-mlc.
Prediction task is to determine the income level for the person represented by the record.  
Incomes have been binned at the $50K level to present a binary classification problem, much like the
original UCI/ADULT database.

```
Dataiku instructions :
The archive contains 3 files:
o A large learning .csv file
o Another test .csv file
o A metadata file describing the columns of the two above mentioned files (identical for both)

The goal of this exercise is to model the information contained in the last column (42nd), i.e., which people make more or less than $50,000 / year, from the information contained in the other columns. The exercise here consists of modeling a binary variable.

Work with R or Python to carry out the following steps:
o Import the learning and text files
o Based on the learning file:

o Make a quick statistic based and univariate audit of the different columns’ content and produce the results in visual / graphic format. This audit should describe the variable distribution, the % of missing values, the extreme values, and so on.
o Create a model using these variables (you can use whichever variables you want, or even create you own; for example, you could find the ratio or relationship between different variables, the one-hot encoding of “categorical” variables, etc.) to model wining more or less than $50,000 / year. Here, the idea would be for you to test one or two algorithms, such as logistic regression, or a decision tree. Feel free to choose others if wish.
o Choose the model that appears to have the highest performance based on a comparison between reality (the 42nd variable) and the model’s prediction.
o Apply your model to the test file and measure it’s real performance on it (same method as above).

The goal of this exercise is not to create the best or the purest model, but rather to describe the steps you took to accomplish it.

Explain areas that may have been the most challenging for you.

Find clear insights on the profiles of the people that make more than $50,000 / year. For example, which variables seem to be the most correlated with this phenomenon?

Finally, you push your code on GitHub to share it with me, or send it via email.

Once again, the goal of this exercise is not to solve this problem, but rather to spend a few hours on it and to thoroughly explain your approach.
```


# Content

## Income_study notebook :
I provided analysis on both continuous and categorical columns.
I chose to remove some weakly informative columns for performance reasons.
I splitted data into train and test perimeter (75/25%).
      - I implemented a standard data scaler :
            - This scaler is fitted with the train data.
            - We use it to transform test data
      - I applied dimension reduction with PCA until it explained at least 91% of the data variance ratio.
            - Like before the PCA is instanciated and fitted with the train data. It only transform the test data.
This way allows to preprocess data by avoiding data leakage.
I implement 3 algorithms with cross validation : logistic regression, support vector classifier and random forest
I make a benchmark of the 3 algorithms.

## Income_final_model notebook :
I automated the preprocessing steps made in "Income_study.ipnb" with a class named "Data_Preprocessor" .
I load all the train ("census_income_learn.csv") and test ("census_income_test.csv") data and preprocess it.
I finally use the train preprocessed data in order to predict the test labels.


# Results

## Income_study notebook :
Accuracies on the 3 classifiers :

![alt text](https://github.com/E-tanok/projects_pictures/blob/master/Classification/AssessmentDataiku/acc_per_clf.png)

Average accuracies per classes and per classifiers :

![alt text](https://github.com/E-tanok/projects_pictures/blob/master/Classification/AssessmentDataiku/avg_acc_per_class_and_clf.png)
*The logistic regression is the algorithm which captures the best the higher income category informations*

## Income_final_model notebook :
The logistic regression is the algorithm which captures the best the higher income category: thatswhy I chosen to implement it on the final code (Notebook "Income_final_model").
Performances are close and slightly better than those of the "Income_study.ipnb" : A global accuracy of 95.3% and, with an accuracy of 38.5%, the model is 4.2% more precise on the higher income category predictions.
Here is this model ROC curve :

![alt text](https://github.com/E-tanok/projects_pictures/blob/master/Classification/AssessmentDataiku/final_model_roc_curve.png)


## Most challenging areas :

* The original columns of the two dataframes are not clean and I had to use the original documentation (census_income_metadata.txt) in order to have a proper schema.
* The dataset is huge : I had remove some weak informative columns and to reduce the dimension of data because models took more than a day to learn.
