# Music Genre Classifier
Day in and day out, as the number of songs keeps growing, it is very important to classify 
these songs into the correct genres so that people can continue to listen to music that they like.
In this project, we aim to create a solution where we use different models in order to classify 
songs into their correct genre. The models will also be tested on their performance using ROC 
Curves.

## The Problem
Everyone has a preference, a particular genre, or a few genres that they like more than the 
others when it comes to music. Therefore, with this project, we aim to build Music Genre 
Classifier which will help with classifying songs into different genres(classes) so that people can continue discovering music according to their taste.

## Description of Dataset
In this project, I will be following the dataset that is present on Kaggle. The file I will be using is named ("train.csv"). This file contains 17,996 rows and 17 columns. Few of the variables are “Popularity, “danceability”, “energy”, “Class”, etc.

## Initial impressions of the data:
*   Tracks had an average popularity score of 44.5
*   Majority of the songs were highly danceable and had high energy
*   Average length of a track was 3.3 minutes
*   3 of the variables have missing values and 'instrumentalnes' has a high missing value percentage. We will check the correlation between these variables later on and decide what to do.
*   There are 11 different classes of tracks and it appears to be imbalanced, and I work on the imbalance later on.

## Insights from Exploratory Data Analysis:
- There are 11 different target classes and they are imbalanced severely.
- From the correlation heatmap I see:
  - Loudness and Energy are highly correlated
  - Acousticness and Energy are highly correlated
  - Loudness and Acousticness are highly correlated
- I can see alot of these variables have outliers, which means later on in the data preprocessing, it would be better not to use Standard Scaler for scaling the dataset. Also, since the number of outliers are high, I am not sure if the dataset has human errors which have caused these outliers, so I will leave the outliers as it is.

## Data preprocessing
- In this step, first I handled missing values by replacing them with the average of the variable of the class to which the record belonged to.
- Then I converted the time signature variable by creating dummies as it is a categorical field
- Then I used Robust Scaler to transform the data as their are lot of outliers and this scaling technique is good for datasets with outliers
- Finally, I used Stratified Shuffle Split to split the dataset as the dataset was highly imbalanced

## Model Selection
- In this step I first started with few models to create a baseline model and get their performance on the processed dataset using different classifiers.
  I found the top two performing classifiers to be Balanced Random Forest Classifier and Balanaced Bagging Classifier with macro f1 scores of 0.605 and 0.598
- As the datasets were unbalanced, I used sampling and weight adjusting to assess performance of the normal Random Forest and Bagging Classifier and see if it performed better than than the balanced baseline models.
- After adjusting weights, the performance of both the normal models improved as for random forest and bagging classfier I got macro f1 scores of 0.630 and 0.639 resepctively.
- After sampling(using SMOTE-Tomek), the performance of both the normal models were better than the baseline models but not better than the models after weight adjusting as the macro f1 scores were 0.621 and 0.612.
- Finally, I selected the Random Forest Classifier and Bagging Clasifiers as the final models after weight adjusting.

## Model Evaluation:
- Here I saw that both the models were struggling to classify Class1 tracks and were also having trouble with class 6 and 10 tracks.
- Both the models performed well above average based on the classification report.

## Final Conclusion:
- As this was a dataset with 11 classes which were highly imbalanced, I tried to implement different methods like, using re-sampling and weight adjusting, the cross validation, using ensemble methods, hyperparameter tuning and feature engineering to handle this imbalance.

- We can see that both the models had very similar performance.

- Both the models are having hard time trying to classify Class 1 tracks.

- I would select the Bagging Classifier as the final model as it is able to classify Class 1 tracks better than the Random Forest Classifier and has comparatively better macro f1 score.

## Future Scope:
- We can select the important features from the dataset and then retrain the models on those particular set of features to see performance improvement.
- As few of the variables are skewed, I tried applying few transformation methods, but the variables were not showing improvement in their distribution, so something can be done about that.
- As there were lot of outliers, we can use different methods to remove outliers above a certain threshold and see the perfomance.
