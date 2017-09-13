---
layout: post
title:  "Comune di Prato, apri il tuo geoserver ai cittadini pratesi"
date:   2017-09-13 09:00:00
categories: blog
tags:
  - pa
  - opendata
image: /assets/article_images/2017-09-13-comune-apri-geoserver/baby-tears-small-child-sad-47090.jpeg
---

In questi giorni mi sono documentato su quelli che sono i sistemi di informazione geografica (detti [GIS](https://it.wikipedia.org/wiki/Geographic_information_system)) in particolare su quanto utilizzato dal mio [Comune di Prato](http://www.comune.prato.it/) per la gestione delle informazioni "georiferite" e su ciò che è a disposizione di noi cittadini un po’ curiosi che tanto amiamo i dati. Iniziamo col dire che per me motivo di soddisfazione che il mio comune abbia un geoportale (così si chiamano i portali dove sono memorizzate le informazioni di tipo geografico) perché significa che (negli anni) il comune si è dotato di strumenti e processi per digitalizzare dati utili. Potete verificare l'esistenza del geoportale tramite l’interfaccia web del server [qui](http://geoserver.comune.prato.it/geoserver/web/). 

![il geoportale di Prato](/assets/article_images/2017-09-13-comune-apri-geoserver/image_0.png)

Il tempo speso in questi giorni per me è stato importante per capire come poterne usufruire in modo agevole, dal momento che quei dati, in quanto dati della pubblica amministrazione, sono un bene pubblico e rappresentano quindi presupposto fondamentale per sviluppo di servizi, analisi, indagini etc...La domanda che mi sono fatto è la seguente : "Perché prima di chiedere nuovi dati da aprire al comune, non agiamo su quelli presenti rendendoli disponibili in modo facile ai cittadini?" Soprattutto perchè come si vede bene da [questa pagina](http://geoserver.comune.prato.it/geoserver/web/wicket/bookmarkable/org.geoserver.web.demo.MapPreviewPage?14) (grazie a Andrea Borruso) i dati effettivamente presenti sono molti (circa 530 dataset). 

Tenete presente che tra questi dati abbiamo dati importantissimi come fabbricati registrati al catasto, posizione delle farmarcie, posizione delle scuole, stradario, punti di interesse e moltissimo altro! C’è tutto quello che serve per effettivamente avere la "città" a portata di mano.e sviluppare servizi o effettuare valutazioni che si basino sulla posizione di questi “oggetti” della città di Prato.

Certo, qualcuno potrebbe obiettare quanti di questi dati sono effettivamente utili o no, ma andiamo con ordine e valutiamo intanto l’accessibilità del cittadino (e di macchine) ai dati che è fondamentale per poter dichiarare il dato effettivamente aperto.

Il Comune di Prato si è dotato di un applicativo chiamato Tolomeo che si integra con il sito del comune (trovate la sua descrizione [qui](http://tolomeogis.comune.prato.it/)) e serve da applicazione per mostrare a chi naviga una parte dei dati memorizzati nel geoserver del comune. Il senso di Tolomeo è avere un’applicazione unica che mostri al cittadino informazioni geografiche disinteressandosi dei dati sul server e permettere alcune opzioni tipo navigazione su mappa, filtraggio, zoom, ricerca. Tra l’altro si capisce dal sito del comune che l’applicazione è in uso in molti apparati della PA e si può trovare alcuni esempi delle sue funzionalità [qui](http://tolomeogis.comune.prato.it/esempi.php).

![l'applicazione Tolomeo](/assets/article_images/2017-09-13-comune-apri-geoserver/image_1.png)

In questi giorni ho usato Tolomeo per capire come possa essere utile ed in effetti ha un sé una funzionalità che consente l’export di alcuni dati e il loro riuso. In particolare ho realizzato due mappe con questi dati ovvero la [rete fognaria di Prato](https://iltempe.github.io/fogne/index) e i confini per [il catasto dei beni immobili](https://iltempe.github.io/mappa_base_immobili/index#11/43.8900/11.1752). 

![la mappa della rete fognaria](/assets/article_images/2017-09-13-comune-apri-geoserver/image_2.png)

Il punto è QUALI DATI si possono esportare con TOLOMEO dei dati memorizzati sul geoportale del comune? Di fatto se ne possono esportare solo una piccolissima porzione ovvero i dati in formato [WMS](http://mappe.comune.prato.it/html/wms/). E qui entriamo nel tecnicismo ma è sostanziale entrarci e capire il punto. I dati cartografici distribuiti sul web possono normalmente attenersi a questi due standard:

Lo Standard **Web Map Service** (WMS) fornisce una semplice interfaccia HTTP per richiedere immagini di mappe da uno o più server distribuiti in Internet. Una richiesta WMS definisce quali sono i layer geografici e l'area di interesse da processare. La risposta alla richiesta è una o più immagini di mappa (nel formato JPEG, PNG, ...) che può essere mostrata in un browser Internet. In effetti se visualizzate le mappe che ho realizzato sono semplici IMMAGINI su mappa e niente di più.

Lo Standard **Web Feature Service** (WFS) fornisce, similmente al WMS, una semplice interfaccia HTTP per richiedere direttamente oggetti geografici (e non immagini di mappe) da uno o più server distribuiti in Internet. I meccanismi di richiesta e risposta sono simili al WMS, con la differenza che non vengono restituite immagini, bensì le descrizioni dei singoli oggetti spaziali contenuti all'interno dell'area di interesse da processare (ovvero coordinate spaziali ed eventuali attributi alfanumerici).

**Si capisce dalla descrizione sopra che i veri dati sono i WFS e non i WMS. E’ quindi con questi dati che si potrebbe creare un reale servizio o fare un’analisi accurata dei dati storicamente prodotti e georiferiti dal Comune.**

**Come si fa allora per usare i "completi" ?  Risposta: attualmente non si può. Il Motivo? Il motivo di questa mancata accessibilità è il fatto che il geoportale comunale non consente l’accesso libero in lettura ai dati WFS. Se si prova ad accedere dal geoportale ad uno di questi dataset la schermata che si ottiene è [questa](http://geoserver.comune.prato.it/geoserver/comunepo/ows?service=WFS&version=1.0.0&request=GetFeature&typeName=comunepo:cciaa_esercizi_commerciali_divisione_03&maxFeatures=50&outputFormat=csv)**. 

Dal una rapida ispezione del geoportale pare esserci un login che impedisce la possibilità di ulteriore accesso al dato.**

Leggo di alcune iniziative come questa all’interno di [Prato Al Futuro](http://www.pratoalfuturo.it/partecipa/il-map-contest/) di partecipazione civica che l’attuale amministrazione ha deciso di lanciare basate su MAPPE su cui i cittadini potrebbero effettivamente proporre come si immaginano il loro quartiere nel futuro e come lo vedono oggi. La liberazione di questi dati potrebbe effettivamente facilitare molte di queste iniziative e simili oltre a consentire tutta una serie di servizi basati sulla georeferenziazione.
