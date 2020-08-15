# <span style ="color: #3b5998"> **The 2015 Canadian Federal Election on Facebook** </span>

## <span style ="color: #dfe3ee"> Table of Contents: </span>
---

1. [Introduction to the Data](#<span-style-="color:-#8b9dc3">-1.-Introduction-to-the-Data-</span>)
2. [Data Collection](#<span-style-="color:-#8b9dc3">-2.-data-collection-</span>)
3. [Variables](#<span-style-="color:-#8b9dc3">-3.-variables-</span>)
4. [Data Cleaning](#<span-style-="color:-#8b9dc3">-4.-data-cleaning-</span>)
5. [How the Data are Organized](#<span-style-="color:-#8b9dc3">-5.-How-the-Data-are-Organized-</span>)
---
<br>

## <span style ="color: #8b9dc3"> 1. Introduction to the Data </span>

This repository contains Facebook user data from the 2015 Canadian general election. Data consists of federal party leaders’ campaign messages (N = 1,711) and the responses to those messages from Facebook users (n = 92,813). Data range from August 4th until October 19th, 2015; the duration of the 2015 election campaign.

The data are organized relationally such that Facebook users’ party identification, political preferences, and emotional responses to campaign messages can be identified and measured. The partisanship of Facebook users may be inferred based on the campaign content that users liked on Facebook during the campaign.

--- 
<br>

## <span style ="color: #8b9dc3"> 2. Data Collection </span>

Data were queried from Facebook using R, a statistical program and language, through an established connection to Facebook’s publicly accessible Graph API (v.2.0). Data were queried using the `Rfacebook` package, which provided various functions for accessing Facebook's public API.

Data were queried from three public Facebook pages belonging to Stephen
Harper, Justin Trudeau, and Tom Mulcair’s candidacies. Data on Facebook users' personal profiles **were not** collected. **This repository's research design ensures that only public posts were scraped.**

<br>

> Note: Facebook terminated all access to its public API in 2018. Consequently, the `Rfacebook` packages is no longer being maintained. As a result, it is impossible to reproduce the data collection used in this repository at this time. 

<br>

### Raw Data
The raw data consist of hundreds of Facebook objects contained within hundreds of lists. The data were queried according to the relational nature of these objects. Three component types were extracted to create a relational data set; namely, `posts` (i.e., Party leaders' campaign messages), `comments` (i.e., Facebook users' text-based responses to party leaders' posts), and `likes` (i.e., Facebook users' history of liking party leaders' posts). For information on how data were organized see the section **How the Data are Organized**. **Figure 1** in this section further illustrates the relationship between data sets. 

For reasons of privacy and practicallity I have uploaded the "raw" data as csv files, which have been modified to remove Facebook users' screen names and anonymize their Facebook IDs.

---
<br>

## <span style ="color: #8b9dc3"> 3. Variables </span>

Table 1 provides a brief summary of the variables scraped from Facebook's Graph API. More information pertaining to these variables can be found on `Rfacebook's` [GitHub repository](https://github.com/pablobarbera/Rfacebook) and [CRAN documentation](https://cran.r-project.org/web/packages/Rfacebook/Rfacebook.pdf). 

<br>

### Table 1. Variables from Facebook's Graph API

| Variable      | Description     |
| :---        | :---- |
| `from_id`  | <span style ="color: red"> (Redacted) </span> Contains unique numeric IDs that identify the author of every comment.  |
| `from_name`   | <span style= "color:red"> (Redacted) </span>  Contains Facebook users' screen names.  |
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

In the interest of user privacy (even though this data is public), both `from_id` and `from_name` have been removed from this repository. `From_name` has been removed entirely (except for party leaders for whom anonymity is not an issue). 

Finally,  `from_id` was used to create `user_id`; an anonymized id for Facebook users (see: Additional Variables). 


<br>

Below is a brief summary of additional variables that were created based on information obtained from Facebook's graph API.

<br>

### Table 2. Additional Variables Created Based on Facebook's Graph API

| Variable      | Description     |
| :---        | :---- |
| `user_id` | <span style = "color: green"> (Anonymized Id) </span> `user_id` was created by anonymizing the numerical ids in `from_id`. All Facebook users are, therefore, uniquely and anonymously identified. 
| `date_published`  | Records the day that the post was published to Facebook based on `created_time`. |
| `time_published` | Records the time of day that the post was published to Facebook based on `created_time`. |
| `month_published`| Records the month that the post was published to Facebook based on `created_time`. |
| `campaign_week` | Identifies in which week of the campaign each post was published to Facebook. The campaign was 11 weeks long. |
---

<br>

> Note: The 2015 election campaign was technically 11 weeks plus one day. Note then that election day was included as part of week 11 in `campaign_week`.

<br>

---
<br>

## <span style ="color: #8b9dc3"> 4. Data Cleaning </span>

The structured data in this repository (e.g., number of likes, shares, comments, etc.) are unchanged since being queried from Facebook's Graph API. The only exception is the creation of `user_id` based on `from_id` to anonymize users ids (see the section above on variables). 

Data cleaning was, however, necessary when working with text-based data contained in Facebook users and party leaders' `messages`. I applied the following preprocessing procedures to this field to facilitate statistical analysis and visualization:
* word tokenization, 
* case-folding to lower-case,
* removal of nonletter and special characters (e.g., %, /, $, #, etc.),
* regular expressions to remove URLs and emoji-related Unicode.

Multiple R packages were used to run these preprocessing tasks. You will find all these packages and operations documented in my scripts, which you can find in the folder, [R](TODO). If you prefer to preprocess the text yourself, you can find the unmodified text data in the folder, [raw](TODO). 

---
<br>

## <span style ="color: #8b9dc3"> 5. How the Data are Organized </span>

This section briefly describes how data were organized. Figure 1 serves as a visual illustration of the relationship between data sets. 

<br>

### Figure 1. The Relationships Between Datasets
![Facebook Relational Data](\images\Facebook_Relational_Data.png)
*Notes. The data pertaining to party leaders in this example are real. All information relating to Facebook users (e.g.,
from_id, from_name, message) are fictionalized.*

<br>

<br>

### **1. The Facebook Pages Dataset**

This data set contains structured data on every post published to the three verified public Facebook pages in this repository. Data range from August 4th until October 19th, 2015, consisting of every post published to Facebook during thistime (N = 1,711).

This data set contains six fields of structured data; namely, `id`, `type`, `created_time`, `likes_count`, `comments_count`, and `shares_count`. The latter three fields record the total number of likes, comments, and shares that each post accumulated on Facebook during the 2015 election campaign. See the 

<br> 

### **2. The Campaign Messages Dataset**

The second data set consists of party leaders’ text-based Facebook posts (n = 1,530). The data queried in this dataset consists of many of the same variables found in the Facebook Pages Dataset; including, `created_time`, `from_id`, and `id`. It also contains a field called `message`, which records UTF-8 encoded text data on every campaign message published to Facebook. Posts that did not contain any text data (after preprocessing) were removed from this dataset.

<br>

### **3. The Facebook Users Dataset**

The final data set is a collection of Facebook user responses to posts that candidates published on Facebook during the election. Data consist of comments published to Facebook between August 4th and October 19th, 2015. The data set contains many of the same fields of structured data as the two previous data sets. The `message` column returns the text-based comments that Facebook users published in response to candidates’ campaign messages during the 2015 election campaign.

<br>

---
## <span style ="color: #8b9dc3"> Disclaimer: </span>

If you use these data I make no warranties regarding the accuracy of this information and disclaim any liability for damages resulting from using this repository. 

While all the data contained in this repository are public, I have taken additional efforts to further anonymize users out of respect for their privacy. However, ff you find any information that you believe to be sensitive, please contact me; I will redact such information at my discretion.

---
