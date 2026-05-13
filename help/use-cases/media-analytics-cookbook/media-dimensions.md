---
title: Cos’è Media Stream Attribution?
description: Scopri come collegare le azioni dell’applicazione ai dati di tracciamento dei contenuti multimediali senza la necessità di ulteriori regole di elaborazione e variabili personalizzate.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/G0RufpSDBB65tr4XJRvPU2keKgKxv1uDviyhqzxEVD4
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e4f5f438-eabb-4c54-9133-b817e3d125f5id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 215
ht-degree: 87%

---

# Attribuzione flusso multimediale {#media-stream-attribution}

Con l’attribuzione del flusso multimediale è possibile collegare le azioni dell’applicazione ai dati di tracciamento dei contenuti multimediali senza la necessità di ulteriori regole di elaborazione e variabili personalizzate.

## Dimensioni multimediali esterne al tracciamento dei contenuti multimediali

È possibile aggiungere dimensioni multimediali alle chiamate di Analytics, come visualizzazioni di pagina e collegamenti personalizzati. Durante l’implementazione, è necessario aggiungere i parametri dei dati contestuali multimediali alle chiamate di tracciamento di Analytics.

Per abilitare questa funzione per un rapporto specifico, riattiva la configurazione di tracciamento dei contenuti multimediali da Admin Console.

>[!NOTE]
>
>Le metriche dei contenuti multimediali sono _not_ disponibili per l&#39;utilizzo al di fuori del tracciamento dei contenuti multimediali, poiché la maggior parte di esse è calcolata dai servizi multimediali in streaming in base a eventi heartbeat. Inoltre, è importante che le metriche dei contenuti multimediali non siano gonfiate da implementazioni diverse.

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
