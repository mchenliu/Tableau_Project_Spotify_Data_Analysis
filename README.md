# Table of Contents
- [Table of Contents](#table-of-contents)
- [Dashboard | Overview](#dashboard--overview)
- [Dashboard | Details](#dashboard--details)
- [Introduction](#introduction)
  - [Tools Used](#tools-used)
- [Steps to Build Dashboards](#steps-to-build-dashboards)
  - [:one: Define User Requirements](#one-define-user-requirements)
  - [:two: Build Data Source (ETL)](#two-build-data-source-etl)
  - [:three: Build Charts](#three-build-charts)
  - [:four: Dashboard Build](#four-dashboard-build)
- [Challenges Faced](#challenges-faced)
- [Conclusion](#conclusion)
  - [Key Insights](#key-insights)
  - [Limitations](#limitations)
  - [Final Thoughts](#final-thoughts)
# Dashboard | Overview
![Overview_dashboard_gif](/Images/OverviewDashboard.gif)  

# Dashboard | Details  
![Details_dashboard_gif](/Images/DetailsDashboard.gif)  

# Introduction
📣 In this project, I utilized a dataset from my [Python Spotify Analysis Project](https://github.com/mchenliu/Capstone_Project_Spotify_Data_Analysis) to create dynamic dashboards analyzing my listening habits from 2018 to 2024. The goal was to uncover trends in my streaming history while enhancing my data visualization skills using Tableau.

This project involved:

**Data Enrichment:** Using ChatGPT to fill in missing data from the original dataset.  
**ETL Process:** Employing Excel Power Query for data cleaning and transformation before importing it into Tableau.
Key insights revealed:

My favorite genre is **Mandarin Pop**, and my top artist is **Hebe Tien**, whose tracks I prefer to play at home in New Zealand compared to while traveling.
My second favorite artist is **JJ Lin**, with a skip rate only half that of Hebe Tien.
My most-played podcast is **童話裡都是騙人的**, although I skipped this show **50%** of the time.
This project also uncovered challenges in data collection and handling, offering valuable lessons for future analytics endeavors.

:mag: Check out my Spotify Streaming dashboard on [Tableau Public](https://public.tableau.com/app/profile/mei.liu4813/viz/SpotifyDashboard_17338950683000/SpotifyOverview). 

## Tools Used
**:bar_chart: Excel:** Used Power Query to clean data before importing to Tableau.  
**🤖 ChatGPT:** Used to generate logos and serves as assistance for the project.  
**:art: Tableau:** A powerful tool for creating data visualizations and business intelligence dashboards, enabling insightful analysis and reporting.  
**:pencil2: draw.io:** Used to sketch the dashboard design and container structures.  
**:computer: Visual Studio Code:** A lightweight, versatile code editor. I utilized Visual Studio Code to edit project scripts and manage images, ensuring seamless integration and synchronization with GitHub for version control and collaboration.  
**:octocat: Git & Github:** My go-to for version control and tracking my project progress.  
# Steps to Build Dashboards
## :one: Define [User Requirements](/UserStory.md)
**🧑‍💼 Identify Target Audience:** The dashboard is designed for myself to address two primary needs:
  1. Overview: Provides high-level insights into key streaming metrics of music tracks and podcast episodes.
  2. Streaming Details View: Enables detailed exploration of individual streaming data.

**🌐 Overview:** Divided into three sections to provide comprehensive metrics:
  1. Overview: Key streaming stats:  
    - Total hours played  
    - Average hours played per day  
    - Number of music tracks and podcast episodes played  
    - Location distribution of podcasts and music played  
  2. Genre Analysis:  
    - Genre composition by time of day  
    - Correlation between genre and skip rate by time of day
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
**:white_check_mark: Chart Selection:** After assessing the user requirements,I analyzed user requirements to select the most effective chart types for presenting data and sketched a blueprint for dashboard design.

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
| Time Slot | IF DATEPART('hour', [Date Time]) > 6 AND DATEPART('hour',[Date Time]) < 12 <br> THEN 'Morning' <br> ELSEIF <br> DATEPART('hour', [Date Time]) >= 12 AND  DATEPART ('hour',[Date Time]) < 18 <br> THEN 'Afternoon' <br> ELSEIF <br> DATEPART ('hour', [Date Time]) >= 18 AND  DATEPART('hour', [Date Time]) < 24 <br> THEN 'Night' <br> ELSE 'Over Night' <br> END |
| Music Hours Played | IF [Type] = 'Music Track' <br> THEN [Ms Played]/1000/60/60 <br> ELSE 0 <br> END |
| Music Skip Count | SUM (IF [Type] = 'Music Track' AND [Skipped] = True <br> THEN 1 <br> ELSE 0 <br> END) | 
| No. of Tracks | COUNT (If [Track Name] <> 'No Track Name'<br> THEN [Track Name] <br> END) |  
| % Genre | { FIXED [Genre] : <br> SUM( [Total Hours Played] ) } / { FIXED : SUM( [Total Hours Played] ) } |
____  

**:abacus: Charts Used**  
Each chart type was selected for its ability to effectively communicate specific insights:  

- 📈 BAN (Big Ass Numbers) + Line Chart: Ideal for presenting KPIs at a glance. I combined BANs with line charts to show KPIs and trends for tracks vs. episodes over time.  
![BAN](/Images/Charts/BAN%20&%20Line.PNG)  

- 📊 Bar Chart: Effective for visualizing distributions. I used bar chart to highlight top 5 genres.
![Bar](/Images/Charts/Bar.PNG)  

- 🗺️ Map: Used to illustrate location.  
![Map](/Images/Charts/Map.PNG)  

- 🍕 Donut Chart: Represented location distribution alongside music tracks vs. podcast episode ratios.
![Pie](/Images/Charts/Pie.PNG)  

- 🔥 Heat Map: Highlighted relationships and distributions between dimensions. The highest percentages and counts were visually emphasized. Two heat maps were created to analyze relationships between:  
  - Genre vs. Time Slot
  - Genre vs. Skipped  


![Heat_map](/Images/Charts/Heatmap1.PNG)  

![Heat_map](/Images/Charts/Heatmap2.png)  

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
  - Overview:  
    - KPIs of total hours played, number of music tracks/ podcast shows played over time
    - Location stats of percentage of hours played between home (New Zealand) and away (All but New Zealand)
  - Genre Analysis: 
    - Top 5 genres
    - Heatmap to reveal relationship between top 5 genres and time slots over playtime
    - Heatmap to reveal relationship between top 5 genres and time slots over skip rate
  - Artist and Show Preference: Discovered correlation between
    - Artist/ podcast playtime, hours played and location group
    - Artist/ podcast playtime, hours played and skip rate

🖌️ Design and Build:  
- Planned and sketched the layout in draw.io, defining container structures for clarity.
- Integrated charts into the Overview Dashboard.
- Refined the dashboard's design, including colors, text styles, and inner/outer spacing for a polished look.
- Added filters, dynamic tooltips, and performed thorough testing.
- Enhanced charts with hierarchies, enabling drill-down functionality and incorporating them into tooltips.
- Added logos and icons to the navigation bar for a cohesive and branded design.

*Overview dashboard containers design*  
![Dashboard_design](/Images/Overview_Dashboard_Containers_Design.png)  


**Details Dashboard**  
**:bricks: Structure:**  
- Navigation bar: Same as Overview Dashboard. 
- Header: Simplified without filters.  
- Filters: Added interactive filters above the streaming history details list.
- Detail Section: Listed streaming history information with drill-down capabilities.


**:paintbrush: Design and Build:**
- Created a sketch in draw.io for layout consistency.  
- Integrated filters to enhance interactivity.
- Added navigation buttons to facilitate seamless switching between the two dashboards.

*Details dashboard containers design*  
![Dashboard_design](/Images/Details_Dashboard_Containers_Design.png)  

*Filter containers design*  
![Filter_design](/Images/Filter_Design.png)  

# Challenges Faced
The primary challenge in this project was **data collection**. Spotify does not provide genre information for all artists, and the Python Spotipy library used to extract artist genres from Spotify returned incomplete data. Many artists lacked genre information, and none of the podcast shows had genres available.

This lack of data impacted the **integrity and depth** of the analysis. To address this, I used ChatGPT to source missing data for artists and decided to exclude genre analysis for podcast shows entirely.

See more details on challenges faced :point_right: [here](/Challenges_Faced.md).

# Conclusion  

This project successfully created a set of Tableau dashboards that analyze my streaming history from 2018 to 2024, covering both music tracks and podcast episodes. Despite challenges with data collection, the dashboards addressed my primary objective of uncovering trends and preferences in my streaming habits, offering valuable insights.

## Key Insights
**1. Music vs. Podcasts:**    

- Music tracks dominated my streaming activity, especially from 2018 to 2020 when I hadn’t started streaming podcasts.
- Once I began streaming podcasts, their longer playtimes resulted in daily hours catching up with music tracks.
- While traveling, I played more music tracks than podcasts, likely due to the shorter and lighter nature of music tracks, which are better suited for the road.  
  
**2. Genre Analysis:**
- Genre analysis focused solely on music tracks due to limited data for podcasts.
- **Pop** emerged as my favorite genre, accounting for **50% of my streamed tracks**, with **Mandarin pop** contributing over **5,000 hours**. 
- Interestingly, **40% of pop tracks** were played during the overnight period, indicating its role as calming background music for sleeping.  
- Among the top 5 genres, **Hip Hop** had the highest skip rate, particularly in the morning (**37.4%**), reflecting a potential mismatch with my morning mood.  
  
**3. Top Artists and Podcasts:**

- My favorite artists are **Hebe Tien** and **JJ Lin**, with similar hours streamed. However, **JJ Lin**'s skip rate was half that of Hebe Tien, suggesting stronger engagement with his tracks.  
- **One Republic** was an outlier—streamed for an average number of hours but with a high skip rate of **42%**, possibly reflecting my exploratory listening behavior.  
- For podcasts, my top shows were **童話裡都是騙人的** and **時間的女兒: 八卦歷史**.
**童話裡都是騙人的** had significantly longer playtime but a higher skip rate, indicating exploration of its content and style.  
- **時間的女兒: 八卦歷史**, streamed earlier, showed more targeted listening behavior.  
  
**4. Location-Based Preferences:**

- Both **童話裡都是騙人的** and **時間的女兒: 八卦歷史** were predominantly played at home in New Zealand, whereas **善嵐慶女** was played equally at home and while traveling. This may be due to its shorter episodes and lighter content, making it more versatile for different settings.

## Limitations
This project faced challenges due to incomplete data from Spotify, particularly the lack of genre information for podcasts and some artists. To address this, **ChatGPT** was used to fill in missing data, but limitations in sourcing impacted the analysis's depth and precision.

## Final Thoughts
Despite these limitations, the dashboards achieved the project’s objectives by uncovering meaningful insights into my streaming preferences. They not only highlighted trends and behaviors (e.g., genre preferences, location-based listening habits) but also offered actionable takeaways, such as understanding which content resonates most during specific times and settings.

This project underscores the importance of data enrichment and the potential for iterative improvements in future analyses. The process also strengthened my skills in ETL workflows, Tableau dashboarding, and storytelling through data visualization.


 

:mag: Explore the full dashboards on [Spotify Dashboard](https://public.tableau.com/app/profile/mei.liu4813/viz/SpotifyDashboard_17338950683000/SpotifyOverview).
