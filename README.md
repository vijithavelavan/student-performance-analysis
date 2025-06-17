# student-performance-analysis
#Mini project analyzing student scores using Python, Pandas, and visualization.
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Data
data = {
    'Name': ['Anu', 'Bala', 'Kavi', 'Deepa', 'Ravi', 'Sara', 'Kavi'],
    'Age': [19, 20, 21, 19, 20, None, 21],
    'Department': ['AI', 'CSE', 'IT', 'AI', 'CSE', 'AI', 'IT'],
    'Maths': [85, 90, 78, 95, 88, None, 78],
    'Science': [80, 85, 75, 92, 90, 88, 75]
}

df = pd.DataFrame(data)

# Data cleaning
df = df.fillna(0)
df = df.drop_duplicates()
df = df.rename(columns={'Maths': 'Math_Score'})

# Summary
print(df.describe())
average_marks = df[['Math_Score', 'Science']].mean()
print("Average Marks:\n", average_marks)

# Groupby
average_science_score = df.groupby('Department')['Science'].mean()
print("Avg Science Score by Dept:\n", average_science_score)

# Total score and sorting
df['total'] = df['Math_Score'] + df['Science']
sorted_df = df.sort_values(by='total', ascending=False)

# Visualization 1: Countplot
plt.figure(figsize=(6, 4))
sns.countplot(x='Department', data=df)
plt.title('Number of Students per Department')
plt.show()
