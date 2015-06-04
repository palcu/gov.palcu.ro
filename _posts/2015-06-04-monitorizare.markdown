---
layout: post
title:  "Monitorizare"
date:   2015-06-04 16:21:30
---

Săptămâna asta m-am ocupat de o monitorizare mai bună a mașinilor de staging și producție. Am setat un [ping extern](http://uptime.statuscake.com/?TestID=8pM4VcMsBu) de uptime care verifică dacă website-ul a fost picat. Apoi am instalat [monit](https://mmonit.com/monit/) pe servăre și le-am configurat astfel încât o parte din alerte să dea în canalul de IRC de pe [Slack](https://govro.slack.com/messages), iar o altă parte direct în email. În final, voi face și configurarea credențialelor prin [ansible-vault](http://docs.ansible.com/playbooks_vault.html).
