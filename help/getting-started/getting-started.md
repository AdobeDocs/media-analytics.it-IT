---
title: Introduzione
description: Guida introduttiva ad Adobe Analytics for Streaming Media.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 660aa29a-2a3d-4a4f-acd6-471551d1047b
source-git-commit: 8b939da2374acb5d573a553c848ba880345e64b5
workflow-type: ht
source-wordcount: '439'
ht-degree: 100%

---

# Introduzione {#getting-started}

Adobe Analytics for Streaming Media offre due metodi di implementazione principali: i Media SDK e l’API Media Collection.

![metodi](assets/getting-started2.png)

Utilizzando la logica integrata di **Media SDK**, è possibile misurare con precisione più piattaforme multimediali, tra cui siti web, telefoni cellulari, TV connesse, tablet, dispositivi OTT, set-top box e console di gioco. Puoi anche misurare il contenuto scaricato. Le informazioni che ottieni approfondiscono il coinvolgimento degli utenti nella visualizzazione, in modo da comprendere quanto tempo, quando e dove interagisce il pubblico. I Media SDK utilizzano le **API Media Collection** per il tracciamento. Le API Media Collection sono personalizzabili se l’applicazione richiede funzionalità di tracciamento personalizzate. Per i dispositivi non supportati dai Media SDK, puoi utilizzare le API Media Collection.

La soluzione di Adobe Analytics Streaming Media è disponibile per le seguenti piattaforme multimediali:

* Web
* Mobile
* Over-the-top
* Qualsiasi dispositivo connesso che può essere utilizzato per lo streaming multimediale o per un’integrazione server-to-server

Per ulteriori informazioni, consulta [Dispositivi e piattaforme supportati](#_Supported_devices_and).

>[!IMPORTANT]
>
>Per implementare Adobe Analytics Streaming Media, contatta il tuo rappresentante commerciale Adobe o l’Account Manager per assicurarti che Streaming Media faccia parte del tuo portfolio di prodotti.

## Media SDK per Streaming Media {#media-sdks}

I Media SDK per Streaming Media sono disponibili per le piattaforme JavaScript, Android, iOS, tvOS, Chromecast e Roku.

Per informazioni sul download e l’installazione dei Media SDK, consulta [Ottenere Media SDK e le estensioni tramite tag e SDK OTT](/help/getting-started/download-sdks.md).


## API Media Collection {#media-collection-apis}

Le **API Media Collection** ti consentono di personalizzare l’implementazione di Media Analytics. Utilizza le API Media Collection per chiamare direttamente i server di Adobe per eseguire quasi tutte le azioni che puoi effettuare utilizzando gli SDK e altro ancora. Personalizza la tua raccolta dati per creare rapporti che esplorino, ottengano informazioni o rispondano a domande importanti sui tuoi dati multimediali in streaming.

Per informazioni sull’utilizzo delle API Media Collection, consulta [Documentazione sulle API per Streaming Media](/help/implementation/media-collection-api/mc-api-overview.md).

## Estensioni Adobe {#adobe-extensions}

* L’[**Estensione Adobe Medium Analytics for Audio and Video**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=it) (Estensione Media Analytics), è necessaria per le implementazioni iOS e tvOS. Questa estensione fornisce le funzionalità necessarie per aggiungere l’istanza di tracciamento a un progetto o sito di tag. L’estensione MA richiede anche l’estensione Analytics e l’estensione Experience Cloud ID.

* [Estensione Analytics v1.6 o versione successiva](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=it): questa estensione consente di caricare la libreria JavaScript del Web SDK di Adobe Experience Platform per inviare dati alle soluzioni Adobe.

* [Estensione Experience Cloud ID](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=it): questa estensione implementa il servizio Experience Cloud ID che identifica i visitatori in tutte le soluzioni di Experience Cloud. Il servizio Experience Cloud ID è un’estensione di personalizzazione in Adobe Experience Platform.
