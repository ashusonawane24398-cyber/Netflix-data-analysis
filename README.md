# Netflix Content Analysis — Exploratory Data Analysis (EDA)

# Business Problem

> **How can Netflix decide what type of content to produce — and where to grow next?**

Netflix has a massive content library across 100+ countries. This project analyzes 8,807 titles to uncover patterns in content type, genre, ratings, and geography — and translates them into actionable business recommendations.

---

## Dataset

| Property | Detail |
|---|---|
| Source | [Kaggle — Netflix Movies and TV Shows](https://www.kaggle.com/datasets/shivamb/netflix-shows) |
| Rows | 8,807 titles |
| Columns | 12 attributes |
| Period | 1925 – 2021 |

**Columns:** `show_id`, `type`, `title`, `director`, `cast`, `country`, `date_added`, `release_year`, `rating`, `duration`, `listed_in`, `description`

---

## Project Structure

```
netflix-eda/
│
├── netflix_eda.ipynb        # Main analysis notebook
├── netflix.csv              # Dataset
└── README.md
```

---

## Methodology

### 1. Data Cleaning
- Converted `date_added` to datetime and extracted year, month, day
- Fixed **data quality bug**: duration values (e.g. "66 min") had leaked into the `rating` column — identified via boxplot, removed using `isin()` filter
- Handled missing values: `director` (30% missing), `cast` and `country` (~9%) filled with `'Unknown'`
- Converted `type` and `rating` to categorical dtype for efficiency

### 2. Data Transformation
- Columns like `country`, `cast`, and `listed_in` contained comma-separated multiple values
- Applied `str.split()` → `explode()` → `str.strip()` to unnest them into individual rows
- **Note:** After exploding, row counts are higher than 8,807 — each row represents one country/genre/cast appearance, not one unique title

### 3. Analysis
- **Univariate:** Histograms, KDE plots, countplots for release year, duration, ratings
- **Bivariate:** Boxplots of rating vs release year, duration by content type

---

## Key Findings

| # | Finding |
|---|---|
| 1 | Movies dominate Netflix (70%) vs TV Shows (30%) |
| 2 | Most content was added between 2018–2020; slight decline after 2020 |
| 3 | United States is the top content-producing country; India is #2 and growing |
| 4 | TV-MA and TV-14 are the most common ratings — Netflix targets mature audiences |
| 5 | Most movies run 80–120 minutes; most TV shows have only 1–2 seasons |
| 6 | Drama and International Movies are the dominant genres globally |
| 7 | July and December see the highest volume of content additions |

---

## Business Recommendations

1. **Invest in TV Shows** — TV Shows drive longer viewer engagement (multiple episodes/seasons). Post-2016 growth trend supports continued investment.
2. **Expand Indian regional content** — India is the #2 content country. Investing in Tamil, Telugu, and Marathi originals could unlock a massive underserved audience.
3. **Double down on Drama and Thriller** — Highest genre representation globally; strong cross-country appeal.
4. **Target content releases in July and December** — Peak content addition months align with viewer demand cycles.
5. **Diversify into family-friendly content** — TV-G and TV-Y content is underrepresented relative to audience size.
6. **Mature content is core** — TV-MA dominates; premium adult drama is Netflix's strongest retention category.

---

## Tools & Libraries

`Python` · `Pandas` · `NumPy` · `Matplotlib` · `Seaborn`

---

## About Me

I'm a career transitioner from healthcare data (M.Pharm + 3.4 years at Cognizant & Indegene) into Data Analytics. This is my first solo end-to-end EDA project, built as part of Scaler's Data Science program.

📧 [Your Email] · 💼 [Your LinkedIn] · 🐙 [Your GitHub]
