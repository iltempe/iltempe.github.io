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
Dal 9 Settembre scorso infatti l'italia è stata soggetta a condizioni meteo avverse. A mio avviso niente di eccezionale. Se non che si trattava dei primi temporali dopo un'estate molto calda. Ci si doveva aspettare? io non lo so. Penso che in ogni caso non si possa continuare a morire (come avvenuto appunto a Livorno) solo perchè piove e che prima o poi qualcuno dovrà rispondere di tutto questo in prima persona, ma questo è un tema che ci porterebbe a discutere per mesi.

Detto questo, dell'[alluvione di Livorno](http://www.ilpost.it/2017/09/11/ci-sono-ancora-due-dispersi-per-le-alluvioni-a-livorno/) ci restano alcune preziose informazioni che rilascia il servizio di Copernicus [Emergency Management Service](http://emergency.copernicus.eu/mapping/) ormai a noi molto caro. Trattasi di un servizio del sistema di osservazione satellitare [Copernicus](http://emergency.copernicus.eu/mapping/ems/what-copernicus) con focus specifico sulle emergenze del pianeta terra. Nel caso specifico qualche giorno fa EMS ha rilasciato su [questa pagina](http://emergency.copernicus.eu/mapping/list-of-components/EMSR238) tutti i dati elaborati sull'alluvione registrato in Toscana.

L'attività di registrazione delle foto satellitari è descritta nel report di Copernicus che indica in quante aree è stata suddivisa l'area monitorata. Nel caso di livorno sono 4 aree come si vede in figura.

![report dell'attività di EMS](/assets/article_images/2017-09-15-alluvione-di-livorno/ems.jpg)

Una delle analisi che si possono fare tramite i dati è ad esempio vedere su mappa quanto sia stata estesa l'area allagata. Dalla [mappa che ho realizzato](https://iltempe.github.io/livorno_flood/index#12/43.6289/10.3605) si può valutare tutto questo in dettaglio.

<div class="map-container">
    <iframe src="https://iltempe.github.io/livorno_flood/index#12/43.6289/10.3605" height="560" width="100%" allowfullscreen="" frameborder="0">
    </iframe>
</div>

Due note su come fare per usare i dati del servizio EMS in modo da creare una visualizzazione come sopra (non è un tutorial, sono semplici indicazioni, prendete questo spunto per documentarvi sul tema ed eventualmente approfondire):
- Recatevi sulla pagina del servizio EMS Copernicus. Ogni pagina dei dati ha un indice alfa-numerico. Nel caso di Livorno è [EMSR238](http://emergency.copernicus.eu/mapping/list-of-components/EMSR238). Nella pagina troverete una serie di indicazioni sull'emergenza in corso e una sezione con i dati divisi per zone su cui sono stati fatti i rilievi;
- Tra i dati, se siete interessati a visionare le foto satellitari senza "smanettarci" troppo ma semplicemente per effettuare le vostre analisi, Copernicus ve le fornisce in vari formati (JPG, TIFF, PDF) divise per le aree su cui sono stati fatti i rilievi;
- Se invece volete realizzare una vostra applicazione sul web, come la mia mappa sopra, che faccia quindi uso dei dati e non foto, dovrete effettuare il download dei file .zip con tutti i dati in formato vettoriale che vi interessa visionare (è denominato "Vector package"). Questi dati sono quelli che Copernicus EMS è riuscito ad elaborare dalle sue foto. Tra questi, nel mio caso, esiste un set di dati relativi alle zone allagate. Scaricando il file .zip si nota che al suo interno queste informazione sono chiamate "crisis_information_poly". Ne dovreste trovare uno per area monitorata.
- Se avete scaricato più di uno zip, adesso dovete ricomporre i dati che Copernicus spesso fornisce "divisi per aree confinanti". Archiviate quindi tutti i file zip in una stessa folder e fate girare uno script python [come questo](https://github.com/iltempe/livorno_flood/blob/master/data/merge.py) che vi consentirà di unire i livelli in un unico livello dai vari file ZIP di dati (ognuno relativo ad una rilevazione satellitare) che conterrà l'informazione di vostro interesse. Il vostro livello complessivo sarà creato in formato .shp con il quale potrete realizzare applicaizoni come quella sopra. Nello script prima di eseguirlo ci sono alcune folder e stringhe da configurare, niente di drammatico. Ce la farete.
- Potete aprire i file .shp con software di analisi dati geografici come [QGIS](https://www.qgis.org/it/site/) elaborarli, salvarli in altri formati, esportali come mappa web usando ad esempio [questo plugin](https://github.com/mayotunde/qgis2leaflet).

Tutti i dati relativi all'alluvione di Livorno sono stati da me uniti in livelli complessivi e li trovate [qui](https://github.com/iltempe/livorno_flood/tree/master/data/EMSR238/out). I sorgenti della mappa sopra sono archiviati [qui](https://github.com/iltempe/livorno_flood). Il geojson del livello relativo agli allagamenti può essere scaricato [qui](https://raw.githubusercontent.com/iltempe/livorno_flood/master/data/crisis_information_poly_merged.geojson).
Alcuni doverosi ringraziamenti : un grazie alla Comunità [Opendata Sicilia](http://opendatasicilia.it/) da cui apprendo ogni tanto cosa si può fare con i dati di utile per gli altri. Un grazie a [Paolo Frizzera](https://github.com/geofrizz) per lo script python, grazie [Giovan Battista Vitrano](https://github.com/gbvitrano) per aver creato [questa mappa](https://siciliahub.github.io/mappe/EMSR213/incendi_sicilia/naso.html#12/38.0915/14.8824) che è stata di ispirazione per me, grazie ad [Andrea Borruso](https://github.com/aborruso) per le sue utilissime pillole GIS che ogni tanto mi regala.

