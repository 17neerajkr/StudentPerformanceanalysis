DAY 1 : UNDERSTOOD THAT DATA SET AND CLEANING THAT DATA BY USING AN PANDAS 


  

    

      
1

      
Load your data
Always the first step

    

    

      

        # import pandas library

        import pandas as pd


        # load your csv file

        df = pd.read_csv("your_file.csv")
      

    

  


  

    

      
2

      
Explore your data
Understand what you have before cleaning

    

    

      

        # see first 5 rows

        df.head()


        # see shape — (rows, columns)

        print(df.shape)


        # see column names and data types

        df.info()


        # see statistics summary

        df.describe()
      

    

  


  

    

      
3

      
Find and fix missing values
Rows with empty/blank cells

    

    

      

        # count missing values per column

        df.isnull().sum()


        # option 1 — remove rows with missing values

        df = df.dropna()


        # option 2 — fill missing with average

        df = df.fillna(df.mean())


        # verify — should show 0

        print(df.isnull().sum().sum())
      

    

  


  

    

      
4

      
Find and fix duplicate rows
Rows that appear more than once

    

    

      

        # count duplicate rows

        print(df.duplicated().sum())


        # remove duplicate rows

        df = df.drop_duplicates()


        # verify — should show 0

        print(df.duplicated().sum())
      

    

  


  

    

      
5

      
Fix column names
Make names clean and consistent

    

    

      

        # make all column names lowercase

        df.columns = df.columns.str.lower()


        # remove spaces from column names

        df.columns = df.columns.str.replace(" ", "_")


        # see all column names

        print(df.columns)
      

    

  


  

    

      
6

      
Fix data types
Make sure numbers are numbers, dates are dates

    

    

      

        # check data types

        df.dtypes


        # convert a column to number

        df["column"] = pd.to_numeric(df["column"])


        # convert a column to date

        df["date"] = pd.to_datetime(df["date"])
      

    

  


  

    

      
7

      
Final check — data is clean!
Verify everything before analysis

    

    

      

        # check shape — rows should be less

        print(df.shape)


        # check no missing values

        print(df.isnull().sum().sum())


        # check no duplicates

        print(df.duplicated().sum())


        # save clean data to new file

        df.to_csv("clean_data.csv", index=False)
      

    # ============================================================
#   COMPLETE MATPLOTLIB AND SEABORN GUIDE
#   Student Performance Factor Dataset
# ============================================================


# ============================================================
# STEP 0 — IMPORTS AND SETUP
# ============================================================

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# load dataset
df = pd.read_csv("your_file.csv")

# clean dataset
df = df.dropna()
df = df.drop_duplicates()

# rename exam_score to report_card
df = df.rename(columns={"exam_score": "report_card"})

# convert Yes/No columns to 1/0
df["internet_access"]             = df["internet_access"].map({"Yes": 1, "No": 0})
df["extracurricular_activities"]  = df["extracurricular_activities"].map({"Yes": 1, "No": 0})
df["learning_disabilities"]       = df["learning_disabilities"].map({"Yes": 1, "No": 0})
df["gender"]                      = df["gender"].map({"Male": 1, "Female": 0})

# take top 10 rows for practice
df_10 = df.head(10)

# seaborn style
sns.set_style("whitegrid")
sns.set_palette("husl")


# ============================================================
# MATPLOTLIB — BEGINNER LEVEL
# ============================================================


# ── 1. LINE CHART ───────────────────────────────────────────
plt.figure(figsize=(10, 6))

data = df.groupby("hours_studied")["report_card"].mean()
x = data.index
y = data.values

plt.plot(x, y, linewidth=2, label="Average Score")

plt.title("Hours Studied vs Report Card")
plt.xlabel("Hours Studied")
plt.ylabel("Average Score")
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()


# ── 2. BAR CHART ────────────────────────────────────────────
plt.figure(figsize=(10, 6))

x = df_10["hours_studied"]
y = df_10["report_card"]

plt.bar(x, y, color="steelblue", edgecolor="black",
        linewidth=2, label="hours_studied")

plt.title("Hours Studied vs Report Card")
plt.xlabel("Hours Studied")
plt.ylabel("Report Card Score")
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()


# ── 3. HISTOGRAM ────────────────────────────────────────────
plt.figure(figsize=(10, 6))

plt.hist(df["report_card"], bins=20, color="steelblue", edgecolor="black")

plt.title("Distribution of Report Card Scores")
plt.xlabel("Score")
plt.ylabel("Number of Students")
plt.grid(True)
plt.tight_layout()
plt.show()


# ── 4. PIE CHART ────────────────────────────────────────────
plt.figure(figsize=(10, 6))

x = df_10["hours_studied"]
y = df_10["report_card"]

plt.pie(y, labels=x, autopct="%1.1f%%")

plt.title("Hours Studied vs Report Card")
plt.legend()
plt.tight_layout()
plt.show()


