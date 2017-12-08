---
layout: post
title:  "Fare Simulazioni di Mobilità Urbana con le mappe di Openstreetmap"
date:   2017-12-08 00:00:00
categories: blog
tags:
  - data mining
  - civic hacking
  - openstreetmap
  - opendata
  - mobilità
image: /assets/article_images/2017-12-08-fare-simulazioni-di-mobilita/1.jpeg
---

Progettare come muoversi mi ha sempre affascinato. Non a caso il mio mestiere di ingegnere impiegato nel settore ferroviario mi piace molto. Il problema del movimento in città è una questione tanto elementare quanto complessa specialmente in città come la mia che hanno visto in questo secolo un cambiamento drastico in termini di aumento della popolazione e quindi dei mezzi di trasporto (non tanto quelli pubblici ma sicuramente le auto). Analizzare se un'infrastruttura stradale o anche solo una parte del sistema di strade è adeguato agli scopi della città significa provare a risolvere un cosiddetto problema "vincolato", ossia un sistema matematico all'interno del quale si ha come difficoltà principale quella di imporre un certo numero di veicoli che si muovo con un certo criterio all'interno di un certo sistema stradale che rappresenta tutte e le sole possibilità di movimento. All'interno di questo scenario (che è matematicamente definibile) può essere interessante valutare ad esempio i luoghi "congestionati" e se e come variano questi congestionamenti se si fanno modifiche alle infrastrutture. Ovvio che il problema va posto bene, cioè va modellato in modo più veritiero possibile (cosa assolutamente non semplice) ma non è questa la sede in cui vi annoierò su come matematicamente questo si può fare.

A parte quindi questo spiegone teorico introduttivo, è interessante scoprire che ci sono strumenti che ci permettono di fare questo tipo di analisi anche in casa con un computer, una connessione internet un po' di voglia di programmare e poco altro.

Ho scoperto infatti l'esistenza del simulatore [SUMO](http://sumo.dlr.de/wiki/Simulation_of_Urban_MObility_-_Wiki) , un software opensource che consente di disegnare appunto scenari di viabilità urbani visualizzando cosa accade quando dei veicoli si muovono in certe infrastrutture. L'applicazione ha un suo wiki molto completo che vi invito a visitare, la si può installare su Windows, su Linux o su Mac (io ho un Mac e per farlo ho seguito quanto scritto nel wiki e ho creato [questo script](https://github.com/iltempe/osmosi/blob/master/sumo/install_sumo.sh)).

![l'interfaccia di SUMO](https://raw.githubusercontent.com/iltempe/osmosi/master/sumo/galciana/Schermata%202017-12-07%20alle%2022.38.03.png)

Oltre ad un utilizzo manuale (che non sottovaluterei perchè consente di disegnare strade e modellare quindi una città vera e propria) l'aspetto secondo me più interessante della piattaforma è quello del suo uso in modo programmatico tramite script che (partendo da dati) generano i file per poter effettivamente visualizzare la simulazione. In particolare mi interessava valutare se e come dai dati aperti di [Openstreetmap](https://www.openstreetmap.org) si potesse creare una simulazione di traffico, vista la mole considerevole di informazioni che Openstreetmap già ha sulle strade, piste ciclabili, vie secondarie etc…ed effettivamente la community di SUMO a questo ha pensato mettendo in piedi un meccanismo niente male che consente di convertire dati Openstreetmap in dati per simulare scenari.

Sumo, semplificando molto, necessita come input di due file: uno contenente i dati sulle strade percorribili (.net.xml) ed uno contenente i dati sul tipo di traffico che si vuol far muovere su quella rete stradale (.rou.xml).

![possibili usi di SUMO](https://github.com/iltempe/osmosi/blob/master/sumo/galciana/Image008.gif?raw=true)

Il metodo che vado ad illustrarvi è sintetizzato in questo script bash che ho creato, studiando lo strumento ed il suo wiki, per visualizzare qualche simulazione sulla  frazione di Prato nella quale abito (Galciana) per vedere quali fossero i punti "caldi" del mio paese in termini di traffico (nel mio caso ho considerato semplicemente autoveicoli). SUMO ha già un set di tool e script per facilitare l'integrazione con i formati dati di Openstreetmap.

<script src="https://gist.github.com/iltempe/a549dd70193f92bc3a22f64bf6cd4d75.js"></script>

![Galciana su OpenStreetMap](/assets/article_images/2017-12-08-fare-simulazioni-di-mobilita/map.png)

In sintesi quello che fa lo script è questo (nei commenti allo script trovate alcuni link di riferimento per capire ogni comando cosa è e quali varianti può avere):

- Scaricare i dati da OpenStreetMap in formato .osm dell'area di vostro interesse. E' possibile farlo direttamente da OpenStreetMap.org usando la funzione di esportazione o con qualche script automatico (io ho fatto manualmente)
- Generare dai dati Openstreetmap il file contenente la rete delle strade compatibile con il formato di SUMO
- Aggiungere eventuali informazioni addizionali da visuazzare durante la simulazione (informazioni relative al paesaggio)
- Creare il file dei veicoli e delle loro rotte.
- Lanciare la simulazione tramite un file di configurazione

Sotto un esempio di quello che viene fuori, i dati di partenza delle mappe sono concessi da [Openstreetmap](www.openstreetmap.org). Il repository su cui ho fatto questo esperimento è al solito su un mio [repo Github](https://github.com/iltempe/osmosi).

![](https://github.com/iltempe/osmosi/blob/master/sumo/galciana/dic-07-2017%2022-32-14.gif?raw=true)
![](https://github.com/iltempe/osmosi/blob/master/sumo/galciana/dic-07-2017%2021-45-04.gif?raw=true)



