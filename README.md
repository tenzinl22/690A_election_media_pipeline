# 690A Final: 2024 Post-US Presidential Election News Coverage ETL Pipeline
Tenzin Lhamo

## Overview
This repository contains an automated ETL pipeline to dynamically monitor and analyze news coverage of the 2024 USA presidential election results using the NewsAPI. As of today, December 6th, 2024, the pipeline contains data from November 6th, 2024 (the day after the election) through November 20th, 2024. The pipeline will automatically update every day to include data for the following day, maintaining an ongoing two-week window of election-related news. This is due to the NewsAPI's limitations in data access. The pipeline includes tasks including extracting, loading, and transformation using Python, as well as automation using Prefect. This information can be used to address questions, including 'what are the key themes and topics that the news focuses on?', 'how does the news cover certain topics, candidates, policies, and events?', 'how does news coverage shift in response to public reaction?', 'what are the differences in news coverage of the election outcome between left- and right-winged sources?'  

## Structure
- '2024_election_news_pipeline.ipynb': The Google CoLab notebook where the pipeline setup is performed.
- 'README.md': This file contains a description of the project.
  
## Transformation
After data wrangling, there is a total of 7 columns and 97 entries. The columns of interest are 'source', 'author', 'title', 'description', 'content', 'pubishedAt', and 'url'. The data transformation process starts with checking for the presence of the columns of interest. There will be an error message should there be any missing columns. The dataframe will be copied to ensure no changes are made to the original set. The 'source' column is transformed to only contain the source name and is replaced with 'None' if the source is missing. The 'publishedAt' column is converted to a MySQL-compatible format. Missing values in the 'author' and 'description' columns are replaced with 'Unknown' and 'No Description', respectively. Rows with titles labeled '[Removed]' are removed from the dataset to ensure all articles are useful. Duplicates rows also are removed. Lastly, the articles are sorted by the published date in the 'publishedAt' column to ensure for chronological ordering. 

## Destination
The destination of the data is MySQL database hosted on Heroku via JawsDB.

## Pipeline Automation
Prefect will be utilized to for schedule handling, errors, and notifications. Slack will be used for sending direct status notifications and in the case of an error. 
