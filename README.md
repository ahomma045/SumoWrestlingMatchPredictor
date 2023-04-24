# SumoWrestlingMatchPredictor

## Overview & Problem Statement 
Sumo wrestling is a sport that originated in Japan, with a history spanning centuries. It has become an integral part of Japanese culture and tradition, captivating audiences with its unique combination of athleticism and strategy.

In this project, we will be analyzing data on sumo wrestlers to predict the outcome of matches. The dataset contains information on wrestlers’ physical characteristics such as their height and weight, as well as details on each wrestler's rank and the result of each tournament match.

The goal is to use machine learning algorithms, such as logistic regression, decision trees, and random forests to build a prediction model that will achieve an accuracy score of at least 0.75.

This model will be valuable for both fans and practitioners of sumo wrestling, providing insights into the key factors that contribute to a wrestler’s success or failure.

Additionally, a Tableau dashboard will be created to visualize the data and predictions, allowing sumo fans and practitioners to explore and interact with the data in a meaningful way.

--- 

## Data
This project uses two datasets, banzuke.csv and results.csv, from [data.world](https://data.world/cervus/sumo-japan). They contain information about sumo rankings, the results of each oturnament match, wrestler's pysical characteristics and personal information such as weight, height, hometown and birth date. The datasets are available in CSV format. 

---

## Tableau Visualizations 
In addition to traditional data analysis using Python, we also used Tableau for exploratory data analysis (EDA). 

- [Sumo Wrestling Outcome Prediction | EDA](https://public.tableau.com/views/SumoWrestlingOutcomePredictionEDA/D_Prediction_Height_Weight?:language=en-US&:display_count=n&:origin=viz_share_link): These charts explore the relationship between various features of sumo wrestlers such as height, weight, age, and rank and their likelihood of winning a match.

In addition, we created interactive dashboards for sumo fans and practitioners.  
- [Sumo Wrestling Matches & Results Dashboards](https://public.tableau.com/views/SumoWrestlingMatchesResults/D_Tournament_Info?:language=en-US&:display_count=n&:origin=viz_share_link): These dashboards allow users to filter and view sumo wrestling matches and results based on various criteria, such as tournament, wrestler, and outcome.

---

## Models 
We use PyCaret, an open-source machine learning library in Python that automates machine learning workflows with minimal coding required. PyCaret allowed us to spend less time coding and more time analyzing data, by automating many of the repetitive tasks involved in the modeling process. Using PyCaret, we developed and tested a variety of different models.

We started by developing classification models using the existing numeric data to see how they performed before any feature engineering was done. Once we had a benchmark, we developed models incorporating new features created as part of our feature engineering process. This allowed us to see how these new features impacted the performance of our models, and whether they improved the ability to predict the outcome of matches.

---

## Results 
The model performance was evaluated using several metrics such as accuracy, AUC, recall, precision, F1-score, Kappa, Matthews correlation coefficient (MCC), and training time (TT). 

While the baseline for model performance was 0.5, all models using the existing numeric data have an accuracy above the baseline. However, the highest accuracy achieved by Extreme Gradient Boosting was only 0.5713, indicating that the performance of all models performed only slightly better than random guessing.

Next, we developed models incorporating new features. Overall, these models perform better than those with existing numeric data only. The evaluation metrics for each model incorporating new features are as follows:

| Model | Description | Accuracy | AUC    | Recall | Prec.  | F1     | Kappa  | MCC    | TT (Sec) |
|--|--|--|--|--|--|--|--|--|--|
| lightgbm | Light Gradient Boosting Machine | 0.7799 | 0.8785 | 0.7795 | 0.7802 | 0.7798 | 0.5598 | 0.5599 | 4.9240 |
| xgboost | Extreme Gradient Boosting | 0.7796 | 0.8781 | 0.7805 | 0.7791 | 0.7798 | 0.5592 | 0.5593 | 48.9350 |
| gbc | Gradient Boosting Classifier | 0.7731 | 0.8730 | 0.7777 | 0.7706 | 0.7741 | 0.5462 | 0.5462 | 65.6110 |
| lda | Linear Discriminant Analysis | 0.7720 | 0.8677 | 0.7695 | 0.7734 | 0.7714 | 0.5440 | 0.5440 | 1.8290 |
| ridge | Ridge Classifier | 0.7719 | 0.0000 | 0.7695 | 0.7733 | 0.7714 | 0.5439 | 0.5439 | 0.6030 |
| rf | Random Forest Classifier | 0.7686 | 0.8678 | 0.7623 | 0.7721 | 0.7671 | 0.5372 | 0.5373 | 53.2930 |
| et | Extra Trees Classifier | 0.7672 | 0.8656 | 0.7616 | 0.7702 | 0.7659 | 0.5344 | 0.5344 | 45.1910 |
| ada | Ada Boost Classifier | 0.7631 | 0.8642 | 0.7598 | 0.7658 | 0.7621 | 0.5262 | 0.5272 | 13.9880 |
| qda | Quadratic Discriminant Analysis | 0.7610 | 0.8454 | 0.7624 | 0.7602 | 0.7613 | 0.5219 | 0.5219 | 1.1990 |
| lr | Logistic Regression | 0.7606 | 0.8430 | 0.7537 | 0.7643 | 0.7589 | 0.5212 | 0.5213 | 24.1150 |
| nb | Naive Bayes | 0.7434 | 0.8282 | 0.7405 | 0.7447 | 0.7426 | 0.4867 | 0.4867 | 0.5010 |
| dt | Decision Tree Classifier | 0.7078 | 0.7078 | 0.7087 | 0.7074 | 0.7081 | 0.4156 | 0.4156 | 3.8840 |
| svm | SVM - Linear Kernel | 0.6626 | 0.0000 | 0.5944 | 0.7376 | 0.6220 | 0.3251 | 0.3668 | 17.4540 | 
| knn | K Neighbors Classifier | 0.5625 | 0.5877 | 0.5630 | 0.5625 | 0.5627 | 0.1250 | 0.1250 | 46.1080 | 
| dummy | Dummy Classifier | 0.50000 | 0.5000 | 0.5000 | 0.2500 | 0.3333 | 0.0000 | 0.0000 | 0.3660 | 

Based on these results, Light Gradient Boosting Machine and Extreme Gradient have similar accuracy and AUC scores, but Light Gradient Boosting Machine performs better in identifying positive values, as shown by its slightly higher precision score.

---

## Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|basho|float64|banzuke.csv|tournament month as yyyy-mm|
|id|int64|banzuke.csv|ID|
|rank|object|banzuke.csv|rank|
|rikishi|object|banzuke.csv|name|
|heya|object|banzuke.csv|'room', an organization of sumo wrestlers|
|shusshin|object|banzuke.csv|hometown|
|birth_date|object|banzuke.csv|birth date|
|height|float64|banzuke.csv|height|
|weight|float64|banzuke.csv|weight|
|prev|object|banzuke.csv|rank in previous tournament|
|prev_w|float64|banzuke.csv|number of wins in previous tournament|
|prev_l|float64|banzuke.csv|number of losses in previous tournament|
|basho|float64|results.csv|tournament month as yyyy-mm|
|day|int64|results.csv|day number (16 for play-off)|
|rikishi1_id|int64|results.csv|first wrestler ID|
|rikishi1_rank|object|results.csv|first wrestler rank|
|rikishi1_shikona|object|results.csv|first wrestler ring name|
|rikishi1_result|object|results.csv|first wrestler result after the bout (final result in brackets)|
|rikishi1_win|int64|results.csv|1 for win, 0 for defeat|
|kimarite|object|results.csv|a type of technique used in sumo by a rikishi to win a match|
|rikishi2_id|int64|results.csv|second wrestler ID|
|rikishi2_rank|object|results.csv|second wrestler rank|
|rikishi2_shikona|object|results.csv|second wrestler ring name|
|rikishi2_result|object|results.csv|first wrestler result after the bout (final result in brackets)|
|rikishi2_win|int64|results.csv|1 for win, 0 for defeat|