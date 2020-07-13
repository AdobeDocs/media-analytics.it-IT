---
title: Attribuzione flusso multimediale
description: null
translation-type: tm+mt
source-git-commit: cab9724476f7864ac23c4293e402e0443771cb1e
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 4%

---


# Attribuzione flusso multimediale

Questa funzione consente di collegare le azioni dell’applicazione ai dati di tracciamento dei supporti senza la necessità di ulteriori regole di elaborazione e variabili personalizzate.

## Tracciamento delle dimensioni del supporto esterno

Con Attribuzione flusso multimediale, i clienti possono ora aggiungere qualsiasi dimensione media a tutte le altre chiamate di analisi, come visualizzazioni di pagina e collegamenti personalizzati. Durante l’implementazione, devi aggiungere i parametri dei dati contestuali ai  chiamate di tracciamento Analytics. L&#39;elenco completo dei parametri dei dati contestuali utilizzati per gli elementi multimediali è disponibile qui: [Parametri audio e video.](/help/metrics-and-metadata/audio-video-parameters.md)

Sarà inoltre necessario riabilitare la configurazione del tracciamento dei supporti dalla console di amministrazione per ogni rapporto per il quale si desidera abilitare questa funzione.

>[!NOTE]
>
>Le metriche relative ai supporti _non_ sono disponibili per l&#39;utilizzo al di fuori del tracciamento dei supporti, perché la maggior parte di queste vengono calcolate da Media  Analytics in base agli eventi heartbeat. Inoltre, è importante che le metriche relative ai contenuti multimediali non vengano ingrandite da implementazioni diverse.

## Come

Nell&#39;esempio JavaScript riportato di seguito viene generata una chiamata di tracciamento dei collegamenti personalizzata con il nome impostato su &quot;Hero Banner&quot;.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

 rapporto Analytics, puoi utilizzare la `Show` Var per suddividere i dati e contare le istanze dei collegamenti di tracciamento. Il rapporto sarà simile al seguente:

![](/assets/myShow-rpt-1.png)

## Casi d’uso

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)

