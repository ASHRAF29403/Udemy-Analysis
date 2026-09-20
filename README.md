<div align="center">

# 📊 Udemy Courses Success Analysis

### Power BI • Power Query • DAX • End-to-End Business Analytics

<p>
  <strong>End-to-End Power BI Project on Udemy Course Performance</strong>
</p>

<p>
  <a href="#-project-overview">Overview</a> •
  <a href="#-dataset-overview">Dataset</a> •
  <a href="#️-data-cleaning--etl">ETL</a> •
  <a href="#-dashboard-pages">Dashboard</a> •
  <a href="#-key-insights--recommendations">Insights</a>
</p>

<br>

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Power Query](https://img.shields.io/badge/Power_Query-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-005B94?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![Data Analysis](https://img.shields.io/badge/Data_Analysis-Project-blue?style=for-the-badge)

<br><br>

<img src="images/dashboard-preview.png" alt="Udemy Courses Dashboard Preview" width="900">

<br>

<em>Udemy Courses Success Analysis — Power BI Interactive Dashboard</em>

</div>

A comprehensive, end-to-end data analysis project on **Udemy** course data using **Power BI**. The project aims to uncover the drivers of course success, identify optimal pricing strategy, and understand subscriber behavior — delivering key recommendations for instructors, training companies, educational platforms, and students.

---

# 📚 Table of Contents

- [📌 Project Overview](#-project-overview)
- [🎯 Target Audience](#-target-audience)
- [📁 Dataset Overview](#-dataset-overview)
- [🛠️ Data Cleaning & ETL](#️-data-cleaning--etl)
- [📐 DAX Measures](#-dax-measures)
- [🖥️ Dashboard Pages](#️-dashboard-pages)
- [💡 Key Insights & Recommendations](#-key-insights--recommendations)
- [👤 Author](#-author)

---

# 📌 Project Overview

This project presents a comprehensive, professional data analysis of course data from the **Udemy** platform using **Power BI**. It aims to uncover the drivers of course success, identify the optimal pricing strategy, and understand subscriber behavior — providing key recommendations for instructors, training companies, educational platforms, and students.

---

# 🎯 Target Audience

- 👨‍🏫 **Instructors**: To identify the most in-demand specializations, how to price courses, and the importance of course duration relative to value.
- 🏢 **Training Companies**: To direct investments toward the most viable and popular subject areas.
- 🎓 **Educational Platforms**: To distribute courses in a balanced way that mirrors market demand.
- 🧑‍🎓 **Students**: To understand the distribution of courses and levels available on the platform.

---

# 📁 Dataset Overview

<div align="center">

| Metric | Value |
|---|---:|
| 📦 Source | **CSV / TSV file of Udemy course data** |
| 📐 Rows | **3,682 courses** |
| 🧮 Columns | **11 columns** |

</div>

### 📋 Data Dictionary

| Column | Data Type | Description |
|---|---|---|
| `course_id` | Integer | Unique course identifier (Primary Key) |
| `course_title` | Text | Course name |
| `is_paid` | Boolean | Course status (`True` = Paid, `False` = Free) |
| `price` | Decimal | Course price in USD |
| `num_subscribers` | Integer | Number of subscribers enrolled in the course |
| `num_reviews` | Integer | Number of ratings and reviews |
| `num_lectures` | Integer | Number of lectures within the course |
| `level` | Text | Target level (Beginner, Intermediate, Expert, All Levels) |
| `content_duration` | Text / Decimal | Course duration in hours/minutes |
| `published_timestamp` | Date/Time | Date and time the course was published on the platform |
| `subject` | Text | Main subject area (Web Development, Business Finance, Graphic Design, Musical Instruments) |

---

# 🛠️ Data Cleaning & ETL

Data processing and transformation were performed using the **Power Query Editor** and **M code**, through the following steps:

## 1️⃣ Deduplication

- Checked `course_id` and found duplicates, which were removed — reducing the row count from **3,682** to **3,676** unique rows.
- Duplicate `course_title` values were kept after verification, since some courses share the same name but differ in level, price, or duration.

## 2️⃣ Text Cleaning

- Applied `Trim` and `Clean` to text columns such as `course_title` and `subject`.
- Used the M function `Text.Remove` to strip special characters from course titles:

```powerquery
Text.Remove([course_title], {"!", "@", "#", "$", "(", ")", "[", "]"})
```

## 3️⃣ Payment Status Transformation

- Added a conditional column `Payment` to convert `is_paid` values (`True`/`False`) into clear labels (`Paid` / `Free`).

## 4️⃣ Price Standardization

- Replaced the word "Free" with `0` in the price column.
- Converted the data type to `Decimal Number` and formatted it as Currency.

## 5️⃣ Content Duration Normalization

- Split the column to separate the number from the unit (Hours / Minutes).
- Added a conditional formula to convert all durations into **minutes** (hours multiplied by 60).

## 6️⃣ Price Categorization

Added a `Price Category` column to segment courses by price:

| Category | Range |
|---|---|
| 🆓 **Free** | $0 |
| 💰 **Cheap** | ≤ $50 |
| 💵 **Average** | $51 – $130 |
| 💎 **Expensive** | > $130 |

---

# 📐 DAX Measures

A dedicated measures folder named `#Measures` was created to organize all calculations.

### Key DAX Formulas Used

```dax
Subscribers = SUM(yudemi[num_subscribers])

Reviews = SUM(yudemi[num_reviews])

Lectures = SUM(yudemi[num_lectures])

Courses = COUNT(yudemi[course_id])

Max Price = MAX(yudemi[price])

Min Price = MIN(yudemi[price])

Average Price = AVERAGE(yudemi[price])
```

---

# 🖥️ Dashboard Pages

The report consists of **4 interactive pages**, designed with a consistent color scheme and direct navigation buttons.

## 1️⃣ Home Page

- Features the platform logo and an engaging design.
- A side **Page Navigator** for moving between report sections.

## 2️⃣ Overview Page

- **KPI Cards**: Total courses, lectures, reviews, and subscribers.
- **Stacked Column Chart**: Number of subscribers by subject (`Subject`).
- **Tree Map**: Distribution of course count by subject and level (`Level`).
- **Line Chart (Time Series)**: Tracks course publishing growth year over year (2011–2017).
- **Bar Chart (Top 10 Courses)**: Displays the 10 most popular and most-subscribed courses.

## 3️⃣ Price Analysis Page

- **Bar Chart**: Average course price by subject (`Average Price by Subject`).
- **Scatter Plot (Price vs Subscribers)**: Analyzes the relationship between course price and subscriber count.
- **Scatter Plot (Duration vs Price)**: Examines the relationship between course duration (minutes) and average price.
- **Pie / Donut Charts**:
  - Subscriber distribution by price category (Free, Cheap, Average, Expensive).
  - Paid vs. Free course share in terms of subscribers, reviews, and lectures.

## 4️⃣ Course Details Page (Drill-Through)

- A detail page accessible via **Drill-Through** when a user clicks into a specific subject level.
- Displays a detailed table including: course name, subject, level, payment status, price, and number of lectures.

---

# 💡 Key Insights & Recommendations

## 1️⃣ 🌐 Record Demand for Web Development

**Web Development** captured more than **7.9 million subscribers**, far outpacing all other subjects.

> 💡 **Recommendation**: Content creators and platforms should focus heavily on Web Development courses to maximize revenue and capture the largest user segment.

## 2️⃣ 💵 Subscriber Behavior vs. Price

The scatter plot analysis showed **no strong inverse relationship** between higher price and subscriber count. Expensive courses (> $130) account for **28%** of total subscribers — a share very close to that of free courses (**30%**).

> 📌 **Conclusion**: The decision to subscribe is driven by **educational value**, not price alone.

## 3️⃣ ⏱️ The Duration Myth

There is **no direct relationship** between increased course duration and higher price. Some short courses are sold at the highest prices, and vice versa.

> 💡 **Recommendation for Instructors**: There is no need to pad course length unnecessarily — price is determined by content quality and value, not runtime.

## 4️⃣ 📈 Course Publishing Trend Over Time

**2016** marked the peak year for course uploads on the platform, with approximately **1,204 courses**, before dropping to **717 courses** in 2017.

## 5️⃣ 💳 Paid vs. Free Courses

Paid courses clearly outperform free ones in total subscribers, reviews, and number of lectures.

---

# 👤 Author

**Ashraf Nabil Mohamed**
Data Analyst Junior & Machine Learning | Transitioning to Data Engineering

- 🎓 B.Sc. Computer Science (AI & Data Science), Zagazig University
- 💻 GitHub: [github.com/ASHRAF29403](https://github.com/ASHRAF29403)
- 🛠️ **Tools**: Power BI, Power Query (M), DAX

---

<div align="center">
<em>This README was created to serve as a comprehensive documentation reference for this project on GitHub.</em>
</div>
