---
title: Cos’è Media Stream Attribution?
description: Scopri come collegare le azioni dell’applicazione ai dati di tracciamento dei contenuti multimediali senza la necessità di ulteriori regole di elaborazione e variabili personalizzate.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 3%

---

# Attribuzione flusso multimediale

Questa funzione ti consente di collegare le azioni dell’applicazione ai dati di tracciamento dei contenuti multimediali senza la necessità di ulteriori regole di elaborazione e variabili personalizzate.

## Dimension multimediali esterni al tracciamento dei file multimediali

Con Media Stream Attribution, i clienti sono ora in grado di aggiungere qualsiasi dimensione per i contenuti multimediali.
a tutte le altre chiamate di analytics, come visualizzazioni di pagina e collegamenti personalizzati. Durante l&#39;attuazione,
devi aggiungere i parametri dei dati contestuali multimediali alle chiamate di tracciamento di Analytics. Elenco completo
i parametri dei dati contestuali utilizzati per i file multimediali sono disponibili qui: [Parametri audio e video.](/help/metrics-and-metadata/audio-video-parameters.md)

Sarà inoltre necessario riabilitare la configurazione del tracciamento dei contenuti multimediali da Admin Console per ogni rapporto per il quale desideri abilitare questa funzione.

>[!NOTE]
>
>Le metriche dei file multimediali sono _non_ disponibili per l’uso al di fuori del tracciamento dei contenuti multimediali, perché la maggior parte di queste sono calcolate da Media Analytics in base a eventi heartbeat. Inoltre, è importante che le metriche dei contenuti multimediali non siano gonfiate da implementazioni diverse.

## Come

L’esempio JavaScript seguente genera una chiamata di tracciamento Custom Link con il nome impostato su &quot;Hero Banner&quot;.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Nel reporting di Analytics, puoi utilizzare l’ `Show` eVar per suddividere i dati e contare le istanze del collegamento di tracciamento. Il rapporto sarà simile al seguente:

![](/assets/myShow-rpt-1.png)

## Casi di utilizzo

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
