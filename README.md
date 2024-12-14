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
- [Challenges Faced](#challenges-faced)
- [Conclusion](#conclusion)
# Dashboard | Overview
![Overview_dashboard_gif](/Images/OverviewDashboard.gif)  

# Dashboard | Details  
![Details_dashboard_gif](/Images/DetailsDashboard.gif)  

# Introducation
📣 In this project, I used dataset from my [Python Spotify Analysis Project](https://github.com/mchenliu/Capstone_Project_Spotify_Data_Analysis) to create a set of dynamic dashboard to uncover insights into my listening habits.  

:mag: Check out my Spotify Streaming dashboard on [Tableau Public](https://public.tableau.com/app/profile/mei.liu4813/viz/SpotifyDashboard_17338950683000/SpotifyOverview). 

## Tools Used
**:bar_chart: Excel:** Used Power Query to clean data before importing to Tableau.  
**🤖 ChatGPT:** Used to genrate logos and serves as assistance for the project.  
**:art: Tableau:** A powerful tool for creating data visualizations and business intelligence dashboards, enabling insightful analysis and reporting.  
**:pencil2: draw.io:** Used to sketch the dashboard design and container structures.  
**:computer: Visual Studio Code:** A lightweight, versatile code editor. I utilized Visual Studio Code to edit project scripts and manage images, ensuring seamless integration and synchronization with GitHub for version control and collaboration.  
**:octocat: Git & Github:** My go-to for version control and tracking my project progress.  
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
    - Top 5 artists/ shows by playtime  
    - Relationship between skip rate and total playtime for top 20 artists/shows.

💡 Streaming Details View:
  1. Detailed list of streaming history (date played, location, tracks played/skipped, episodes played/skipped and hours played).
  2. Fully filterable by any column.


## :two: Build Data Source (ETL)
- **Extract:** Connected the dataset to Tableau and conducted an initial inspection to verify data quality and ensure accurate data type mapping.
- **Transform:**
  - *Music_Streaming_History* and *Podcast_Streaming_History*: Standardized column structures and unioned the files in Tableau for seamless integration.
  - *Cleaned_Artist_Genre*: Cleaned the columns to ensure each row represents a single genre and added missing genre data for artists. Faced some challenges during data collection; see [Challenges Faced](/Challenges_Faced.md) for details..
- **Load:**
  - Loaded the cleaned dataset into Tableau.
  - Built a data model by unioning *Music_Streaming_History* and *Podcast_Streaming_History*, renaming it as *All Streaming History*. Established a relationship between *All Streaming History* and *Cleaned_Artist_Genre* by mapping the `artist name` column in both tables.
  - Explored the data using Tableau worksheets to understand relationships and potential insights.

## :three: Build Charts  
**:white_check_mark: Chart Selection:** After assessing the user requirements,I analyzed user requirements to select the most effective chart types for presenting data and sketached a blueprint for dashboard design.

*Overview Dashbboard Design*
![overview dashboard](/Images/Overview_Dashboard_Design.png)  

*Details Dashboard Design*  
![details dashboard](/Images/Details_Dashboard_Design.png)  
**:triangular_ruler: Template Design:** Created a reusable template defining the following:  
  - Colors: `#418dcc`, `#de075a`, `#787878` and `#e3e3e3`
  - Font: Trebuchet MS
  - Background: Dark theme  

**:1234: Calculated fields** developed to enhance chart functionality:  
| Field Name | Formula |  
|------------|---------|
| Total Days | DATEDIFF ('day', MIN ([Date Time]), MAX ([Date Time])) |
| Music Group | IF [Type] ='Music Track' <br> THEN 'Music Tracks' <br> END |
| Time Slot | IF DATEPART('hour' ,[Date Time]) > 6 AND DATEPART('hour',[Date Time]) < 12 THEN 'Morning' <br> ELSEIF  DATEPART('hour' ,[Date Time]) >=12 AND  DATEPART ('hour',[Date Time]) < 18 THEN 'Afternoon' <br> ELSEIF DATEPART ('hour', [Date Time]) >= 18 AND  DATEPART('hour', [Date Time]) < 24 THEN 'Night' <br> ELSE 'Over Night' <br> END |
| Music Hours Played | IF [Type] = 'Music Track' <br> THEN [Ms Played]/1000/60/60 <br> ELSE 0 <br> END |
| Music Skip Count | SUM(IF [Type] = 'Music Track' AND [Skipped] = True <br> THEN 1 <br> ELSE 0 <br> END) | 
| No. of Tracks | COUNT(If [Track Name] <> 'No Track Name'<br> THEN [Track Name] <br> END) |  
____  

**:abacus: Charts Used**  
Each chart type was selected for its ability to effectively communicate specific insights:  

- 📈 BAN (Big Ass Numbers) + Line Chart: Ideal for presenting KPIs at a glance. I combined BANs with line charts to show KPIs and trends for tracks vs. episodes over time.  
![BAN](/Images/Charts/BAN%20&%20Line.PNG)  

- 📊 Bar Chart: Effective for visualizing distributions. I used bar chart to highlight top 5 genres.
![Bar](/Images/Charts/Bar.PNG)  

- 🗺️ Map: Used to illustrate location.  
![Map](/Images/Charts/Map.PNG)  

- 🍕 Pie Chart: Represented location distribution alongside music tracks vs. podcast episode ratios.
![Pie](/Images/Charts/Pie.PNG)  

- 🔥 Heat Map: Highlighted relationships and distributions between dimensions. The highest percentages and counts were visually emphasized. Two heat maps were created to analyze relationships between:  
  - Genre vs. Time Slot
  - Genre vs. Skipped (True/False)  


![Heat_map](/Images/Charts/Heatmap1.PNG)  

![Heat_map](/Images/Charts/Heatmap2.PNG)  

- 🔴➖⚪ Barbell Chart: Revealed the location playtime gap across top five artists/ podcast shows, providing a clear view of disparities.  

![Barbell1](/Images/Charts/Barbell1.PNG)  



![Barbell2](/Images/Charts/Barbell2.PNG)

- 🌌 Scatter Plot: Demonstrated the relationship between hours played and skip rate for music tracks and podcast shows, uncovering potential trends and correlations.  

![Scatter1](/Images/Charts/Scatter1.PNG)  

![Scatter2](/Images/Charts/Scatter2.PNG)  

## :four: Dashboard Build  
**Overview Dashboard**  
**:bricks: Structure:**  
- Navigation Bar: Included logo and navigation icons.  
- Header: Contained a dashboard title and filters.
- Charts:  
  - Overview: Displayed .
  - Genre Analysis: 
  - Artist and Show Preference: Discovered correlation between artist/ podcast playtime, hours played and location group.  

🖌️ Design and Build:  
- Planned and sketched the layout in draw.io, defining container structures for clarity.
- Integrated charts into the Overview Dashboard.
- Refined the dashboard's design, including colors, text styles, and inner/outer spacing for a polished look.
- Added filters, dynamic tooltips, and performed thorough testing.
- Enhanced charts with hierarchies, enabling drill-down functionality and incorporating them into tooltips.
- Added logos and icons to the navigation bar for a cohesive and branded design.

*Overview dashboard containers design*  
![Dashboard_design](/Images/Overivew_Dashboard_Containers_Design.png)  


**Details Dashboard**  
**:bricks: Structure:**  
- Navigation bar: Same as Overview Dashboard. 
- Header: Simplified without filters.  
- Filters: Added interactive filters above the streaming history details list.
- Detail Section: Listed streaming history information with drill-down capabilities.


**:paintbrush: Design and Build:**
- Created a sketch in draw.io for layout consistency.  
- Integrated filters to enhanced interactivity.
- Added navigation buttons to facilitate seamless switching between the two dashboards.

*Details dashboard containers design*  
![Dashboard_design](/Images/Details_Dashboard_Containers_Design.png)  

*Filter containers design*  
![Filter_design](/Images/Filter_Design.png)  

# Challenges Faced
See challenges faced :point_right: [here](/Challenges_Faced.md).

# Conclusion  
:mag: Explore the full dashboards on [Spotify Dashboard](https://public.tableau.com/app/profile/mei.liu4813/viz/SpotifyDashboard_17338950683000/SpotifyOverview).
