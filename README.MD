# Team Rider Project 1

# Introduction:

**In this project detail study provided to get the stats of the healthness of the people who are in tech Industry, primary focus is to compare the people in tech and non tech industries., since healthness of the people and their stability to required solution on ongoing issues are more important for the industry to provide competitive product in the raising demands. Also team member coordination and their team work considered more as wellness and health measure.**

* Source of the data
    1. https://www.kaggle.com
    2. https://healthdata.gov
    3. https://data.cdc.gov/
    
# Description:

** The health awareness and the stability on the emloyees working in tech and non tech sectors plays critical role on the stability and success of the company, in this project a detail study of the mental stability of the employees in tech and non tech sectors are covered, also the employees visiting the hospitals/doctors for mental issues are gone in details and comparative charts are provided and stats/metrics report created across tech and non tech firm.

The unique set of data is pulled for the year from 2013 to 2020 from the kaggle for analysis purposes., each file has few hundred columns and required columns are filtered from the CSV file for the report.


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

There are inbuilt functions developed to clean up the data , specifically html tags, blank space, special characters, number signs, <strong> and </strong> and <em> and </em> and None.

functions were also built to merge columns, drop duplicate columns, reset indexes, NAN, None, data type conversion from float to int and int to string.., cleanup the data and retrofitting to the filtered columns that are required for reports.


['self-employed', 'num-employees', 'tech-employer', 'tech-role', 'has-mental-health-benefits', 'know-mental-health-options', 'discussed-mental-health', 'has-mental-health-resources', 'anonymity-protected', 'mental-health-leave-ease', 'comfort-discussing-health', 'discuss-mental-health-supervisor', 'discussed-mental-health-employer', 'discuss-mental-health-coworkers', 'discussed-mental-health-coworkers', 'coworker-mental-health-discussion', 'importance-physical-health', 'importance-mental-health', 'mental-health-coverage', 'know-mental-health-resources', 'reveal-mental-health-clients', 'effect-reveal-mental-health', 'reveal-mental-health-coworkers', 'impact-reveal-mental-health', 'productivity-mental-health', 'percentage-affected-mental-health', 'previous-mental-health-talk-coworkers', 'current-mental-health-disorder', 'diagnosed-mental-health', 'past-mental-health-disorder', 'sought-treatment', 'family-history-mental-illness', 'mental-health-interference-treated', 'mental-health-interference-untreated', 'observations-mental-health-discussion', 'share-mental-illness', 'physical-health-interview', 'mental-health-interview', 'open-mental-health', 'mental-health-career', 'mental-health-career-effect', 'team-reaction', 'unsupportive-response', 'supportive-response', 'industry-support', 'interview-mental-health', 'age', 'gender', 'country-live', 'us-state-live', 'race', 'year', 'submit-date', 'network-id', 'disorders']      

The final charts that in the power points ** 

# Scope

The final solution of the product is to provide healthness of the people in tech industry and non tech industry and their metrics data.
