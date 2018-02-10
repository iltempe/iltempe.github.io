---
layout: post
title:  "Usare le immagini satellitari per analizzare come cambia una città nel tempo"
date:   2018-02-02 10:00:00
categories: blog
tags:
  - opendata
  - satellitari
  - opendata
  - civic hacking
  - iptyhon
  - copernicus
image: /assets/article_images/2018-02-10-sentinel-hub/4.jpg
---

Premessa: Il post serve per spiegare che si può creare effettivamente servizi (anche a pagamento) a partire dai dati pubblici (ad esempio quelli di [Copernicus](http://www.copernicus.eu/) ma non solo) ed anche l'uso che se ne può fare per monitorare le nostre città.

[Sentinel Hub](https://www.sentinel-hub.com/) è un servizio che vi consente [in questa pagina](https://apps.sentinel-hub.com/sentinel-playground/) di navigare da browser e visualizzare le acquisizioni satellitari di una certa area geografica del mondo usando una serie di filtri che consentano di evidenziare alcune aree piuttosto che altre, si può ad esempio mettere in risalto i corsi d'acqua o le zone verdi della terra.

![](/assets/article_images/2018-02-10-sentinel-hub/2.png)
![](/assets/article_images/2018-02-10-sentinel-hub/3.png)


Il servizio è un servizio che vi consente inoltre di sviluppare la vostra applicazione attivando una trial gratuita di accesso ai dati satellitari in modo pittosto semplice e usando programmazione python e che ha già un modo di visualizzare le immagini e scaricarle (a scopo di prova) in modo gratuito. Chi poi volesse usare le fonti in modo serio può far riferimento ai questi [costi](https://www.sentinel-hub.com/pricing-plans)

Mi sono quindi cimentato nel riuso delle immagini satellitari per provare a vedere le acquisizioni fatte sulla città di Prato in un certo lasso di tempo.

Dopo aver registrato un account trial di prova configurate un'applicazione in [questa pagina](https://apps.sentinel-hub.com/configurator/#/configurations/) vi viene fornito un codice chiamato "Service end-points" da inserire nel vostro codice. Il codice seguente è piuttosto commentato e si comprende bene, il risultato è che le immagini che vengono trovate nel tempo che avete impostato sono scaricate sul vostro computer in formato PNG e possono essere analizzate.

Fonte http://sentinelhub-py.readthedocs.io/en/latest/examples/ogc_request.html#Imports
configuazione e import, la configurazione dell'applicazione deve essere fatta qui https://apps.sentinel-hub.com/configurator/#/ inserendo INSTANCE_ID che viene fornito


```python
INSTANCE_ID = 'XXXXXXXXXXXXXX'
%reload_ext autoreload
%autoreload 2
%matplotlib inline
import matplotlib.pyplot as plt
import numpy as np
import datetime
from sentinelhub.data_request import WmsRequest, WcsRequest
from sentinelhub.constants import MimeType
from sentinelhub.common import BBox, CRS
```

Disegnare l'immagine in colore RGB e mostrarla.


```python

def plot_image(data, factor=1):
    fig = plt.subplots(nrows=1, ncols=1, figsize=(15, 7))
    rgb = np.zeros(data.shape, dtype=np.float32)
    rgb[..., 0] = data[..., 2]
    rgb[..., 1] = data[..., 1]
    rgb[..., 2] = data[..., 0]
    plt.imshow(rgb*factor)
```

Definizione dell area geografica da monitorare, nel mio caso Prato.


```python
prato_coords_wgs84 = [43.9351, 11.0004, 43.8327, 11.1681]
prato_bbox = BBox(bbox=prato_coords_wgs84,crs=CRS.WGS84)
```

Configurazione della richiesta dei dati satellitari.


```python
wms_true_color_request = WmsRequest(data_folder='immagini',
                                    layer='TRUE-COLOR',
                                    bbox=prato_bbox,
                                    time=('2018-01-01', '2018-01-31'),
                                    width=1000, height=1000,
                                    maxcc=0.2,
                                    instance_id=INSTANCE_ID)
```

Richiesta dei dati al servizio e salvataggio delle immagini.


```python
wms_true_color_img = wms_true_color_request.get_data()
wms_bands_img = wms_true_color_request.save_data()
```


```python
print('Ci sono %d immagini di Sentinel-2 disponibili con una copertura nuvole inferiore al %1.0f%%.' % (len(wms_true_color_img), wms_true_color_request.maxcc * 100.0))
```

    Ci sono 1 immagini di Sentinel-2 disponibili con una copertura nuvole inferiore al 20%.



```python
plot_image(wms_true_color_img[-1], 1./255)
```


![png](/assets/article_images/2018-02-10-sentinel-hub/1.png)



```python
print('Le %d immagini prelevate hanno queste date:' % len(wms_true_color_img))
for index, date in enumerate(wms_true_color_request.get_dates()):
    print(' - image %d was taken on %s' % (index, date))
```

    Le 1 immagini prelevate hanno queste date:
     - image 0 was taken on 2018-01-24 10:13:52

