---
title: Scopri come tracciare la riproduzione di base utilizzando JavaScript 2.x
description: Scopri come implementare il tracciamento di base utilizzando Media SDK in un browser che utilizza le app JavaScript 2.x.
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
exl-id: d8af37a0-9048-4e6b-8cba-809386cbed5f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/efxauhuL5aOcMQhSuayeodzUOtgfppMgZTAiwTiHsEE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 693
ht-degree: 99%

---

# Tracciare la riproduzione di base in JavaScript 2.x{#track-core-playback-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l’implementazione negli SDK 2.x.

>[!IMPORTANT]
>Se stai implementando una versione 1.x di SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK](/help/getting-started/download-sdks.md)

1. **Configurazione del tracciamento iniziale**

   Identifica quando l’utente attiva l’intenzione di riproduzione (l’utente fa clic su play e/o l’esecuzione automatica è attiva) e crea un’istanza `MediaObject`.

   [API createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nome variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome file multimediale | Sì |
   | `mediaid` | Identificatore univoco del file multimediale | Sì |
   | `length` | Lunghezza del file multimediale | Sì |
   | `streamType` | Tipo di flusso (vedi _Costanti StreamType_ sotto) | Sì |
   | `mediaType` | Tipo di file multimediale (vedi _Costanti MediaType_ sotto) | Sì |

   **`StreamType`Costanti:**

   | Nome costante | Descrizione   |
   |---|---|
   | `VOD` | Tipo di flusso per Video on Demand. |
   | `LIVE` | Tipo di flusso per il contenuto LIVE. |
   | `LINEAR` | Tipo di flusso per contenuti LINEAR. |
   | `AOD` | Tipo di flusso per audio on-demand. |
   | `AUDIOBOOK` | Tipo di flusso per audiolibro. |
   | `PODCAST` | Tipo di flusso per podcast. |

   **`MediaType`Costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di file multimediale per flussi Audio. |
   | `Video` | Tipo di file multimediale per i flussi Video. |

   ```
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,
                                     MediaHeartbeat.StreamType.VOD,
                                     <MEDIA_TYPE>);
   ```

1. **Allega metadati**

   Facoltativamente, allega oggetti metadati standard e/o personalizzati alla sessione di tracciamento tramite variabili di dati di contesto.

   * **Metadati standard**

     [Implementazione dei metadati standard in JavaScript](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)

     >[!NOTE]
     >
     >Il collegamento dell’oggetto metadati standard all’oggetto multimediale è facoltativo.

      * Riferimento API per le chiavi di metadati multimediali: [Chiavi di metadati standard - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

   * **Metadati personalizzati**

     Crea un oggetto variabile per le variabili personalizzate e compila i dati per questo elemento multimediale. Ad esempio:

     ```js
     /* Set custom context data */
     var customVideoMetadata = {
         isUserLoggedIn: "false",
         tvStation: "Sample TV station",
         programmer: "Sample programmer"
     };
     ```

1. **Tracciare l’intenzione di inizio riproduzione**

   Per iniziare a tracciare una sessione multimediale, chiama `trackSessionStart` sull’istanza Media Heartbeat:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >Il secondo valore è il nome dell’oggetto metadati multimediali personalizzati creato al passaggio 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni di riproduzione dell’utente, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare dati/metadati e per stimare la metrica di qualità del servizio relativa al tempo necessario per l’avvio (tempo che trascorre ta `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzi metadati personalizzati, invia semplicemente un oggetto vuoto per l’argomento `data` in `trackSessionStart`, come mostrato nella riga esterna di commento nell’esempio di iOS precedente.

1. **Tracciare l’inizio effettivo della riproduzione**

   Identifica l’evento dal lettore multimediale per l’inizio della riproduzione, dove viene eseguito il rendering del primo fotogramma del file multimediale sullo schermo ed effettua una chiamata `trackPlay`.

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Tracciare il completamento della riproduzione**

   Identifica l’evento dal lettore multimediale per il completamento della riproduzione in cui l’utente ha guardato il contenuto fino alla fine ed effettua una chiamata `trackComplete`.

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Tracciare la fine della sessione**

   Identifica l’evento dal lettore multimediale per lo scaricamento/la chiusura della riproduzione in cui l’utente chiude l’elemento multimediale e/o l’elemento multimediale viene completato e scaricato ed effettua una chiamata `trackSessionEnd`.

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` indica la fine di una sessione di tracciamento. Se la sessione è stata guardata correttamente fino al completamento, dove l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` venga chiamato prima di `trackSessionEnd`. Qualsiasi altra chiamata API `track*` viene ignorata dopo `trackSessionEnd`, tranne `trackSessionStart` per una nuova sessione di tracciamento.

1. **Tracciare tutti gli scenari di pausa possibili**

   Identifica l’evento dal lettore multimediale per la pausa ed effettua una chiamata `trackPause`.

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Scenari di pausa**

   Identifica uno scenario in cui il lettore multimediale si interrompe e verifica che `trackPause` sia chiamato correttamente. Tutti gli scenari seguenti richiedono che l’app chiami `trackPause()`:

   * L’utente mette esplicitamente in pausa l’app.
   * Il lettore si mette in pausa da solo.
   * (*App per dispositivi mobili*): l’utente mette l’applicazione in background, ma si desidera invece che l’app mantenga aperta la sessione.
   * (*App mobili*): si verifica una qualsiasi interruzione del sistema causando l’esecuzione in background dell’applicazione. Ad esempio, l’utente riceve una chiamata oppure la notifica da un’altra applicazione, ma desideri che l’applicazione mantenga aperta la sessione per dare all’utente l’opportunità di riprendere l’elemento multimediale dal punto in cui è stato interrotto.

1. Identifica l’evento dal lettore per la riproduzione e/o la ripresa dalla pausa ed effettua una chiamata `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Potrebbe trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni chiamata API `trackPause()` sia associata a una seguente `trackPlay()` quando riprende la riproduzione.

* Scenari di tracciamento: [Riproduzione VOD senza annunci](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con l’SDK JavaScript per un esempio di tracciamento completo.
