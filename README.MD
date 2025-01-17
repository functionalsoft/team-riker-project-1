# Team Riker Project 1

Team Members:
 - Brendan O'Hara
 - Dhruba Chakrabarti
 - Ravichandran Chinnamanaidu

Final Code File: <em>main-worksheet.ipynb</em>

# Introduction:

In this project, we have attempted to study some mental health survey data, gathered over several years, to determine whether people in tech are more prone to mental health issues compared to those in non tech companies or roles.**

Source of the data
 - <a href=https://www.kaggle.com>Kaggle</a>
    
# Description:

**The stability and success of a company can often be measured by the relative health on an employee. Which physical health, ailments etc. are very apparent, and provided for, the mental health on an employee is often overlooked in both the tech and non tech industries. We have acquired mental health survey data and have used it to determine whether mental issues are more common among employees in tech companies/roles or non tech companies. We originally acquired data spanning over several years from 2016 to 2023. Inconsistencies in the schema of the survey data in the earlier years prompted us to use data from surveys performed in more recent years. We were eventually able to use data from 2020 to 2022 for the purposes of our analysis.

```
The python modules imported
import pandas as pd
from prophet import Prophet
import datetime as dt
import numpy as np
from bs4 import BeautifulSoup
import markdown
import string
import re
import matplotlib.pyplot as plt
import plotly.express as px
import seaborn as sns
from wordcloud import WordCloud
from wordcloud import ImageColorGenerator
from wordcloud import STOPWORDS
```
There are inbuilt functions developed to clean up the data , specifically html tags, blank space, special characters, number signs, <strong> and </strong> and <em> and </em> and None.

functions were also built to merge columns, drop duplicate columns, reset indexes, NAN, None, data type conversion from float to int and int to string.., cleanup the data and retrofitting to the filtered columns that are required for reports.

```
['self-employed', 'num-employees', 'tech-employer', 'tech-role', 'has-mental-health-benefits', 'know-mental-health-options', 'discussed-mental-health', 'has-mental-health-resources', 'anonymity-protected', 'mental-health-leave-ease', 'comfort-discussing-health', 'discuss-mental-health-supervisor', 'discussed-mental-health-employer', 'discuss-mental-health-coworkers', 'discussed-mental-health-coworkers', 'coworker-mental-health-discussion', 'importance-physical-health', 'importance-mental-health', 'mental-health-coverage', 'know-mental-health-resources', 'reveal-mental-health-clients', 'effect-reveal-mental-health', 'reveal-mental-health-coworkers', 'impact-reveal-mental-health', 'productivity-mental-health', 'percentage-affected-mental-health', 'previous-mental-health-talk-coworkers', 'current-mental-health-disorder', 'diagnosed-mental-health', 'past-mental-health-disorder', 'sought-treatment', 'family-history-mental-illness', 'mental-health-interference-treated', 'mental-health-interference-untreated', 'observations-mental-health-discussion', 'share-mental-illness', 'physical-health-interview', 'mental-health-interview', 'open-mental-health', 'mental-health-career', 'mental-health-career-effect', 'team-reaction', 'unsupportive-response', 'supportive-response', 'industry-support', 'interview-mental-health', 'age', 'gender', 'country-live', 'us-state-live', 'race', 'year', 'submit-date', 'network-id', 'disorders']      
```
** 

# Scope of the project

*  The project scope as we proceed with data and preparing the metrics reports

        1. Clean the data
        2. Prepare 3 visualizations that will provide some insight
        3. Split the data into tech and non tech company
        4 . Count entries in each new DF to find out sample size
        5 . Sample from both DFs
        6. Merge Sampled DFs back together
        7. Run visualization



# Sample data
```
..
100000,0,25-Jun,1,,No,Yes,Yes,Yes,Yes,Somewhat easy,No,No,Maybe,Yes,Yes,No,,,,,,,,,1,"Yes, they all did",I was aware of some,None did,Some did,"Yes, always",None of them,None of them,"No, at none of my previous employers",Some of my previous employers,Some did,None of them,Maybe,"It would depend on the health issue. If there is a health issue that would not immediately affect my job performance, such as diabetes, I woul
..
```

