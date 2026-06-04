---
title: Accesso ai collegamenti per scaricare gli SDK di Media Analytics
description: Collegamenti ai download dell’SDK per le piattaforme disponibili, inclusi Android, iOS, JavaScript, Chromecast e Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-L2tSDNue-GheYE-krKkpnOh05s5GKZZBz5sFXsBJ3I
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdbid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 524
ht-degree: 73%

---

# Ottieni Media SDK e le estensioni tramite tag e SDK OTT {#download-sdks}

Le informazioni in questa pagina includono collegamenti per scaricare i Media SDK correnti e ottenere le estensioni per file multimediali che utilizzano i tag.

I tag in Adobe Experience Platform Launch costiuiscono la nuova generazione di funzionalità di gestione di tag per siti web e SDK per dispositivi mobili di Adobe. I tag offrono ai clienti un modo semplice di implementare e gestire le soluzioni di analisi, marketing e annunci pubblicitari necessarie per fornire ai clienti esperienze personalizzate significative. Per ulteriori informazioni sui tag, consulta [Panoramica sui tag](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=it).

## Media SDK e librerie mobili {#media-sdks-libraries}

### Implementazione web {#download-web-sdk}

| Piattaforma supportata | Soluzioni supportate | Metodo di implementazione | Versione |  API   |  Documentazione  |  Esempio  |
|:---:|---|---|---|---| ---| ---|
| ![Icona JavaScript ](assets/javascript-icon.png)</br>**API JavaScript** | Adobe Analytics | Solo Analytics | Web - [Media SDK per JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Riferimento API per JavaScript](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/APIReference.md) | [Configura JavaScript per Streaming Media](/help/implementation/analytics-only/javascript.md) | [Esempio SDK per contenuti multimediali per JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![Icona JavaScript ](assets/javascript-icon.png)</br>**API JavaScript** | Adobe Analytics | Solo Analytics | Web - Estensione Media |  | [Estensione Adobe Media Analytics (3.x SDK) for Audio and Video — utilizzando tag (raccolta dati)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=it) | [Esempio Estensione Adobe Media Analytics (3.x SDK) for Audio and Video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**Web** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Web - Experience Platform Edge |  | [Panoramica sull&#39;implementazione di Edge](/help/implementation/edge/overview.md) <p>e</p><p>[Configura Web SDK per Streaming Media](/help/implementation/edge/web-sdk.md)</p> | |

### Implementazione mobile {#get-mobile-extension}

| Piattaforma supportata | Soluzioni supportate | Metodo di implementazione | Versione |  Documentazione   |  Esempi  |
|:---:|---|---|---|---|---|
| ![Icona Android ](assets/android-icon.png)</br>**Android** | Adobe Analytics | Solo Analytics | Android - Estensione Media | [Documentazione di Mobile SDK](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Esempio Estensione Media Analytics for Audio and Video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Icona Apple iOS ](assets/ios-icon.png)<br>**tvOS** | Adobe Analytics | Solo Analytics | iOS / tvOS - Estensione Media | [Documentazione di Mobile SDK](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Esempio Estensione Media Analytics for Audio and Video](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![Icona Android ](assets/android-icon.png)</br>**Android** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | ANDROID - EXPERIENCE PLATFORM EDGE | [Configura Android per Streaming Media](/help/implementation/edge/android.md) | |
| ![Icona Apple iOS ](assets/ios-icon.png)<br>**tvOS** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS / tvOS - Experience Platform Edge | [Configura iOS per Streaming Media](/help/implementation/edge/ios.md) |  |

### Implementazione Over-The-Top {#download-ott-libraries}

| Piattaforma supportata | Soluzioni supportate | Metodo di implementazione | Versione |  API   |  Documentazione  |
|:---:|---|---|---|---|---|
| ![Icona Chromecast ](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | Solo Analytics | [SDK per Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Riferimento API per Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Imposta SDK Chromecast](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/docs/2.x/chromecast-setup.md) |
| ![Icona Roku ](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [SDK Adobe Experience Platform Roku](https://github.com/adobe/aepsdk-roku/tree/main) |  | [Configura Roku per Streaming Media](/help/implementation/edge/roku.md) |
