---
title: Tracciamento delle dimensioni del supporto esterno
seo-title: Tracciamento delle dimensioni del supporto esterno
translation-type: tm+mt
source-git-commit: 5d20df537cd244a10f6c2e66cea622e98aa17a16

---


# Tracciamento delle dimensioni del supporto esterno

Questa funzione consente di collegare le azioni dell’applicazione ai dati di tracciamento dei supporti senza la necessità di ulteriori regole di elaborazione e variabili personalizzate.

I clienti possono ora aggiungere qualsiasi dimensione media a tutte le altre chiamate di analisi, come visualizzazioni di pagina e collegamenti personalizzati. Durante l'implementazione, devi aggiungere i parametri dei dati contestuali dei supporti alle chiamate di tracciamento di Analytics. L'elenco completo dei parametri dei dati contestuali utilizzati per gli elementi multimediali è disponibile qui: Parametri [audio e video.](/help/metrics-and-metadata/audio-video-parameters.md)

Sarà inoltre necessario riabilitare la configurazione del tracciamento dei supporti dalla console di amministrazione per ogni rapporto per il quale si desidera abilitare questa funzione.

>[!NOTE]
>Le metriche relative ai supporti _non_ sono disponibili per l'utilizzo al di fuori del tracciamento dei supporti, poiché la maggior parte di queste sono calcolate da Media Analytics
>basati su eventi heartbeat. Inoltre, è importante che le metriche relative ai contenuti multimediali non vengano ingrandite da implementazioni diverse.

## Come

Nell'esempio JavaScript riportato di seguito viene generata una chiamata di tracciamento dei collegamenti personalizzata con il nome impostato su "Hero Banner".

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Nella generazione dei rapporti di Analytics, puoi utilizzare la `Show` Var per suddividere i dati e contare le istanze dei collegamenti di tracciamento. Il rapporto sarà simile al seguente:

![](/assets/myShow-rpt-1.png)

## Casi d'uso

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
