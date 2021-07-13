---
title: Informazioni sul tracciamento dello stato del lettore
description: Scopri la funzione di tracciamento dello stato del lettore, compresi i requisiti e le linee guida per l’implementazione e il reporting degli stati del lettore.
exl-id: c678e182-74e4-4f46-8596-7be57e645c66
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---

# Informazioni sul tracciamento dello stato del lettore

Per ottimizzare l’esperienza dei prodotti e il valore delle unità aziendali, è importante comprendere il comportamento dei clienti durante la visualizzazione dei video. Ciò include il tempo trascorso all&#39;interno di diversi stati di riproduzione.  È anche importante avere la flessibilità di creare e misurare nuovi stati e eventi di giocatore in base alle esigenze.

Il tracciamento dello stato del lettore consente di acquisire l’interazione del visualizzatore durante la riproduzione utilizzando un set standard di variabili della soluzione per schermo intero, sottotitoli, muto, immagine nell’immagine e messa a fuoco.  Il tracciamento dello stato del lettore offre anche la flessibilità necessaria per creare stati di lettore personalizzati. Puoi utilizzare le variabili di tracciamento dello stato del lettore per il reporting in Analysis Workspace.

Per acquisire le modifiche allo stato del lettore, il tracciamento dello stato del lettore aggiorna i metadati della misurazione video. Ad esempio, per determinare il coinvolgimento &quot;vero&quot; del video, il tracciamento dello stato del lettore misura il tempo trascorso con il suono acceso rispetto alle visualizzazioni video passive o non impegnate quando il suono è spento o il tempo trascorso in modalità Normale rispetto a Schermo intero.

Il tracciamento dello stato del lettore offre i seguenti vantaggi:

* Fornisce variabili standard che misurano gli stati comuni come schermo intero o sottotitoli codificati
* Fornisce variabili personalizzabili per misurare gli stati personalizzati durante una sessione di riproduzione
* Misura il tempo trascorso all&#39;interno di uno stato del lettore personalizzato
* Misura più stati che possono essere simultanei

![Tracciamento dello stato del lettore](assets/player_state_tracking.png)

## Requisiti

Il tracciamento dello stato del lettore richiede uno dei seguenti elementi per la raccolta dati:
* Media JS SDK 3.0+
* Chromecast 3.0 SDK per soluzioni Adobe Marketing Cloud
* Estensione Media Analytics (per l&#39;utilizzo con l&#39;SDK Adobe Experience Platform (AEP))
   * Web: Adobe Medium Analytics (3.x SDK) for Audio and Video v1.0+
   * Mobile: Adobe Medium Analytics for Audio and Video v2.0+
* API Media Collection

## Linee guida

Prima di implementare il tracciamento dello stato del lettore, considera le seguenti linee guida.

* Lo stato del lettore viene calcolato in tutti gli stati di riproduzione (nessuna suddivisione).
* È possibile misurare più stati del lettore contemporaneamente.
* Il numero massimo di stati del lettore che è possibile tracciare durante una riproduzione è 10.
* Le metriche dello stato del lettore vengono inviate ad Analytics per la generazione di rapporti solo sulla chiamata Media Close.
* La conoscenza dello stato dell’applicazione non viene mantenuta dopo l’arresto di uno stato. Al termine di uno stato, è necessario riavviare lo stato per continuare il tracciamento. Per ogni nuovo stato di riproduzione, è necessario riavviare lo stato del lettore.
* Gli stati del lettore vengono acquisiti per ogni singola sessione di riproduzione; lo stato del lettore non viene calcolato tra i riproduzioni.
