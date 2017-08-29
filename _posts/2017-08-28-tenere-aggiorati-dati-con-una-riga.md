---
layout: post
title:  "Aggiornare un gruppo di dataset con uno script di una riga"
date:   2017-08-28 09:00:00
categories: blog
tags:
  - opendata
  - opensource
  - civic hacking
  - tutorial
image: /assets/article_images/2017-08-28-tenere-aggiorati-dati-con-una-riga/1.jpeg
---

Esigenza: ho un set di dati archiviati da qualche parte in remoto che si aggiornano spesso (magari!) e ho necessità di copiarli su qualche cartella in locale o altro server per usarli per una mia applicazione. Come si fa? Un modo molto semplice è il seguente:

- Creare un file di testo fatto chiamato **remote_datasets.txt**. Per solo esempio io ho scelto di fare l'operazione con tre dataset di Openstreetmap (prelevati con le query di [Overpass-Turbo](https://overpass-turbo.eu/)). Dove ho inserito tre terne composte ognuna da (sono 9 righe, vanno lette a 3 a 3): il link ai dati, il simbolo -o e il nome che voglio dare il locale al file che intendo aggiornare.

- Creare un file **update_datasets.sh** in cui scriverete una sola riga di codice. Esguite questo script nella stessa folder di remote_datasets.txt con il comando "bash update_datasets.sh". Nella cartella avrete i file con i dati aggiornati.

<script src="https://gist.github.com/iltempe/8add8bb847d0d8488f2c6b05b64318cf.js"></script>
