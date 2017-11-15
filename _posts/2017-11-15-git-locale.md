---
layout: post
title:  "Tenere traccia delle modifiche del proprio lavoro sul proprio PC"
date:   2017-11-15 10:00:00
categories: blog
tags:
  - git
  - civic hacking
  - pa
image: /assets/article_images/2017-11-15-git-locale/1.jpeg
---

Oggi un brevissimo tutorial sulla possibilità di tenere traccia costante del proprio lavoro per un progetto usando esclusivamente il proprio PC.

Il concetto che sta alla base del tutorial è il seguente: vi è mai capitato di lavorare ad un progetto per molto tempo? e di dover tenere traccia nel tempo di "cosa e come" modificate di quel progetto? Non sto solo parlando di codice sorgente ma anche solo di testo. A me capita spesso. Certo tool come [Github](www.github.com) sono l'ideale per memorizzare quotidianamente il proprio mestiere e, se si può pubblicare costantemente il proprio lavoro per condividerlo, effettivamente questi sistemi di archiviazione del proprio lavoro sono l'ottimo perché consentono di tracciare le modifiche fatte ogni giorno e di archiviare contemporaneamente tutto.

Ma se il vostro progetto non è pubblicabile... come fare? E come gestirlo se ancora non è in una forma definitiva? Il principio è piuttosto semplice e si basa su [git](https://medium.com/@iltempe/sviluppare-in-modo-collaborativo-come-si-usa-git-fbe9817b5bf4)  (lo stesso strumento che sta alla base di Github). Il tool git è come detto più volte un sistema di controllo versionamento del proprio lavoro, tiene cioè traccia delle modifiche che si realizzano al proprio testo. Normalmente lo si usa in modo condiviso installando il controllo in modo "centralizzato" su un server, ma la cosa interessante che ho voluto sperimentare in questi giorni è che il tool può essere usato anche sul proprio PC (da soli)  con il solo scopo di non perdere la storia di quanto fatto. Chi non ha quindi un server può provare ad usare git per imparare ad usarlo ed iniziare ad usarlo sui progetto in cui non ha bisogno di collaborare con altre persone. Come si fa quindi? Semplice.

1. Installate Git. [Qui](https://git-scm.com/book/it/v1/Per-Iniziare-Installare-Git) una buona guida in italiano per farlo in base al vostro sistema operativo.

2. Create un utente in questo modo (qui è creato l'utente tempe ma potete chiamarlo come volete)

   ```
   $ sudo adduser tempe
   ```

3. Digitate la password nel momento in cui vi viene richiesta e procedete

4. Andate nel terminale e digitate

   ```
   $ su tempe
   ```

5. Inserire la password e digitate di seguito

```
$ cd ~
```

6. Adesso create un archivio (repository) ed inizializzatelo

   ```
   $ mkdir progetto1
   $ cd progetto1
   $ git --bare init
   ```

   Adesso potete uscire da GIT digitando

   ```
   $ exit
   ```

7. Posizionatevi nella cartella dove volete lavorare al vostro progetto

   ```
   $ mkdir progetto1
   $ cd progetto1
   ```

8. Inizializzate git a lavorare nella vostra cartella e aggiungete un file README

   ```
   $ git init
   $ touch README
   $ git add README
   $ git commit -m "Adding README file" README
   [master (root-commit) f6f5b10] Adding README file
   0 files changed
   create mode 100644 README
   ```

   Se adesso provate a fare un commit del vostro file nel sistema di versionamento otterrete un errore in quanto ancora non avete configurato "il luogo" dove controllare le modifiche fatte.

   ```
   $ git pushfatal: No configured push destination.Either specify the URL from the command-line or configure a remote repository using

   ​```
   git remote add
   ​```

   and then push using the remote name
   ```

   ​

9. A questo punto basta configurare il controllo sul vostro PC (in locale) e avete fatto.

   ```
   $ git remote add origin tempe@localhost:progetto1
   $ git push origin master
   ```

Adesso avete terminato ed effettuando il commit e push delle modifiche del vostro progetto terrete traccia del vostro lavoro sul vostro PC. [Qui](https://medium.com/@iltempe/sviluppare-in-modo-collaborativo-come-si-usa-git-fbe9817b5bf4) una semplice guida fatta da me dei comandi base di GIT.

In bocca a lupo!!