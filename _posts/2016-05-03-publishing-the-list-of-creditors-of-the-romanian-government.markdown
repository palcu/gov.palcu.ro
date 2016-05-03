---
title: Publishing the list of creditors of the Romanian government
layout: post
---

Today ANAF, the Romanian IRS, is going to publish the list of the creditors who have debt more than 1.5k lei to the [budgets](http://www.digi24.ro/Stiri/Digi24/Economie/Stiri/LISTA+RUSINII+DATORNICI+ANAF+PUBLICATA). The information will appear on [data.gov.ro](https://data.gov.ro/dataset/datoriile-catre-bugetul-de-stat) and I will have to [scale](https://github.com/govro/datagovro/issues/43) and cache parts of the website, so it keeps up with the whole traffic.

**Live Blogging**

07:30am - I arrive in an Uber at the office. Nice driver, we talked about the sharing economy and how will ratings affect drivers and customers.

08:41am - This has been getting [lots of press coverage](https://twitter.com/search?f=tweets&vertical=default&q=lista%20datornicilor&src=typd) early in the morning. We are still waiting for the ANAF president to sign the release of the data.

09:40am - We are still waiting for the files from ANAF. I've made some updates to the nginx config. By default, it caches a file after it first served it. However, since we will be serving big PDFs, I've made it cache it in chunks.

11:00am - I've learnt that there is a meeting where they are discussing the status of the things now. I've been tweaking the Apache2 [mod_cache](http://httpd.apache.org/docs/2.4/mod/mod_cache.html) settings. I tried doing a `MMapFile` to have stuff directly in RAM, but I found out it's better to trust the operating system. It knows when to raise the files in memory.

11:27am - Because news always comes from TV, [we've found out](http://www.digi24.ro/Stiri/Digi24/Economie/Stiri/LISTA+DATORII+ANAF+AMANATA) that they are postponing showing the lists for people. We still don't have a final decision for companies.
