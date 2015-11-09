---
layout: post
title: "Stres test pentru legislatie.just.ro"
date: "Mon Nov 09 16:04:28 +0200 2015"
---

Pe 23 octombrie, ROSEdu a organizat [Hacktoberfest](https://www.facebook.com/events/1031851323569615/), un hackathon destinat dezvoltării programelor libere. Unul dintre proiectele propuse de mine a fost realizarea unui test de stres folosind clientul de API pentru [legislatie.just.ro](https://github.com/govro/legislatie-just-python-soap-client). [Cristian Banu](https://github.com/cbanu96) a [adăugat](https://github.com/govro/legislatie-just-python-soap-client/pull/2) error handling și multi-threading, așa că am putut să dăm în API fără să fim limitați de bandă.

Am observat că după câteva secunde suntem automat trecuți într-un rate limit de unul-două request-uri per secundă. Dar, am reușit să descărcăm toate legile din 2015 cu succes.
