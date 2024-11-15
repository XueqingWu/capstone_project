# Social Insider Prediction Problem

**Capstone project delivered by Kelly (Hoi Mei) Tong, Annie (Xueqing) Wu, Harry (Haochong) Xia, Jaxon Yue**

**(Include Final Project for IDS 707 Data Visualization Course)**

## Index

1. [Problem Statement](#problem-statement)
    - [Goal](#goal)
2. [Benchmark Study](#benchmark-study)
    - [Conversion Problem](#conversion-problem)
    - [Imbalance](#imbalance)
    - [Background on Methods and Literature Review](#background-on-methods-and-literature-review)
3. [Data and Methods (Modeling)](#data-and-methods-modeling)
    - [Technical Details of Data Set](#technical-details-of-data-set)
    - [Methods and Model Links](#methods-and-model-links)
4. [Results](#results)
    - [Interpretation of Results](#interpretation-of-results)
        - [Data Visualization(For IDS 707 Final)](#data-visualization-(for-ids-707-final))
    - [Explanation of Results Tying to Goal](#explanation-of-results-tying-to-goal)
5. [Technical Documentation](#technical-documentation)
    - [Files Included](#files-included)
        - [Repo Files](#repo-files)
            - [Pipeline Files](#pipeline-files)
                - [What is Included](#what-is-included)
                - [How to Use](#how-to-use)
            - [App](#app)
                - [Functionality](#functionality)
                - [App Folder Contents](#app-folder-contents)
                - [How to Use the App](#how-to-use-the-app)

## 1. Problem Statement

*Socialinsider* is a social media analytics company that provides data and services for users, like influencers and marketers, to compare performance across channels, get competitor analysis, benchmarks and listening insights. Users have a 14 days free-trial and then can decide to subscribe to the service. *Socialinsider* is trying to gain more subscribed users in order to improve their revenue. The goal of the project is to discover patterns in user activities within *Socialinsider* website and to predict the likelihood of users subscribing the service. 

### 1.1 Goal

**To be completed by Annie**

## 2. Benchmark Study

### 2.1 Motivation
To compare our approach and results with industry-standard practices, we have discovered a benchmark study conducted by a researcher at Northwestern University. The original paper can be found [here](https://sites.northwestern.edu/aprilzhizhou/improving-e-commerce-conversion-rates-with-machine-learning/).

We picked this study because:
* **The study has a similar research problem:** predicting conversion rate from user event data from an e-commerce site.
* **The study uses similar data:** user event data on the e-commerce site from users around the world.
* **The study has an unbalanced dataset:** the overall conversion rate is around 3%. The study uses SMOTE (an oversampling method) to balance the dataset.

### 2.2 Benchmark Performance
The best-performing non-regression model in the benchmark study is an XGBoost classifier, which achieves a precision of 0.360 and a recall of 0.909. These metrics were used as a benchmark to compare our model's performance. Achieving similar results would indicate that our model is competitive with industry-standard practices.

## 3. Data and Methods (Modeling)

**To be completed by Annie**

### 3.1 Technical Details of Data Set

**To be completed by Annie**

### 3.2 Methods and Model Links

**To be completed by Annie**

## 4.Results

### 4.1 Interpretation of Results

With primarily optimization for recall while keeping a reasonable balance between tradeoff of precision for recall, Gradient Boosting model is considered as the best performing model among the list of models we experimented. This Gradient Boosting model trained with the transformed resampled data, has reached a recall of 0.8696 and a precision of 0.125. The recall indicates that the model accurately identifies 86.96% of all the users who would have converted and ensures an optimal capture of potential convertors. The precision of 0.125 indicates that 12.5% of predicted positives convert, with the remaining 87.5% identified as prospects—users who show traits of converters but haven’t converted yet. By directing more focused marketing toward these prospects, we anticipate increasing conversions. 

With comparison to the industry benchmark we have researched on, this result is very close to the goal. The industry benchmark has a recall of 0.909 and a precisio of 0.360. However, their data shows an original conversion rate of 3%, which is more than three times our conversion rate. With an even more umbalance dataset compared to the benchmark study, we consider our recall of 0.8696 and precision of 0.125 as huge improvement on the model prediction performance already. 

#### 4.1.1 Data Visualization(For IDS 707 Final)

<img width="567" alt="Screen Shot 2024-11-16 at 2 31 15 AM" src="https://github.com/user-attachments/assets/0880a174-c4d6-47fc-a5b8-851bc5d5b476">


### 4.2 Explanation of Results Tying to Goal

As demonstrated by the visualization and previous context, our model is selected mainly based on recall optimization. Optimizing for recall ensures least probability in losing our potential user who would have converted. While optimizing for precision would make the model overly conservative, predicting most cases as negative due to the data’s imbalance. In the case of optimizing for precision, only 2 to 5 cases will be predicted as positive and actually converted in real life. This would be less effective for a marketing-focused model like ours. 

(More explanation on the difference between precision and recall is explained in conextual section of "Final Project for IDS 707 Data Visualization Course."

## 5. Technical Documentation

### 5.1 Repo Files

This repo contains all the necessary files and code to replicate our project. The main folders are `Data_Pipeline`, `EDA_Files`, and `App`. Each folder contains the necessary files to run the pipeline, exploratory data analysis, and the web application. 
- **requirements.txt**: Lists all the dependencies required to run the pipeline code smoothly.

#### 5.1.1 Pipeline Files

The pipeline files are located in the `Data_Pipeline` folder. They include all the processes required to transform the original event-level data to user-level data. This step is essential for data preprocessing before modeling.

##### What is Included

- **Social_Insider_Data_Pipeline.ipynb**: This Jupyter notebook contains all the necessary transformations for the original event-level data to user-level data. It involves data cleaning, feature engineering, and aggregation steps to prepare the data for the modeling phase.


##### How to Use

1. Clone the repository from GitHub to your local machine.
2. Install the required packages by running `pip install -r requirements.txt` in your terminal.
3. Open the `Social_Insider_Data_Pipeline.ipynb` Jupyter notebook and run the cells step by step to transform the original data into user-level features.
4. Make sure all the paths specified in the notebook align with your local file structure.

## 6. Web App

### 6.1 App Introduction
The **Customer Conversion Prediction Tool** is a Streamlit web application that automates our pipeline for predicting user conversion rates. The app takes in raw event data, preprocesses it,  uses our best-performing model (Gradient Boosting Classifier) to predict the conversion rate of each user, and outputs the results in a downloadable CSV file.

### 6.2 Components of the App Folder
The `App` folder contains the following components:

| File Name           | Description                                         |
|---------------------|-----------------------------------------------------|
| `best_model.pkl`    | The best-performing model we trained (Gradient Boosting). |
| `cvr_prediction_app.py` | The main Streamlit application script.          |
| `requirements.txt`  | A list of dependencies required to run the app. This includes libraries such as Streamlit, pandas, and scikit-learn. |
| `scaler.pkl`        | A saved `StandardScaler` object used to scale the data during model training and inference. This ensures the uploaded data is scaled correctly before making predictions. |
| `socialinsider_logo.png` | The logo displayed in the app interface.         |

### 6.3 Using the App

1. **Go to the App website:**  
   [http://sipredict.streamlit.app](http://sipredict.streamlit.app)

2. **Upload the event data:**
    - Click the `Browse files` button to upload your event data in CSV format.
    - The app expects the data to have the same format as the raw event data, which can be found in the `Data` folder.

3. **View/Download the prediction results:**
    - The app will preprocess the data, applies necessary transformations, and computes predictions using the best model.
    - The results will be displayed in a sortable and interactive table.
    - You can also download the results as a CSV file by clicking the `Download Results CSV` button.
  
------------------------------------------------------------------------------------------------------------------------

#### Final Project for IDS 707 Data Visualization Course

The same information can be found in [Capstone_Visual_Final_Project_IDS707.pdf](Capstone_Visual_Final_Project_IDS_707.pdf) on the main branch here. This pdf version provides a clearer view for the plot. 

###### Contextual Explanation: 

This prediction project is done in collaboration with our client Social Insider. Social Insider provides business insights to marketing teams in large corporations by offering data analysis and comparison across business social media accounts. They have provided a 14-days free trial for trials before official subscription to their service. Currently, they would like to predict whether their free users will purchase subscriptions base on their event logs. Our classification machine learning model targets at correctly predicting these converted subscribe users. 

The current conversion rate (number of subscribed users over total users) is less than 1%, which leads to an extremely imbalance dataset. This has cause “accuracy” no longer a valid and appropriate matrix for measuring model performance. Hence, it was a common agreement reached during our discussion with client Social Insider that Recall is the performance matrix we should optimize for. The core of the reason lies in the formula difference between recall and precision: 

Recall = TP / (TP+FN), and 

Precision = TP = (TP+FP), 

Where: 
TP = True Positive (Users who would have subscribed and has correctly been predicted as positive subscribe user)
FN = False Negative (Users who would have subscribed and has incorrectly been predicted as non-subscribe user)
FP = False Positive (Users who would NOT have subscribed and has incorrectly been predicted as subscribe user)

Optimizing recall tries minimizes False Negative (FN) which has a larger cost than False Positive (FP) in our scenario. Our current conversion rate is less than 1%. The cost of losing a user who would have subscribed (due to wrong prediction) is larger than the cost of extra marketing to users who would not have subscribed (no matter how much marketing they receive). Hence, we primarily use recall as the indicator matrix for choosing our best prediction model. 

###### Visualization:

<img width="567" alt="Screen Shot 2024-11-16 at 2 31 15 AM" src="https://github.com/user-attachments/assets/383edbc5-c046-429c-905d-ea165cc15593">


#### Description
This Github repository serves as the primarily record of our capstone team project. The project cooperates with the Social Insider company to accomplish 2 main goals: 1. developing an algorithm to predict user behavior (subscribe/purchase to Social Insider services) base on a series of events conducted by the user; 2. predicting the follower count and average engagement rate of social media pages based on historical performance data. 

#### Using Guide

`Step 1: ` Clone the entire Github repository to local. (Make sure everything is up to date with Git Pull) 

`Step 2: ` Directly run the code from the jupyter notebooks. (everything, including path, is already set up and prepared for direct running) 

`Step 3: ` Descriptions and commennts in the jupyter notebooks support better understanding of the process. 

#### Overall Timeline

![timeline](https://github.com/user-attachments/assets/13acd1ba-d3a2-4f16-82e2-ceb16a748575)

#### Important Files Included: 
- `Data Folder: `
    - socialinsider_events_2024.csv data files which are labeled with the associated month. Ex. socialinsider_events_2024-05.csv is the event data in May 2024. 
- `Data_Pipeline Folder: `
    - Social_Insider_Data_Pipeline.ipynb: a jupyter notebook that involves all processes for transforming original event-level data to user-level data, which serves as the data preprocessing stage before modeling.
- `EDA Files Folder: `
    - Social_Insider_EDA_DataViz.ipynb: a jupyter notebook that includes all the processing code for generating the exploratory data analysis visualizations
    - Socialinsider Exploratory Data Analysis.pdf: a report that includes main details of our exploratory analysis outcomes. The report explains data insights with visualizations as well as pipeline transformation process. 
 
#### Example User Journey on Social Insider Platform

![whiteboard_exported_image](https://github.com/user-attachments/assets/1e245042-408c-42d0-8607-1b02f862e7bb)
 
#### Exploratory Analysis Summary

`1. Data Overview: `

<img width="759" alt="截屏2024-10-08 04 22 17" src="https://github.com/user-attachments/assets/aaaa0f6a-8624-4ce8-89f9-59d87a85de50">

`2. Example Visualizations: `

More visualizations and exploratory analysis details can be fold in "Social Insider Exploratory Data Analysis" file. 

![visual1](https://github.com/user-attachments/assets/69135750-9b38-4841-940e-032b8df9da71)

![visual2](https://github.com/user-attachments/assets/7fca8f0f-d0b8-45cb-9975-f378c0673d82)

`3. Pipeline Transformation: `
A simplified diagram for explaining the pipeline transformation:

<img width="1161" alt="截屏2024-10-08 04 20 17" src="https://github.com/user-attachments/assets/a4c18974-8c1b-4da8-a0f5-a82b57340b1b">

Based on our EDA insights, we have done data cleaning and feature engineering, in which we have built a pipeline for transforming the original event-level data to user-level data. In the original data, each row is representing each event done by the user and its associated information such as load time, platform etc. In the transformed data, each row is representing behaviors and features related to every unique user. There are in total 50 features that have been transformed by the pipeline currently. These mainly include conversion, country, country_xxx (whether the user belong to one of the top 5 buy sucess country), load time, count of specific events, count of each specific platform and count for each type of view.

Transformed Features Include: 
- Conversion
- Country--select the first country shown at the event
- Country_"countryname" -- whether the user belongs to one of the top 5 conversion rate countries
- Aggregated Load Time
  - Average Load time
  - Maximum load time
- Count of events for each user (events that can potentially distinguish whether users can convert)
  - bench load success
  - profile search success
  - add profile success
  - pricing modal visited
  - profile load fail
  - email receipt
- Count of each platform--combined categories
  - Examples: 
  - Facebook & fb -----> fb -----> platform_fb_count
  - Twitter & tw  -----> tw -----> platform_tw_count
- Count for each type of view (19 categories)
  - Examples: 
  - Profile  ----->  view_profile
  - Projecthome ----->  view_projecthome
