# Disordered Sleep

<p>The goal of  this project is to determine if there is a relationship  between sleep disorders and several variables, including gender, age, and BMI. The project also takes a deeper look at the correlation between stress and the quality of sleep</p>

The project aims to answer the following two questions: 
- How are sleep disorders related to the gender, age, and the BMI of individuals? 
- Is there a correlation between stress levels and the quality of sleep?

Alternate hypothesis: Sleep disorders are more common in people who are: males, older adults, and overweight. Stress negatively affects the quality of sleep. 

Null hypothesis: sleep disorders are not related to a person’s gender, age, and weight. The is no correlation between stress and the quality of sleep. 


----

## Installation
- Use the package manager  [pip](https://pip.pypa.io/en/stable/) to install pandas and seaborn
```
pip install pandas
pip install seaborn
```
- Also, import the following dependencies: numpy, scipy, and matplotlib.
----
## Data Source
<p>The "Sleep Health and Lifestyle" dataset by Laksika Tharmalingam on Kaggle was used for this project. <p>

- Source URL: [dataset](https://www.kaggle.com/datasets/uom190346a/sleep-health-and-lifestyle-dataset/data)
- The dataset is a synthetically generated data that includes variables like gender, age, occupation, BMI, sleep disorders, stress level, physical activity, quality of sleep, and duration of sleep. 
---
## Data Processing
- In this step, the dataframe was inspected for any missing values using the info() function.

- Some data values were converted into a consistent metric:
  - "Normal Weight" value in the BMI column was converted into "Normal"
  - "None" value in the 'Sleep Disorder' column was converted into "Normal"
```python
sleep_data.loc[sleep_data['BMI Category'] == 'Normal Weight', 'BMI Category'] = 'Normal'
sleep_data.loc[sleep_data['Sleep Disorder'] == 'None', 'Sleep Disorder'] = 'Normal'
```
- Next, the groupby() function was used to combine variables together:
  - The sleep disorders  were grouped by the gender column, and percentages for each disorder per gender was calculated.
  - The age column was grouped by the gender, then filtered by the age of 50 years old.
  - Sleep disorders was grouped by age and percentages for each disorder were calculated. 
  - Sleep disorders were grouped by BMI.
  - The quality of sleep was grouped by the stress level.
---
## Data analysis
- In this step, dataframes were printed for all the grouped variables.
- The count, mean, median, min, max, standard deviation, and percentile for each variable was calculated.
- Extra attention was paid for the values of the filtered age dataframe.
- The mean and median age for each sleep disorder were calculated and assembled in a separate dataframe. 
```
mean = sleep_data['Age'].groupby(sleep_data['Sleep Disorder']).mean()
median = sleep_data['Age'].groupby(sleep_data['Sleep Disorder']).median()

summary_mean= pd.DataFrame({" Mean Age": mean, "Median Age": median})
summary_mean

```
-  A linear regression model was fitted to predict the quality of sleep across different stress levels. 
   - The "stats.pearsonr" function was used to calculate the correlation coefficient (R-value) between "Stress Level" and "Quality of Sleep."
```
reg_plot = sns.regplot(x=x, y=y, scatter=False, color='red', line_kws={"linewidth": 2})
```
- Visualizations:
  - A bar graph displayed the count of sleep disorders per gender.
  - A line graph displayed the percentage of sleep disorders by age.
  - Three pie graphs displayed the distribution of each sleep disorder across the three BMI categories: normal, overweight, obese.
  - A bubble chart displayed the quality of sleep across different stress levels.
  - A bubble chart with a linear regression line showed the correlation between the quality of sleep and stress. 
## Findings
- Sleep disorder vs gender:
   -  Most people don’t suffer from sleep disorders. 
  - Contrary to real-life, this dataset showed sleep apnea more prevalent in females than males by a 15% difference in cases.
  - Insomnia slightly more common in males than females by 1% difference in cases. 
- Key obsevations regarding the age data in this dataset:
   - The age of the people in the dataset ranged from 27 - 59 years old, averaging at 42. 
  - No men above 50 years old were included. However, there was several females above the age of 50 in the dataset. 
- Sleep disorder vs. age:
  - Sleep disorders become more prevalent with age.
  - Per dataset, insomnia common in mid 40’s.
  - Sleep apnea more common in 50 year olds and above.
- Sleep disorder vs BMI:
  - 91.3% of people who don’t suffer from a sleep disorder have a normal BMI.
  - 83.1% of insomniac people are overweight.
  - 83.3% of people with sleep apnea are overweight.
- Sleep Quality vs Stress level:
  - As the stress level increases, the quality of sleep decreases.
  - With an r-value of -0.81, there is a strong negative linear correlation between the stress level and the quality of sleep.
## Conclusion
- The alternate hypothesis can be partially accepted, and the null hypothesis can be partially rejected.
- Sleep disorders are more common in older and overweight people. 
- Stress level does negatively affect the quality of sleep.
- However, no conclusion can be made from this dataset that sleep disorders are more common in females, as this data didn’t include males from the same age as the older females. 
## Recommendations and limitations
- More testing is needed to analyze the relationship between sleep disorder and gender.
- The dataset is synthetic; therefore, the results are not applicable to real life.
- The dataset consisted of only 374 individuals. The sample size was small to produce strongly significant results.
