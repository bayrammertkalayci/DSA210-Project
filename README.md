Personal YouTube Watch Habits Analysis: Modeling Popularity, Category, and Timing

(October 31, 2025)

Abstract

This project analyzes my personal YouTube viewing history to explore the relationship between my digital consumption patterns and public video metrics. The core methodology involves combining a private dataset of my watch history, obtained via Google Takeout, with a public dataset of video metadata, collected using the YouTube Data API v3. The aim is to understand how my viewing habits (e.g., time of day, day of week) correlate with content attributes (e.g., category, view count, like count). The project applies the full data science pipeline—including JSON parsing, API data collection, data merging, feature engineering, statistical testing, and machine learning—to identify significant relationships and build a predictive model of my content choices.

Motivation

I chose this topic because YouTube is a significant and integrated part of my daily information consumption. I am interested in uncovering the hidden patterns within my own digital behavior, moving beyond simple screen time metrics to understand the drivers of my choices. This project allows me to explore the relationship between my personal, private decisions (what I click on) and public, external factors (such as a video's category or its mainstream popularity). By applying data science techniques to a dataset that is uniquely my own, I can gain practical experience in data enrichment (merging personal and public data), API usage, and behavioral modeling, all of which are core interests of mine.

Objectives

To apply the full data science pipeline to a unique, personal dataset.

To statistically analyze the relationship between my viewing time (hour of day, day of week) and the category of content I consume.

To test whether my viewing habits lean towards "niche" (low view-count) or "mainstream" (high view-count) content, and whether this differs by category.

To build and evaluate a machine learning model (e.g., Decision Tree) that predicts the category of a video I watch based only on the temporal context (time and day) of the viewing.

To gain hands-on experience with JSON parsing, API integration, and data merging.

Data Sources

This project uses a hybrid model, combining a private dataset with a public API-driven dataset. Both are ethically obtained and clearly sourced.

Dataset

Description

Source

Personal Watch History

My private, timestamped watch history (watch_timestamp, video_title, video_ID).

Google Takeout

Video Metadata (Enrichment)

Public video details (categoryName, viewCount, likeCount, duration).

YouTube Data API v3

Both datasets will be merged using the video_ID as the primary key.

Methodology

1. Data Collection & Cleaning

Request and download the "YouTube and YouTube Music" data archive from Google Takeout.

Write a Python script to parse the watch-history.json (or .html) file to extract watch_timestamp and video_ID.

Obtain a free API key for the YouTube Data API v3 from the Google Cloud Console.

Write a second Python script to loop through the unique video_ID list from my Takeout data.

Send an API request (call) for each video_ID to fetch its public metadata.

Handle errors for deleted, private, or region-locked videos (e.g., using try-except blocks) to prevent script failure.

Store the API results and merge the two datasets on video_ID.

2. Feature Engineering

Convert the raw watch_timestamp string into new features: hour_of_day, day_of_week, and is_weekend (binary).

Convert the API's duration string (ISO 8601 format, e.g., "PT10M5S") into total seconds or minutes for numerical analysis.

3. Exploratory Data Analysis (EDA)

Generate descriptive statistics (mean, median, min, max) for viewCount and likeCount.

Visualize viewing frequency using a heatmap (x-axis: day_of_week, y-axis: hour_of_day).

Plot histograms to understand the distribution of viewCount and likeCount (likely requiring a log transformation).

Create bar charts for the top 10 most-watched categoryName and channels.

4. Statistical Testing & Modeling

Hypothesis Testing:

Chi-Square Test: To check for independence between day_of_week (categorical) and categoryName (categorical).

T-Test / ANOVA: To compare the mean viewCount (numerical) across different categoryName groups (categorical).

Pearson Correlation: To test the relationship between viewCount and likeCount (numerical vs. numerical).

Machine Learning (Classification):

Goal: Predict categoryName (e.g., "Education", "Gaming").

Features (X): hour_of_day, day_of_week, is_weekend.

Target (Y): categoryName.

Model: Decision Tree Classifier or Random Forest to identify the most predictive temporal features.

Hypotheses

#

Hypothesis

Null Hypothesis (H₀)

Alternative Hypothesis (H₁)

1

Time-Category Relationship

There is no statistically significant relationship between the hour_of_day and the categoryName of consumed content.

There is a significant relationship between viewing time and content category (e.g., "Education" is higher in the morning, "Gaming" is higher at night).

2

Popularity Bias Analysis

There is no significant difference in the average viewCount of videos I watch across different categories.

The average viewCount of videos I watch differs significantly between categories (e.g., "Music" is mainstream, "Education" is niche).

3

Time-Popularity Relationship

There is no significant relationship between the hour_of_day and the viewCount of the content I consume.

There is a relationship between viewing time and content popularity (e.g., I watch low-view-count "niche" videos at specific times).

Expected Findings

A clearly identifiable pattern in the EDA heatmap, showing that my viewing habits are not random (e.g., high activity on weeknight evenings).

Rejection of H₀ for Hypothesis 1: A significant Chi-square result showing that I reliably watch certain categories (like "Education" or "News") at specific times of day.

Rejection of H₀ for Hypothesis 2: A significant ANOVA result showing that my consumption of categories like "Gaming" or "Entertainment" involves much more popular (higher view-count) videos than "Education" or "How-to" categories.

A Decision Tree model that can predict the content category with reasonable accuracy, based only on time-based features.

Tools & Environment

Language: Python 3.x

Libraries:

pandas, numpy (For data manipulation)

matplotlib, seaborn (For visualization)

requests, google-api-python-client (For API interaction)

json, BeautifulSoup (For parsing Takeout data)

scipy, statsmodels (For statistical tests)

scikit-learn (For Machine Learning models)

Development Environment: Jupyter Notebook / VS Code

Version Control: Git and GitHub

Ethical & AI Statement

All data sources are clearly cited. The primary dataset is my own personal data, obtained consentfully from Google Takeout, and will remain private. The enrichment data is from a public, documented API.

No private, sensitive, or personally identifiable information (PII) about other individuals will be used or shared.

AI tools (like LLMs) may be used for documentation clarity, code debugging, and syntax suggestions, but not for generating the core analysis, statistical interpretation, or final conclusions of the project. All analytical work and model building will be done independently by me.

Future Work

Extend the analysis to a time-series model to see if my interests (categoryName popularity) have changed over the years.

Incorporate NLP (Natural Language Processing) on the video_title to create sub-categories (e.g., "Python Tutorial" vs. "History Lecture" within the "Education" category).

Analyze likeCount vs. viewCount ratios as a proxy for "video quality" and see if it correlates with my viewing habits.
