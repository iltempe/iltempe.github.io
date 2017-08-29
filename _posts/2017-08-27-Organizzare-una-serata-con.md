---
layout: post
title:  "Organizzare una serata con 3 amici: Github, Jekyll e Travis"
date:   2017-08-27 09:00:00
categories: blog
tags:
  - opendata
  - opensource
  - civic hacking
  - tutorial
image: /assets/article_images/2017-08-27-Organizzare-una-serata-con/1.jpg
---
Da qualche giorno sto usando [Github ](https://github.com/)per sviluppare [JMAP](http://iltempe.github.io/jmap). Come già avuto modo di narrare [qui](http://iltempe.github.io/blog/2016/05/05/primi-passi-con-github.html), Github è una piattaforma molto utile per lo sviluppo in modo condiviso. Non solo per chi sviluppa software come me ma anche per chi fa progettualità in senso più lato. Consente infatti di risolvere il problema del "controllo versione" di un insieme di file su cui fate modifiche. Github integra nativamente in sè la funzione di pubblicazione di un sito web tramite le [Github Pages](https://pages.github.com/), avete cioè la possibilità di gestire un vostro repository come fosse un sito web che automaticamente verrà pubblicato in modo gratuito. Nel caso in cui stiate lavorando con l’ambiente [Jekyll](https://jekyllrb.com/), se il vostro repository è impostato come Github Pages il sito sarà automaticamente compilato e pubblicato. Infatti Jekyll è un ambiente usato per sviluppare siti web statici ossia siti che hanno necessità di una fase di “build” (costruzione) che deve esser fatta in un ambiente che provveda ad avere in sè tutto il necessario, oltre al vostro codice, per potere costruire il sito. Ecco le Github Pages sono un ambiente adeguato quindi per costruire un sito sviluppato in Jekyll, consentono di essere rapidi e sono la soluzione ideale se si vuole effettivamente avere controllo versione e build immediato del vostro progetto web. Per dettagli rimando a [questa guida](https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/).

Usando nel tempo questi due ambienti in modo un po’ più avanzato di renderete però conto dei limiti di questa soluzione specie se state effettivamente pensando di creare un vero e proprio progetto per cui sia richiesta non solo la fase di prototipazione ma anche, come accade spesso con i clienti, della fase di pubblicazione e qualifica di ciò che avete sviluppato. La qualifica è la fase che dimostra infatti che il vostro progetto è conforme ai criteri che voi stessi vi siete dati per accettare il vostro sviluppo, troppo spesso oggi viene sottovalutata specie in un settore (quello della tecnologia) dove si può realizzare in forma prototipale qualcosa molto rapidamente. La differenza la fa appunto un progetto ben qualificato.

Oltre al controllo versione e ad un semplice "build" del progetto avrete quindi necessità di un ambiente che vi consenta di gestire quello che normalmente è chiamato “deploy” del vostro sviluppo ossia la pubblicazione. Durante questa fase è possibile avere controllo completo di ciò che deve avvenire durante il build dell’applicazione ma anche di quelle che sono le fasi di qualifica e dei test che volete effettuare.

Ho trovato un ambiente che si chiama [Travis](https://travis-ci.org/) che si sposa perfettamente con gli strumenti Github Pages e Jekyll, nel senso che si integra con loro in modo piuttosto agevole e amplia le funzionalità quindi del vostro processo di deploy senza troppo sforzo. Tra le altre cose effettuare le operazioni di build su Travis vi consente di ovviare ad un paio di limitazioni delle Github Pages ovvero la possibilità di usare ogni tipo di plugin Jekyll (alcuni non sono compatibili con le Pages) e la possibilità di gestire variabili di ambiente che non volete pubblicare sul vostro repository Github pubblico.

Il flusso di lavoro che ho deciso di adottare è quindi:

1. Sviluppo in Jekyll e commit delle modifiche su un branch del progetto Github denominato "development".

2. Build e Qualifica dello sviluppo su Travis connesso al branch su cui si sviluppa al passo 1

3. Pubblicazione di quanto costruito al passo 2 sul branch principale del progetto Github (master) che è quello che è connesso alle Github Pages e consente di ospitare un sito web all’indirizzo: http://username.github.io/repo_name

![processo di produzione](/assets/article_images/2017-08-27-Organizzare-una-serata-con/2.jpg)

Come far incontrare una sera  quindi i vostri nuovi amici Jekyll, Github e Travis? Ecco le operazioni da seguire. Per tutti i dettagli potete guardare come ho impostato [il repository Github di JMAP](https://github.com/iltempe/jmap).  La seguente procedura presuppone che abbiate incontrato per lo meno una volta nella vita Github, Jekyll e Travis, se non è mai accaduto prima prendete un appuntamento singolarmente con ognuno di loro e poi tornate a questa pagina.

* Create su Github un "locale" dove far incontrare i tre amici. Trattasi di repository che usi le Github Pages. In questo “locale” dove sviluppare (in un branch che creerete voi e che chiamerete development) e dove archiviare il vostro prodotto finito (nel branch di default chiamato master). Per creare un branch fate riferimento a [questa guida](https://help.github.com/articles/creating-and-deleting-branches-within-your-repository/). Create una variabile Token nella pagina del vostro account Github "Settings > Personal access tokens"

* Nella vista di sviluppo potete preparare un tavolo con le bevute per la serata...ovvero potete inserire i sorgenti della prima versione del vostro sito committando i sorgenti che saranno quindi archiviati e versionati.

* Adesso dobbiamo comunicare a Travis come accedere al luogo dove si trova Github. Per farlo dovete loggarvi in Travis, selezionare il locale (repository) su Github che avete appena creato. Per fare questo dovrete settare le impostazioni del repository selezionato nel modo indicato sotto. I valori della variabile di ambiente GH_REF sarà "github.com/username/repository" e quello della variabile GH_TOKEN deve essere quello della variabile token creata al primo passo.

![travis settings](/assets/article_images/2017-08-27-Organizzare-una-serata-con/3.png)

* A questo punto inserite nel vostro repository Github un file di configurazione per l’amico Travis. E' denominato .travis.yml ed è il file che contiene "le indicazioni stradali" per arrivare al locale a cui Github lo attende. Il mio file spiega a Travis che deve recarsi da Github e prelevare i sorgenti nella vista di sviluppo, deve incontrare Travis per costruire il sito, ma poi deve riunirsi nuovamente con il sito costruito su Github nella vista master. In queste indicazioni avete anche spiegato a Travis come incontrarsi con Jekyll prima che il prodotto del vostro deploy sia inserito nel locale dove lo attende Github e le sue Pages per rendere il sito visibile online. L' esempio di file che ho fatto io è [quello sotto](https://github.com/iltempe/jmap/blob/development/.travis.yml) ma potete impostarlo anche da soli seguendo le istruzioni di [questa pagina](https://docs.travis-ci.com/user/customizing-the-build).

<script src="https://gist.github.com/iltempe/9656da6d124871bb498294804a7af9d2.js"></script>

Da questo momento in poi ogni volta che modificate i sorgenti nella vista *development* automaticamente Travis incontrerà Github per prelevarli, incontrerà Jekyll per costruire il vostro sito e poi nuovamente Github per pubblicarlo.

Considerate che il file di impostazione di Travis è il cuore del vostro processo di produzione e qualifica. E può essere impostato secondo tutte le operazioni che volete effettuare prima e dopo la costruzione del sito. Ad esempio è possibile eseguire degli script bash prima e dopo la costruzione del sito, oppure si può pensare di eseguire alcuni tool di validazione come [html proofer](https://github.com/gjtorikian/html-proofer). Alcune indicazioni per ampliare il vostro script di produzione e qualifica sono riportate [qui](http://jekyllrb.com/docs/continuous-integration/travis-ci/).

Buon lavoro!!

