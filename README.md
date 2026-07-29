## Experiment 1: EDA in IPL Dataset

## Aim:
To perform Exploratory Data Analysis (EDA) on the IPL matches dataset and derive insights about matches per season, winning teams, toss decisions, and top venues.

**Algorithm / Procedure:**

1.Start the program.

2.Import the required Python libraries (pandas, numpy, matplotlib if needed).

3.Load the IPL dataset using pandas.read_csv().

4.Display the first few records of the dataset.

5.Check the dataset information and identify missing values.

6.Remove or fill missing values if necessary.

7.Select the required columns for analysis.

8.Perform basic data analysis (such as total matches, teams, winners, or player statistics).

9.Display the analysis results.

10.Visualize the results using graphs (optional).

## 1.Import Libraries
  Import pandas for data handling.
  Import matplotlib and seaborn for visualization.
## 2.Load Dataset
  Use pd.read_csv() to load the IPL matches dataset.
  Check dataset shape using .shape.
  View first 5 rows using .head().
## 3.Matches per Season (Univariate Analysis)
  Group data by season and count matches.
  Plot a bar chart to visualize growth/decline in matches.
## 4.Top Winning Teams (Univariate Analysis)
  Use value_counts() on the winner column.
  Plot top 5 winning teams in a bar chart.
## 5.Toss Decisions (Univariate Analysis)
  Count toss decision preferences (bat vs field).
  Plot results using a bar chart.
## 6.Top Venues (Univariate Analysis)
  Count matches per venue.
  Display top 5 venues with a horizontal bar chart.
## 7.Draw Insights
  Observe patterns in toss decisions.
  Identify teams with consistent winning trends.
  
  ## Program
  ```
   import pandas as pd
import matplotlib.pyplot as plt

# --------------------------
# Load Dataset
# --------------------------
df = pd.read_csv("C:/Users/acer/Downloads/matches.csv")

# --------------------------
# A. Understanding the Dataset
# --------------------------

print("\nA. UNDERSTANDING THE DATASET")
print("-"*50)

print("Rows and Columns:")
print(df.shape)

print("\nFirst 5 Records:")
print(df.head())

print("\nColumn Names:")
print(df.columns)

print("\nData Types:")
print(df.dtypes)

print("\nPossible Primary Key:")
if "id" in df.columns:
    print("Primary Key:", "id")
elif "match_id" in df.columns:
    print("Primary Key:", "match_id")
else:
    print("Check the unique match identifier column.")

# --------------------------
# B. Data Quality and Cleaning
# --------------------------

print("\nB. DATA QUALITY")
print("-"*50)

print("Missing Values:")
print(df.isnull().sum())

print("\nDuplicate Records:")
print(df.duplicated().sum())

# Remove duplicates
df = df.drop_duplicates()

# Fill missing values
df = df.fillna("Unknown")

print("\nMissing values handled and duplicates removed.")

# --------------------------
# C. Matches Per Season
# --------------------------

print("\nC. MATCHES PER SEASON")
print("-"*50)

season_matches = df.groupby("season").size()

print(season_matches)

print("\nSeason with Highest Matches:")
print(season_matches.idxmax(), "-", season_matches.max())

plt.figure(figsize=(8,5))
season_matches.plot(kind="bar")
plt.title("Matches Played Per Season")
plt.xlabel("Season")
plt.ylabel("Matches")
plt.tight_layout()
plt.show()

# --------------------------
# D. Top Winning Teams
# --------------------------

print("\nD. TOP WINNING TEAMS")
print("-"*50)

team_wins = df["winner"].value_counts()

print(team_wins)

print("\nTop 5 Winning Teams:")
print(team_wins.head())

plt.figure(figsize=(8,5))
team_wins.head().plot(kind="bar", color="orange")
plt.title("Top 5 Winning Teams")
plt.xlabel("Team")
plt.ylabel("Wins")
plt.tight_layout()
plt.show()

# --------------------------
# E. Filtering CSK Wins
# --------------------------

print("\nE. CHENNAI SUPER KINGS")
print("-"*50)

csk = df[df["winner"] == "Chennai Super Kings"]

print(csk)

print("\nTotal Matches Won by CSK:")
print(len(csk))

# --------------------------
# F. Toss Decision Analysis
# --------------------------

print("\nF. TOSS DECISION")
print("-"*50)

toss = df["toss_decision"].value_counts()

print(toss)

plt.figure(figsize=(6,4))
toss.plot(kind="bar", color="green")
plt.title("Toss Decision")
plt.xlabel("Decision")
plt.ylabel("Count")
plt.tight_layout()
plt.show()

# --------------------------
# G. Pivot Table Analysis
# --------------------------

print("\nG. PIVOT TABLE")
print("-"*50)

pivot = pd.crosstab(df["season"], df["toss_decision"])

print(pivot)

# --------------------------
# H. Venue Analysis
# --------------------------

print("\nH. VENUE ANALYSIS")
print("-"*50)

venue = df["venue"].value_counts()

print(venue)

print("\nTop 5 Venues")
print(venue.head())

plt.figure(figsize=(10,5))
venue.head().plot(kind="bar")
plt.title("Top 5 Venues")
plt.xlabel("Venue")
plt.ylabel("Matches")
plt.tight_layout()
plt.show()

# --------------------------
# I. Winning Margin Analysis
# --------------------------

print("\nI. WINNING MARGIN")
print("-"*50)

if "margin" in df.columns:

    print("Largest Winning Margin:")
    print(df["margin"].max())

    print("\nMatch with Largest Winning Margin:")
    print(df[df["margin"] == df["margin"].max()])

    print("\nTop 10 Winning Margins:")
    print(df.sort_values(by="margin", ascending=False).head(10))

# --------------------------
# J. Match Result Analysis
# --------------------------

print("\nJ. MATCH RESULT ANALYSIS")
print("-"*50)

print(df["result"].value_counts())

plt.figure(figsize=(6,4))
df["result"].value_counts().plot(kind="bar", color="purple")
plt.title("Match Result Types")
plt.xlabel("Result")
plt.ylabel("Count")
plt.tight_layout()
plt.show()

# --------------------------
# K. Data Transformation
# --------------------------

print("\nK. DATA TRANSFORMATION")
print("-"*50)

# Convert Date

df["date"] = pd.to_datetime(df["date"])

# Create Year

df["year"] = df["date"].dt.year

# Create Win Type

def win_type(row):

    if row["result"] == "runs":
        return "Won by Runs"

    elif row["result"] == "wickets":
        return "Won by Wickets"

    elif row["result"] == "tie":
        return "Tie"

    else:
        return "No Result"

df["win_type"] = df.apply(win_type, axis=1)

print(df[["date","year","result","win_type"]].head())

print("\nAnalysis Completed Successfully!")
  ```

  ## Output
  <img width="657" height="833" alt="eda 1" src="https://github.com/user-attachments/assets/09542ffe-7e49-4c1d-b3f0-133dd1649442" />
