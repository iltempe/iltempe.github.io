---
layout: post
title:  "Produrre dati da un archivio mail"
date:   2017-11-25 10:00:00
categories: blog
tags:
  - data mining
  - civic hacking
image: /assets/article_images/2017-11-25-estrarre-dati-da-un-archivio-mail/1.jpeg
---

In questi giorni ho avuto l'esigenza di fare una valutazione su quante notifiche mail avessi ricevuto su un certo tema con soggetto ben preciso. Lo scopo era valutare quanto "tempo" ho dedicato ad una certa attività basandomi sulle comunicazioni intercorse via mail.

Mi era necessario quindi fare una stima "di massima" delle mail ricevute con un certo oggetto (o simile), ma mi sono chiesto se si potesse fare qualcosa di più accurato intervenendo direttamente sui dati contenuti nella mia posta elettronica.

In particolare ho esportato l'intero archivio della posta del mio pc in formato [mbox](https://en.wikipedia.org/wiki/Mbox#Familymbox) e mi sono posto il problema di analizzarlo in modo automatico per creare un dataset degli "oggetti" di tutte le mie mail per poi poterlo analizzare con calma. Il formato mbox è un formato piuttosto diffuso che consente di "esportare" un set di mail archiviate su un PC in un'unico contenitore facilmente analizzabile. Vi invito ad andare alla pagina Wikipedia per capire come è strutturato questo archivio.

Caso vuole che da un po' di tempo stia anche studiando un nuovo linguaggio di programmazione, ovvero [Go](https://golang.org/). Go è un linguaggio di programmazione opensource ideato da [Google](www.google.it), non farò qui una guida su come programmare con questo linguaggio, vi basti sapere quanto sotto:

- E' un linguaggio tipizzato al contrario di molti linguaggi oggi utilizzati. Questo lo rende più sicuro e consente un rapido sviluppo in fase di debug. Soprattutto questo vi permette di identificare errori sui dati prima di compilare. Il linguaggio infatti prevede un compilatore.
- Per una serie di motivi tecnici Go garantisce delle ottime performance quando dovete sviluppare applicazioni di media alta complessità.
- Non avete bisogno di un framework per sviluppo web con Go. Si tratta di installarlo e stop perchè molti componenti utili sono nativamente compresi nell'installazione.
- Il [motore di ricerca](https://godoc.org/) per pacchetti Go è molto vasto e contiente molte estensioni utili installabili direttamente dal vostro programma tramite il loro link.

Detto questo andiamo al sodo. Come si realizza uno script di analisi di un archivio mbox e produzione di un dataset con dati utili?

Il mio script lo trovate su [Github](www.github.com) a [questo link](https://github.com/iltempe/EmailDataMine/blob/master/main.go) ed una volta installato Go sul vostro computer potrete lanciarlo semplicemente ponendolo nella cartella del vostro file map mbox e lanciarlo con 

```
go run main.go archiviomail.mbox
```

Il codice dello script è molto semplice (Go facilita la comprensione di quanto elaborato perchè molto simile al linguaggio [C](https://it.wikipedia.org/wiki/C_(linguaggio))) ad ogni modo la magia la fa la funzione seguente

	func readEmail(b []byte) {
	// per leggere una mail sono da rimuovere
	// le righe nuove e il "From "
	const NL = "\n"
	trimmed := strings.TrimLeft(string(b), NL)
	var msgString string
	if strings.Index(trimmed, "From ") == 0 {
		msgString = strings.Join(strings.Split(trimmed, NL)[1:], NL)
	} else {
		msgString = trimmed
	}
	
	msg, err := mail.ReadMessage(strings.NewReader(msgString))
	if err != nil {
		fmt.Println(err)
		return
	}
	
	fmt.Println("Subject:", msg.Header.Get("Subject"))
	//stampa su CSV i dati
	var data = []string{msg.Header.Get("Subject")}
	csvWriter(data)
	}
al termine del run un file data.csv con tutti gli oggetti delle vostre mail sarà prodotto nella vostra folder di lavoro.

Ovviamente seguendo le specifiche del file mbox potete divertirvi ad estrarre dati diversi dal Subject, ad esempio potete analizzare chi invia la mail per analizzare i mittenti da cui ricevete posta elettronica. Sarà sufficiente al termine della funzione sopra inserire : 

```
fmt.Println("Subject:", msg.Header.Get("From"))
//stampa su CSV i dati
var data = []string{msg.Header.Get("From")}
csvWriter(data)
```

Fatto. Buon divertimento a tutti….e analizzate le vostre mail, non limitatevi a leggerle, io ci ho trovato informazioni molto utili.

