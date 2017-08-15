---
layout: post
title:  "Generare Mappe di Dati in Jekyll"
date:   2017-08-15 10:34:25
categories: blog
tags:
  - opendata
  - web design
  - jekyll
image: /assets/article_images/2017-08-15-generare-mappe-in-jekyll/1.jpeg
---

In [questo post](https://iltempe.github.io/blog/2017/08/05/generare-siti-da-dataset.html) abbiamo visto come generare contenuti web a partire dai dati all'interno dell'ambiente [Jekyll](https://jekyllrb.com/).

E' piuttosto semplice, combinando questa funzionalità con le caratteristiche del plugin javascript [Leaflet](http://leafletjs.com/), usare i dati dentro Jekyll per mapparli. Sicuramente ci sono molti altri ambienti che consentono di mappare dei punti in un file di dati, ma il fatto di poterlo fare dentro Jekyll consente almeno due vantaggi ossia la customizzazione della mappa in modo piuttosto rapido (anche se si deve durare un po' di fatica con qualche linea di codice in più) e soprattutto il riuso di quanto fatto per ulteriori mappe. Andiamo ad un esempio.

Il caso di uso è : devo creare una mappa dei musei della Regione Toscana. Come fare?

- Ho prelevato il dataset dei musei presente sul portale [OpenToscana](http://open.toscana.it/), il CSV trovate [qui](http://mappe.regione.toscana.it/db-webgis/musei/example_postgis.jsp?format=csv&_ga=2.41993573.1701934011.1502803639-2104128018.1501614393).
- Archiviate questo dataset nella folder _data del vostro sito jekyll
- Create un file con estensione html (io l'ho chiamato musei_map.html) che contenga il seguente codice:

<script src="https://gist.github.com/iltempe/36af83c43a7c74d62b0273af0ff3dc79.js"></script>

- Come è fatto questo file? Ho cercato di commentare abbastanza il codice, in sostanza è un file html che fa le seguenti operazioni in sequenza:
  - Importa le librerie e gli stili di Leaflet
  - Definisce nella pagina una sezione HTML denominata "map"
  - Tramite uno script definisce lo stile dei Marker su mappa, crea la lista dei marker dai dati jekyll
  - Imposta il formato dei POPup su mappa
  - Mostra il livello appena creato
- Salvate il file HTML creato nella folder `_includes` di jekyll, in modo da renderlo un modulo riusabile
- Importate la vostra mappa in qualunque post o pagina con l'istruzione "% include musei_map.html %"

Fatto, il risultato si vede sotto. Ora potete divertirvi a customizzare di più il mio codice, aggiungendo link, livelli, dati etc.

{% include musei_map.html %}
