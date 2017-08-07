---
layout: post
title:  "Creare dati dai post di un sito Jekyll"
date:   2017-08-07 10:34:25
categories: blog
tags:
  - opendata
  - web design
  - jekyll
image: /assets/article_images/2017-08-07-creare-dati-da-un-sito-web/1.jpeg
---

In [questo post](https://iltempe.github.io/blog/2017/08/05/generare-siti-da-dataset.html) abbiamo visto come generare contenuti web a partire dai dati. Oggi vediamo un esempio di processo contrario, ovvero come generare dati dai contenuti web.

Con [Jekyll](https://jekyllrb.com/) è infatti possibile generare un file di dati relativi al sito in formato JSON in modo piuttosto semplice e automatico. Come? Seguite questi passaggi.

- Creare un file dal nome site.json e salvatelo nella root del vostro sito
- Inseriteci questo codice

<script src="https://gist.github.com/iltempe/3bc085abcd82782abdb2d883190f08eb.js"></script>

Fatto.

Adesso presso l'indirizzo "root/site.json" state generando i dati del vostro sito in formato JSON. Metodo semplice ma efficace nel caso si voglia generare dati oppure creare un "punto di aggancio" per caricare contenuti del sito in modo dinamico.
