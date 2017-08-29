---
layout: post
title:  "Come fare un bot con Facebook Messenger"
date:   2016-04-16 10:10:00
categories: blog
tags:
  - bot
  - messenger
  - social
  - tutorial
image: /assets/article_images/2016-04-16-come-fare-un-bot-con-facebook-messenger/fb.jpg
---


Mi pareva doveroso dopo molte cose realizzate con [Telegram](https://telegram.org/), dare un po' di soddisfazione anche al mio carissimo amico Mark Zuckerberg, cioè, come dire, lui mi da un nuovo strumento per creare servizi ed io c'avevo una voglia matta di capire come si poteva usarlo. La conferenza di qualche giorno fa per gli sviluppatori Facebook potete rivederla [qui](https://www.fbf8.com/).
Lascio ai giornalisti ed ai cronisti le analisi su quali siano le potenzialità del servizio con i BOT, che io dai tempi di Emergenzeprato con Telegram definisco rivoluzionario. Qui oggi mi limito a mettere le basi per creare un oggetto che risponde in chat sulla piattaforma [Messenger](https://www.messenger.com) di Facebook.

Ovviamente siamo agli inizi, pare ancora tutto è un po' rudimentale, sperimentale anche la piattaforma di sviluppo stessa, ma possiamo aspettarci che col tempo la cosa sarà resa più facile, esiste già una Dashboard per sviluppatori più "user friendly" ad oggi non ancora disponibile a tutti. Mi interessa di tutto questo che Facebook si apre ad essere piattaforma per servizi appunto, tramite Messenger, cosa non affatto scontata.  Intanto iniziamo col dire che rispetto a piattaforme come Telegram Facebook non risulta ancora di cosi immediato approccio dal momento che Mark Zuckerberg vuole comunque avere un controllo piuttosto importante (in termini di informazioni) sull' Applicazione che viene sviluppata per creare il BOT.

Come fare a creare un bot su Facebook? Ho studiato le [istruzioni di Facebook](https://developers.facebook.com/docs/messenger-platform/quickstart) per gli sviluppatori. Tutti possono approfondire come funziona anche con la [guida ufficiale completa](https://developers.facebook.com/docs/messenger-platform/implementation). Ma cerchiamo di andare con ordine e capire come si procede.

* Iscriviti alla piattaforma [Facebook for Developers](https://developers.facebook.com), non costa nulla devi solo dare un po' di dati a Mark.
* Crea una [Pagina Facebook](https://www.facebook.com/pages/create) e una [App Facebook](https://developers.facebook.com/quickstarts/?platform=web). Se vuoi puoi usarne due esistenti. La tua applicazione può non essere pubblica e la tua pagina sarà usata come profilo utente con cui chattare su Messenger. La pagina funge quindi da utente fittizio che impersona il BOT.

![screenshot](https://raw.githubusercontent.com/iltempe/robot/master/demo/4.png)


* Vai nei settings della tua APP e alla voce prodotti seleziona Messenger.


* Imposta il tuo UNCINO SUL WEB: come con Telegram per mettere in comunicazione in tempo reale quello che l'utente scrive in chat con il robot Facebook occorre creare sul web un "uncino", ossia un host all'interno del quale ci sia oltre al software che consente di gestire la logica di domanda/risposta del bot anche lo scambio di dati tra questa logica e la app appena creata su Facebook. Nella sezione Messenger della Dashboard da sviluppatori alla voce webhook inserite la callback URL al vostro webhook (serve la connessione https) e definite un codice di verifica che Facebook chiama Validation Token. Selezionate le funzioni da sottoscrivere per questa app che sono message_deliveries, messages, messaging_optins e messaging_postbacks.
* Adesso inizia la parte vera e propria da "smanettoni". Occorre aggiungere il codice per la verifica presso il webhook che è stato impostato al punto precedente. Il codice che serve è un codice che verifichi su una precisa richiesta di GET dalla app creata che il codice di verifica è quello impostato. Dopodichè è possibile cliccare sul pulsante Verifica e Salva. Il codice in forma Javascript può essere come quello indicato qui sotto:

```
// facebook messenger webook
app.get('/webhook/', function (req, res) {
  if (req.query['hub.verify_token'] === 'token_opendatagentediprato') {
    res.send(req.query['hub.challenge'])
  }
  res.send('Error, wrong token')
})
```

* Nella sezione di generazione del Token adesso è possibile generare un Token per la Pagina che si vuole usare come profilo del BOT. Copia questo token. Il token non viene salvato nelle impostazioni puoi rigenerarlo quante volte vuoi, i vecchi token resteranno attivi.

![screenshot](https://raw.githubusercontent.com/iltempe/robot/master/demo/shot2.jpg)


* A questo punto è necessario connettere la tua APP Facebook con la Pagina Facebook. Usa il token copiato al punto precedente per digitare questo comando dal tuo computer

```

curl -ik -X POST "https://graph.facebook.com/v2.6/me/subscribed_apps?access_token=<token>"

```
* Aggiungete alla vostra Applicazione la gestione delle richieste POST tramite le API Facebook. Facebook indica codice javascript come questo:

```
// postare dati
app.post('/webhook/', function (req, res) {
  messaging_events = req.body.entry[0].messaging
  for (i = 0; i < messaging_events.length; i++) {
    event = req.body.entry[0].messaging[i]
    sender = event.sender.id
    if (event.message && event.message.text) {
      text = event.message.text
      if (text === 'Generic') {
        sendGenericMessage(sender)
        continue
      }
      sendTextMessage(sender, "Ho ricevuto questo testo: " + text.substring(0, 200))
    }
    if (event.postback) {
      text = JSON.stringify(event.postback)
      sendTextMessage(sender, "Ho ricevuto un postback: "+text.substring(0, 200), token)
      continue
    }
  }
  res.sendStatus(200)
})

```
Indipendentemente dal linguaggio, quando avrete settato la gestione del POST inviando un messaggio alla pagina dovreste vederlo comparire tramite il webhook che hai terminato di configurare.

* A questo punto non vi resta che definire cosa rispondere a precisi messaggi ricevuti in chat ampliando il codice che avete sul vostro webhook. In particolare potete sviluppare un bot che invii:
	* Semplici Messaggi di Testo (stringhe)
	* Messaggi Strutturati (messaggi costituiti da dati con un certo formato ben definito)
Oltre a queste possibilità avete la possibilità (se gestite dati strutturati in risposta) di impostare pulsanti di opzione di scelta per l'utente (esattamente come con Telegram). Ad esempio un pulsante con dati strutturati si può definire cosi:

```
{
    "title": "Second card",
    "subtitle": "Element #2 of an hscroll",
    "image_url": "http://messengerdemo.parseapp.com/img/gearvr.png",
    "buttons": [{
    "type": "postback",
    "title": "Postback",
    "payload": "Payload for second element in a generic bubble",
}
```
Se impostate pulsanti per l'utente dobbiamo ricordarci di gestire la chiamata Postback, ossia l'azione che il bot deve compiere nel momento in cui l'utente preme il pulsante. In Javascript Facebook consiglia codice di questo tipo.

```
  if (event.postback) {
    text = JSON.stringify(event.postback);
    sendTextMessage(sender, "Postback received: "+text.substring(0, 200), token);
    continue;
  }
```
Questo è un inizio. A questo punto il vostro BOT è interrogabile da voi stessi in modo privato (che ne siete amministratori), potete renderlo pubblico sottoponendo la vostra applicazione pubblica tramite il processo di Review di Facebook, grande differenza rispetto a Telegram appunto: Facebook deve fare una verifica delle vostre applicazioni prima di renderle pubbliche.

Consiglio personale: iniziate studiando la guida ufficiale di Facebook. Per l'implementazione, io non sono partito da 0, esistono già molte soluzioni software con cui implementare il vostro webhook nel vostro linguaggio di programmazione preferito. Oltre al Javascript che è il linguaggio con cui Facebook vi guida, segnalo ad esempio [questo progetto](https://github.com/luisbebop/facebook-robot-sinatra) già pronto per il deploy in linguaggio Ruby. Io per il mio esperimento ho selezionato il linguaggio Javascript, lavorando su [questa soluzione](https://github.com/jw84/messenger-bot-tutorial) con licenza ICS.
Ho effettuto un fork che trovate [qui](https://github.com/iltempe/robot) fatto deploy su [Heroku](https://dashboard.heroku.com/) e "agganciato" il webhook ad una Facebook APP con Messenger.
Si tratta di una soluzione composta da un unico file index.js che gestisce  le API, la logica di risposta del BOT, un insieme di file Messages che consentono in modo facile di usare le risposte testo semplice, dati strutturati, pulsanti. Con questo codice riadeguato per i miei scopi e seguendo la guida sopra, ho provato a creare un bot per [OpendataGentediPrato](http://iltempe.github.io/opendatagentediprato). In questo momento il BOT se interrogato risponde ripetendo ciò che viene inviato come testo ed inviando due dataset di prova in caso si invii la BOT la stringa Generic.

![screenshot](https://raw.githubusercontent.com/iltempe/robot/master/demo/5.png)

![screenshot](https://raw.githubusercontent.com/iltempe/robot/master/demo/6.png)
