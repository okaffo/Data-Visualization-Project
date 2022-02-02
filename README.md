# Data-Visualization-Project
Data Visualization Lab
Estimated time needed: 45 to 60 minutes

In this assignment you will be focusing on the visualization of data.

The data set will be presented to you in the form of a RDBMS.

You will have to use SQL queries to extract the data.

Objectives
In this lab you will perform the following:

Visualize the distribution of data.

Visualize the relationship between two features.

Visualize composition of data.

Visualize comparison of data.

Demo: How to work with database
Download database file.

!wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DA0321EN-SkillsNetwork/LargeData/m4_survey_data.sqlite
--2022-02-02 18:40:39--  https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DA0321EN-SkillsNetwork/LargeData/m4_survey_data.sqlite
Resolving cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud (cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud)... 198.23.119.245
Connecting to cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud (cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud)|198.23.119.245|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 36679680 (35M) [application/octet-stream]
Saving to: ‘m4_survey_data.sqlite’

m4_survey_data.sqli 100%[===================>]  34.98M  43.1MB/s    in 0.8s    

2022-02-02 18:40:40 (43.1 MB/s) - ‘m4_survey_data.sqlite’ saved [36679680/36679680]

Connect to the database.

import sqlite3
conn = sqlite3.connect("m4_survey_data.sqlite") # open a database connection
Import pandas module.

