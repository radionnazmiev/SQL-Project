#### Question 1:

Are there any duplicate member ID entries in the dataset?

* SQL query:

```
SELECT "fullVisitorId"
      , COUNT("fullVisitorId") AS entries 
FROM all_sessions 
GROUP BY "fullVisitorId" 
HAVING COUNT("fullVisitorId") > 1 
ORDER BY entries;
```
*  Answer: 

    794 duplicate member ID entries in the dataset.

#### Question 2:

What is the average time spent by visitors on each web page?

* SQL query:

```
SELECT SUM("timeOnSite") / SUM("pageviews") AS avg_time_on_each_page 
FROM all_sessions;
```

* Answer: 

    The average time spent by visitors on each web page is 38 seconds.

#### Question 3:

What is the total number of unique visitors by referring sites?

* SQL query:

```
SELECT COUNT(DISTINCT visitid) 
FROM all_sessions 
WHERE channelGrouping = 'Referral';

```
* Answer: 

    The total number of unique visitors referred to the site is 2488
