---
title: Accesso ai collegamenti per scaricare gli SDK di Media Analytics
description: Collegamenti ai download dell’SDK per le piattaforme disponibili, inclusi Android, iOS, JavaScript, Chromecast e Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 26%

---

# Ottenere SDK per contenuti multimediali, estensioni tramite tag e SDK OTT {#download-sdks}

Le informazioni in questa pagina includono collegamenti per scaricare gli SDK per contenuti multimediali correnti e ottenere le estensioni per file multimediali.

Le informazioni contenute in questa pagina includono collegamenti per scaricare gli SDK per contenuti multimediali correnti e per ottenere le estensioni multimediali che utilizzano i tag.

I tag in Adobe Experience Platform sono la nuova generazione di funzionalità di gestione tag per siti web e SDK per dispositivi mobili di Adobe. I tag forniscono un modo semplice per implementare e gestire le soluzioni di analisi, marketing e pubblicità necessarie per fornire ai clienti esperienze personalizzate. Per ulteriori informazioni sui tag, consulta [Panoramica sui tag](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=it)


>[!NOTE]
>
>Per informazioni sul download degli SDK legacy, vedi [Legacy - Download degli SDK](/help/legacy/legacy-download-sdks.md).<br>
>Per informazioni importanti sulla fine del supporto, consulta [Domande frequenti sulla fine del supporto](/help/additional-resources/end-of-support-faqs.md).

## SDK per contenuti multimediali e librerie mobili {#media-sdks-libraries}

### Implementazione web {#download-web-sdk}

| Piattaforma supportata | Versione |  API   |  Documentazione  |  Esempio  |
|:---:|---|---|---|---|
| ![Icona JavaScript](assets/javascript-icon.png) | Web - [Media SDK per JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Riferimento API JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [Configurare Media SDK v3.x per JavaScript](/help/implementation/media-sdk/setup/web-implementation.md) | [Esempio di Media SDK per JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![Icona JavaScript](assets/javascript-icon.png) | Web - Estensione multimediale |  | [Estensione Adobe Medium Analytics (3.x SDK) for Audio and Video — using Tags (Data Collection)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=en) | [Esempio di estensione Adobe Medium Analytics (3.x SDK) for Audio and Video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |

### Implementazione mobile {#get-mobile-extension}

| Piattaforma supportata | Versione |  Documentazione   |  Esempi  |
|:---:|---|---|---|
| ![Icona Android](assets/android-icon.png) | Android - Estensione Media | [Documentazione di Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics - Esempio di Media Analytics per audio e video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Icona Apple iOS](assets/ios-icon.png)<br>icona aggiungi tvOS | iOS / tvOS - Estensione Media | [Documentazione di Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics - Esempio di Media Analytics per audio e video](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |

### Implementazione Over-The-Top {#download-ott-libraries}

| Piattaforma supportata | Versione |  API   |  Documentazione  |
|:---:|---|---|---|
| ![Icona Chromecast](assets/chromecast-icon.png) | [SDK per Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Riferimento API per Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Configurare Mobile SDK v3.x per Chromecast](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Icona Roku](assets/roku-icon.png) | [SDK per Roku v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) | [Riferimento API Roku](/help/implementation/media-sdk/setup/set-up-roku.md) | [Configurare l’SDK mobile v2.x per Roku](/help/implementation/media-sdk/setup/set-up-roku.md) |

## Estensioni Adobe {#adobe-extensions}

### Estensione per contenuti multimediali in streaming {#streaming-media-extension}

La **Estensione Adobe Medium Analytics for Audio and Video** richiede l’SKU del componente aggiuntivo Adobe Analytics for Media. Per ulteriori informazioni, contatta il tuo rappresentante commerciale Adobe, Account Manager o Customer Success Manager.

Per informazioni dettagliate sull&#39;installazione, la configurazione e l&#39;implementazione di **Estensione Adobe Medium Analytics for Audio and Video**, vedi [Estensione Adobe Medium Analytics for Audio and Video: panoramica](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=en) e [Configurare l’estensione Media Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics#configure-the-media-analytics-extension).

### Estensione Analytics {#analytics-extension}

[Estensione Analytics v1.6 o versione successiva](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en)- Questa estensione consente di caricare la libreria JavaScript dell&#39;SDK per web Adobe Experience Platform per inviare dati alle soluzioni Adobe. La **Estensione Analytics** È richiesta la versione 1.6 o successiva.

Per informazioni sulla configurazione di questa estensione, vedi [Configura l&#39;estensione Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en).

### Estensione Experience Cloud ID {#cloud-id-extension}

[Estensione Experience Cloud ID](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en)- Questa estensione implementa il servizio Experience Cloud ID che identifica i visitatori in tutte le soluzioni Experience Cloud. Il servizio Experience Cloud ID è un’estensione di personalizzazione in Adobe Experience Platform.

Usa questa estensione per integrare Experience Cloud Identity Service nella tua proprietà. Con Experience Cloud Identity Service, puoi creare e memorizzare identificatori univoci e costanti per i visitatori del tuo sito.

Per informazioni sulla configurazione di questa estensione, vedi [Configura l&#39;estensione Experience Cloud ID](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en)