import pandas as pd
Demo: How to run an sql query
# print how many rows are there in the table named 'master'
QUERY = """
SELECT COUNT(*)
FROM master
"""
​
# the read_sql_query runs the sql query and returns the data as a dataframe
df = pd.read_sql_query(QUERY,conn)
df.head()
COUNT(*)
0	11398
Demo: How to list all tables
# print all the tables names in the database
QUERY = """
SELECT name as Table_Name FROM
sqlite_master WHERE
type = 'table'
"""
# the read_sql_query runs the sql query and returns the data as a dataframe
pd.read_sql_query(QUERY,conn)
​
Table_Name
0	EduOther
1	DevType
2	LastInt
3	JobFactors
4	WorkPlan
5	WorkChallenge
6	LanguageWorkedWith
7	LanguageDesireNextYear
8	DatabaseWorkedWith
9	DatabaseDesireNextYear
10	PlatformWorkedWith
11	PlatformDesireNextYear
12	WebFrameWorkedWith
13	WebFrameDesireNextYear
14	MiscTechWorkedWith
15	MiscTechDesireNextYear
16	DevEnviron
17	Containers
18	SOVisitTo
19	SONewContent
20	Gender
21	Sexuality
22	Ethnicity
23	master
Demo: How to run a group by query
QUERY = """
SELECT Age,COUNT(*) as count
FROM master
group by age
order by age
"""
pd.read_sql_query(QUERY,conn)
Age	count
0	NaN	287
1	16.0	3
2	17.0	6
3	18.0	29
4	19.0	78
5	20.0	109
6	21.0	203
7	22.0	406
8	23.0	581
9	24.0	679
10	25.0	738
11	26.0	720
12	27.0	724
13	28.0	787
14	29.0	697
15	30.0	651
16	31.0	531
17	32.0	489
18	33.0	483
19	34.0	395
20	35.0	393
21	36.0	308
22	37.0	280
23	38.0	279
24	39.0	232
25	40.0	187
26	41.0	136
27	42.0	162
28	43.0	100
29	44.0	95
30	45.0	85
31	46.0	66
32	47.0	68
33	48.0	64
34	49.0	66
35	50.0	57
36	51.0	29
37	52.0	41
38	53.0	32
39	54.0	26
40	55.0	13
41	56.0	16
42	57.0	11
43	58.0	12
44	59.0	11
45	60.0	2
46	61.0	10
47	62.0	5
48	63.0	7
49	65.0	2
50	66.0	1
51	67.0	1
52	69.0	1
53	71.0	2
54	72.0	1
55	99.0	1
Demo: How to describe a table
table_name = 'master'  # the table you wish to describe
​
QUERY = """
SELECT sql FROM sqlite_master
WHERE name= '{}'
""".format(table_name)
​
df = pd.read_sql_query(QUERY,conn)
print(df.iat[0,0])
CREATE TABLE "master" (
"index" INTEGER,
  "Respondent" INTEGER,
  "MainBranch" TEXT,
  "Hobbyist" TEXT,
  "OpenSourcer" TEXT,
  "OpenSource" TEXT,
  "Employment" TEXT,
  "Country" TEXT,
  "Student" TEXT,
  "EdLevel" TEXT,
  "UndergradMajor" TEXT,
  "OrgSize" TEXT,
  "YearsCode" TEXT,
  "Age1stCode" TEXT,
  "YearsCodePro" TEXT,
  "CareerSat" TEXT,
  "JobSat" TEXT,
  "MgrIdiot" TEXT,
  "MgrMoney" TEXT,
  "MgrWant" TEXT,
  "JobSeek" TEXT,
  "LastHireDate" TEXT,
  "FizzBuzz" TEXT,
  "ResumeUpdate" TEXT,
  "CurrencySymbol" TEXT,
  "CurrencyDesc" TEXT,
  "CompTotal" REAL,
  "CompFreq" TEXT,
  "ConvertedComp" REAL,
  "WorkWeekHrs" REAL,
  "WorkRemote" TEXT,
  "WorkLoc" TEXT,
  "ImpSyn" TEXT,
  "CodeRev" TEXT,
  "CodeRevHrs" REAL,
  "UnitTests" TEXT,
  "PurchaseHow" TEXT,
  "PurchaseWhat" TEXT,
  "OpSys" TEXT,
  "BlockchainOrg" TEXT,
  "BlockchainIs" TEXT,
  "BetterLife" TEXT,
  "ITperson" TEXT,
  "OffOn" TEXT,
  "SocialMedia" TEXT,
  "Extraversion" TEXT,
  "ScreenName" TEXT,
  "SOVisit1st" TEXT,
  "SOVisitFreq" TEXT,
  "SOFindAnswer" TEXT,
  "SOTimeSaved" TEXT,
  "SOHowMuchTime" TEXT,
  "SOAccount" TEXT,
  "SOPartFreq" TEXT,
  "SOJobs" TEXT,
  "EntTeams" TEXT,
  "SOComm" TEXT,
  "WelcomeChange" TEXT,
  "Age" REAL,
  "Trans" TEXT,
  "Dependents" TEXT,
  "SurveyLength" TEXT,
  "SurveyEase" TEXT
)
Hands-on Lab
Visualizing distribution of data
Histograms
​
Plot a histogram of ConvertedComp.

import matplotlib as mpl
import matplotlib.pyplot as plt
import seaborn as sns
# your code goes here
QUERY= """
​
"""
df=pd.read_sql_query("SELECT*FROM master",conn)
df
​
plt.hist(df["ConvertedComp"])
plt.title("Histogram of ConvertedComp")
plt.xlabel("ConvertedComp")
plt.ylabel("Number of Respondents")
plt.show()

Box Plots
Plot a box plot of Age.

# your code goes here
QUERY="""
​
"""
df=pd.read_sql_query("SELECT*FROM master",conn)
​
df['Age'].plot(kind='box',figsize=(20,8),vert=False)
plt.title('Box Plot of Age')
plt.show()

Visualizing relationships in data
Scatter Plots
Create a scatter plot of Age and WorkWeekHrs.

# your code goes here
column = "Age"
column2 = "WorkWeekHrs"
table_name = "master"
​
QUERY= """
SELECT Age, AVG(WorkWeekHrs) FROM master GROUP BY Age
""".format(column,column2,table_name)
​
df_age_work=pd.read_sql_query(QUERY,conn)
​
df_age_work.dropna(inplace=True)
df_age_work.rename(columns={"AVG(WorkWeekHrs)":"WorkWeekHrs"},inplace=True)
df_age_work.plot(kind="scatter",x="Age",y="WorkWeekHrs",figsize=(9,6),color="red")
​
plt.title("Scatter Plot of Work Hours by Age")
plt.xlabel("Age")
plt.ylabel("Week Work Hours")
plt.show()
plt.close()

