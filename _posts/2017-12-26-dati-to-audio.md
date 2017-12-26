---
layout: post
title:  "Usare i feed rss per suonare un'allerta"
date:   2017-12-26 10:00:00
categories: blog
tags:
  - opendata
  - copernicus
  - emergenze
  - civic hacking
image: /assets/article_images/2017-12-26-dati-to-audio/1.png
---

I [feed rss](https://it.wikipedia.org/wiki/RSS) sono un particolare formato di dati, ormai piuttosto datato, ma molto usato per creare "canali di aggiornamento" su un particolare tema. Sono molto presenti in servizi web come blog, siti web, ma sono anche molto usati per inviare aggiornamenti via internet riguardo ad un particolare evento che nel tempo necessita di aggiornamenti. Pensate ad una situazione di emergenza in cui costantemente si debba divulgare cosa sta accadendo, è necessario un formato dati come il feed rss facilmente leggibile con servizi quali [Feedly](https://feedly.com/) in cui monitorare periodicamente le vostre fonti ed essere sempre informati solo su ciò che effettivamente vi interessa.
Tanto più questo tipo di formato se divulgato con licenza aperta diventa utilissimo per creare semplici applicazioni e/o servizi utente quali ad esempio l'invio di messaggi in chat.

Con il crescente uso dell'internet delle cose è possibile immaginare che i dati, laddove effettivamente esistano, possano essere usati per "pilotare" oggetti connessi in internet così da creare veri e propri feedback percepibili dall'uomo, anche da chi non è esperto di tecnologia. In caso di emergenza, ad esempio, viene da pensare che il "cittadino non esperto di dati" non si interessa certamente all'aggiornamento del dato in sè o alla produzione di un dataset sul sito del suo Comune, quanto eventualmente a come questo dataset può essere percepito tramite servizi vicini a lui e alla vita di tutti i giorni. C'è un'allerta meteo? Bene, mi interessa sapere se devo stare chiuso in casa o no. Se poi questo viene comunicato con la TV, la radio, il giornale o i dati ..."chisseneimporta", per l'utente finale. La cosa interessante resta però il fatto che dall'aggiornamento costante dei dati si possono "pilotare" tanti strumenti oggi (grazie alla connessione internet) compresi oggetti che "storicamente" fanno parte della nostra vita quotidiana.

Supponiamo allora di avere una fonte dati strutturata in formato FEED RSS, ho preso per questo esperimento [questa allerta](http://emergency.copernicus.eu/mapping/list-of-components/EMSN046) sul sito di [Copernicus EMS](http://emergency.copernicus.eu/) attivata per un alluvione in Germania che sta avvenendo in questi giorni. Il feed attivato per dare aggiornamenti è [questo](http://emergency.copernicus.eu/mapping/list-of-components/EMSN046/feed).

Supponiamo di voler suonare un allarme ogni volta che Copernicus EMS invia un aggiornamento su questa allerta tramite il Feed RSS. Se ipotizziamo di avere una "centrale" connessa al web il nostro sistema si implementa anche a basso costo. La centrale per fare questo è implementabile oggi con una semplice scheda elettronica come un [Raspberry PI](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/) che si può connettere con un'uscita audio ad una periferica di vostro piacimento (megafono, altoparlanti...).

![esempio di connessione cassa audio con Raspberry](https://www.dexterindustries.com/wp-content/uploads/2016/11/Speaker-Speaker_and_Raspberry_Pi.jpg)

Con questa scheda potete implementare adesso un servizio di monitoraggio dei dati che consenta di rilevare un aggiornamento ed in caso di tale aggiornamento fare un normalissimo play di un file musicale .mp3 come l'audio presente [in questo video](https://www.youtube.com/watch?v=S_aZw7Rr8h4).

Il software che ho usato per fare il monitor dei dati feed rss è [RssTail](http://python-rsstail.readthedocs.io/en/latest/) una libreria python anche usabile da riga di comando in script bash. Lo script è effettivamente semplicissimo lo vedete qui sotto.

<script src="https://gist.github.com/iltempe/07082e2eee9f32dd90bc05b90742c31d.js"></script>

RssTail ha molte opzioni ma nella mia implementazione:
- ogni 3 secondi verifica se ci sono aggiornamenti
- monitora [questo feed](http://emergency.copernicus.eu/mapping/list-of-components/EMSR261/feed)
- inizialmente non registra nessun aggiornamento
- ogni aggiornamento effettua un play del file allarme.mp3 tramite il lettore "afplay" che sul mio mac è invocabile da riga di comando, in caso di server Linux potete rimpazzarlo con qualche player come [questi](http://www.tuxarena.com/2011/12/10-console-music-players-for-linux/)

Fatto. L'esperimento è molto semplice, ai limite del banale, ma dimostra molto bene come tramite una fonte di dati strutturata ed aggiornata si possa effettivamente inviare un feedback "sonoro" alle persone simulando così un megafono connesso ad internet.
