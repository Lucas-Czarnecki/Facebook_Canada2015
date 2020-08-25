# <span style ="color: #3b5998">  Raw Facebook Data </span>

## 1. Overview

Data were queried from Facebook using R, a statistical program and language, through an established connection to Facebook’s publicly accessible Graph API (v.2.0). Data were queried using the [`Rfacebook`](https://github.com/pablobarbera/Rfacebook) package, which provided various functions for accessing Facebook's public API.

Data were queried from three public Facebook pages belonging to Stephen
Harper, Justin Trudeau, and Tom Mulcair’s candidacies. **This project's research design ensures that only public posts were scraped - data from Facebook users' personal profiles was not collected.**

> Note: As a result of Facebook terminating access to its public Graph API, the `Rfacebook` package is no longer being maintained. The methods below, at this time, cannot be replicated. 

---

## 2. Data Collection 

The functions used to query data from Facebook are documented in
[Rfacebook](https://cran.r-project.org/web/packages/Rfacebook/Rfacebook.pdf). The methods are summarized below with the hope that Facebook policies will change again; making data available to researchers.

Data collection was carried out according to a three-step procedure:
1. <b>Step One:</b> Identify page IDs from target Facebook pages. 
2. <b>Step Two:</b> Use these page IDs to query additional data from Facebook including post IDs to further data collection.
3. <b>Step Three:</b> Collect data connected to post IDs.

The following summarizes the `Rfacebook` functions used and their purpose: 
* `searchPage`: retrieved the page IDs for Stephen Harper, Justin Trudeau, and Tom Mulcair’s Facebook pages. These were also manually verified.
* `getPage`: queried data from each candidate’s Facebook page was returned according to parameters `since` and `until`, which specified the duration of the 2015 Canadian general election. The returned data included `id` which identified every post published to Facebook throughout the campaign. 
* `getPost`: Was used to retrieve a large list of party leaders' messages and Facebook users' responses to those messages based on the posts documented in `id`. Retrieved data included three components `post`, `likes`, and `comments`. The former included the text-based messages from party leaders' posts, while the latter two documented Facebook users' responses to these posts either as text-based replies or in the form of Facebook likes. 

---

## 3. Organization

The raw data are organized into four folders. The first is <br>"Facebook Pages"</br> which contains the raw structured data obtained using `Rfacebook's` `getPage` function. The remaining three folders pertain to each candidate's Facebook page; namely, Harper, Trudeau, and Mulcair. Each folder contains the raw data queried from Facebook using the `getPost` function. For convenience, the data in candidates' folders are presented as .rds files (for R users) and as csvs (for non-R users).

---

## 4. Privacy Note

Note that the data in the candidate's folders have been modified to preserve Facebook users' privacy. To this end, `from_id` and `from_name` have been redacted for Facebook users. 

IDs contained in `from_id` have been replace with `user_id` (an anonymized id that hashed the values found in `from_id`), while `from_name` has been removed entirely. The only exception is for party leaders for whom anonymity was not a concern. In their case both `from_id` and `from_name` are left unmodified.

While all the data contained in this repository are public, should you find any information that you believe to be sensitive, please contact me.