Bubble Plots
Create a bubble plot of WorkWeekHrs and CodeRevHrs, use Age column as bubble size.

import plotly.express as px
# your code goes here
QUERY= """
SELECT Age, ConvertedComp, WorkWeekHrs, CodeRevHrs
FROM master
"""
df=pd.read_sql_query(QUERY,conn)
norm_age=(df['Age']-df['Age'].min())/(df['Age'].max()-df['Age'].min())
​
df.plot(kind='scatter',x='WorkWeekHrs',y='CodeRevHrs',s=norm_age*1000,figsize=(10,6),color='yellow')
​
plt.title('Bubble Plot of Work Week Hours and Code Rev Hours')
plt.xlabel('WorkWeekHrs')
plt.ylabel('CodeRevHrs')
​
plt.show
<function matplotlib.pyplot.show(close=None, block=None)>

Visualizing composition of data
Pie Charts
Create a pie chart of the top 5 databases that respondents wish to learn next year. Label the pie chart with database names. Display percentages of each database on the pie chart.

# your code goes here
QUERY= """
SELECT DatabaseDesireNextYear, Count(*)as count
FROM DatabaseDesireNextYear 
group by DatabaseDesireNextYear
order by Count desc limit 5
"""
df=pd.read_sql_query(QUERY,conn)
df.head()
DatabaseDesireNextYear	count
0	PostgreSQL	4328
1	MongoDB	3649
2	Redis	3331
3	MySQL	3281
4	Elasticsearch	2856
#code to create a pie chart
QUERY= """
SELECT DatabaseDesireNextYear, Count(*)as count
FROM DatabaseDesireNextYear 
group by DatabaseDesireNextYear
order by Count desc limit 5
"""
df=pd.read_sql_query(QUERY,conn)
df.head()
df.set_index('DatabaseDesireNextYear',inplace=True)
​
sizes=df.iloc[:,0]
color_list=['red','yellowgreen','gold','blue','lightcoral','pink','lightgreen']
labels=['PostgreSQL','MongoDB','Redis','MySQL','Elasticsearch']
df.plot(kind='pie',
               figsize=(20,6),
               autopct='%1.1f%%',
               startangle=90,
               shadow=True,
               labels=None,
               pctdistance=1.12,
               subplots=True,
               colors=color_list)
​
plt.title('Pie Chart of Top 5 Database Desire Next Year')
plt.axis('equal')
plt.legend(labels, loc='upper left')
plt.show()
No handles with labels found to put in legend.

Stacked Charts
Create a stacked chart of median WorkWeekHrs and CodeRevHrs for the age group 30 to 35.

# your code goes here
QUERY= """
SELECT Age, WorkWeekHrs, CodeRevHrs
FROM master
WHERE Age BETWEEN 30 AND 35
"""
df=pd.read_sql_query(QUERY,conn)
df=df.groupby('Age').median()
print(df)
      WorkWeekHrs  CodeRevHrs
Age                          
30.0         40.0         4.0
31.0         40.0         4.0
32.0         40.0         4.0
33.0         40.0         4.0
34.0         40.0         4.0
35.0         40.0         4.0
# your code goes here
QUERY= """
SELECT Age, WorkWeekHrs, CodeRevHrs
FROM master
WHERE Age Between 30 AND 35
"""
df=pd.read_sql_query(QUERY,conn)
df.set_index('Age',inplace=True)
order=['WorkWeekHrs','CodeRevHrs']
df.groupby('Age')[order].median().plot.bar(stacked=True)
<AxesSubplot:xlabel='Age'>

Visualizing comparison of data
Line Chart
Plot the median ConvertedComp for all ages from 45 to 60.

