# Netflix Content EDA — What should Netflix produce next?

![Python](https://img.shields.io/badge/Python-3.10-blue) ![Pandas](https://img.shields.io/badge/Pandas-EDA-green) ![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

## What this project is about

I took a real Netflix dataset — 8,807 titles across 123 countries — cleaned the mess out of it, fixed a few bugs I stumbled into, and tried to answer one question:

**What type of content should Netflix produce, and where should it grow next?**

This is my first solo data project. I built it entirely in Python after transitioning from 3+ years in healthcare data analytics.

---

## Dataset

| Property | Detail |
|---|---|
| Source | [Kaggle — Netflix Movies and TV Shows](https://www.kaggle.com/datasets/shivamb/netflix-shows) |
| Rows | 8,807 titles |
| Columns | 12 |
| Period covered | 1925 – 2021 |

---

## The part that took the longest — data cleaning

Columns like `country`, `cast`, and `listed_in` stored multiple values in a single cell, comma-separated. For example, one title could show `"India, United States, United Kingdom"` in the country column.

To handle this I used a 3-step process:

```python
# Step 1 — split the string into a list
df['country'] = df['country'].str.split(',')

# Step 2 — explode: each list value becomes its own row
df = df.explode('country')

# Step 3 — clean up extra spaces
df['country'] = df['country'].str.strip()
```

> **Important:** After exploding, the row count goes above 8,807. That's expected — each row now represents one country/genre *appearance*, not one unique title. I kept this in mind when reporting counts.

---

## A bug I found mid-analysis

While plotting a boxplot of Rating vs Release Year, I noticed something weird on the x-axis — values like `"66 min"`, `"74 min"`, `"84 min"` showing up as ratings. Duration values had somehow ended up in the rating column.

I fixed it by filtering to only valid rating categories:

```python
valid_ratings = ['TV-MA','TV-14','R','PG-13','PG','G','TV-Y','TV-Y7','TV-G','NR','NC-17']
df_clean = df[df['rating'].isin(valid_ratings)]
```

Lesson I learned: always visualize before you analyze. Dirty data hides in places you don't expect.

---

## What I found

- Movies make up 70% of Netflix content — TV Shows are only 30%, but they're growing faster post-2016
- Most content on Netflix was added between 2018–2020, with a dip after 2020 (likely COVID impact on production)
- The US is the #1 content-producing country. India is #2 — and the gap is closing
- TV-MA and TV-14 dominate the ratings — Netflix is clearly targeting mature audiences
- Drama and International Movies are the most common genres by far
- July and December see the highest content additions — likely tied to subscriber demand peaks

---

## Business recommendations

1. **Keep investing in TV Shows** — they drive longer watch time and bring viewers back across seasons
2. **India is the biggest growth opportunity** — regional language content (Tamil, Telugu, Marathi) is underserved relative to the audience size
3. **Drama and Thriller are safe bets** — highest engagement genres, consistent across countries
4. **Time new releases for July and December** — that's when content addition peaks, suggesting those months drive results
5. **Mature content is Netflix's core** — TV-MA dominates, doubling down on premium adult drama makes sense

---

## Tools used

`Python` · `Pandas` · `NumPy` · `Matplotlib` · `Seaborn`

---

## About me

I spent 3.4 years working in healthcare data at Cognizant and Indegene. I always worked *with* data — but never truly analyzed it on my own terms. In May 2025 I left my job and joined Scaler's Data Science program full-time. This Netflix project is my first solo end-to-end EDA build.

📧 [Your Email] · 💼 [Your LinkedIn] · 🐙 [Your GitHub]
