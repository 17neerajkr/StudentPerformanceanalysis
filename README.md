📊 Student Performance Factor Analysis
----------- basic -----------

A data analysis project to find which factors affect student academic results the most.



🛠️ Tools Used


Python | Pandas | NumPy | Matplotlib | Seaborn



📁 What I Did


Day 1 — Data Cleaning


Loaded dataset of 6,378 students
Removed missing values using df.dropna()
Removed duplicates using df.drop_duplicates()
Converted Yes/No columns to 1/0
Removed outliers using IQR method


Day 2 — Data Analysis


Correlation analysis using df.corr()
Groupby analysis by gender, attendance, hours studied
Used np.where(), np.median(), np.percentile() for stats


Day 3 — Data Visualization


Bar chart, Line chart, Histogram, Pie chart, Scatter plot using Matplotlib
Barplot, Boxplot, Heatmap, Pairplot using Seaborn



📈 Key Findings




Factor
Correlation
Strength




Attendance
0.68
Strong ✅


Hours Studied
0.50
Medium ✅


Previous Scores
0.20
Weak


Internet Access
0.01
No Effect


Gender
0.02
No Effect





✅ Conclusion


Attendance and study hours are the two most important factors for student performance. Gender and internet access had almost no effect on scores.




Key Recommendation — Regular attendance + daily study habits = better results.





🚀 How to Run


# install libraries
pip install pandas numpy matplotlib seaborn

# run the notebook
jupyter notebook student_analysis.ipynb

