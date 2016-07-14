---
title: Publishing the list of creditors of the Romanian government
layout: post
---

# Day 1

Today ANAF, the Romanian IRS, is going to publish the list of the creditors who have debt more than 1.5k lei to the [budgets](http://www.digi24.ro/Stiri/Digi24/Economie/Stiri/LISTA+RUSINII+DATORNICI+ANAF+PUBLICATA). The information will appear on [data.gov.ro](https://data.gov.ro/dataset/datoriile-catre-bugetul-de-stat) and I will have to [scale](https://github.com/govro/datagovro/issues/43) and cache parts of the website, so it keeps up with the whole traffic.

07:30 - I arrive in an Uber at the office. Nice driver, we talked about the sharing economy and how will ratings affect drivers and customers.

08:41 - This has been getting [lots of press coverage](https://twitter.com/search?f=tweets&vertical=default&q=lista%20datornicilor&src=typd) early in the morning. We are still waiting for the ANAF president to sign the release of the data.

15:23 - I have received the [files](https://data.gov.ro/dataset/datoriile-catre-bugetul-de-stat). However, they are only a small part of the entire dataset that should have been released. I was expecting for something around ~300MB, but these are only ~2MB so any server can keep up with them. Maybe in the next few days there will be some true scaling problems.

15:40 - Got 300 users and we have 30% load

15:50 - Now 500 users and 70% load. Activating Redis.

16:11 - 600 users in the last 60 seconds and 25% load. Caching is great. And still not using our CDN. Oh, and we are doing 40MB/s on the network.

17:17 - 1.200 uniques in the last minute, with a 60% load. The naive implementation of Redis was not dumping any keys and it was slowly eating my whole RAM. I've activated expiring keys after I flushed the whole database and now everything looks normal.

17:48 - Well, I tried to set [some nifty](http://redis.io/topics/lru-cache) things in Redis. However, the load went in 500%. I reverted back after some 504 errors. Just to sleep well, I've set [this option](https://github.com/ckan/ckan/blob/c3b1a37a3ecf8703035cf35235b6e6e5d2ebea39/ckan/config/middleware.py#L483) to `True`. It will make absolutely all the pages cachable (_nifty hack_) and won't update them afterwards. This is will stop updates on the websites but who needs modifying something in the night.

19:59 - Left the building to eat. Arrived home, however the website loads slowly. Freaking memory leaks. The perks of working for the government is no remote SSH access. So, I'm going back to Victoria's Palace.

22:29 - I've arrived home. I don't know really what was the culprit and did not have the patience to investigate. I have a cron set every hour that restarts the Apache2, Redis and empties the Redis cache. Never though I will be hacking at the office at this time.

# Day 7

11:00 - The dataset is still in works.

18:00 - I am called at the office to publish the new dataset.

21:00 - Still waiting for the final go.

22:00 - The dataset is published.

23:30 - After some hours of monitoring, we've decided to go home. The best decision was to serve the 100MB PDF from the Cloudflare CDN.

# Day 8

12:00 - We've decided to take down Redis just to see how well it scales. The server is now in 180% load and the average response time is 0.8s. However, lots of people are querying it using the API.

14:40 - In the Cloudflare dashboard I see over 2TB of data served and over 50k requests to the PDF in the last 12h. Not bad for a free service. Kudos to them for building such a great product.

17:00 - Went to the office again because for some reason the 50MB CSV was not fully indexed in the database. I found out that we had 2 indexer actvated (one old and one new), disabled the old one and reindexed the full resource.

17:30 - I've disabled offloading the PDF to Cloudflare and we're now serving everything inhouse. Cloudflare served us 3.27TB and 78k requests.

![cloudflare graph](/assets/cloudflare_graph.png)
![cloudflare bandwidth](/assets/cloudflare_bandwidth.png)

# Some last numbers from the logs

Day 1

18:12 - 726,000 requests + 23,850 users
19:15 - 1,020,000 req + 34,261 users
20:18 - 1,919,301 req + 76,000 users

Day 2

17:13 - 14,319,183 req + 514,403 users