# ── 5. SCATTER PLOT ─────────────────────────────────────────
plt.figure(figsize=(10, 6))

plt.scatter(df_10["hours_studied"], df_10["report_card"],
            color="steelblue", alpha=0.5, label="Students")

plt.title("Hours Studied vs Report Card")
plt.xlabel("Hours Studied")
plt.ylabel("Report Card Score")
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()


# ============================================================
# MATPLOTLIB — INTERMEDIATE LEVEL
# ============================================================


# ── 6. ADD GRID + STYLE + VALUES ON BAR ─────────────────────
plt.figure(figsize=(10, 6))

data = df.groupby("hours_studied")["report_card"].mean().round(2)
x = data.index
y = data.values

plt.bar(x, y, color="steelblue", edgecolor="black")
plt.grid(axis="y", linestyle="--", alpha=0.7)

# add value on top of each bar
for i, v in enumerate(y):
    plt.text(i, v + 0.2, str(round(v, 1)), ha="center", fontsize=10)

plt.title("Average Score by Hours Studied")
plt.xlabel("Hours Studied")
plt.ylabel("Average Score")
plt.tight_layout()
plt.show()


# ── 7. MULTIPLE CHARTS SIDE BY SIDE ─────────────────────────
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(14, 6))

# first chart — bar
data1 = df.groupby("hours_studied")["report_card"].mean()
ax1.bar(data1.index, data1.values, color="steelblue")
ax1.set_title("Score by Hours Studied")
ax1.set_xlabel("Hours Studied")
ax1.set_ylabel("Average Score")

# second chart — pie
data2 = df_10["report_card"]
labels = df_10["hours_studied"]
ax2.pie(data2, labels=labels, autopct="%1.1f%%")
ax2.set_title("Score Distribution Top 10")

plt.tight_layout()
plt.show()


# ── 8. SAVE CHART AS IMAGE ──────────────────────────────────
plt.figure(figsize=(10, 6))

data = df.groupby("hours_studied")["report_card"].mean()
plt.plot(data.index, data.values, linewidth=2)

plt.title("Hours Studied vs Report Card")
plt.xlabel("Hours Studied")
plt.ylabel("Average Score")
plt.grid(True)
plt.tight_layout()
plt.savefig("student_score_chart.png")   # save before show
plt.show()


# ============================================================
# SEABORN — BEGINNER LEVEL
# ============================================================


# ── 1. BARPLOT ──────────────────────────────────────────────
plt.figure(figsize=(10, 6))

sns.barplot(data=df_10, x="gender", y="report_card")

plt.title("Average Score by Gender")
plt.tight_layout()
plt.show()


# ── 2. HISTPLOT ─────────────────────────────────────────────
plt.figure(figsize=(10, 6))

sns.histplot(data=df_10, x="report_card", bins=10)

plt.title("Distribution of Report Card Scores")
plt.tight_layout()
plt.show()


# ── 3. SCATTERPLOT ──────────────────────────────────────────
plt.figure(figsize=(10, 6))

sns.scatterplot(data=df_10, x="hours_studied", y="report_card")

plt.title("Hours Studied vs Report Card")
plt.tight_layout()
plt.show()


# ── 4. BOXPLOT ──────────────────────────────────────────────
plt.figure(figsize=(10, 6))

sns.boxplot(data=df_10, x="gender", y="report_card")

plt.title("Score Distribution by Gender")
plt.tight_layout()
plt.show()


# ── 5. COUNTPLOT ────────────────────────────────────────────
plt.figure(figsize=(10, 6))

sns.countplot(data=df_10, x="gender")

plt.title("Count of Students by Gender")
plt.tight_layout()
plt.show()


# ============================================================
# SEABORN — INTERMEDIATE LEVEL
# ============================================================


# ── 6. HEATMAP ──────────────────────────────────────────────
plt.figure(figsize=(12, 8))

sns.heatmap(df.corr(numeric_only=True),
            annot=True, fmt=".2f", cmap="coolwarm")

plt.title("Correlation Heatmap")
plt.tight_layout()
plt.show()


# ── 7. HUE — COLOR BY CATEGORY ──────────────────────────────
plt.figure(figsize=(10, 6))

sns.scatterplot(data=df_10, x="hours_studied",
                y="report_card", hue="gender")

plt.title("Hours Studied vs Score by Gender")
plt.tight_layout()
plt.show()


# ── 8. PAIRPLOT ─────────────────────────────────────────────
sns.pairplot(df_10, hue="gender")
plt.show()


# ── 9. LINEPLOT ─────────────────────────────────────────────
plt.figure(figsize=(10, 6))

sns.lineplot(data=df_10, x="hours_studied",
             y="report_card", hue="gender")

plt.title("Score Trend by Hours Studied")
plt.tight_layout()
plt.show()


# ============================================================
# END OF FILE
# ============================================================

  




