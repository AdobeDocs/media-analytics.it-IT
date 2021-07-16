---
title: Scopri come tenere traccia della riproduzione core su Android
description: Scopri come implementare il tracciamento di base utilizzando Media SDK su Android.
uuid: ab5fab95-76ed-4ae6-aedb-2e66eece7607
exl-id: d5f5a3f0-f1e0-4d68-af7f-88a30faed0db
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 3%

---

# Tracciamento riproduzione core su Android{#track-core-playback-on-android}

Questa documentazione tratta il tracciamento nella versione 2.x dell&#39;SDK.
>[!IMPORTANT]
>Se stai implementando una versione 1.x dell&#39;SDK, puoi scaricare la Guida per gli sviluppatori 1.x per Android qui: [Scaricare gli SDK](/help/sdk-implement/download-sdks.md)

1. **Configurazione del tracciamento iniziale**

   Identifica quando l&#39;utente attiva l&#39;intenzione di riproduzione (l&#39;utente fa clic su play e/o autoplay è attivato) e crea un&#39;istanza `MediaObject`.

   [API createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | Nome variable | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome file multimediale | Sì |
   | `mediaId` | Identificatore univoco del supporto | Sì |
   | `length` | Lunghezza del supporto | Sì |
   | `streamType` | Tipo di flusso (vedere _Costanti StreamType_ di seguito) | Sì |
   | `mediaType` | Tipo di supporto (vedi _Costanti MediaType_ di seguito) | Sì |

   **`StreamType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `VOD` | Tipo di flusso per Video on Demand. |
   | `LIVE` | Tipo di flusso per il contenuto live. |
   | `LINEAR` | Tipo di flusso per il contenuto lineare. |
   | `AOD` | Tipo di flusso per Audio On Demand |
   | `AUDIOBOOK` | Tipo di flusso per audio book |
   | `PODCAST` | Tipo di flusso per Podcast |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di supporto per flussi audio. |
   | `Video` | Tipo di supporto per i flussi video. |

   ```
   MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
     <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);
   ```

1. **Allega metadati**

   Facoltativamente, allega oggetti metadati standard e/o personalizzati alla sessione di tracciamento tramite variabili di dati di contesto.

   * **Metadati standard**

      [Implementazione dei metadati standard su Android](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

      >[!NOTE]
      >
      >Il collegamento dell&#39;oggetto metadati standard all&#39;oggetto multimediale è facoltativo.

      * Riferimento API per le chiavi di metadati multimediali - [chiavi di metadati standard - Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * Vedi il set completo di metadati video disponibili qui: [Parametri audio e video](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Metadati personalizzati**

      Crea un dizionario per le variabili personalizzate e popolalo con i dati per questo supporto. Ad esempio:

      ```java
      HashMap<String, String> mediaMetadata =  
        new HashMap<String, String>();
      mediaMetadata.put("isUserLoggedIn", "false");
      mediaMetadata.put("tvStation", "Sample TV Station");
      mediaMetadata.put("programmer", "Sample programmer");
      ```


1. **Tracciare l&#39;intenzione di avviare la riproduzione**

   Per iniziare a monitorare una sessione multimediale, chiama `trackSessionStart` sull&#39;istanza Media Heartbeat. Ad esempio:

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata);
   }
   ```

   >[!TIP]
   >
   >Il secondo valore è il nome dell&#39;oggetto metadati multimediali personalizzati creato al passaggio 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni dell&#39;utente in merito alla riproduzione, non dell&#39;inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati multimediali e per stimare la metrica QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzi metadati multimediali personalizzati, invia semplicemente un oggetto vuoto per il secondo argomento in `trackSessionStart`.

1. **Tracciare l&#39;inizio effettivo della riproduzione**

   Identificare l&#39;evento dal lettore multimediale per l&#39;inizio della riproduzione multimediale, dove viene eseguito il rendering del primo fotogramma del file multimediale sullo schermo, e chiamare `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) {
       _heartbeat.trackPlay();
   }
   ```

1. **Tracciare il completamento della riproduzione**

   Identifica l&#39;evento dal lettore multimediale per il completamento della riproduzione multimediale, dove l&#39;utente ha guardato il contenuto fino alla fine, e chiama `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) {
       _heartbeat.trackComplete();
   }
   ```

1. **Monitora la fine della sessione**

   Identificare l&#39;evento dal lettore multimediale per lo scaricamento/la chiusura della riproduzione multimediale, in cui l&#39;utente chiude il supporto e/o il supporto è stato completato e scaricato, e chiamare `trackSessionEnd`:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd();
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento dei contenuti multimediali. Se la sessione è stata controllata correttamente al completamento, dove l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` venga chiamato prima di `trackSessionEnd`. Qualsiasi altra chiamata API `track*` viene ignorata dopo `trackSessionEnd`, tranne `trackSessionStart` per una nuova sessione di tracciamento dei contenuti multimediali.

1. **Tracciare tutti gli scenari di pausa possibili**

   Identifica l&#39;evento dal lettore multimediale per la pausa e chiama `trackPause`:

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause();
   }
   ```

   **Pausa scenari**

   Identifica qualsiasi scenario in cui il lettore video verrà messo in pausa e assicurati che `trackPause` sia chiamato correttamente. I seguenti scenari richiedono tutti che la chiamata all&#39;app `trackPause()`:

   * L’utente inserisce esplicitamente una pausa nell’app.
   * Il lettore si mette in stato di Pausa.
   * (*App mobili*) - L&#39;utente mette l&#39;applicazione in background, ma desideri che l&#39;app mantenga aperta la sessione.
   * (*App mobili*) - Si verifica un qualsiasi tipo di interruzione del sistema che causa lo sfondo di un&#39;applicazione. Ad esempio, l&#39;utente riceve una chiamata, o si verifica un pop-up da un&#39;altra applicazione, ma si desidera che l&#39;applicazione mantenga in vita la sessione per dare all&#39;utente la possibilità di riprendere il supporto dal punto di interruzione.

1. Identifica l&#39;evento dal lettore per la riproduzione di contenuti multimediali e/o la ripresa di contenuti multimediali dalla pausa e chiama `trackPlay`.

   ```java
   // trackPlay()
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay();
   }
   ```

   >[!TIP]
   >
   >Può trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni `trackPause()` chiamata API sia associata a una seguente `trackPlay()` chiamata API quando la riproduzione multimediale riprende.

Per ulteriori informazioni sul tracciamento della riproduzione core, consulta quanto segue:

* Scenari di tracciamento: [Riproduzione VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Esempio di lettore incluso con l&#39;SDK per Android per un esempio di tracciamento completo.
