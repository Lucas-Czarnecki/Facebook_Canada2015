# Facebook Datasets

## 1. The Facebook Pages Dataset
This data set contains strictly structured data on every post published to the three verified public Facebook pages in this repository. Data range from August 4th until October 19th, 2015, consisting of every post published to Facebook during this time (N = 1,711).

This data set contains six fields of structured data; namely, id, type, created_time, likes_count, comments_count, and shares_count. The latter three fields record the total number of likes, comments, and shares that each post recieved on Facebook during the 2015 election campaign.

This data set will be useful to researchers interested in gaging how well a candidate's campaign performed on Facebook. For example, the data demonstrates the popularity of each candidates' online campaign based on overall engagement (i.e., number of likes, shares, and/or comments recieved from Facebook users over time).

---

## 2. The Campaign Messages Dataset
The second data set includes party leaders’ text-based Facebook posts (n = 1,530). The data queried in this dataset consists of many of the same variables found in the Facebook Pages Dataset; including, created_time, from_id, and id. More importantly, it contains a field called message, which records UTF-8 encoded text data on every campaign message published to Facebook. Posts that did not contain any text data (after preprocessing) were removed from this dataset.

This data set will be useful to researchers interested in studying campaign messaging or those wishing to conduct a text analysis on these data.

---

## 3. The Facebook Users Dataset
The final data set is a collection of Facebook user responses to campaign messages from candidates published to Facebook during the election. Data consist of comments published to Facebook between August 4th and October 19th, 2015. The data set contains many of the same fields as the two previous data sets. The message column returns the text-based comments that Facebook users published in response to candidates’ campaign messages during the 2015 election campaign.

This data set will be of interest to researchers looking to study campaign effects online.