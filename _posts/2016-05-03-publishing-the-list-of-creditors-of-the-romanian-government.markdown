---
title: Publishing the list of creditors of the Romanian government
layout: post
---

# Day 1

Today ANAF, the Romanian IRS, is going to publish the list of the creditors who have debt more than 1.5k lei to the [budgets](http://www.digi24.ro/Stiri/Digi24/Economie/Stiri/LISTA+RUSINII+DATORNICI+ANAF+PUBLICATA). The information will appear on [data.gov.ro](https://data.gov.ro/dataset/datoriile-catre-bugetul-de-stat) and I will have to [scale](https://github.com/govro/datagovro/issues/43) and cache parts of the website, so it keeps up with the whole traffic.

07:30 - I arrive in an Uber at the office. Nice driver, we talked about the sharing economy and how will ratings affect drivers and customers.

08:41 - This has been getting [lots of press coverage](https://twitter.com/search?f=tweets&vertical=default&q=lista%20datornicilor&src=typd) early in the morning. We are still waiting for the ANAF president to sign the release of the data.

09:40 - We are still waiting for the files from ANAF. I've made some updates to the nginx config. By default, it caches a file after it first served it. However, since we will be serving big PDFs, I've made it cache it in chunks.

11:00 - I've learnt that there is a meeting where they are discussing the status of the things now. I've been tweaking the Apache2 [mod_cache](http://httpd.apache.org/docs/2.4/mod/mod_cache.html) settings. I tried doing a `MMapFile` to have stuff directly in RAM, but I found out it's better to trust the operating system. It knows when to raise the files in memory.

11:27 - Because news always comes from TV, [we've found out](http://www.digi24.ro/Stiri/Digi24/Economie/Stiri/LISTA+DATORII+ANAF+AMANATA) that they are postponing showing the lists for people. We still don't have a final decision for companies.

15:23 - I have received the [files](https://data.gov.ro/dataset/datoriile-catre-bugetul-de-stat). However, they are only a small part of the entire dataset that should have been released. I was expecting for something around ~300MB, but these are only ~2MB so any server can keep up with them. Maybe in the next few days there will be some true scaling problems.

15:40 - Got 300 users and we have 30% load

15:50 - Now 500 users and 70% load. Activating Redis.

16:11 - 600 users in the last 60 seconds and 25% load. Caching is great. And still not using our CDN. Oh, and we are doing 40MB/s on the network.

17:17 - 1.200 uniques in the last minute, with a 60% load. The naive implementation of Redis was not dumping any keys and it was slowly eating my whole RAM. I've activated expiring keys after I flushed the whole database and now everything looks normal.

17:48 - Well, I tried to set [some nifty](http://redis.io/topics/lru-cache) things in Redis. However, the load went in 500%. I reverted back after some 504 errors. Just to sleep well, I've set [this option](https://github.com/ckan/ckan/blob/c3b1a37a3ecf8703035cf35235b6e6e5d2ebea39/ckan/config/middleware.py#L483) to `True`. It will make absolutely all the pages cachable (_nifty hack_) and won't update them afterwards. This is will stop updates on the websites but who needs modifying something in the night.

19:59 - Left the building to eat. Arrived home, however the website loads slowly. Freaking memory leaks. The perks of working for the government is no remote SSH access. So, I'm going back to Victoria's Palace.

22:29 - I've arrived home. I don't know really what was the culprit and did not have the patience to investigate. I have a cron set every hour that restarts the Apache2, Redis and empties the Redis cache. Never though I will be hacking at the office at this time.

# Day 2

07:30 - Woke up to update the CSVs because a column in them was wrong. I hate mornings like these.
