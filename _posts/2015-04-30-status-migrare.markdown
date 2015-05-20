---
layout: post
title:  "Status migrare data.gov.ro"
date:   2015-04-30 16:25:16
---

Ieri am încercat să upgradăm data.gov.ro la versiunea 2.3 a CKAN-ului, dar am făcut revert după o oră. Principalele două motive pentru care am făcut asta:

* data.gov.ro conține o versiune custom a fișierului de limbă, care e valabil pentru versiunea 2.0 și care a rămas în urmă. Deoarece unele stringuri care s-au tradus nu au fost puse și în proiectul original CKAN, am încercat să îmbin fișierul nou `.po` cu cel vechi. Din nefericire, câteva stringuri au fost potrivite prost, iar unele template-uri crăpau când încercai să accesezi pagina unde erau folosite. Am modificat de mână manual direct în cod în două locuri, dar când am dat drumul în producție la noul website, au apărut și alte erori în locuri unde nu testasem.

* în urma upgrade-ului, nu s-au mai putut descărca fișierele resursă din `FileStore`. Pentru că am crezut că trebuie urmat și acest [pas](http://docs.ckan.org/en/ckan-2.2/filestore.html#filestore-21-to-22-migration), am rulat comanda `paster db migrate-filestore`. Dar, aceasta mai mult a stricat câteva seturi de date existente. Problema am descoperit că era faptul că noi în procedurile noastre de upgrade, am scris că trebuia să înlocuim variabila `ofs.storage_dir` în `ckan.storage_path` datorită unui warning. Dar, apoi am [citit](http://docs.ckan.org/en/ckan-2.3/maintaining/configuration.html#ofs-storage-dir) în documentație că defapt ambele variabile trebuie păstrate, chiar dacă prima este `deprecated`. Voi deschide un issue în repo-ul CKAN în care le voi expune problema pe care am avut-o.

Pentru a evita problemele de mai sus, am creat o listă de lucruri pentru care trebuie făcut QA manual în mediul nostru de [staging](http://en.wikipedia.org/wiki/Staging_site).
