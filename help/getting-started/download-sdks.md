---
title: Accesso ai collegamenti per scaricare gli SDK di Media Analytics
description: Collegamenti ai download dell’SDK per le piattaforme disponibili, inclusi Android, iOS, JavaScript, Chromecast e Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8a0f2c0b367b48ee5ac94e7fc6bcd0eadafbc5d8
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 84%

---

# Ottieni Media SDK e le estensioni tramite tag e SDK OTT {#download-sdks}

Le informazioni in questa pagina includono collegamenti per scaricare i Media SDK correnti e ottenere le estensioni per file multimediali che utilizzano i tag.

I tag in Adobe Experience Platform Launch costiuiscono la nuova generazione di funzionalità di gestione di tag per siti web e SDK per dispositivi mobili di Adobe. I tag offrono ai clienti un modo semplice di implementare e gestire le soluzioni di analisi, marketing e annunci pubblicitari necessarie per fornire ai clienti esperienze personalizzate significative. Per ulteriori informazioni sui tag, consulta [Panoramica sui tag](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=it).


>[!NOTE]
>
>Per informazioni sul download degli SDK legacy, consulta [Legacy: scaricare gli SDK](/help/legacy/legacy-download-sdks.md).<br>
>Per informazioni importanti sulla fine del supporto, consulta [Domande frequenti sulla fine del supporto](/help/additional-resources/end-of-support-faqs.md).

## Media SDK e librerie mobili {#media-sdks-libraries}

### Implementazione web {#download-web-sdk}

| Piattaforma supportata | Soluzioni supportate | Metodo di implementazione | Versione |  API   |  Documentazione  |  Esempio  |
|:---:|---|---|---|---| ---| ---|
| ![Icona JavaScript](assets/javascript-icon.png) | Adobe Analytics | Solo Analytics | Web - [Media SDK per JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Riferimento API per JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [Installare Media Analytics utilizzando JavaScript](/help/implementation/media-sdk/setup/web-implementation.md) | [Esempio SDK per contenuti multimediali per JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![Icona JavaScript](assets/javascript-icon.png) | Adobe Analytics | Solo Analytics | Web - Estensione Media |  | [Estensione Adobe Media Analytics (3.x SDK) for Audio and Video — utilizzando tag (raccolta dati)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=it) | [Esempio Estensione Adobe Media Analytics (3.x SDK) for Audio and Video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| ![Icona JavaScript](assets/javascript-icon.png) | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Web - Experienci Platform Edge (disponibile a breve) |  | [Installare Media Analytics con Experienci Platform Edge](/help/implementation/edge/implementation-edge.md) | |

### Implementazione mobile {#get-mobile-extension}

| Piattaforma supportata | Soluzioni supportate | Metodo di implementazione | Versione |  Documentazione   |  Esempi  |
|:---:|---|---|---|---|---|
| ![Icona Android](assets/android-icon.png) | Adobe Analytics | Solo Analytics | Android - Estensione Media | [Documentazione di Mobile SDK](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Esempio Estensione Media Analytics for Audio and Video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Icona Apple iOS ](assets/ios-icon.png)<br>**tvOS** | Adobe Analytics | Solo Analytics | iOS / tvOS - Estensione Media | [Documentazione di Mobile SDK](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Esempio Estensione Media Analytics for Audio and Video](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![Icona Android](assets/android-icon.png) | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Android: Experienci Platform Edge | [Installare Media Analytics con Experienci Platform Edge](/help/implementation/edge/implementation-edge.md) | |
| ![Icona Apple iOS ](assets/ios-icon.png)<br>**tvOS** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS / tvOS - Experienci Platform Edge | [Installare Media Analytics con Experienci Platform Edge](/help/implementation/edge/implementation-edge.md) |  |

### Implementazione Over-The-Top {#download-ott-libraries}

| Piattaforma supportata | Soluzioni supportate | Metodo di implementazione | Versione |  API   |  Documentazione  |
|:---:|---|---|---|---|---|
| ![Icona Chromecast](assets/chromecast-icon.png) | Adobe Analytics | Solo Analytics | [SDK per Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Riferimento API per Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Configurare Mobile SDK v3.x per Chromecast](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Icona Roku](assets/roku-icon.png) | Adobe Analytics | Solo Analytics | [SDK per Roku v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) | [Riferimento API per Roku](/help/implementation/media-sdk/setup/set-up-roku.md) | [Configurare Mobile SDK v2.x per Roku](/help/implementation/media-sdk/setup/set-up-roku.md) |
