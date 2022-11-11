---
title: Introduzione
description: Guida introduttiva ad Adobe Analytics per i file multimediali in streaming.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 6%

---


# Introduzione {#getting-started}

Adobe Analytics for Streaming Media offre due metodi di implementazione principali: Media SDK e API Media Collection.

![Metodi](assets/getting-started2.png)

Utilizzo della logica integrata di **SDK per contenuti multimediali**, è possibile misurare con precisione più piattaforme multimediali, tra cui siti web, telefoni cellulari, TV connesse, tablet, dispositivi OTT, set-top box e console di gioco. Puoi anche misurare il contenuto scaricato. Le informazioni che ottieni approfondiscono il coinvolgimento degli utenti nella visualizzazione, in modo da comprendere quanto tempo, quando e dove si interagiscono gli spettatori. Gli SDK per contenuti multimediali utilizzano le **API di Media Collection** per il tracciamento. Le API di Media Collection sono personalizzabili se l’applicazione richiede funzionalità di tracciamento personalizzate. Per i dispositivi non supportati dagli SDK di Media, puoi utilizzare le API di Media Collection.

La soluzione Adobe Analytics Streaming Media è disponibile per le seguenti piattaforme multimediali:

* Web
* Mobile
* In alto
* Qualsiasi dispositivo connesso che può essere utilizzato per lo streaming multimediale o per un&#39;integrazione server-to-server

Per ulteriori informazioni, consulta [Dispositivi e piattaforme supportati](#_Supported_devices_and).

>[!IMPORTANT]
>
>Per implementare Adobe Analytics Streaming Media, contatta il tuo rappresentante commerciale Adobe o l&#39;Account Manager per assicurarti che Streaming Media faccia parte del tuo portfolio di prodotti.

## SDK per contenuti multimediali per file multimediali in streaming {#media-sdks}

Gli SDK per i file multimediali in streaming sono disponibili per le piattaforme JavaScript, Android, iOS, tvOS, Chromecast e Roku.

Per informazioni sul download e l’installazione degli SDK per Media, vedi [Ottenere SDK per contenuti multimediali, estensioni tramite tag e SDK OTT](/help/getting-started/download-sdks.md).


## API di Media Collection {#media-collection-apis}

La **API di Media Collection** ti consente di personalizzare l’implementazione di media analytics. Utilizza le API di Media Collection per chiamare direttamente i server di Adobe per eseguire quasi tutte le azioni che puoi eseguire utilizzando gli SDK e altro ancora. Personalizza la tua raccolta dati per creare rapporti che esplorino, ottengano informazioni o rispondano a domande importanti sui tuoi dati multimediali in streaming.

Per informazioni sull’utilizzo delle API di Media Collection, consulta [Documentazione dell’API per contenuti multimediali in streaming](/help/implementation/media-collection-api/mc-api-overview.md).

## Estensioni Adobe {#adobe-extensions}

>[!NOTE]
>
>NECESSITÀ DI INTRODUZIONE PER LE ESTENSIONI

* La [**Estensione Adobe Medium Analytics for Audio and Video**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=en) (Estensione Media Analytics), è necessario per le implementazioni iOS e tvOS. Fornisce la funzionalità per aggiungere l’istanza di tracciamento a un sito o a un progetto di tag. L&#39;estensione MA richiede anche l&#39;estensione Analytics e l&#39;estensione Experience Cloud ID.

* [Estensione Analytics v1.6 o versione successiva](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en)- Questa estensione consente di caricare la libreria JavaScript dell&#39;SDK per web Adobe Experience Platform per inviare dati alle soluzioni Adobe.

* [Estensione Experience Cloud ID](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en)- Questa estensione implementa il servizio Experience Cloud ID che identifica i visitatori in tutte le soluzioni Experience Cloud. Il servizio Experience Cloud ID è un’estensione di personalizzazione in Adobe Experience Platform.
