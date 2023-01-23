---
title: Cos’è Media Stream Attribution?
description: Scopri come collegare le azioni dell’applicazione ai dati di tracciamento dei contenuti multimediali senza la necessità di ulteriori regole di elaborazione e variabili personalizzate.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '231'
ht-degree: 100%

---

# Attribuzione flusso multimediale {#media-stream-attribution}

Con l’attribuzione del flusso multimediale è possibile collegare le azioni dell’applicazione ai dati di tracciamento dei contenuti multimediali senza la necessità di ulteriori regole di elaborazione e variabili personalizzate.

## Dimensioni multimediali esterne al tracciamento dei contenuti multimediali

È possibile aggiungere dimensioni multimediali alle chiamate di Analytics, come visualizzazioni di pagina e collegamenti personalizzati. Durante l’implementazione, è necessario aggiungere i parametri dei dati contestuali multimediali alle chiamate di tracciamento di Analytics. Per visualizzare l’elenco completo dei parametri di dati contestuali disponibili utilizzati per gli elementi multimediali, consulta [Parametri audio e video.](/help/implementation/variables/audio-video-parameters.md)

Per abilitare questa funzione per un rapporto specifico, riattiva la configurazione di tracciamento dei contenuti multimediali da Admin Console.

>[!NOTE]
>
>Le metriche relative ai file multimediali _non_ sono disponibili per l’utilizzo al di fuori del tracciamento dei contenuti multimediali, poiché la maggior parte di esse è calcolata da Streaming Media Analytics in base agli eventi heartbeat. Inoltre, è importante che le metriche dei contenuti multimediali non siano gonfiate da implementazioni diverse.

## Utilizzo di Attribuzione flusso multimediale

L’esempio JavaScript seguente genera una chiamata di tracciamento del collegamento personalizzato con il nome impostato su “Hero Banner”.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Nella generazione rapporti di Analytics puoi utilizzare la eVar `Show` per suddividere i dati in modo da poter contare le istanze di tracciamento dei collegamenti. Il reporting sarà simile al seguente:

![](/assets/myShow-rpt-1.png)

## Casi di utilizzo

Gli esempi seguenti mostrano casi d’uso per i seguenti elementi:

* Posizionamento categoria
* Posizionamento Hero
* Coinvolgimento
* Abbonamenti

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
