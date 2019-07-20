---
seo-title: Percorsi di implementazione
title: Percorsi di implementazione
uuid: 8400 c 938-e 77 e -4 c 88-b 23 b -5 f 5977 a 5316 c
translation-type: tm+mt
source-git-commit: ca7e63d9af1f84c7d5d620c72df5f62555f68c03

---


# Implementation Paths {#implementation-paths}

Media Analytics (Heartbeats) è la soluzione video standardizzata di Adobe. Ha sostituito il vecchio modello Milestone di Adobe.

Per ognuno di questi percorsi di implementazione, i clienti devono contattare il proprio rappresentante vendite/Account Manager per firmare un nuovo ordine di vendita in quanto Media Analytics dispone di un SKU univoco e le modifiche da un modello di tariffazione in base alle chiamate del server a un modello in base ai flussi video:

* **Lato client -** Sono integrazioni solo per Media Analytics. Potete scegliere Video Heartbeat SDK e/o le integrazioni API di Media Collection. Questo percorso può essere usato in qualsiasi lettore video, inclusi lettori di clienti e/o OVP quali Brightcove, Ooyala, theplatform e così via.

   If Media Analytics is your intended path, see the [Media SDK Implementation](../../sdk-implement/setup/setup-overview.md) and the [Media Collection API.](../../media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Per utilizzare Media Analytics, i clienti devono utilizzare anche Adobe Analytics.

* **Adobe Experience Platform Launch -** Adobe Experience Platform Launch, il prodotto di follow-on per Gestione tag dinamica, offre un'estensione Lancio di Media Analytics che semplifica l'implementazione di tracciamento video nei tuoi lettori.

   You can learn more about Experience Platform Launch here: [Adobe Media Analytics for Audio and Video Extension](https://docs.adobelaunch.com/extension-reference/web/adobe-media-analytics-for-audio-and-video-extension)
* **Adobe Primetime:** Adobe Primetime è una soluzione Adobe Experience Cloud che consente a programmatori e distributori di contenuto di monetizzare i contenuti multimediali su ogni schermo connesso.

   Primetime elimina la complessità di raggiungere, monetizzare e attivare audience globali tra dispositivi fornendo una piattaforma modulare per la pubblicazione di video, la pubblicità, la personalizzazione e l'analisi. Inoltre, Primetime offre soluzioni e valori intorno a quanto segue:

   * Supporto per misurare con precisione i tipi di contenuto lineare e VOD.
   * Supporto per misurare interruzioni di annunci pubblicitari con l'inserimento dinamico degli annunci.
   * Il modello di inserimento annunci di TVSDK consente analisi che misurano direttamente la riproduzione degli annunci, aumentando l'accuratezza.
   * Un set robusto di eventi e metadati per garantire precisione nel buffering di qos o nelle interruzioni di connessione mobile, come i problemi e le interazioni degli utenti finali, come la ricerca, la pausa e l'implementazione su dispositivi mobili.
   * Supporto integrato per Nielsen DTVR (lineare) con metadati ID 3 e DCR con metadati CMS.
   TVSDK è già integrato con l'SDK di Media Analytyics (Heartbeats), che rende l'implementazione molto più semplice e veloce su tutte le piattaforme supportate. Primetime supporta anche la partnership con Nielsen. To leverage Primetime, follow the same guidelines and prerequisites found in [Client-side](../../intro-to-ava/implementation-paths/client-side-path.md) along with the following docs for your platform(s): [Primetime User Guide.](https://helpx.adobe.com/primetime/user-guide.html)

   Dovreste anche contattare il rappresentante vendite/Account Manager per discutere cosa dovete fare per acquistare TVSDK.
