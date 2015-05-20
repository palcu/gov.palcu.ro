---
layout: post
title:  "Migrare terminată"
date:   2015-05-20 17:25:16
---

[Website-ul](http://data.gov.ro) a fost migrat fără a pierde date și fără downtime la versiunea 2.3 a CKAN. Am activat și pluginul `datapusher` care actualizează automat în `DataStore` (locul de unde API-ul preia date) atunci când un set de date este urcat în `FileStore` (locul unde se urcă propriu-zis fișierele). Următorii pași sunt:

* contribuția în upstream a fișierului de limbă care a fost actualizat
* publicarea pe [Github](http://github.com/govro) a repo-ului cu mediul de development care se provizionează prin Vagrant și Puppet
* configurarea unei alte mașini prin care să putem monitoriza producția și stagingul (load, loguri, etc.)
* procedura de backup și restore pentru date, fără a mai crea o replică a hard-diskului
* provizionarea stagingului și a producției prin scripturile de Ansible
* integrarea comentariilor printr-un plugin intern
* replicarea setup-ului [data.gov.uk](http://data.gov.uk/), unde ei au un Drupal în față ca și CMS, și țin CKAN pentru vizualizarea seturilor de date.
