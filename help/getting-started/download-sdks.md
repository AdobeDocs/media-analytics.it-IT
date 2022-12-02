---
title: Accesso ai collegamenti per scaricare gli SDK di Media Analytics
description: Collegamenti ai download dell’SDK per le piattaforme disponibili, inclusi Android, iOS, JavaScript, Chromecast e Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '645'
ht-degree: 100%

---

# Ottieni Media SDK e le estensioni tramite tag e SDK OTT {#download-sdks}

Le informazioni in questa pagina includono collegamenti per scaricare i Media SDK correnti e ottenere le estensioni per file multimediali.

Le informazioni contenute in questa pagina includono collegamenti per scaricare i Media SDK correnti e per ottenere le estensioni per file multimediali che utilizzano i tag.

I tag in Adobe Experience Platform Launch costiuiscono la nuova generazione di funzionalità di gestione di tag per siti web e SDK per dispositivi mobili di Adobe. I tag offrono ai clienti un modo semplice di implementare e gestire le soluzioni di analisi, marketing e annunci pubblicitari necessarie per fornire ai clienti esperienze personalizzate significative. Per ulteriori informazioni sui tag, consulta [Panoramica sui tag](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=it)


>[!NOTE]
>
>Per informazioni sul download degli SDK legacy, consulta [Legacy: scaricare gli SDK](/help/legacy/legacy-download-sdks.md).<br>
>Per informazioni importanti sulla fine del supporto, consulta [Domande frequenti sulla fine del supporto](/help/additional-resources/end-of-support-faqs.md).

## SDK per contenuti multimediali e librerie mobili {#media-sdks-libraries}

### Implementazione web {#download-web-sdk}

| Piattaforma supportata | Versione |  API   |  Documentazione  | Esempio  |
|:---:|---|---|---|---|
| ![Icona JavaScript](assets/javascript-icon.png) | Web - [Media SDK per JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Riferimento API per JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [Configurare l’SDK per contenuti multimediali v3.x per JavaScript](/help/implementation/media-sdk/setup/web-implementation.md) | [Esempio SDK per contenuti multimediali per JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![Icona JavaScript](assets/javascript-icon.png) | Web - Estensione Media |  | [Estensione Adobe Media Analytics (3.x SDK) for Audio and Video — utilizzando tag (raccolta dati)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=it) | [Esempio Estensione Adobe Media Analytics (3.x SDK) for Audio and Video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |

### Implementazione mobile {#get-mobile-extension}

| Piattaforma supportata | Versione | Documentazione   | Esempi  |
|:---:|---|---|---|
| ![Icona Android](assets/android-icon.png) | Android - Estensione Media | [Documentazione di Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics - Esempio Estensione Media Analytics for Audio and Video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Icona Apple iOS ](assets/ios-icon.png)<br> icona aggiungi tvOS | iOS / tvOS - Estensione Media | [Documentazione di Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics - Esempio Estensione Media Analytics for Audio and Video](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |

### Implementazione Over-The-Top {#download-ott-libraries}

| Piattaforma supportata | Versione |  API   |  Documentazione  |
|:---:|---|---|---|
| ![Icona Chromecast](assets/chromecast-icon.png) | [SDK per Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Riferimento API per Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Configurare Mobile SDK v3.x per Chromecast](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Icona Roku](assets/roku-icon.png) | [SDK per Roku v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) | [Riferimento API per Roku](/help/implementation/media-sdk/setup/set-up-roku.md) | [Configurare Mobile SDK v2.x per Roku](/help/implementation/media-sdk/setup/set-up-roku.md) |

## Estensioni Adobe {#adobe-extensions}

### Estensione per Streaming Media {#streaming-media-extension}

L’**Estensione Adobe Medium Analytics for Audio and Video** richiede l’SKU del componente aggiuntivo Adobe Analytics for Media.Per ulteriori informazioni, contatta il tuo rappresentante commerciale Adobe, Account Manager o Customer Success Manager.

Per informazioni dettagliate sull’installazione, la configurazione e l’implementazione dell’**estensione Adobe Medium Analytics for Audio and Video**, vedi [Panoramica dell’estensione Adobe Medium Analytics for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=it) e [Configurare l’estensione Media Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics#configure-the-media-analytics-extension).

### Estensione Analytics {#analytics-extension}

[Estensione Analytics v1.6 o versione successiva](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=it): questa estensione consente di caricare la libreria JavaScript del Web SDK di Adobe Experience Platform per inviare dati alle soluzioni Adobe.È richiesta la versione dell’**Estensione Analytics** 1.6 o successiva.

Per informazioni sulla configurazione di questa estensione, consulta [Configurare l’estensione Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=it).

### Estensione Experience Cloud ID {#cloud-id-extension}

[Estensione Experience Cloud ID](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=it): questa estensione implementa il servizio Experience Cloud ID che identifica i visitatori in tutte le soluzioni Experience Cloud. Il servizio Experience Cloud ID è un’estensione di personalizzazione in Adobe Experience Platform.

Usa questa estensione per integrare Experience Cloud Identity Service nella tua proprietà. Con Experience Cloud Identity Service, puoi creare e memorizzare identificatori univoci e costanti per i visitatori del tuo sito.

Per informazioni sulla configurazione di questa estensione, consulta [Configurare l’estensione Experience Cluod ID](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=it)
