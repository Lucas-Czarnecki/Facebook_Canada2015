# The 2015 Canadian Federal Election on Facebook

## Introduction to the Data

This repository contains Facebook user data from the 2015 Canadian general election. Data consists of federal party leaders’ campaign messages (N = 1,711) and the responses to those messages from everyday Facebook users (n = 92,813). 

The data are organized relationally such that Facebook users’ party identification, political preferences, and emotional responses to campaign messages can be identified and measured. The partisanship of Facebook users *may* be inferred based on the campaign content that users liked on Facebook.

## Data Collection

Data were queried from Facebook using R, a statistical program and language, through an
established connection to Facebook’s publicly accessible Graph API (v.2.0). The most important package for data collection was `Rfacebook`, which provided various functions for accessing Facebook's public API.

> Note: Facebook terminated all access to its public API in 2018. Note then that the `Rfacebook` packages is no longer being maintained. Unfortunately, because of these developments it is impossible to collect Facebook data with the methods used in this repository.

Data were queried from three public Facebook pages belonging to Stephen
Harper, Justin Trudeau, and Tom Mulcair’s candidacies. Data on Facebook users' personal profiles **were not** collected. The research design, therefore, ensures that only public posts were scraped. 

## Data Cleaning

Numerous packages from the Comprehensive R Archive Network (CRAN) were used to make data preprocessing and text analysis possible. 

---

## How the Data are Organized

The data are organized in two separate folders. Below I will briefly describe each folder and summarize its contents. 

In each folder you will be able to find the raw and cleaned version of the data.

### **1) The Facebook Pages Dataset**

This data set contains structured data on every post published to the three verified public Facebook pages in this repository. Data range from August 4th until October 19th, 2015, consisting of every post published to Facebook during thistime (N = 1,711).

This data set contains six fields of structured data; namely, `id`, `type`, `created_time`, `likes_count`, `comments_count`, and `shares_count`. The latter three fields record the total number of likes, comments, and shares that each post accumulated on Facebook during the 2015 election campaign. See the 

### **2) The Campaign Messages Dataset**

The second data set consists of party leaders’ text-based Facebook posts (n = 1,530). The data queried in this dataset consists of many of the same variables found in the Facebook Pages Dataset; including, `creation_time`, `from_id`, and `id`. It also contains a field called `message`, which records UTF-8 encoded text data on every campaign message published to Facebook. Posts that did not contain any text data (after preprocessing) were removed from this dataset.

### **3) The Facebook Users Dataset**

The final data set is a collection of Facebook user responses to posts that candidates published on Facebook during the election. Data consist of comments published to Facebook between August 4th and October 19th, 2015. The data set contains many of the same fields of structured data as the two previous data sets. The `message` column returns the text-based comments that Facebook users published in response to candidates’ campaign messages during the 2015 election campaign.

## Variables 



---
## Credits: