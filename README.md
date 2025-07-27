# Google-Playstore-Analysis-using-PowerBI-SQL
Power BI &amp; SQL Project: The goal is to analyze google play store app's dataset to drive insight into the app market. We aim to understand the factors that contribute to apps success, including its user rating, reviews, and category. The ultimate objective is performance and user satisfaction.

## Problem Statement
The goal is to analyse google play store app's dataset to drive insight into the app market. We aim to understand the factors that contribute to apps success, including its user rating, reviews, and category. We want to explore users sentiments towards app by analysing the users review datasets. Additionally, we can see insights into the popularity of app categories based on total number of installs and the sentiment polarity of user reviews. The ultimate objective is performance and user satisfaction.
### Project Steps:
1) Create the problem statement.
2) Overview of the dataset.
3) Data Cleaning.
4) Processing of dataset.
5) Data Visualization.
6) Create a dashboard using Power BI software.
7) Create a report of all findings.
### Overview of Dataset:
Provide the overview of the dataset by how many total unique apps and categories are in the dataset.
- Explore App Categories and Counts: Retrive the unique app categories and count of apps in each category.
- Top-rated free Apps: Identify the top-rated free apps.
- Most Reviewed Apps: Find the apps with the highest number of reviews.
- Average Rating by Categories: Calculate the average rating for each app category.
- Top Categories by Number of Installs: Identify the app categories with the highest total number of installs.
- Average Sentiment Polarity by App Categories: Analyse the average sentiment polarity of user reviews for each app category.
- Sentiment Reviews by App Category: Provide the distribution sentiments across different app categories.
## SQL Analysis
1. Overview of Dataset:

        SELECT 
        COUNT(DISTINCT APP) AS total_apps,
        COUNT(DISTINCT Category) AS total_categories
        FROM googleplaystore
2. Exploring App Categories:

        SELECT TOP 5
        Category,
        COUNT(App) AS Total_app
        FROM googleplaystore
        GROUP BY Category
        ORDER BY Total_app DESC
3. Top Rated Free Apps:

        SELECT TOP 10
        App,
        Category,
        Rating,
        Reviews
        FROM googleplaystore
        WHERE Type = 'Free' AND Rating <> 'NaN'
        ORDER BY Rating DESC
4. Most Reveiwed Apps:

        SELECT TOP 10
        Category,
        App,
        Reveiews
        FROM googleplaystore
        ORDER BY Reviews DESC
5. Average Rating by Category:

        SELECT TOP 5
        Category,
        AVG(TRY CAST(Rating AS FLOAT)) AS avg_rating
        FROM googleplaystore
        GROUP BY Category
        ORDER BY avg_rating DESC
6. Top Categories by Number of Installs:

        SELECT TOP 10
        Category,
        SUM(CAST(REPLACE(SUBSTRING(Installs, 1, PATINDEX('%[^0-9]%', Installs + ' ')- 1),',', ' ') AS INT)) AS total_installs
        FROM googleplaystore
        GROUP BY Category
        ORDER BY total_installs DESC
7. Average Sentiment Polarity by App Category:

        SELECT TOP 10
        Category,
        AVG(TRY CAST(Sentiment_Polarity AS FLOAT)) AS avg_sentiment_polarity
        FROM googlepalystore
        JOIN googleplaystore_user_reviews
        ON googleplaystore.App = googleplaystore_user_revies.App
        GROUP BY Category
        ORDER BY avg_sentiment_polarity DESC
8. Sentiment Reviews by App Category:

        SELECT TOP 10
        Category,
        Sentiment,
        COUNT(*) AS total_sentiment
        FROM googleplaystore
        JOIN gogleplaystore_user_reviews
        ON googleplaystore.APP = googleplaystore_user_reviews.APP
        WHERE Sentiment <> 'nan'
        GROUP BY Category, Sentiment
        ORDER BY total_sentiment DESC
## Data Analysis & Visualization
For analysis of the dataset and visualization we used Power BI software as the clients wanted a dashboard for presentation of the findings.
### Dashboard:
![image](https://github.com/user-attachments/assets/be84b4ba-d180-4db4-b92f-3fa9086bceda)
## Findings & Insights
- The total number of apps are 8K and 33 categories.
- Robolox is the top-rated free app and Nick is the lowest rated app.
- The app with the highest number of reviews is Subway surfer and Candy Crush.
- The average rating for each app category is displayed on the dashboard and the most reviewed category is Personalized category.
- The highest total number of installs in app is games category, and the average sentiment polarity of user reviews for app is 0.28 for personalization category.
- The distribution of sentiments across sentiments across different app categories is 1.22K positive, 1.13K negative, and 1.04K neutral sentiments.

These are all the findings that we have got while analyzing the dayaset provided for the analysis. Hope it will help the client to gain valuable insights on the app and act according to it.

