---
layout: post
title:  "Nascondere parole segrete in un progetto Opensource"
date:   2017-08-29 09:00:00
categories: blog
tags:
  - opensource
  - civic hacking
  - tutorial
image: /assets/article_images/2017-08-29-nascondere-le-parole-segrete-nei-vostri-progetti/1.jpeg
---

Esigenza: normalmente sviluppare in modalità opensource implica la condivisione dei file sorgenti su Github o su altro repository condiviso. Sempre più spesso però capita che per usare servizi esterni dentro l'applicazione che state sviluppando siano richieste alcune "parole chiave personali" che (in quanto legate ad un account personale) vorremmo non esplicitare nel codice sorgente (almeno non in modo eclatante diciamo).

Come si fa quindi per nascondere questi dati sensibili e continuare a condividere i sorgenti senza paura di rivelare dati personali ad altri?

Un modo che ho testato e funziona è quello di usare [Travis](www.travis.org) in modo congiunto con [Github](www.github.com) come vi ho illustrato preliminarmente [qui](http://iltempe.github.io/blog/2017/08/27/Organizzare-una-serata-con.html).

Una volta messo in piedi la vostra "catena di sviluppo" supponiamo che all'interno del vostro file di configurazione di [Jekyll](https://jekyllrb.com/) abbiate inserito una vostra parola chiave per avere accesso ai dati di un'applicazione in questo modo: `mapillary_client_id: XXXXXXXXXXXXXXXXXXXX`.

Ridefinitela in modo simbolico così: `mapillary_client_id: MAPILLARY_CLIENT_ID_SECRET`.

A questo punto andate in Travis, "More Options->Settings" del vostro progetto definite la variabile che volete tenere segreta con il suo reale valore come scritto [qui](https://docs.travis-ci.com/user/environment-variables/#Defining-Variables-in-Repository-Settings). Nel mio caso la variabile definita si chiama MAPILLARY_CLIENT_ID.

![](/assets/article_images/2017-08-29-nascondere-le-parole-segrete-nei-vostri-progetti/2.png)

A questo punto sarà sufficiente istruire Travis in modo tale che prima di effettuare il deploy della vostra applicazione sostituisca al posto del vostro simbolo inserito nel codice la variabile di ambiente. Questo si può fare aggiungendo al file _travis.yml la seguente istruzione:

`before_install: sed -i "s/MAPILLARY_CLIENT_ID_SECRET/$MAPILLARY_CLIENT_ID/" _config.yml`

Notate che l'istruzione per sostiuire MAPILLARY_CLIENT_ID_SECRET con il valore della variabile $MAPILLARY_CLIENT_ID è tra doppie virgolette il che serve per far espandere la variabile d'ambiente in modo corretto a travis. Fatto.

Se in locale volete invece mantenere un ambiente per sviluppare e quindi anche con tutti i dati sensibili vi conviene avere un file _config_dev.yml da non condividere su Github e da usare solo localment e per effettuare i vostri test. Se state usando Jekyll si può facilmente scegliere quale file di configurazione usare con il comando per il build:
`bundle exec jekyll serve --config _config_dev.yml`



