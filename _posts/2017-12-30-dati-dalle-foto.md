---
layout: post
title:  "Mappare oggetti tramite le foto"
date:   2017-12-30 10:00:00
categories: blog
tags:
  - opendata
  - mappe
  - mobile
  - civic hacking
image: /assets/article_images/2017-12-30-dati-dalle-foto/1.jpg
---

In questi giorni mi è stato chiesto un suggerimento su una soluzione "semplice" da mettere in piedi per fare una mappatura completa di oggetti disposti nei luoghi pubblici di una città. Esistono milioni di applicazioni software e di soluzioni che vi consentono di creare questo tipo di mappe semplicemente muovendosi con uno smartphone in mano. Tutte però richiedono l'installazione di specifiche APP e non tutte son completamente "aperte" nel senso che non tutte vi consentono l'accesso ai dati raccolti.

Supponiamo poi che a mappare debba essere qualcuno che ha poco tempo e poco skill tecnologico, questo soggetto deve essere messo in condizioni di dover fare poche semplici azioni ed in modo rapido.

Lo scenario che ho ipotizzato quindi è il seguente: operatori ecologici che distribuiscono i cassonetti per la raccolta differenziata ai condomini e alle aziende della mia zona. Mentre lo fanno la loro direzione richiede anche di tenere traccia della posizione dell'installazione dei raccoglitori dei rifiuti in modo da visionare lo stato della distribuzione nella città e (con mio sommo piacere) pubblicare le posizioni dei cassonetti come dati pubblici.

![](/assets/article_images/2017-12-30-dati-dalle-foto/8.jpg)

La soluzione secondo me più rapida che si può suggerire è quella di scattare una foto ai raccoglitori una volta consegnati. Una foto? Si avete capito bene. Una foto con uno smartphone (su cui è stata accuratamente abilitato la localizzazione durante lo scatto della fotografia) consente di memorizzare la posizione in un'immagine, posizione geografica che può essere analizzazione in seguito. E' esattamente ciò che molti sistemi operativi fanno quando vi consentono di visualizzare le vostre fotografie su mappa così che facilmente possiate navigarle e ripercorrere i vostri ricordi associandoli ai luoghi che avete visitato.

Una volta raccolto un set di fotografie corrispondenti ai vostri "cassonetti" non vi resta che copiarle in una cartella sul vostro computer ed installare il tool [ExifTool](https://www.sno.phy.queensu.ca/~phil/exiftool/). Questo strumento software (invocabile anche da riga di comando) consente l'analisi di tutti i dati in formato [EXIF](https://it.wikipedia.org/wiki/Exchangeable_image_file_format) che nativamente il vostro smartphone associa alle foto che scattate. Ad esempio digitando "exiftool 1.jpg" si possono vedere tutti i dati relativi all'immagine 1.jpg:

<script src="https://gist.github.com/iltempe/de5f49094de2ffe20d8c2713af4bd8e3.js"></script>

In questi dati son memorizzate moltissime informazioni tra cui la posizione geografica nella quale avete scattato la vostra foto. Come la si può facilmente isolare? Con exiftool sarà sufficiente digitare il seguente comando dalla folder dove avete memorizzato le foto per generare un dataset contenente il nome del file della foto, latitudine e longitudine dell'oggetto mappato.

<script src="https://gist.github.com/iltempe/80d0ece33d01d9dd02b358424b042ed1.js"></script>

Fatto. A questo punto avete un CSV contenente le posizioni dei vostri cassonetti dei rifiuti che potete facilmente visionare con un qualunque software di mappatura come [Umap](https://umap.openstreetmap.fr/it/) ma anche lo stesso [My Maps](https://www.google.com/intl/it/maps/about/mymaps/) di Google come ho fatto qui sotto.

<script src="https://gist.github.com/iltempe/59032be24703580b3dd028536b54e0e8.js"></script>

<iframe src="https://www.google.com/maps/d/embed?mid=1KA-ofpOIgc1D2kudJr0jPuil4XSafHB9" width="640" height="480"></iframe>

Il metodo è uno dei tanti metodi che si possono certamente ideare per data collection ma tra i tanti ha due aspetti importanti che lo rende di semplice utilizzo:
- non obbliga ad installare nessuna app sul vostro smartphone che deve solo avere la localizzazione abilitata associata allo scatto delle fotografie
- separa completamente la fase di raccolta dati sul campo (quella in cui si scattano le foto) da quella in cui si estraggono i dati utili rendendoli visionabili online