# data cleanup functions

```
pd.set_option('display.max_columns', None)

def remove_html_tags(text):
    return BeautifulSoup(text, "html.parser").get_text()


def remove_markdown(text):
    html = markdown.markdown(text)
    return BeautifulSoup(html+ "html.parser").get_text()

def clean_row(row):
    return row.apply(lambda x: remove_markdown(remove_html_tags(x)) if isinstance(x, str) else x)

def clean_text(text):
    text = re.sub(r'-', ' ', text)
    text = re.sub(r'#', 'unique_column_heading', text)
    text = re.sub(r'None', 'unique_column_heading', text)
    text = re.sub(r'<strong>', '', text)
    text = re.sub(r'</strong>', ' ', text)
    text = re.sub(r'<em>', ' ', text)
    text = re.sub(r'</em>', ' ', text)
    # Remove punctuation
    text = text.translate(str.maketrans('', '', string.punctuation))
    # Convert to lowercase
    text = text.lower()
    # Replace spaces with dashes
    text = re.sub(r'\s+', '-', text)
    return text

def rename_duplicate_columns(mhs_df):
    cols = pd.Series(mhs_df.columns)
    for dup in cols[cols.duplicated()].unique():
        cols[cols[cols == dup].index.values.tolist()] = [dup + '_' + str(i) if i != 0 else dup for i in range(sum(cols == dup))]
    mhs_df.columns = cols
    return mhs_df

def preprocess_df(df):
    df = df.astype(str)
    df = rename_duplicate_columns(df)
    df = df.reset_index(drop=True)
    return df
```



# Activities


## Part1  Do people in Tech Companies or with Tech Roles have more MH issues than their counterparts?

    1. Clean the data
    2. Prepare 3 visualizations that will provide some insight
    3. Split the data into tech and non tech company
    4. Count entries in each new DF to find out sample size
    5. Sample from both DFs
    6. Merge Sampled DFs back together
    7. Run visualization

The charts from PPT

![P1C1](./images/P1C1.png)
![P1C1](./images/P1C2.png)
![P1C1](./images/P1C3.png)

    * Conclusion
    ** There doesn’t seem to be any correlation between Tech and MH Issues **
    1. Is this because of sample size?
    2. Is this because of the burdensome way the survey was structured?
    3. Is Age a factor? Perhaps or it is more about the stress associated with career progression.

## Part 2 Do people in Companies with Wellness Programs have more MH issues then their counterparts?
    Clean the data
    Prepare 2 visualizations that will provide some insight
    Split data into wellness and non wellness companies
    Count entries in each new DF to find out sample size
    Sample from both DFs
    Merge Sampled DFs back together
    Run visualization
    Consider our life choices

The charts from PPT

![P2C1](./images/P2C1.png)
![P2C2](./images/P2C2.png)

    * Conclusion
    There does not seem to be any correlation between Wellness Programs and MH Issues
    Is this because of wellness programs that more people are less reluctant to admit it?
    Is this because of wellness programs that more people seek help?

## Part 3 Do USA Tech Employees have more MH issues than International Tech Employees?

    Clean the data
    Prepare ~2 visualizations that will provide some insight
    Split the data into USA and International locations
    Count entries in each new DF to find out sample size
    Sample from both DFs
    Merge Sampled DFs back together
    Run visualization
    Weep

The charts from PPT

![P3C1](./images/P3C1.png)
![P3C2](./images/P3C2.png)


    Conclusion
    Tech employees in the USA have more Mental Health issues.
    Is this because of overall work culture?
    Is this because of wellness programs that are built into national health systems
    Is it because there is less of a culture of coming forward with MH issues


# Overall Conclusion

    Although I am sure some people could try and use this data to make more correlations, we simply didn’t think many of the ones we could have attempted would have been defendable
    Data as a Time Series not reliable enough to use a Prophet Model and attempt a projection
    Yes they are mostly bar charts… Mea culpa
    Lies, Damn Lies and Statistics and Star Trek does have something to say about it…
