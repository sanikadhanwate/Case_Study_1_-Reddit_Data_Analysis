# Case Study 1: Collecting High-Quality Reddit Data Using PRAW

## Overview
This case study focuses on the **data gathering and cleaning stage** of a real-world data science project.  
The objective was to collect and curate meaningful discussions from the **r/datascience** subreddit on Reddit to understand common concerns among data science practitioners and aspiring professionals.

Since Reddit allows anonymous participation, it provides more candid and unfiltered insights compared to platforms like X (Twitter).

---

## Problem Statement
The goal of this project was to:

- Collect the **top 100 meaningful posts** from the `r/datascience` subreddit
- Restrict posts to the **year 2025**
- Ensure posts have **high engagement and relevance**
- Collect the **top 3 comments** for each post
- Store the final cleaned data in a structured format for future analysis

This case study intentionally focuses **only on data collection and cleaning**, not modeling or visualization.

---

## Tools & Technologies
- Python
- PRAW (Python Reddit API Wrapper)
- Pandas
- Jupyter Notebook
- Reddit API

---

## Step 1: Reddit API Setup and Data Access
- Created a Reddit developer account and configured API credentials
- Used the PRAW library to authenticate and connect to Reddit
- Successfully retrieved posts from the `r/datascience` subreddit
- Verified API access by printing post titles

This step ensured that data retrieval was functional before applying filters.

---

## Step 2: Data Collection Strategy and Filters
To ensure **data quality and relevance**, the following constraints were applied:

| Filter Applied | Purpose |
|---------------|--------|
| Posts from year **2025 only** | Match project requirement |
| Post score **greater than 50** | Remove low-impact posts |
| Title length **more than 5 words** | Exclude memes and joke posts |
| Converted timestamps | Improve readability |
| Top **3 comments per post** | Capture discussion context |

All filters were applied **after fetching the data** from Reddit.

---

## Key Challenge: Collecting 100 Valid Posts
Initially, the script returned **fewer than 100 posts** (approximately 70).

### Reason:
- Many posts failed one or more filters
- Reddit API does not guarantee enough qualifying posts in small query limits
- High filtering criteria significantly reduced the usable dataset

This reflects a **real-world API and data availability challenge**, not a coding error.

---

## How the Issue Was Fixed (Critical Improvement)
To reliably collect **at least 100 valid posts**, the data retrieval strategy was adjusted:

- Retrieved a **large pool of posts** using:
  ```python
  subreddit.new(limit=200000)

