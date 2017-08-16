---
layout: post
title:  "Un generatore di mappe opensource"
date:   2017-08-16 09:00:00
categories: blog
tags:
  - opendata
  - web design
  - jekyll
  - opensource
  - github
image: /assets/article_images/2017-08-16-un-generatore-di-mappe-opensource/1.jpg
---

Dopo aver studiato [Jekyll](https://jekyllrb.com/) in questi mesi, mi sono reso conto che la potenza di questo ambiente è la possibilità di personalizzarlo completamente per uno scopo specifico.

Ho quindi provato a mettere in piedi un progetto nuovo completamente basato su Jekyll. Si chiama [JMAP](https://iltempe.github.io/jmap/) ed è un progetto per generare mappe in moto "semiautomatico" a partire da dataset.

Il progetto nasce da un "sito base" fatto jekyll al cui interno ho creato una ["collezione"](https://jekyllrb.com/docs/collections/) denominata maps. Leggendo cosa sono le collezioni si capisce bene come mai è importante usarle, in sostanza vi basti sapere che al posto dei post di un normale blog ho creato un oggetto "mappa" che diventa l'elemento base del sito di mappe che andremo a generare.

![](/assets/article_images/2017-08-16-un-generatore-di-mappe-opensource/2.png)

La collezione "mappe" è costituita da un insieme di file .md con un header che definisce per ogni mappa una serie di metadati necessari al generatore di mappe. Tra questi metadati compare anche una voce "dataset" che indica quale file di dati in jekyll è il file sorgente della mappa che si vuole elaborare.

Una volta impostato il motore, per aggiungere una mappa al vostro sito vi sarà sufficiente:

  - Inserire un file .md nella cartella maps con il formato definito dal template
  - Inserire un file nella folder _data contenente i dati da mappare

I file dei dataset devono essere i [formati compatibili con Jekyll](https://jekyllrb.com/docs/datafiles/) e devono avere almeno due colonne che contengono la latitudine e la longitudine del punto che si vuole mappare.

Il tutto si basa su una versione di jekyll usabile anche tramite le [Github Pages](https://pages.github.com/), quindi è sufficiente fare un fork del mio progetto su Github ed editarlo direttamente online per implementarne nuove funzionalità e personalizzarlo.

![](/assets/article_images/2017-08-16-un-generatore-di-mappe-opensource/3.png)

Attualmente sono inserite nel framework tre mappe di esempio, il progetto però è solo all'inizio e cerca [su github](https://github.com/iltempe/jmap) la collaborazione di tutti per ampliarlo, non tanto in termini di mappe quanto in termini di funzionalità. Che aspetti a darmi una mano? Aspetto i tuoi suggerimenti, i tuoi issue e le tue pull request!
