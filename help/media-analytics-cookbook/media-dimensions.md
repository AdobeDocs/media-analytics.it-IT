---
title: Cos’è Media Stream Attribution?
description: Scoprite come collegare le azioni dell'applicazione ai dati di tracciamento dei supporti senza necessità di ulteriori regole di elaborazione e variabili personalizzate.
translation-type: tm+mt
source-git-commit: 901539a2095b23f9108a934eb61d182b14ccd9e8
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 3%

---


# Attribuzione flusso multimediale

Questa funzione consente di collegare le azioni dell’applicazione ai dati di tracciamento dei supporti senza la necessità di ulteriori regole di elaborazione e variabili personalizzate.

## Dimension multimediali esterni al tracciamento dei file multimediali

Con l&#39;attribuzione di Media Stream, i clienti possono ora aggiungere qualsiasi dimensione media
a tutte le altre chiamate di analisi, come visualizzazioni di pagina e collegamenti personalizzati. Durante l&#39;attuazione,
devi aggiungere i parametri dei dati contestuali ai dati multimediali alle chiamate di tracciamento di Analytics. Elenco completo
i parametri dei dati contestuali utilizzati per i supporti sono disponibili qui: [Parametri audio e video.](/help/metrics-and-metadata/audio-video-parameters.md)

Sarà inoltre necessario riabilitare la configurazione del tracciamento dei supporti dalla console di amministrazione per ogni rapporto per il quale si desidera abilitare questa funzione.

>[!NOTE]
>
>Le metriche relative ai supporti sono _non_ disponibili per l&#39;utilizzo al di fuori del tracciamento dei supporti, poiché la maggior parte di queste sono calcolate da Media Analytics in base agli eventi heartbeat. Inoltre, è importante che le metriche relative ai contenuti multimediali non vengano ingrandite da implementazioni diverse.

## Come

Nell&#39;esempio JavaScript riportato di seguito viene generata una chiamata di tracciamento dei collegamenti personalizzata con il nome impostato su &quot;Hero Banner&quot;.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Nel reporting di Analytics, puoi utilizzare il eVar `Show`  per suddividere i dati, e potrai contare le istanze dei collegamenti di tracciamento. Il rapporto sarà simile al seguente:

![](/assets/myShow-rpt-1.png)

## Casi di utilizzo

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
