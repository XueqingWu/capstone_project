# Social Insider Prediction Problem

Capstone project delivered by Kelly (Hoi Mei) Tong, Annie (Xueqing) Wu, Harry (Haochong) Xia, Jaxon Yue

## Index of Markdown

1. [Final Project for IDS 707 Data Visualization Course](#Final-Project-for-IDS-707-Data-Visualization-Course)
    - [Contextual Explanation](#Contextual-Explanation)
    - [Visualization](#visualization)
2. [Description](#description)
3. [Using Guide](#using-guide)
4. [Overall Timeline](#overall-timeline)
5. [Important Files Included](#important-files-included)
6. [Example User Journey on Social Insider Platform](#example-user-journey-on-social-insider-platform) 
7. [Exploratory Analysis Summary](#exploratory-analysis-summary)
   
## Customer Conversion Prediction Tool (Web App)
### Introduction
The **Customer Conversion Prediction Tool** is a Streamlit web application designed to help you predict customer conversions based on uploaded event data.

 By leveraging a machine learning model, the app analyzes user behavior, computes conversion probabilities, and displays results in an easy-to-understand format. Users can sort and explore the results directly in the app and download the predictions as a CSV file for further analysis.




#### Final Project for IDS 707 Data Visualization Course

The same information can be found in [Capstone_Visual_Final_Project_IDS707.pdf](Capstone_Visual_Final_Project_IDS707.pdf) on the main branch here. This pdf version provides a clearer view for the plot. 

###### Contextual Explanation: 

This prediction project is done in collaboration with our client Social Insider. Social Insider provides business insights to marketing teams in large corporations by offering data analysis and comparison across business social media accounts. They have provided a 14-days free trial for trials before official subscription to their service. Currently, they would like to predict what conditions lead to the conversion of their free users in purchasing subscriptions. Our classification machine learning model targets at correctly predicting these converted subscribe users. 

It was a common agreement reached during our discussion with client Social Insider that Recall is the performance matrix we should optimize for. The core of the reason lies in the formula difference between recall and precision: 

Recall = TP / (TP+FN), and 

Precision = TP = (TP+FP),

Where: 

TP = True Positive (Users who would have subscribed and has correctly been predicted as positive subscribe user)

FN = False Negative (Users who would have subscribed and has incorrectly been predicted as non-subscribe user)

FP = False Positive (Users who would NOT have subscribed and has incorrectly been predicted as subscribe user)

Optimizing recall tries minimizes False Negative (FN) which has a larger cost than False Positive (FP) in our scenario. Our current conversion rate is less than 1%. The cost of losing a user who would have subscribed (due to wrong prediction) is larger than the cost of extra marketing to users who would not have subscribed (no matter how much marketing they receive). Hence, we primarily use recall as the indicator matrix for choosing our best prediction model. 

###### Visualization:

<img width="571" alt="Capstone_Visual_Final" src="https://github.com/user-attachments/assets/4b5c8d58-6fb2-47d4-a28b-461d90aff62b">


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
