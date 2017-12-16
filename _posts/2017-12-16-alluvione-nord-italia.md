---
layout: post
title:  "L'estensione dell'alluvione del Nord Italia del Dicembre 2017"
date:   2017-12-16 00:00:00
categories: blog
tags:
  - openstreetmap
  - copernicus
  - emergenze
  - civic hacking
image: /assets/article_images/2017-12-16-alluvione-nord-italia/2.png
---

Come già fatto per l'[alluvione di Livorno](http://iltempe.github.io/blog/2017/09/14/alluvione-di-livorno.html) ho voluto esaminare l'estensione dell'[alluvione avvenuto questa settimana in Emilia Romagna](http://www.meteoweb.eu/foto/maltempo-alluvione-emilia-romagna/id/1014896/), alluvione che ha interessato un'area molto più vasta di quello che avvenne qualche settimana fa in Toscana. L'evento mette in risalto nuovamente (per la seconda volta in pochi giorni) tutta la fragilità del territorio italiano davanti ad eventi come questo. Qui non si tratta di terremoti o incendi, che nella disgrazia, hanno una loro specificità emergenziale, qui si tratta di questioni relative alla "gestione delle acque nel territorio italiano" e se è vero che più del 10% dei territori italiani sono a rischio alluvione allora forse è il caso di riflettere e lavorare in tempi di sole anzichè sempre e solo in emergenza.

Il sistema EMS di Copernicus di osservazione dati satellitari riporta il monitoraggio dell'evento [qui](http://emergency.copernicus.eu/mapping/list-of-components/EMSR260/). L'area, essendo molto vasta, è stata divisa in 10 sottomappe come si vede dalla mappa sul sito di Copernicus. I dati da esaminare e da fondere quindi in questo caso non sono pochi.

![area monitorata da Copernicus](http://cdn-h.copernicus-ems.eu/mapping/sites/default/files/thumbnails/EMSR260-AEM-1513327517-r02-v1.jpg)

Mi sono quindi avvalso dell'aiuto della [EMS Toolbox](http://iltempe.github.io/blog/2017/09/20/toolbox-per-ems.html) che per chi non ricordasse è un set di script che consente, definita un'emergenza sul sito di Copernicus, di scaricare i dati ricavati dalle osservazioni satellitari, scaricare le foto stesse ed eventualmente fondere i dati di varie zone geografiche assieme in file georiferiti unici di tipo [shape](https://it.wikipedia.org/wiki/Shapefile) così che siano visionabili in un unico progetto di un'applicazione per gestione informazioni georiferite come [QGIS](https://www.qgis.org/it/site/).

Per l'occasione ho voluto rendere la EMS Toolbox più generica aggiungedo la possibilità di configurare gli script con un file conf.csv che contiene i dati di configurazione necessari all'analisi dell'emergenza. In questo modo il codice python si può non guardare e non modificare, basta editare un file di configurazione così come sotto:

<script src="https://gist.github.com/iltempe/6e9c450cb3bb2722eb58c3c46920f698.js"></script>

dove la prima riga rappresenta l'ID di Copernicus dell'emergenza da analizzare (se sono più di una si possono aggiungere separandole con un ;), la seconda riga sono i dati che si vogliono produrre e fondere tra le varie zone dell'emergenza (nel caso in esame il layer utile è quello denominato 'observed_event_a', ma ho scaricato anche gli altri layer), la terza riga rappresenta il formato delle immagini satellitari che si vogliono scaricare e la loro risoluzione.

Compilato il conf.csv fate un run del file con un'instruzione del tipo 'python ems.py' e la "macchina" si mette in moto scaricandovi tutti i dati dell'emergenza e fondendoli assieme. Al termine dello script nella cartella EMSR260_merged troverete un file EMSR260_observed_event_a_merged.shp che contiene l'area dell'alluvione.

La mappa che ne risulta è [qui](https://iltempe.github.io/flood_dic_2017_nordita/) ed è ottenuta tramite QGIS con il layer ottenuto dallo script precedente e il plugin QGIS [qgis2leaf](https://github.com/geolicious/qgis2leaf).
I dati elaborati da Copernicus su questo evento sono tutt'ora in aggiornamento quindi si potranno aggiungere ulteriori zone a quelle evidenziate attualmente.


<div class="map-container">
    <iframe src="https://iltempe.github.io/flood_dic_2017_nordita/" height="560" width="100%" allowfullscreen="" frameborder="0">
    </iframe>
</div>