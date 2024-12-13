# Table of Contents
- [Table of Contents](#table-of-contents)
- [Dashboard | Overview](#dashboard--overview)
- [Dashboard | Details](#dashboard--details)
- [Introducation](#introducation)
  - [Tools Used](#tools-used)
- [Steps to Build Dashboards](#steps-to-build-dashboards)
  - [:one: Define User Requirements](#one-define-user-requirements)
  - [:two: Build Data Source (ETL)](#two-build-data-source-etl)
  - [:three: Build Charts](#three-build-charts)
  - [:four: Dashboard Build](#four-dashboard-build)
- [Conclusion](#conclusion)
# Dashboard | Overview
# Dashboard | Details
# Introducation
📣 In this project, I used dataset from my [Python Spotify Analysis Project](https://github.com/mchenliu/Capstone_Project_Spotify_Data_Analysis) to create a set of dynamic dashboard to uncover insights into my listening habits.  

:mag: Check out my Spotify Streaming dashboard on [Tableau Public](/https://public.tableau.com/app/profile/mei.liu4813/viz/SpotifyDashboard_17338950683000/SpotifyOverview). 

## Tools Used
**:bar_chart: Excel:** Used Power Query to clean data before importing to Tableau.  
**:art: Tableau:** A powerful tool for creating data visualizations and business intelligence dashboards, enabling insightful analysis and reporting.  
**:pencil2: draw.io:** Used to sketch the dashboard design and container structures.  
**:computer: Visual Studio Code:** A lightweight, versatile code editor. I utilized Visual Studio Code to edit project scripts and manage images, ensuring seamless integration and synchronization with GitHub for version control and collaboration.  
**:octopus: Git & Github:** My go-to for version control and tracking my project progress.  
# Steps to Build Dashboards
## :one: Define [User Requirements](/UserStory.md)
**🧑‍💼 Identify Target Audience:** The dashboard is designed for myself to address two primary needs:
  1. Overivew: Provides high-level insights into key streaming metrics of music tracks and podcast episodes.
  2. Streaming Details View: Enables detailed exploration of individual streaming data.

**🌐 Overview:** Divided into three sections to provide comprehensive metrics:
  1. Overivew: Key streaming stats:  
    - Total hours played  
    - Average hours played per day  
    - Number of music tracks and podcast episodes played  
    - Location distribution of podcasts and music played  
  2. Genre Analysis:  
    - Genre composition by time of day  
    - Correlation between genre and total skips
  3. Artist Preference:  
    - Total playtime by home vs. away  
    - Top 10 artists/ shows by playtime  
    - Relationship between skip rate and total playtime for top 20 artists/ shows.

💡 Streaming Details View:
  1. Detailed list of streaming history (show name, artist name & genre, episode name, track name, date played).
  2. Fully filterable by any column.


## :two: Build Data Source (ETL)
- **Extract:** Connected the dataset to Tableau and conducted an initial inspection to verify data quality and ensure accurate data type mapping.
- **Transform:**
  - *Music_Streaming_History* and *Podcast_Streaming_History*: Standardized column structures and unioned the files in Tableau for seamless integration.
  - *Cleaned_Artist_Genre*:
- **Load:**
  - Loaded the cleaned dataset into Tableau.
  - Built a data model by unioning *Music_Streaming_History* and *Podcast_Streaming_History*, renaming it as *All Streaming History*. Established a relationship between *All Streaming History* and *Cleaned_Artist_Genre* by mapping the `artist name` column in both tables.
  - Explored the data using Tableau worksheets to understand relationships and potential insights.

## :three: Build Charts  
**:white_check_mark: Chart Selection:** After assessing the user requirements,I analyzed user requirements to select the most effective chart types for presenting data and sketached a blueprint for dashboard design.

*Overview Dashbboard Design*
![overview dashboard](/Images/Overview%20Dashboard%20Design.png)  

*Details Dashboard Design*  
![details dashboard](/Images/Details%20Dashboard%20Design.png)  
**:triangular_ruler: Template Design:** Created a reusable template defining the following:  
  - Colors: `#418dcc`, `#de075a`, `#787878` and `#e3e3e3`
  - Font: Trebuchet MS
  - Background: Dark theme  

**:1234: Calculated fields** developed to enhance chart functionality:  
**:abacus: Charts Used**  
Each chart type was selected for its ability to effectively communicate specific insights:
## :four: Dashboard Build  
**Overview Dashboard**  

**:bricks: Structure:**  
**:paintbrush: Design and Build:**  


**Details Dashboard**  
**:bricks: Structure:**  
**:paintbrush: Design and Build:**
# Conclusion  
:mag: Explore the full dashboards on [Spotify Dashboard](/https://public.tableau.com/app/profile/mei.liu4813/viz/SpotifyDashboard_17338950683000/SpotifyOverview).
