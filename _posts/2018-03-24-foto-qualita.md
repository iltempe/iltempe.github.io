---
layout: post
title:  "Determinare la qualità di una strada dalle fotografie"
date:   2018-03-24 10:00:00
categories: blog
tags:
  - civic hacking
  - opencv
  - strade
  - image processing
image: /assets/article_images/2018-03-24-foto-qualita/strada2.jpg
---

Avvertenza: il presente tutorial ha come fonte [questo](https://medium.com/a-r-g-o/classifying-nyc-bike-lane-quality-with-image-processing-and-computer-vision-in-python-76b13147ec2d), ma non è una sua copia quanto piuttosto un riadattamento per comprenderne le basi teoriche che ci stanno alla base. Necessita di una minimo di informazioni tecniche di base sulla teoria dell'informazione, intesa come approccio matematico a come le informazioni possono essere elaborate estraendole da una qualunque fonte o canale di comunicazione. Negli ultimi anni ricavare informazioni dalle immagini digitalizzate (computer vision) si è affermata come una metodologia che ha preso sempre più campo e che ha consentito piano piano la creazione di vere e proprie professioni nell'ambito. Qui a me interessa dimostrare come l'ingegneria dell'informazione applicata ad un caso pratico (ovvero la fotografia delle stade delle nostre città) ci consente con un po' di programmazione python di ricavare un dato utile sulla qualità dell'asfalto stesso. Se poi questo tutorial lo combinate [a quest'altro tutorial](http://www.iltempe.it/blog/2017/12/30/dati-dalle-foto.html) capite che di tutto questo si può fare dato georiferito a partire esclusivamente dalle foto.

Per chi volesse approfondire il tema della teoria dell'informazione rimando a [Wikipedia](https://it.wikipedia.org/wiki/Teoria_dell%27informazione) per iniziare. Si può poi approfondire cosa sia la [computer vision](https://it.wikipedia.org/wiki/Visione_artificiale) specificamente per l'interpretazione delle immagini.

Il linguaggio usato è python 3, ma solo perchè fornisce già tutta una serie di strumenti pronti per interpretare le immagini e usarle come fonte di dati utili. Ad esempio qui si usa [opencv](https://opencv.org/) e [scipy](https://www.scipy.org/) libreri di cui consiglio lo studio prima di cimentarvi in questo campo. Non è necessario conoscere tutto la teorica che c'è dietro ad ogni singolo strumento ma per lo meno comprendere cosa ci si può fare e come ogni funzione delle librerie può tornare utile..

Il punto di partenza sono delle immagini scattate all'asfalto delle vostre strade. Potete usare un normale smartphone per farlo, meglio se abilitate la localizzazione mentre lo fate, oppure anche una fotocamera più costosa. Per comodità ho usato un notebook ipython, ma potete lavorare a riga di comando. L'algoritmo seguente non fa altro che estrarre un punteggio tanto più alto quanto più difetti dell'asfalto sono identificati. Di seguito trovate il codice commentato.

Istruzioni per importare le librerie python. Definizione di una funzione per mostrare le immagini durante l'analisi. Lettura dell'immagine da file .jpg


```python
import numpy as np
import scipy.ndimage as nd
import imageio
import cv2
from matplotlib import pyplot as plt
%matplotlib inline

def mostra_immagine(img, titolo):
    plt.imshow(img)
    plt.title(titolo)
    plt.show()

img = imageio.imread("/Users/TeoPro/Desktop/strade/strada4.jpg")
mostra_immagine(img, "foto")
```


![png](/assets/article_images/2018-03-24-foto-qualita/output_1_0.png)


E' necessario ritagliare l'immagine in modo che resti solo una parte dell'asfalto interessante per l'analisi. Per fare questo in questo caso si taglia metà dell'immagine (quella sottostante) rimuovendo la parte alta ed i lati della strada, viene anche rimosso un 10% della parte inferiore dell'immagine. Variando sui parametri si può fare tagli in modo diverso sulla base della modalità delle acquisizioni fatte.


```python
nrow, ncol = img.shape[:2]
img = img[nrow//2:(nrow-nrow//10),:,:]
mostra_immagine(img, "foto")
```


![png](/assets/article_images/2018-03-24-foto-qualita/output_3_0.png)


E' necessario l'applicazione di un sistema di filtraggio per la riduzinone del rumore dell'immagine.


```python
md = nd.filters.median_filter
md_blurPhoto = md(img, 5)
mostra_immagine(md_blurPhoto, "foto")
```


![png](/assets/article_images/2018-03-24-foto-qualita/output_5_0.png)


E' necessario convertire l'immagine da formato RGB a formato HSV in modo da rendere i difetti facilmente riconoscibili.


```python
lower = np.array([0, 10, 50])
upper = np.array([360, 100, 100])
hls = cv2.cvtColor(md_blurPhoto, cv2.COLOR_BGR2HSV)
mask = cv2.inRange(hls, lower, upper)
res = cv2.bitwise_and(hls, hls, mask = mask)
mostra_immagine(res, "foto")
```


![png](/assets/article_images/2018-03-24-foto-qualita/output_7_0.png)


A questo punto si devono detettare i difetti rimasti, ridurre il rumore attorno ad essi mantenendo le linee oltre una soglia di rumore. Al termine dell'analisi' è possibile quantificare il punteggio di difetti presenti.


```python
#detezione dei difetti (linee) rimasti in modo da poter estrarre i difetti dell'asfalto
edges_cv = cv2.Canny(res, 200, 400)

#riduzione rumore attorno alle linee
blurred_edges = cv2.GaussianBlur(edges_cv,(3,3),0)

#mantenere le linee oltre una certa soglia di rumore
bdilation = nd.morphology.binary_dilation
berosion = nd.morphology.binary_erosion
edges_cv_2 = bdilation(berosion(blurred_edges, iterations=2), iterations=2)

mostra_immagine(edges_cv_2, "foto")

defect_score = edges_cv_2.mean()
defect_score
```


![png](/assets/article_images/2018-03-24-foto-qualita/output_9_0.png)



    0.0759078429437279