<img width="378" height="307" alt="eda 2" src="https://github.com/user-attachments/assets/62c8db4e-247f-4ce7-a8dc-29f38d38fc34" />
<img width="717" height="602" alt="eda 3" src="https://github.com/user-attachments/assets/9f7856cb-cd12-4bcc-8ab1-702ee60ea2c7" />
<img width="725" height="680" alt="eda 4" src="https://github.com/user-attachments/assets/05734da5-ac2d-4323-8904-62d5866bf475" />
<img width="585" height="885" alt="eda 5" src="https://github.com/user-attachments/assets/1c734bd0-ec95-4d33-9c80-16598087b6b4" />
<img width="848" height="507" alt="eda 6" src="https://github.com/user-attachments/assets/2fc2695d-7e64-497b-b8e3-ed3f9956e13b" />
<img width="605" height="397" alt="eda 7" src="https://github.com/user-attachments/assets/a45c9991-a8c4-4ccd-b4b5-a0c5ae159f91" />
<img width="595" height="877" alt="eda 8" src="https://github.com/user-attachments/assets/5254289e-1fd3-44d2-9505-4ce4fd7d2d98" />
<img width="757" height="462" alt="eda 9" src="https://github.com/user-attachments/assets/528a3b85-bffe-47d8-b0f2-421a0a63b56b" />
<img width="357" height="122" alt="eda 10" src="https://github.com/user-attachments/assets/f10254db-1aa8-46f6-92a4-82643c24c8a0" />


 ## Result
 
This experiment is executed successfully



Highlight the stadiums hosting maximum matches.
