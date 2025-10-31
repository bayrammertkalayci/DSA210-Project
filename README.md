# DSA210-Project

1. Project Proposal & Motivation

This project will perform a comprehensive analysis of my personal YouTube watching habits. The primary goal is to move beyond simple "what I watched" metrics and explore the statistical relationship between my viewing patterns (e.g., when I watch) and the objective, public attributes of the content I consume (e.g., what I watch).

My core motivation is to apply the full data science pipeline (collection, cleaning, enrichment, analysis, and modeling) to a dataset that is both unique and personal. I will investigate whether my viewing behavior is predictable and if external factors, such as a video's public popularity or its content category, correlate with my personal consumption schedule.

This project will seek to answer questions such as:

Is there a statistically significant relationship between the time of day (or day of the week) and the category of content I consume (e.g., "Education" vs. "Gaming")?

Do I tend to watch more "niche" (low-view-count) or "mainstream" (high-view-count) videos?

Can a machine learning model be trained to predict the category of a video based solely on the time I watched it?

2. Data Sources and Collection Plan

This project will follow the "enrichment" model outlined in the course guidelines. It will combine a private, personal dataset (my watch history) with a public, external dataset (YouTube's video metadata).

2.1. Primary Data Source: Personal Google Takeout Archive

This is the core dataset of my personal viewing behavior.

Data to be Used: My personal YouTube and YouTube Music watch history.

Collection Plan:

I will use the Google Takeout service to request my "YouTube and YouTube Music" data archive.

This archive will contain a watch-history.json (or .html) file.

I will write a Python script to parse this file, extracting the following key fields for every video I have watched:

watch_timestamp: The exact date and time I watched the video.

video_title: The title of the video.

video_ID: The unique 11-character identifier for the video (e.g., dQw4w9WgXcQ), which will be extracted from the video URL.

2.2. Enrichment Data Source: YouTube Data API v3 (Public)

This public API will be used to "enrich" the "blind" video_ID data collected from my personal archive.

Data to be Used: Publicly available metadata for every unique video ID from my watch history.

Collection Plan:

I will obtain a free API key from the Google Cloud Console for the "YouTube Data API v3".

I will write a second Python script that takes the unique list of video_IDs from my Takeout data.

This script will loop through the list and send an automated query (API call) for each video_ID.

For each video, the API will return a JSON object, from which I will extract the following public data points:

categoryName (e.g., "Education", "Gaming", "Music", "Entertainment")

viewCount

likeCount

duration (e.g., PT10M5S for 10 minutes 5 seconds)

3. High-Level Analysis Plan (Outline)

Data Processing & Merging:

Clean the parsed Takeout data.

Clean the collected API data.

Merge the two tables on the video_ID key to create a single, unified dataset.

Feature Engineering:

Convert the raw watch_timestamp into new features like hour_of_day, day_of_week, and is_weekend.

Convert the duration string (e.g., "PT10M5S") into total seconds or minutes.

Exploratory Data Analysis (EDA) & Hypothesis Testing (for Nov 28):

Analyze viewing habits over time (e.g., heatmap of day vs. hour).

Perform T-tests or ANOVA to compare metrics (like viewCount) across different categories.

Perform Chi-square tests to check for independence between time (day_of_week) and content (categoryName).

Machine Learning (for Jan 2):

Train a classification model (e.g., Decision Tree) to predict the categoryName of a video using only my personal viewing patterns (like hour_of_day, day_of_week) as features.

4. Initial Tools & Technologies

Python 3.x

Pandas & NumPy: For data cleaning, merging, and manipulation.

json and/or BeautifulSoup: To parse the initial Google Takeout file.

google-api-python-client (or requests): To interact with the YouTube Data API.

Scikit-learn: For machine learning and statistical tests.

Matplotlib & Seaborn: For data visualization.
