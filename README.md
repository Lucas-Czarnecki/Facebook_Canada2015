# <span style ="color: #3b5998"> **The 2015 Canadian Federal Election on Facebook** </span>

## <span style ="color: #dfe3ee"> Table of Contents: </span>
---

1. [Introduction to the Data](#1-Introduction-to-the-Data)
2. [Data Collection](#2-data-collection)
3. [Variables](#3-variables)
4. [Data Cleaning](#4-data-cleaning)
5. [How the Data are Organized](#5-How-the-Data-are-Organized)
---

## 1. Introduction to the Data

This repository contains Facebook user data from the 2015 Canadian general election. The data consist of federal party leaders’ campaign messages (N = 1,711) and the responses to those messages from Facebook users (n = 92,516). Data range from August 4th until October 19th, 2015; the duration of the 2015 election campaign.

The data are organized relationally such that Facebook users’ party identification, political preferences, and emotional responses to campaign messages can be identified and measured. The partisanship of Facebook users may also be inferred based on the campaign content that users liked on Facebook during the campaign.

> Note: As of 2018 Facebook has terminated access to its public Graph API. As such it is no longer possible to scrape the data collected in this repository. Making the data herein especially valuable to researchers. (I can only hope that Facebook will open the door to researchers in the future). 

--- 

## 2. Data Collection 

Data were queried from Facebook using R, a statistical program and language, through an established connection to Facebook’s publicly accessible Graph API (v.2.0). Data were queried using the [`Rfacebook`](https://github.com/pablobarbera/Rfacebook) package, which provided various functions for accessing Facebook's public API.

Data were queried from three public Facebook pages belonging to Stephen
Harper, Justin Trudeau, and Tom Mulcair’s candidacies. **This project's research design ensures that only public posts were scraped - data from Facebook users' personal profiles was not collected.**

> Note: As a result of Facebook terminating access to its public Graph API, the `Rfacebook` package is no longer being maintained. 

### Raw Data
The raw data consist of hundreds of Facebook objects contained within hundreds of lists. The data were queried according to the relational nature of these objects. Three component types were extracted to create a relational data set; namely, `posts` (i.e., Party leaders' campaign messages), `comments` (i.e., Facebook users' text-based responses to party leaders' posts), and `likes` (i.e., user IDs of individuals who liked party leaders' posts). 

For reasons of privacy I have uploaded the "raw" data as csv files, but have modified the contents to remove Facebook users' screen names and anonymize their Facebook IDs. The data can be found [HERE](https://github.com/Lucas-Czarnecki/Facebook_Canada2015/tree/master/data/raw).

---

## 3. Variables 

Table 1 provides a brief summary of the variables scraped from Facebook's Graph API. More information pertaining to these variables can be found on `Rfacebook's` [GitHub repository](https://github.com/pablobarbera/Rfacebook) and [CRAN documentation](https://cran.r-project.org/web/packages/Rfacebook/Rfacebook.pdf). 



### Table 1. Variables from Facebook's Graph API

| Variable      | Description     |
| :---        | :---- |
| `from_id`  | <span style ="color: red"> (Redacted for users) </span> Contains unique numeric IDs that identify the author of every comment.  |
| `from_name`   | <span style= "color:red"> (Redacted for users) </span>  Contains Facebook users' screen names.  |
| `message` | Are the text-based messages published to Facebook. Text data come either from Facebook users' comments or party leaders' posts.|
| `id` | Are unique numeric values that uniquely identify every Facebook post. (In this repo, the numerical values to the left of an underscore identify the party leaders while values to the right identify the post). |
| `likes_count` | Records the total number of likes a post or comment recieved. |
| `comments_count` | Records the total number of comments a post recieved. |
| `shares_count` | Records the total number of shares a post recieved. |
|`created_time` | Consists of timestamps, which record when each post or comment was published to Facebook. |
| `link` | Includes URLs from links that were added to status updates. |
| `type` | Records the kinds of media that accompanied each post; namely, “event”, “link”, “photo”, “status”, or “video”. |
---
<br>

As noted above, `from_id` and `from_name` have been redacted, but only for Facebook users. The exception then is for party leaders for whom anonymity is not a concern. IDs contained in `from_id` have been replace with `user_id`, which used a well-known algorithm to hash the original IDs. `from_name` has been removed entirely for Facebook users. 

<br>

Table 2 provides a summary of additional variables that I created based on the information obtained from Facebook's graph API. 

### Table 2. Additional Variables Created Based on Facebook's Graph API

| Variable      | Description     |
| :---        | :---- |
| `user_id` | <span style = "color: green"> (Anonymized Id) </span> `user_id` was created by anonymizing the numerical ids in `from_id`. All Facebook users are, therefore, uniquely and anonymously identified. 
| `candidate_page` | Identifies from which party leader's Facebook Page posts or comments were scraped. |
| `post_id` | Separates the numerical id located to the left of the underscore in `id`. This value identifies the Facebook post. Useful for data wrangling. |
| `comment_id` | Separates the numerical id located to the right of the underscore in `id`. This value uniquely identifies comments made in response to Facebook posts. Useful for data wrangling. |
| `date_published`  | Records the day that the post or comment was published to Facebook based on `created_time`. |
| `time_published` | Records the time of day that the post or comment was published to Facebook based on `created_time`. |
| `month_published`| Records the month that the post or comment was published to Facebook based on `created_time`. |
| `campaign_week` | Identifies in which of the 11 weeks of campaigning each post was published to Facebook where the beginning of each week is a Monday. This variable has 12 possible values; one for each week and Election Day. |
| `partisanship` | Identifies possible partianship of Facebook users. Users are labelled "Conservative", "Liberal", or "Social Democrat" if they exclusively liked content from one candidate.  |

---

> Note: The 2015 election campaign was technically 11 weeks plus one day. Election Day is, therefore, included as a stand alone value in `campaign_week`.

---

## 4. Data Cleaning 

Data cleaning procedures were applied to text-based data contained in Facebook users' and party leaders' `messages`. The following preprocessing tasks were appliead to facilitate statistical analysis and data visualization:
* word tokenization, 
* case-folding to lower-case,
* removal of nonletter and special characters (e.g., %, /, $, #, etc.),
* regular expressions to remove URLs and emoji-related Unicode.

You will find all the packages and operations used in cleaning these data documented in my scripts, which you can find in the folder, [R](https://github.com/Lucas-Czarnecki/Facebook_Canada2015/tree/master/R). If you prefer to preprocess the text yourself, you can find the unmodified text data in the folder, [raw](https://github.com/Lucas-Czarnecki/Facebook_Canada2015/tree/master/data/raw). 

---

## 5. How the Data are Organized 

This section briefly describes how data were organized. Figure 1 serves as a visual illustration of the relationship between data sets. 

### Figure 1. The Relationships Between Datasets
![Facebook Relational Data](https://github.com/Lucas-Czarnecki/Facebook_Canada2015/blob/master/images/Facebook_Relational_Data.png)
*Notes. The data pertaining to party leaders in this example are real. All information relating to Facebook users (e.g.,
from_id, from_name, message) are fictionalized.*


### **1. The Facebook Pages Dataset**

This data set contains strictly **structured data** on every post published to the three verified public Facebook pages in this repository. Data range from August 4th until October 19th, 2015, consisting of every post published to Facebook during this time (N = 1,711).

This data set contains six fields of structured data; namely, `id`, `type`, `created_time`, `likes_count`, `comments_count`, and `shares_count`. The latter three fields record the total number of likes, comments, and shares that each post recieved on Facebook during the 2015 election campaign. 

This data set will be useful to researchers interested in gaging how well a candidate's campaign performed on Facebook. For example, the data demonstrates the popularity of each candidates' online campaign based on overall engagement (i.e., number of likes, shares, and/or comments recieved from Facebook users over time).

### **2. The Campaign Messages Dataset**

The second data set includes party leaders’ **text-based Facebook posts** (n = 1,530). The data queried in this dataset consists of many of the same variables found in the Facebook Pages Dataset; including, `created_time`, `from_id`, and `id`. More importantly, it contains a field called `message`, which records UTF-8 encoded text data on every campaign message published to Facebook. Posts that did not contain any text data (after preprocessing) were removed from this dataset.

This data set will be useful to researchers interested in studying campaign messaging or those wishing to conduct a text analysis on these data.

### **3. The Facebook Users Dataset**

The final data set is a collection of Facebook user responses to campaign messages from candidates published to Facebook during the election. Data consist of comments published to Facebook between August 4th and October 19th, 2015. The data set contains many of the same fields as the two previous data sets. The `message` column returns the text-based comments that Facebook users published in response to candidates’ campaign messages during the 2015 election campaign.

This data set will be of interest to researchers looking to study campaign effects online.

---
## Disclaimer: 

If you use these data I make no warranties regarding the accuracy of this information and disclaim any liability for damages resulting from using this repository. 

While all the data contained in this repository are public, I have taken additional efforts to further anonymize users out of respect for their privacy. However, if you find any information that you believe to be sensitive, please contact me.

---
