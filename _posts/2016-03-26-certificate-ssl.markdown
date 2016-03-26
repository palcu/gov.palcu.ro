---
layout: post
title: "Certificate SSL"
date: "Sat Mar 26 16:25:35 +0200 2016"
---

Datorită unor probleme cu firewall-ul intern, am fost nevoiți să [migrăm](https://github.com/govro/datagovro/pull/24) întreg website-ul de pe `HTTP` pe `HTTPS`. Pentru o perioadă scurtă de timp cât nu am avut un certificat actualizat la zi, nu s-au putut face cereri de tip `POST`. Îmi cer scuze pentru această problemă. Apoi, a trebuit să [migrăm](https://github.com/govro/datagovro/issues/27) toate firele de conversație de pe Disqus.

În acest moment, toate cererile `HTTP` sunt redirectate către versiunea securizată.
