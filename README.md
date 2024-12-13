# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
           



from google.colab import drive
drive.mount('/content/drive')

ls drive/MyDrive/DS2024/Data_set.csv



# **Data Cleaning**

import pandas as pd
# READ CSV FILE HERE
df=pd.read_csv('drive/MyDrive/DS2024/Data_set.csv')

df
![Screenshot 2024-12-13 142736](https://github.com/user-attachments/assets/532734cd-963f-4e92-a028-9981e4f48dde)

# CHECK OUT NULL VALUES IN DATA SET USING FUNCTION
df_null=df.isnull()

df_null

![Screenshot 2024-12-13 142759](https://github.com/user-attachments/assets/a14953df-39c6-4321-89e7-c17811ebf3d6)


# DISPLAY THE SUM ON NULL VALUES IN EACH ROWS
df_null_sum=df.isnull().sum()

df_null_sum

![Screenshot 2024-12-13 142817](https://github.com/user-attachments/assets/3c7fd606-245f-492d-9d48-c3943a6ba5f4)

# DROP NULL VALUES
df_dropna=df.isnull().dropna()

df_dropna

![Screenshot 2024-12-13 142834](https://github.com/user-attachments/assets/9d643e24-3d26-43f8-97c7-88b937b5efe3)

# FILL NULL VALUES WITH CONSTANT VALUE "O"
df_nafill_0=df.fillna(0)

df_nafill_0

![Screenshot 2024-12-13 142849](https://github.com/user-attachments/assets/b7993cd4-79fa-47d0-934b-a64700caa3ec)

# FILL NULL VALUES WITH ffill METHOD
df_ffill=df.ffill()

df_ffill

![Screenshot 2024-12-13 142905](https://github.com/user-attachments/assets/a12bec16-c210-42be-880f-0bd73eebfdc8)

# FILL NULL VALUES WITH bfill METHOD
df_bfill=df.bfill()

df_bfill

![Screenshot 2024-12-13 142926](https://github.com/user-attachments/assets/d02e1303-633b-4a6e-b664-3d42f63f49dd)

# CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
df_mean1=df['num_episodes'].fillna(df['num_episodes'].mean())

df_mean1

![Screenshot 2024-12-13 142940](https://github.com/user-attachments/assets/3363c7e9-2c8b-496e-b23a-5af8b944e9d4)


df_mean2=df['rating'].fillna(df['rating'].mean())

df_mean2

![Screenshot 2024-12-13 142954](https://github.com/user-attachments/assets/b7dc52bd-24dc-4b62-8863-cdcb7f08ef0f)

df_mean3=df['current_overall_rank'].fillna(df['current_overall_rank'].mean())

df_mean3

![Screenshot 2024-12-13 143004](https://github.com/user-attachments/assets/31d00943-f61a-4a01-bfed-c1988d233d7e)

df_mean4=df['lifetime_popularity_rank'].fillna(df['lifetime_popularity_rank'].mean())

df_mean4

![Screenshot 2024-12-13 143015](https://github.com/user-attachments/assets/8bc44c25-f03e-4392-a592-06ef1393af44)

df_mean5=df['watchers'].fillna(df['watchers'].mean())

df_mean5

![Screenshot 2024-12-13 143028](https://github.com/user-attachments/assets/ea670717-0615-4d82-ae62-6e011e5f02dd)

# DROP NULL VALUES
df_dropna=df.dropna()

df_dropna

![Screenshot 2024-12-13 143042](https://github.com/user-attachments/assets/9a82086a-124d-4d32-aeb4-1b1ab2fe6e9f)

# **Outlier Detection and Removal - IQR**

import pandas as pd
import seaborn as sns

age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)

af
![Screenshot 2024-12-13 143057](https://github.com/user-attachments/assets/f7ac553f-fb2b-4a79-92f9-e7fe0a484dcf)

# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
sns.boxplot(af)

![Screenshot 2024-12-13 143117](https://github.com/user-attachments/assets/d40f78d4-f2fb-4240-ba53-84cc881f8d5b)

sns.scatterplot(af)

![Screenshot 2024-12-13 143132](https://github.com/user-attachments/assets/1f515060-2073-458b-8465-26021880f08c)

q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)


iqr=q3-q1

iqr

![Screenshot 2024-12-13 143211](https://github.com/user-attachments/assets/8bc75f95-7ad7-4b5a-a8bb-01226d118d42)

import numpy as np

Q1=np.percentile(af,25)
Q2=np.percentile(af,50)
Q3=np.percentile(af,75)

IQR=Q3-Q1

lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR

outliers = [x for x in age if x < lower_bound or x > upper_bound]


print('Q1:',Q1)

print('Q3:',Q3)

print('IQR:',IQR)

print('Lower bound:',lower_bound)

print('Upper bound:',upper_bound)

print('Outliers:',outliers)

![Screenshot 2024-12-13 143220](https://github.com/user-attachments/assets/7c37b202-f20b-48ea-8582-2053019e6099)

af=af[((af>=lower_bound)&(af<=upper_bound))]

af

![Screenshot 2024-12-13 143228](https://github.com/user-attachments/assets/f33ed4f8-84f9-4dcb-9881-ee36de462cef)

af.dropna()

![Screenshot 2024-12-13 143235](https://github.com/user-attachments/assets/34c451cd-e6c8-4f13-8655-5d0ffea713c3)

sns.boxplot(af)

![Screenshot 2024-12-13 143243](https://github.com/user-attachments/assets/079c24dc-cf5d-49a8-8c00-57f4ef88488c)

sns.scatterplot(af)

![Screenshot 2024-12-13 143252](https://github.com/user-attachments/assets/4c00a248-5213-4dc5-95e0-2bce4abf0117)

# **Z Score**

from scipy import stats #STATS METHOD IS USED TO IMPLEMENT Z SCORE METHOD
import numpy as np
import pandas as pd
import seaborn as sns

data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93]
df=pd.DataFrame(data)

# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
sns.boxplot(df)

![Screenshot 2024-12-13 143305](https://github.com/user-attachments/assets/3b514642-5693-441b-86a3-7c2f1692c5a8)

mean=np.mean(data)

mean

![Screenshot 2024-12-13 143432](https://github.com/user-attachments/assets/eefb1ebe-9602-4937-a9e8-b54a2530d1df)

std=np.std(data)

std

![Screenshot 2024-12-13 143439](https://github.com/user-attachments/assets/601cfe19-4803-4ed3-b529-3e58cdbca87b)

# PERFORM Z SCORE METHOD AND DETECT OUTLIER VALUES
z=np.abs(stats.zscore(df))

z

![Screenshot 2024-12-13 143548](https://github.com/user-attachments/assets/747c87e4-46e9-4fc0-bf63-7ed6acff471b)
![Screenshot 2024-12-13 143600](https://github.com/user-attachments/assets/9a2f3d85-6b52-4863-9c60-3bc32d2edaa8)

threshold=3

outliers = df[abs(df) > 3]

print("Outliers:")

print(outliers)

![Screenshot 2024-12-13 143624](https://github.com/user-attachments/assets/3bb51331-1742-4abf-8a5b-a9e630bcba61)

# Remove outliers
df_cleaned = df[(z <= threshold)]

df_cleaned

![Screenshot 2024-12-13 143650](https://github.com/user-attachments/assets/2e18b785-c870-4a7b-b761-e6a49e51abad)
![Screenshot 2024-12-13 143701](https://github.com/user-attachments/assets/de074d1b-ecc3-48fe-9d86-b633743a5b0f)

# USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
sns.boxplot(df_cleaned)

![Screenshot 2024-12-13 143710](https://github.com/user-attachments/assets/83b1bbee-19b5-4e7a-93ea-8a65276231da)

sns.scatterplot(df_cleaned)

![Screenshot 2024-12-13 143719](https://github.com/user-attachments/assets/2750c407-d563-4719-8a77-d938c0c0541d)

# Result
the code is run sucessfully.
