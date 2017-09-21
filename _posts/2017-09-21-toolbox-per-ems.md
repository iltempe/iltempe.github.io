---
layout: post
title:  "Una toolbox per il sistema di Emergenze di Copernicus (EMS)"
date:   2017-09-20 00:00:00
categories: blog
tags:
  - opensource
  - civic hacking
  - emergenze
image: /assets/article_images/2017-09-21-toolbox-per-ems/sfondo.jpg
---

Dopo avere creato [questa mappa](https://iltempe.github.io/blog/2017/09/14/alluvione-di-livorno.html) ed aver usato i dati satellitari del servizio [EMS di Copernicus](http://emergency.copernicus.eu/mapping/) è emersa l'esigenza di avere qualche strumento software in più che consenta e faciliti l'uso di questi dati anche per progetti più complessi.

L'idea di base è stata quella di creare un [repository su Github](https://github.com/emergenzeHack/ems_toolkit) che possa contenere nel tempo un set di script utili a chi vorrà usare i dati satellitari durante le emergenze automatizzando operazioni che in alternativa si dovrebbero fare manualmente.

Come si può vedere da [questa pagina relativa all'alluvione di Livorno](http://emergency.copernicus.eu/mapping/list-of-components/EMSR238) i dati di Copernicus EMS sono associati ad uno specifico tag che identifica l'emergenza in modo univoco.

![il tag dell'emergenza](/assets/article_images/2017-09-21-toolbox-per-ems/1.png)

Nella pagina dell'emergenza si possono visualizzare quali siano le aree geografiche in cui è suddivisa la zona interessata dall'emergenza. Queste sono le unità minime di cui si può avere accesso ai dati. In particolare per ogni zona si può avere accesso alle immagini satellitari in vari formati e ai dataset vettoriali (questi file sono i veri e propri dataset elaborati da EMS e sono denominati "Vector package").

![i vector package di un'emergenza](/assets/article_images/2017-09-21-toolbox-per-ems/2.png)

Ogni file vettoriale ZIP contenente i dati, normalmente presenta un set di file al suo interno. Dando un'occhiata si può capire facilmente di quali dati si ha bisogno.

![il tag dell'emergenza](/assets/article_images/2017-09-21-toolbox-per-ems/4.png)

In questo momento nel repo trovate quindi due script (speriamo col tempo di poterli aumentare o migliorare se ci fossero altre esigenze):
- **get_ems_zips**: per effettuare il download di tutti i file vettoriali (ZIP) presenti in una pagina di una specifica emergenza (identificata con un tag del tipo EMSRXXX). Si può usare questo script anche per fare il download di tutti i dataset di più emergenze (basterà configurare lo script con più tag, così [EMSRXXX, EMSRYYY...])
- **merge_ems_zips**: per effettuare un'operazione di merge di un set di Vector package relativi a più zone della stessa emergenza in modo da "fonderli assieme" e visualizzarli complessivamente come livelli di un'emergenza. In questo script oltre ai tag dell'emergenza vanno indicati anche i dati di interesse di cui si vuole fare il merge (tra quelli contenuti nel file .ZIP stesso)

La configurazione degli script si effettua nelle prime righe rispettivamente editando queste variabili:

<script src="https://gist.github.com/iltempe/cf0972c32876736a887180096c2eda93.js"></script>

Il repository è ovviamente aperto a ricevere issue e pull request per essere migliorato. che aspettate?

**CREDITS**: L'[ems toolkit](https://github.com/emergenzeHack/ems_toolkit) è un progetto che cerca di generalizzare un nobilissimo intento che alcuni attivisti del progetto [terremotocentroitalia.info](http://www.terremotocentroitalia.info) hanno realizzato durante i terremoti del 2016 in Italia. Un particolare grazie va ad [Andrea Borruso](https://github.com/aborruso), [Alessandro Sarretta](https://github.com/alesarrett) e [Paolo Frizzera](https://github.com/geofrizz). Il repository usato per terremoto è [questo](https://github.com/emergenzeHack/terremotocentro_geodata/tree/gh-pages/CopernicusEMS). L'[ems_toolkit](https://github.com/emergenzeHack/ems_toolkit) è rilasciato con licenza di libero riuso (MIT) e accetta pull request e issue.

