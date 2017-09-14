---
layout: post
title:  "L'alluvione di Livorno: un caso di riuso di dati satellitari"
date:   2017-09-14 09:00:00
categories: blog
tags:
  - opendata
  - civic hacking
  - emergenze
image: /assets/article_images/2017-09-15-alluvione-di-livorno/flood.jpeg
---

In questi giorni ho avuto modo di documentarmi sull'alluvione avvenuto nella provincia di Livorno lo scorso weekend.
Dal 9 Settembre scorso infatti l'italia è stata soggetta a condizioni meteo avverse. A mio avviso niente di eccezionale. Se non che si trattava dei primi temporali dopo un'estate molto caldo. Ci si aspettava? io non lo so. Penso che in ogni caso non si possa continuare a morire (come avvenuto appunto a Livorno) solo perchè piove e che prima o poi qualcuno dovrà rispondere di tutto questo in prima persona, ma questo è un tema che i porterebbe a discutere per mesi.

Detto questo, dell'[alluvione di Livorno](http://www.ilpost.it/2017/09/11/ci-sono-ancora-due-dispersi-per-le-alluvioni-a-livorno/) ci restano alcune prezione informazione che rilascia il servizio di Copernicus [Emergency Management Service](http://emergency.copernicus.eu/mapping/) ormai a noi molto caro. Trattasi di un servizio del sistema [Copernicus](http://emergency.copernicus.eu/mapping/ems/what-copernicus) di osservazione satellitare con focus specifico sulle emergenze del pianeta terra. Nel caso specifico qualche giorno fa EMS ha rilasciato su [questa pagina](http://emergency.copernicus.eu/mapping/list-of-components/EMSR238) tutti i dati in loro possesso sull'alluvione registrato appunto in Toscana. Una delle analisi che si possono fare tramite i dati è ad esempio vedere su mappa quanto sia stata estesa l'area allagata. Dalla [mappa che ho realizzato](https://iltempe.github.io/livorno_flood/index#12/43.6289/10.3605) si può valutare tutto questo in dettaglio.

<div class="map-container">
    <iframe src="https://iltempe.github.io/livorno_flood/index#12/43.6289/10.3605" height="560" width="100%" allowfullscreen="" frameborder="0">
    </iframe>
</div>


Due note su come fare per usare i dati del servizio EMS in modo da creare una visualizzazione come sopra (non è un tutorial, sono indicazioni sulla procedura da seguire, prendete questo spunto per documentarvi sul tema ed imparare):
- Recatevi sulla pagina del servizio EMS Copernicus. Ogni pagina dei dati ha un indice alfa-numerico (nel caso di Livorno è EMSR238);
- Se siete interessati a visionare foto satellitari Copernicus ve le fornisce in vari formati (JPG, TIFF, PNG);
- Se invece volete realizzare una vostra applicazione sul web, come la mia mappa sopra, dovrete effettuare il download dei file .zip con tutti i dati in formato vettoriale che vi interessa visionare. Questi dati sono tutti i dati che Copernicus EMS è riuscito a estrarre dalle sue foto. Tra questi nel mio caso esiste un set di dati relativi alle zone allagate.
- Archiviate gli zip in una stessa folder e fate girare uno script python [come questo](https://github.com/emergenzeHack/terremotocentro_geodata/blob/gh-pages/CopernicusEMS/scripts/copernicus_EMSR.py) che vi consentirà da vari file ZIP di dati (ognuno relativo ad una rilevazione satellitare) di unire i livelli in un unico livello che conterrà l'informazione di vostro interesse. Il vostro livello complessivo sarà creato in formato .shp con il quale potrete realizzare applicaizoni come quella sopra.

Tutti i dati relativi all'alluvione di Livorno sono stati da me uniti in livelli complessivi e li trovate [qui](https://github.com/iltempe/livorno_flood/tree/master/data/EMSR238/out). I sorgenti della mappa sopra sono archiviati [qui](https://github.com/iltempe/livorno_flood). Il geojson del livello relativo agli allagamenti può essere scaricato [qui](https://raw.githubusercontent.com/iltempe/livorno_flood/master/data/crisis_information_poly_merged.geojson).
ALcuni doverosi ringraziamentig Grazie a [Paolo Frizzera](https://github.com/geofrizz) per lo script, grazie [Giovan Battista Vitrano](https://github.com/gbvitrano) per aver creato [questa mappa](https://siciliahub.github.io/mappe/EMSR213/incendi_sicilia/naso.html#12/38.0915/14.8824) di ispirazione per me, grazie ad [Andrea Borruso](https://twitter.com/gbvitrano) per le sue utilissime pillole GIS che ogni tanto mi regala.