# your code goes here
QUERY= """
SELECT(ConvertedComp) as ConvertedComp, Age as Age
FROM master
WHERE Age BETWEEN 45 AND 60
"""
df=pd.read_sql_query(QUERY,conn)
df.set_index('Age',inplace=True)
df.dropna(subset=['ConvertedComp'],inplace=True)
​
order=['ConvertedComp']
df.groupby('Age')[order].median().plot(kind='line',figsize=(14,8))
plt.title('Line Chart of ConvertedComp by Age')
plt.show()

Bar Chart
Create a horizontal bar chart using column MainBranch.

# your code goes here
QUERY= """
SELECT Count(MainBranch) as count, MainBranch
FROM master
group by MainBranch
"""
df=pd.read_sql_query(QUERY,conn)
df['MainBranch'].value_counts().plot(kind='barh',figsize=(10,10),color='skyblue')
​
plt.title('Bar Chart of Main Branch')
plt.show()

# What is the rank of Python in most popular Language?
# write code here
QUERY= """
SELECT LanguageWorkedWith
FROM LanguageWorkedWith
"""
df=pd.read_sql_query(QUERY,conn)
df['LanguageWorkedWith'].value_counts()
JavaScript               8687
HTML/CSS                 7830
SQL                      7106
Bash/Shell/PowerShell    4642
Python                   4542
Java                     4506
C#                       4288
TypeScript               3232
PHP                      2913
C++                      1946
C                        1578
Ruby                     1149
Go                       1114
Other(s):                 840
Kotlin                    751
Swift                     707
VBA                       628
R                         585
Objective-C               518
Scala                     492
Assembly                  437
Rust                      324
Dart                      237
Elixir                    187
Clojure                   164
F#                        158
WebAssembly               133
Erlang                     98
Name: LanguageWorkedWith, dtype: int64
# How many respondents indicated they currently work with SQL?
# write your code here
QUERY= """
SELECT LanguageWorkedWith, count(Respondent) as count
FROM LanguageWorkedWith
WHERE LanguageWorkedWith ='SQL'
"""
df=pd.read_sql_query(QUERY,conn)
df
LanguageWorkedWith	count
0	SQL	7106
# How many respondents indicated they work on MySQL only?
# write your code here
QUERY= """
SELECT DatabaseWorkedWith, Respondent
FROM DatabaseWorkedWith
"""
df=pd.read_sql_query(QUERY,conn)
df1=df.groupby('Respondent').sum()
df1[df1['DatabaseWorkedWith']=='MySQL'].count()
DatabaseWorkedWith    474
dtype: int64
# Majority of the Survey Responders are?
# write your code here
QUERY= """
SELECT DevType
FROM DevType
"""
df=pd.read_sql_query(QUERY,conn)
df['DevType'].value_counts()
Developer, full-stack                            6928
Developer, back-end                              6290
Developer, front-end                             3920
Developer, desktop or enterprise applications    2575
Developer, mobile                                1959
DevOps specialist                                1639
Database administrator                           1413
System administrator                             1202
Designer                                          988
Developer, QA or test                             911
Developer, embedded applications or devices       854
Engineer, data                                    832
Data scientist or machine learning specialist     803
Data or business analyst                          802
Student                                           766
Academic researcher                               556
Educator                                          514
Product manager                                   480
Developer, game or graphics                       472
Engineer, site reliability                        449
Engineering manager                               386
Scientist                                         354
Senior executive/VP                               160
Marketing or sales professional                    61
Name: DevType, dtype: int64
QUERY= """
SELECT DevType, count(Respondent) as count
FROM DevType
"""
df=pd.read_sql_query(QUERY,conn)
df
DevType	count
0	Developer, full-stack	35314
Close the database connection.

conn.close()
Authors
Ramesh Sannareddy

Other Contributors
Rav Ahuja

Change Log
Date (YYYY-MM-DD)	Version	Changed By	Change Description
2020-10-17	0.1	Ramesh Sannareddy	Created initial version of the lab
Copyright © 2020 IBM Corporation. This notebook and its source code are released under the terms of the MIT License.

