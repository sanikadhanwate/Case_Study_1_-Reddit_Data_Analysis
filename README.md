# 📌 Case Study 1: Data Gathering from Reddit using PRAW

## 🔍 Problem Statement

As a beginner in data science, I wanted to understand what real data scientists and aspiring professionals are concerned about.
Since Reddit allows anonymous discussions, I chose the **r/datascience** subreddit as a reliable source of honest opinions. As it provides more candid and unfiltered insights compared to platforms like X (Twitter).

### **The goal of this case study was to:**

- Collect the **top 100 meaningful posts** from the `r/datascience` subreddit
- Restrict posts to the **year 2025**
- Ensure posts have **high engagement and relevance**
- Collect the **top 3 comments** for each post
- Store the final cleaned data in a structured format for future analysis
- **while applying strict quality filters**

This case study intentionally focuses **only on data collection and cleaning**, not modeling or visualization.

---

## 🧠 Why This Problem Matters

In real-world data projects:
- Data is messy
- APIs don’t return exactly what you expect
- Meeting constraints (like “exactly 100 records”) often requires debugging and iteration

This case study focuses only on data gathering and cleaning, which is a critical first step in any data science pipeline.

## ⚙️ Tools & Technologies
- Python
- PRAW (Python Reddit API Wrapper)
- Pandas
- Jupyter Notebook
- Reddit API

---

## 🧪 Step-by-Step Approach

### Step 1: Reddit API Setup and Data Access
- Created a Reddit developer account and configured API credentials
- Used the PRAW library to authenticate and connect to Reddit
- Successfully retrieved posts from the `r/datascience` subreddit
- Verified API access by printing post titles

```
reddit = praw.Reddit(client_id="7BD_UFkt0T4S6YyUmejREw",
                     client_secret="mz8ascyf3MBG5JmpTHxTK77TYSYrqg",
                     username="Avocado_2468",
                     password="New_avocado",
                     user_agent="case_study"
)
subreddit=reddit.subreddit("datascience")
hot_python=subreddit.hot(limit=5)
for submission in hot_python:
    print(submission.title)
``` 

**This step ensured that data retrieval was functional before applying filters.**

---

## Step 2: Data Collection Logic (Core of the Case Study)

To ensure quality and relevance, I applied the following filters:

| Condition                     | Reason                       |
| ----------------------------- | ---------------------------- |
| Posts from **year 2025 only** | Match project requirement    |
| Post score **> 50**           | Avoid low-impact posts       |
| Title length **> 5 words**    | Remove memes/jokes           |
| Converted timestamps          | Improve readability          |
| Top **3 comments per post**   | Capture community discussion |


## 🚨 Key Challenge: Why I Initially Got Only ~70 Posts

At first, my script returned only ~70 posts, **even though the goal was 100 posts.**

### Why this happened:
- Many posts failed at least one filter
     - Wrong year
     - Score ≤ 50
     - Short titles
- Reddit’s API does not guarantee enough qualifying posts in smaller query windows
- Using small limits (hot or low limit) caused early exhaustion of valid posts

This is a real-world API limitation, not a coding mistake.

---

## 🔧 How I Fixed it: (Critical Improvement)
I changed the strategy to:
```posts = subreddit.new(limit=200000)```

To reliably collect **at least 100 valid posts**, the data retrieval strategy was adjusted:

### Why this works:
- Fetches a large pool of posts
- Filters are applied after retrieval
- Loop continues until exactly 100 valid posts are collected
- Stops automatically once the requirement is satisfied
```
if len(posts_dict["Title"]) >= 100:
    break
```
## ✅ Result I got: 
- Successfully collected exactly 100 high-quality posts
- All grading constraints satisfied
- No API errors encountered

  **This demonstrates:**
✔️ Debugging
✔️ API understanding
✔️ Data filtering under constraints

## 📊 Final Dataset (csv file saved )
- Rows: 100 posts (+ header) and Columns: 7

  | Column           | Description           |
| ---------------- | --------------------- |
| Date             | YYYY-MM-DD            |
| Post score       | Reddit score          |
| Post title       | Title text            |
| Body of the post | Post content          |
| Top comment 1    | Most relevant comment |
| Top comment 2    | Second comment        |
| Top comment 3    | Third comment         |
