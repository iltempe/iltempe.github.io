---
layout: post
title:  "Gli archivi delle Notizie del Comune di Prato: come ricavare dati aperti da un sito web"
date:   2017-04-24 10:34:25
categories: blog
tags:
  - opendata
  - civic hacking
  - tutorial
image: /assets/article_images/2017-04-24-scrape-trasformare-sito-dati-utili/1.jpg
---

Esiste una tecnica molto nota tra gli hacker, denominata [**web scraping**](https://it.wikipedia.org/wiki/Web_scraping), che consente di prelevare in modo selettivo e programmatico i contenuti da un sito web così da maneggiarli ed elaborarli a proprio piacimento.
Questa tecnica è molto comoda nel caso abbiate a che fare con siti della pubblica amministrazione molto "ricchi" di contenuti e molto aggiornati, ma molto poco strutturati in termini di dati riusabili: cosa significa questo? Significa che quando la fonte di informazione è un sito web basato su contenuti (principalmente testuali) è possibile usare la tecnica dello scraping (dall' inglese letteralmente "raschiatura") per selezionare le parti che più sono di interesse per trasformarle in dati con una struttura ben definita in modo tale che siano analizzabili facilmente, interpretabili da un software, aggregati, siano insomma un vero "dataset" pronto al riuso.
**Lo scrape è una vera e propria arte** perchè si basa sulla capacità dell'hacker di non chiedere assolutamente nessuna modifica al sito web, di analizzarlo per come è, capirne i processi di aggiornamento e prelevare le informazioni di interesse tramite un'applicazione esterna (ovviamente è possibile farlo dove i termini legali lo consentano).
Il [Sito del Comune di Prato](http://www.comune.prato.it/) ha una [sezione di comunicati stampa](http://comunicati.comune.prato.it/generali/) ben curata ed aggiornata contenente i comunicati stampa dell'anno in corso e tutti quelli degli anni dal 2004 in poi. Mi ero proposto da tempo di creare un archivio di tutte le notizie pubblicate (dal 2004 ad oggi) che sono diverse migliaia, così che fosse possibile la loro analisi e la loro ridistrubuzione in modo più semplice.
Ho pensato di spiegarvi come ho fatto nella speranza sia utile ad altri il procedimento e siano utili anche i dati estratti.
Ho iniziato per prima cosa ad analizzare come è strutturato un comunicato stampa del Comune, come [questo](http://comunicati.comune.prato.it/generali/?action=dettaglio&comunicato=14201700000001) e quali siano i dati da "liberare" di ogni comunicato.
E' importante in questa valutazione verificare che tutti i comunicati abbiano in linea di principio la stessa struttura in temini di "stili" nella pagina web, cioè i titoli devono essere tutti con lo stesso formato, i sottotitoli idem, i link idem etc...
![un comunicato stampa e la selezione dei dati da aprire](/assets/article_images/2017-04-24-scrape-trasformare-sito-dati-utili/2.jpg)
Un modo per "raschiare" i dati di interesse da un sito è usare il linguaggio [xpath](https://it.wikipedia.org/wiki/XPath), ovvero un linguaggio che consente di individuare elementi di una pagina web localizzandoli con un percorso come fossero dei file archiviati su un computer. Come trovare questi percorsi? Un modo molto semplice è usare il browser Google Chrome, selezionare l'elemento da raschiare e col tasto destro fare click su Ispeziona. All'apertura della finesta di ispezione col tasto destro del mouse sulla riga evidenziata selezionare Copia->Copia Xpath in modo che venga copiato negli appunti il path dell'elemento selezionato nella pagina e sia possibile incollarlo altrove.
![come trovare Xpath con Chrome](/assets/article_images/2017-04-24-scrape-trasformare-sito-dati-utili/3.jpg)
Questa operazione va ripetuta per tutte le parti della pagina che si desidera estrarre come dati utili. Nel caso del comunicato stampa ho scelto queste:
- Canale
- Data
- Ora
- Titolo
- Occhiello
- Catenaccio
- Testo
Idividuati gli Xpath è semplice con un'applicazione come [Google Sheet](https://www.google.it/intl/it/sheets/about/) intabellare i dati di un comunicato stampa o più di uno in modo tale che siano dati visionabili e scaricabili da chiunque come ho fatto con [questo foglio Google](https://docs.google.com/spreadsheets/d/1uns2k_aD1MyCOtGHBZ1OG05bU9o62xZxT6cCiye2KOo/edit?usp=sharing) dove a parte le informazioni delle prime due colonne (che sono ID del comunicato e l'anno) il resto dei dati sono ricavati automaticamente e dove è necessario sono estratti dalla pagina web usando la formula
```
=IMPORTXML(URL, query)
```
dove URL è il link della pagina web da analizzare e query è il path Xpath che avete analizzato.
![Esempio di Scraping con Google Sheet](/assets/article_images/2017-04-24-scrape-trasformare-sito-dati-utili/4.jpg)
GOOGLE Sheet è adatto per creare dataset con pochi dati in modo rapido quindi se volete prelevare i dati ad esempio di 10 articoli del 2017. Non è possibile gestire con un foglio Google un archivio come quello di tutti i comunicati stampa del comune di Prato perchè i dati da analizzare sono moltissimi e lo strumento non riesce a estrarre tutto quello che vi serve perchè l'operazione è molto "pesante", occorre quindi qualcosa di più potente, uno script fatto in casa che memorizzi tutti i dati e crei i dataset richiesti. Ho scelto di creare un file CSV per ogni anno dal 2004 ad oggi che contenga tutti i comunicati stampa di quell'anno con i dati richiesti. Per fare scrape normalmente lavoro con linguaggio PHP, ma solo per semplicità perchè questo linguaggio consente di essere eseguito via browser o su un PC senza setup complessi, ma il principio è riapplicabile con un altro linguaggio che preferite.
Il codice è visionabile [qui](https://github.com/iltempe/prato_news). Si tratta di un solo file (che da prompt dei comandi è possibile lanciare con "php data_news.php"). Nello script ci sono due funzioni: una effettua lo scrape vero e proprio, la seconda è di ausilio e serve per trovare quanti comunicati sono presenti in un anno definito (le notizie sono divise per anno).

In sequenza nel codice si eseguono queste operazioni (ho commentato il codice quindi è possibile individuarle anche se non si conosce il PHP in dettaglio)
- Scelgo gli archivi delle notizie di tutti gli anni (o di solo quelle che mi interessano);
- Definisco il nome dell'archivio dell'anno scelto (es. 2004_news.csv)
- Ricavo il massimo numero di notizie presenti per l'anno selezionato
- Scrivo nel file archivio l'intestazione
- Per tutte le notizie dell'anno prelevo i dati prescelti tramite gli Xpath individuati e le scrivo nell' archivio CSV. E' importante notare che il link delle notizie sono composti dalla stessa forma con una parte che resta sempre uguale e una parte che varia sulla base dell'anno e del numero di notizia che si va ad analizzare. In questo modo è piuttosto semplice creare dinamicamente tutti i link delle notizie di cui prelevare i dati.

Da tenere presente che il "cuore" dello script sono queste istruzioni che rappresentano la vera tecnica di "scrape":
```
$dom = new DOMDocument();
$dom->loadHTML($html);
$xpath = new DOMXPath($dom);

//CANALE
$my_xpath_query = "//*[@id='c-canale']";
$canale = $xpath->query($my_xpath_query);
.........
//creo un elemento da scrivere nel file con tutti i campi estratti
$data=array($i,$url,$data,$ora,$canale->item(0)->nodeValue,$titolo->item(0)->nodeValue,$occhiello->item(0)->nodeValue,$catenaccio->item(0)->nodeValue,$testo->item(0)->nodeValue);
```

Tutti i dati raccolti sono in questo [repository](https://github.com/iltempe/Comune-di-Prato/tree/master/news).

Per scaricare i dati direttamente ecco i link alle notizie:

[Anno 2004](https://raw.githubusercontent.com/iltempe/Comune-di-Prato/master/news/2004_news.csv)
[Anno 2005](https://raw.githubusercontent.com/iltempe/Comune-di-Prato/master/news/2005_news.csv)
[Anno 2006](https://raw.githubusercontent.com/iltempe/Comune-di-Prato/master/news/2006_news.csv)
[Anno 2007](https://raw.githubusercontent.com/iltempe/Comune-di-Prato/master/news/2007_news.csv)
[Anno 2008](https://raw.githubusercontent.com/iltempe/Comune-di-Prato/master/news/2008_news.csv)
[Anno 2009](https://raw.githubusercontent.com/iltempe/Comune-di-Prato/master/news/2009_news.csv)
[Anno 2010](https://raw.githubusercontent.com/iltempe/Comune-di-Prato/master/news/2010_news.csv)
[Anno 2011](https://raw.githubusercontent.com/iltempe/Comune-di-Prato/master/news/2011_news.csv)
[Anno 2012](https://raw.githubusercontent.com/iltempe/Comune-di-Prato/master/news/2012_news.csv)
[Anno 2013](https://raw.githubusercontent.com/iltempe/Comune-di-Prato/master/news/2013_news.csv)
[Anno 2014](https://raw.githubusercontent.com/iltempe/Comune-di-Prato/master/news/2014_news.csv)
[Anno 2015](https://raw.githubusercontent.com/iltempe/Comune-di-Prato/master/news/2015_news.csv)
[Anno 2016](https://raw.githubusercontent.com/iltempe/Comune-di-Prato/master/news/2016_news.csv)
[Anno 2017](https://raw.githubusercontent.com/iltempe/Comune-di-Prato/master/news/2017_news.csv)

I dataset in formato CSV sono composti come segue (ove alcuni dati non fossero presenti il campo relativo è vuoto):
- **ID** della notizia ricavata dal sito
- **URL** link alla notizia pubblicata sul sito del Comune di Prato
- **DATA** data di pubblicazione della notizia
- **ORA** ora di pubblicazione della notizia
- **CANALE** argomento della notizia
- **TITOLO** titolo della notizia
- **OCCHIELLO** campo occhiello della notizia
- **CATENACCIO** campo catenaccio della notizia
- **TESTO** campo testo della notizia
