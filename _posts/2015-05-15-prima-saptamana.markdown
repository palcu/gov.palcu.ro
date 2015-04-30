---
layout: post
title:  "Prima Săptămână"
date:   2015-04-15 20:07:16
---

Noi rulăm o versiune de [CKAN](http://ckan.org/), aplicația scrisă în Python care _alimentează_ website-ul data.gov.ro destul de învechită (2.0). Primul lucru pe care va trebui să îl facem este să updatăm website-ul la 2.3. Problema este că nu putem chiar să rulăm update-urile peste fără a avea un backup la tot ce e acum ca să facem rollback în caz că se strică. Colegul meu Seluan încearcă să facă o imagine a servărului ca să lucrăm pe aia. Eu am preluat și modificat un script de Ansible care să ridice un Vagrant, cu CKAN instalat din sursă. Voi scoate tot codul custom din instalarea curentă de CKAN, voi face o temă care să se suprapună peste codul nemodificat și vom face update la cod.
