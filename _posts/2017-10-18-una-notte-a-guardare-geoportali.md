---
layout: post
title:  "Una notte a guardare geoportali: non è un belvedere"
date:   2017-10-18 09:00:00
categories: blog
tags:
  - civic hacking
  - pa
  - opendata
image: /assets/article_images/2017-10-18-una-notte-a-guardare-geoportali/pexels-photo.jpg
---


**NdR**: questo post è una reazione chimica generata da 4 elementi: [la rosa](https://twitter.com/lrssvt), la [tempesta](https://twitter.com/il_tempe), il [Pi greco](https://twitter.com/totofiandaca) e l'[aborruso](https://twitter.com/aborruso). 

# Introduzione

Il web consente di fare partire effetti domino inaspettati. Per fortuna delle volte sono proprio belli. L’onda di oggi l’ha sollevata [Totò](https://www.facebook.com/photo.php?fbid=10215055066958956&set=a.4809453763102.2189843.1498961577&type=3&theater), segnalando che il Geoportale della Regione Siciliana (anzi uno dei due geoportali) fosse in manutenzione.

![image alt text](/assets/article_images/2017-10-18-una-notte-a-guardare-geoportali/image_0.png)

Andrea ha [fatto notare](https://www.facebook.com/pigreco314/posts/10215055071039058?comment_id=10215055428087984&comment_tracking=%7B"tn"%3A"R9"%7D) allora che si tratta di un servizio che nell’ultimo mese è stato spento per quasi 15 giorni.

A quel punto si sono aggiunti [Matteo](https://www.facebook.com/pigreco314/posts/10215055071039058?comment_id=10215055458168736&comment_tracking=%7B%22tn%22%3A%22R9%22%7D) e [Salvatore](https://www.facebook.com/pigreco314/posts/10215055071039058?comment_id=10215055553971131&comment_tracking=%7B"tn"%3A"R9"%7D) e si è creato un crescendo informativo interessante e anche un po’ allarmante: alcuni dei geoportali italiani sono quasi inutilizzabili, altri pubblicano pochissimi dati realmente aperti.

A seguire un elenco.

## Geoportale della Regione Siciliana

È già stato citato sopra, ed espone due servizi principali:

* [http://map.sitr.regione.sicilia.it/gis/rest/services/](http://map.sitr.regione.sicilia.it/gis/rest/services/)

* [http://map.sitr.regione.sicilia.it/ArcGIS/rest/services/](http://map.sitr.regione.sicilia.it/ArcGIS/rest/services/)

Il secondo è down per la metà del tempo (almeno negli ultimi 30 giorni).

![image alt text](/assets/article_images/2017-10-18-una-notte-a-guardare-geoportali/image_1.png)

## Geoportale di Prato

Matteo segnala la situazione di Prato, comune che ha un geoportale con circa 530 dataset, ma i dati non sono aperti. Il link al geoserver è il seguente [http://geoserver.comune.prato.it/geoserver/web/](http://geoserver.comune.prato.it/geoserver/web/). Come si vede in alto i dati sono protetti da password. Questa situazione fa riflettere su quanti dati effettivamente siano già in possesso delle Pubbliche Amministrazioni e il problema dei dati aperti sia esclusivamente un problema di accesso al dato. In particolare sono inaccessibili i dati in formato WFS. E’ proprio con questi dati che si potrebbe creare un reale servizio o fare un’analisi accurata Un’analisi del problema e un invito al Comune ad aprire i dati è stata fatta [qui](http://iltempe.github.io/blog/2017/09/13/comune-apri-geoserver.html). 

 

![image alt text](/assets/article_images/2017-10-18-una-notte-a-guardare-geoportali/image_2.png)

Attualmente se si prova ad accedere ad un dataset questo è l’errore che si genera.

![image alt text](/assets/article_images/2017-10-18-una-notte-a-guardare-geoportali/image_3.png)

## Regione Calabria

![image alt text](/assets/article_images/2017-10-18-una-notte-a-guardare-geoportali/image_4.png)

Il Geoportale della Regione Calabria, che negli ultimi mesi ha cambiato aspetto attraverso un’interfaccia più gradevole alla vista, per la consultazione della propria banca dati geografica mette a disposizione diversi servizi (http://geoportale.regione.calabria.it/servizi), molti dei quali però sono inaccessibili.

Quello relativo al visualizzatore cartografico (WebGIS CTR:[ http://pr5sit.regione.calabria.it/mapbuilderWeb/browser.noSec](http://pr5sit.regione.calabria.it/mapbuilderWeb/browser.noSec)) per la consultazione della Carta Tecnica Regionale molto spesso non è disponibile e provando ad accedervi risponde come sotto. Anzi, non risponde :-(

![image alt text](/assets/article_images/2017-10-18-una-notte-a-guardare-geoportali/image_5.png)

Stesso messaggio si ottiene provando ad accedere sia al servizio WebGIS che a a quello relativo alla Rete planimetrica.

Il Navigatore SIRV e quello FotoCartografico non consentono un accesso libero alle informazioni presenti, viene richiesta l’autenticazione per poter consultare i dati. Entrambi i servizi dovrebbero fornire un "*importante strumento a supporto *del monitoraggio dei beni e dei vincoli che esistono su di essi" (copio ed incollo cosa viene riportato sul sito del geoportale stesso).

![image alt text](/assets/article_images/2017-10-18-una-notte-a-guardare-geoportali/image_6.png)

La consultazione della Carta dei luoghi, raggiungibile dal medesimo servizio, non è visibile nonostante il framework utilizzato come visualizzatore viene caricato correttamente (senza errori) dal browser. L’accesso al servizio porta ad una pagina con molti strumenti ma senza dati :-(

![image alt text](/assets/article_images/2017-10-18-una-notte-a-guardare-geoportali/image_7.png)

Note finali (di cui una positiva), si riscontrano spesso disservizi e dati non accessibili ed a parte le diverse tecnologie software utilizzate per la creazione del servizio, nel geoportale è carente l’accessibilità al dato attraverso servizi Web (WMS, WFS, WCS etc), ricordiamo che tali servizi sono fondamentali per garantire l’interoperabilità delle informazioni che si vogliono rendere disponibili. 

La nota positiva è che il Geoportale della Regione Calabria mette a disposizione una serie di dataset (in realtà non tantissimi) con licenza IODL e liberamente scaricabili.

![image alt text](/assets/article_images/2017-10-18-una-notte-a-guardare-geoportali/image_8.png)

## Regione Emilia Romagna, Catalogo Moka

Il catalogo Moka della Regione Emilia Romagna [http://www.mokagis.it/html/applicazioni_mappe.asp](http://www.mokagis.it/html/applicazioni_mappe.asp) è basato su una tecnologia che è disabilita da tempo *by default* nel web browser oggi più usato (vedi ad esempio [qui](https://www.digitaltrends.com/web/chrome-56-browser-html5-default-flash-block/)).  

Nei fatti è una barriera di ingresso.

![image alt text](/assets/article_images/2017-10-18-una-notte-a-guardare-geoportali/image_9.png)

## Regione Molise

![image alt text](/assets/article_images/2017-10-18-una-notte-a-guardare-geoportali/image_10.png)

Il portale cartografico regionale del Molise [http://cartografia.regione.molise.it](http://cartografia.regione.molise.it) va in *timeout* :(

![image alt text](/assets/article_images/2017-10-18-una-notte-a-guardare-geoportali/image_11.png)

## Regione Campania

Sul sistema informativo territoriale campano si legge:

*La visione dei dati territoriali presenti nel sito deve intendersi a carattere indicativo e non sostituisce la consultazione presso gli uffici competenti.Si prega di prendere visione delle note legali per il corretto utilizzo dei contenuti del GeoPortale. Il Servizio SIT provvede a inserire nel Geoportale informazioni per quanto possibile aggiornate, ma non garantisce circa la loro completezza o accuratezza, alcuni dati potrebbero cambiare prima dell aggiornamento.Per proseguire nella consultazione dei dati si dichiara di essere consapevole delle note legali suddette e di accettarle integralmente.*

Dopo - anche se questa premessa non è incoraggiante - si fa click su  Web GIS [http://sit.regione.campania.it/portal/portal/default/Cartografia/](http://sit.regione.campania.it/portal/portal/default/Cartografia/) e si ottiene l’errore di sotto.

![image alt text](/assets/article_images/2017-10-18-una-notte-a-guardare-geoportali/image_12.png)

E anche la ricerca dei Metadati porta ad una pagina di errore.

![image alt text](/assets/article_images/2017-10-18-una-notte-a-guardare-geoportali/image_13.png)

In extremis, [Massimiliano Moraca](https://www.facebook.com/pigreco314/posts/10215055071039058?comment_id=10215055735095659&reply_comment_id=10215055758896254), ci informa che la Regione ha un nuovo SIT, ma è stata dura a scovarlo, solo dopo avere inserito nella magica casella di testo di Google la frase "sit2 geoportale campania" è apparso il nuovo geoportale regionale.

# Per chiudere

Questo mini *report* vuole mostrare come dei servizi di enorme interesse e importanza, di alcune importanti pubbliche amministrazioni italiane, siano o in gravi situazioni operative o necessitino scelte di processo differenti.

Fare in modo che questi servizi funzionino e che restituiscano alla cittadinanza dati aperti è da considerarsi un risultato di base. E proprio per questo è anche un fatto politico, che lascia a tutti noi la valutazione dello stato delle cose.

