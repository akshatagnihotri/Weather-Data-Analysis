# Weather-Data-Analysis
We have a Weather dataset containing hourly data on temperature, dew point, humidity, wind speed, visibility, pressure, and conditions at a specific location. This data, stored in a CSV file, will be analyzed using Python's Pandas library in Google Collab. We'll solve various questions about the dataset step-by-step to gain insights.


Q. 1) Find all the unique 'Wind Speed' values in the data.

Q. 2) Find the number of times when the 'Weather is exactly Clear'.

Q. 3) Find the number of times when the 'Wind Speed was exactly 4 km/h'.

Q. 4) Find out all the Null Values in the data.

Q. 5) Rename the column name 'Weather' of the dataframe to 'Weather Condition'.

Q. 6) What is the mean 'Visibility' ?

Q. 7) What is the Standard Deviation of 'Pressure' in this data?

Q. 8) What is the Variance of 'Relative Humidity' in this data ?

Q. 9) Find all instances when 'Snow' was recorded.

Q. 10) Find all instances when 'Wind Speed is above 24' and 'Visibility is 25'.

Q. 11) What is the Mean value of each column against each 'Weather Condition ?

Q. 12) What is the Minimum & Maximum value of each column against each 'Weather Condition ?


Q. 13) Show all the Records where Weather Condition is Fog.

Q. 14) Find all instances when 'Weather is Clear' or 'Visibility is above 40'.

Q. 15) Find all instances when : A. 'Weather is Clear' and 'Relative Humidity is greater than 50' or B. 'Visibility is above 40'



#code:
df.head(2)

Date/Time	Temp_C	Dew Point Temp_C	Rel Hum_%	Wind Speed_km/h	Visibility_km	Press_kPa	Weather
0	1/1/2012 0:00	-1.8	-3.9	86	4	8.0	101.24	Fog
1	1/1/2012 1:00	-1.8	-3.7	87	4	8.0	101.24	Fog

df.nunique()

df['Wind Speed_km/h'].nunique()

df['Wind Speed_km/h'].unique() # Answer


So, here are the all 34 unique values of the column ‘Wind Speed_km/h’.

**Q.2) Find the number of times when the ‘Weather is exactly Clear’.**

To get the answer of this question we have three methods, first is using value_counts function, second is filtering, and third is using groupby function.

Let’s first check what are the unique values (with their count) in the column ‘Weather’, using the value_count function.



df['Weather'].value_counts()

df['Weather'].value_counts()['Clear']

**Now, we will do filtering of the dataset.**

df[df.Weather=='Clear']

**Now with groupby method :**

df.groupby('Weather').get_group('Clear')

## **Q) 3. Find the number of times when the ‘Wind Speed was exactly 4 km/h’.**

df[df['Wind Speed_km/h']==4]

df['Wind Speed_km/h'].value_counts()[4]

# **Q. 4) Find out all the Null (Missing) Values in the data.**

df.isnull().sum()

df.notnull().sum()

df.isna().sum()

# **Q. 5) Rename the column name ‘Weather’ of the dataframe to ‘Weather Condition’.**

df['Weather'].head()

df.rename(columns={'Weather':'Weather Condition'})

# **Q. 6) What is the mean 'Visibility' ?**

df.Visibility_km.mean()

# **Q. 7) What is the Standard Deviation of ‘Pressure’ in this data?**

df

df.Press_kPa.std()

# **Q. 8) What is the Variance of 'Relative Humidity' in this data ?**

df

df['Rel Hum_%'].var()

# **Q. 9) Find all instances when ‘Snow’ was recorded.**

df.head()

df['Weather'].value_counts()

df[df['Weather']=='Snow']

df[df['Weather'].str.contains('Snow')]

# **Q. 10) Find all instances when ‘Wind Speed is above 24’ and ‘Visibility is 25’.**

df[(df['Wind Speed_km/h']>24) & (df['Visibility_km']==25)]

For our first condition i.e., ‘Wind Speed is above 24’, we will use the comparison operator - Greater Than ( > ). For the second condition i.e., ‘Visibility is 25’, we will use the comparison operator - Equal To ( == ).

And now, using the Logical AND Operator ( & ) between these two conditions, we will get only those records where ‘Wind Speed is above 24’ and ‘Visibility is 25’. Hence, there are 308 records satisfying both the conditions.

# **Q. 11) What is the Mean value of each column against each ‘Weather Condition’ ?**

df.head()

To solve this, first we have to form groups for each unique value of the column ‘Weather Condition’ using groupby( ), as we did above.

After having the groups, we can use the mean( ) , as shown in the output below.

df.groupby('Weather').mean('numeric_only')

Here we have to pass numeric_only inside the mean function, so that it will consider the numeric columns only.

Hence, you can see, for example, when the weather was ‘Clear’ the mean value of Temperature was 6.825716, and when the weather was ‘Freezing Fog’ the mean Pressure was 102.320000.

# **Q. 12) What is the Minimum & Maximum value of each column against each ‘Weather Condition’ ?**

df.groupby('Weather').min('numeric_only')

df.groupby('Weather').max('numeric_only')

# **Q. 13) Show all the Records where Weather Condition is Fog.**

df[df['Weather']== 'Fog']

we found that there were 150 records when there was ‘Fog’.

# **Q. 14) Find all instances when ‘Weather is Clear’ or ‘Visibility is above 40’.**

df[(df['Weather']=='Clear') & (df['Visibility_km']>40)]

For our first condition i.e., ‘Weather is Clear’, we will use the comparison operator ‘Equal To ( == )’. It will consider all those records when weather is clear.

For the second condition i.e., ‘Visibility is above 40’, we will use the comparison operator ‘Greater Than ( > )’. It will consider all those records when visibility is more than 40.

And now, using the Logical OR Operator ( | ) between these two conditions, we will get both the records where you will see in the output either ‘Weather is Clear’ or ‘Visibility is above 40’. Hence, there are 3027 records in this case.

# **Q. 15) Find all instances when :**
# A. ‘Weather is Clear’ and ‘Relative Humidity is greater than 50’
# or
# B. ‘Visibility is above 40’

df[(df['Weather']=='Clear') & (df['Rel Hum_%']>50) | (df['Visibility_km']>40)]

df[df['Visibility_km']>40]

First, we will consider the Weather Condition column to get the records where weather is ‘Clear’ only, with the Rel Hum_% column to get the records where Relative Humidity is greater than 50. Here we will use the AND ( & ) operator between these two.

These two combined conditions will be our one single Condition 1 now i.e., (df[‘Weather Condition’] == ‘Clear’) & (df[‘Rel Hum_%’] > 50).

Then we will consider the Visibility_km column to get the records where Visibility is above 40. This will become our second Condition 2 i.e., (df([‘Visibility_km’] > 40).

Now we have to combine the Condition 1 and Condition 2 using the OR (|) operator as shown in the output above to get the desired results. Hence, there are 2921 records satisfying the given conditions of the question.





# ***So, that’s all friends for this project.***
