---
title: Cos’è Media Stream Attribution?
description: Scopri come collegare le azioni dell’applicazione ai dati di tracciamento dei contenuti multimediali senza la necessità di ulteriori regole di elaborazione e variabili personalizzate.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '231'
ht-degree: 100%

---

# Attribuzione flusso multimediale

Questa funzione ti consente di collegare le azioni dell’applicazione ai dati di tracciamento dei contenuti multimediali senza la necessità di ulteriori regole di elaborazione e variabili personalizzate.

## Dimensioni multimediali esterne al tracciamento dei file multimediali

Con Media Stream Attribution, i clienti possono ora aggiungere qualsiasi dimensione multimediale
a tutte le altre chiamate di analisi, come le visualizzazioni di pagina e i collegamenti personalizzati. Durante l’implementazione,
devi aggiungere i parametri dei dati contestuali multimediali alle chiamate di tracciamento di Analytics. L’elenco completo
dei parametri dei dati contestuali utilizzati per gli elementi multimediali è disponibile qui: [Parametri audio e video.](/help/metrics-and-metadata/audio-video-parameters.md)

Sarà inoltre necessario riabilitare la configurazione del tracciamento dei contenuti multimediali da Admin Console per ogni rapporto per il quale desideri avere disponibile questa funzione.

>[!NOTE]
>
>Le metriche relative ai file multimediali sono _non_ disponibili per l’utilizzo al di fuori del tracciamento dei contenuti multimediali, poiché la maggior parte di esse è calcolata da Media Analytics in base a eventi heartbeat. Inoltre, è importante che le metriche dei contenuti multimediali non siano gonfiate da implementazioni diverse.

## Come fare

L’esempio JavaScript seguente genera una chiamata di tracciamento dei collegamenti personalizzati con il nome impostato su “Hero Banner”.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Nella generazione rapporti di Analytics puoi utilizzare la eVar `Show` per suddividere i dati in modo da poter contare le istanze di tracciamento dei collegamenti. Il reporting sarà simile al seguente:

![](/assets/myShow-rpt-1.png)

## Casi di utilizzo

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
