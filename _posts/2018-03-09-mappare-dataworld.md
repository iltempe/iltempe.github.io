---
layout: post
title:  "Mappare le panchine della tua città senza saper programmare"
date:   2018-03-09 10:00:00
categories: blog
tags:
  - opendata
  - opendata
  - civic hacking
  - ifttt
  - dataworlds
image: /assets/article_images/2018-03-09-mappare-dataworld/0.jpeg
---


Di seguito un brevissimo tutorial per chi vuole mappare oggetti, vuole al contempo produrre dati e non vuole usare server propri per archiviare i dati bensi usare piattaforme esistenti. Si esegue tutto gratuitamente in circa un 'ora di tempo senza una riga di codice.

## Ingredienti:

- Un account sulla piattaforma di creazione semplici servizi [IFTTT](https://ifttt.com)
- Un account sulla piattaforma di archiviazione dati [Data.World](https://data.world/)
- Un dispositivo mobile (io ho usato il mio Ipad) da usare per la mappatura degli oggetti, io ho fatto una simulazione ipotizzando di mappare le panchine di Prato.

Il materiale è solo questo. Non vi serve altro.

## Ricetta:

- Create uno stream (progetto) su [Data.World](https://data.world/) trovate un esempio [qui](https://data.world/iltempe/prova)

![](/assets/article_images/2018-03-09-mappare-dataworld/5.png)

- Usando il [canale di IFTTT di Data.World](https://ifttt.com/datadotworld) creare una ricetta su IFTTT come indicato in figura sotto

![servizio IFTTT di dataworld](/assets/article_images/2018-03-09-mappare-dataworld/1.png)

![](/assets/article_images/2018-03-09-mappare-dataworld/2.png)

é importante che nello spazio relativo allo stream inseriate l'identificativo del vostro "stream" che è l'ultima parte del link relativo ad un progetto da voi creato su Data.World.

- Assicuratevi che IFTTT abbia accesso alla localizzazione del vostro dispositivo mobile (tra i setting del vostro account)

- Create con IFTTT un widget sulla Home del vostro dispositivo mobile dalla sezione widget, questo vi consentirà di attivare la ricetta come un semplice pulsante sul telefono. Scegliete nella sezione widget la ricetta appena creata, in questo modo la vedrete comparire sulla home come una normalissima APP!

![la sezione widget di IFTTT](/assets/article_images/2018-03-09-mappare-dataworld/1.jpg)
![la ricetta sulla home del dispositivo mobile](/assets/article_images/2018-03-09-mappare-dataworld/7.png)

Fatto. a questo punto ogni volta che sarete davanti alla panchina da mappare dovrete solo premere la vostra ricetta sul dispositivo mobile e catturerete la posizione della panchina ed automaticamente  aggiornerete i dati su Data.World!

![i dati relativi alla posizione salvati online](/assets/article_images/2018-03-09-mappare-dataworld/6.png)

Per usare i dati del file su Data.World sarà sufficiente un qualenque software di mappatura che possa leggere i dati di localizzazione (si rimanda per questo all'uso di [Umap](https://umap.openstreetmap.fr/it/).

