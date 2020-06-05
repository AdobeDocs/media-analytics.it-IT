---
title: Domande frequenti relative alla fine del supporto per l’SDK di Media Analytics
description: Questo argomento include domande frequenti sulla fine del supporto per gli SDK di Media Analytics.
translation-type: tm+mt
source-git-commit: 38adc54438f85ca8ece8c77d9ff0d0aa14eb6605
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 1%

---


# Domande frequenti relative alla fine del supporto per l’SDK di Media Analytics

Con la fine del supporto per gli SDK della versione 4 per dispositivi mobili il 31 agosto 2021, Adobe interromperà anche il supporto per gli SDK di Media Analytics per iOS e Android. Dopo il 31 agosto 2021, Adobe non fornirà correzioni, aggiornamenti relativi al sistema operativo o supporto per l’SDK di Media Analytics.  Durante il processo di migrazione a questi nuovi SDK della piattaforma Experience, tenete presente che le estensioni [](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) Media Analytics devono essere implementate per abilitare Adobe Analytics per Audio e Video.

## Le 5 cose più importanti da sapere

1. Gli SDK di Mobile v4 non saranno più supportati dopo il 31 agosto 2021. Devi effettuare la migrazione agli SDK Adobe Experience Platform (AEP) per iOS e Android. Per ulteriori informazioni, consulta le domande frequenti relative alla [versione 4 degli SDK per dispositivi mobili](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq).

1. L’implementazione di Analytics per audio e video richiede l’SDK AEP e l’utilizzo delle estensioni Analytics e Media Analytics. A partire dal 1° settembre 2021, è necessario utilizzare i nuovi SDK AEP e le nuove estensioni.  Le estensioni di Media Analytics sono configurate tramite Adobe Launch.  Per ulteriori informazioni, consulta [Migrazione dall’SDK per contenuti multimediali indipendenti ad Adobe Launch.](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. Lo sviluppo di funzioni è terminato per gli SDK di Media Analytics per iOS e Android.  Le nuove funzioni introdotte a partire dall’autunno 2019 sono abilitate utilizzando le estensioni Media Analytics e l’API Media Collection.

1. Gli SDK Roku e Chromecast rimangono disponibili per i clienti di Analytics per audio e video. Gli SDK Roku e Chromecast continueranno a essere migliorati e supportati come SDK standalone.  Se utilizzi l’SDK JS per Media Analytics, puoi continuare a utilizzare l’SDK autonomo o abilitare l’estensione Media Analytics tramite Adobe Launch.

1. Prima del 1° settembre 2021, Adobe può, a propria discrezione, sviluppare nuove correzioni per problemi di forte impatto tecnico o di esposizione aziendale. In base all&#39;input del cliente, Adobe determinerà il grado di impatto e di esposizione e le attività che ne derivano.

Per qualsiasi domanda, contattate il vostro Adobe Customer Success Manager.

## Domande frequenti

1. **Il supporto per gli SDK Roku e Chromecast verrà influenzato? &#x200B;**

   No.  Gli SDK Roku e Chromecast continueranno a essere supportati come SDK standalone per il momento. &#x200B; &#x200B;
1. **La modifica interesserà le implementazioni dell&#39;SDK JS di Media Analytics? &#x200B;**

   No.  I clienti che utilizzano l’SDK JS per Media Analytics possono continuare a utilizzare l’SDK o attivarlo tramite Adobe Launch.
&#x200B;
1. **Qual è il livello di sforzo per migrare alle estensioni Media Analytics &#x200B;?**

   LOE dipende dall’implementazione di ciascun cliente, quindi varia.  Dopo aver esaminato la documentazione sulla migrazione riportata di seguito, consulta e/o l’assistenza clienti per ulteriore assistenza.

   [Estensioni di Media Analytics: Migrazione Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Estensioni di Media Analytics: Migrazione iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Estensioni di Media Analytics: nuove implementazioni](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **È necessario disporre di Launch come sistema di gestione tag? Cosa succede se non si desidera utilizzare Launch?**

   Per l’uso delle app per dispositivi mobili, Launch non viene utilizzato come sistema di gestione tag, ma come sistema Web.  Per configurare le estensioni SDK è necessario utilizzare l&#39;interfaccia utente di Launch. Questa procedura è simile a quella utilizzata dall&#39;interfaccia utente di Adobe Mobile Services per configurare l&#39;SDK di Mobile v4. Per l&#39;installazione, l&#39;utilizzo di Launch offre istruzioni di installazione personalizzate in base all&#39;estensione scelta.

1. **Questa fine del supporto influisce sull’SDK per tvOS?**

   Sì, per tvOS (versione 10+) l&#39;implementazione consigliata consiste nella migrazione alle estensioni di Media Analytics.  Il supporto per AEP SDK e il supporto per Media Analytics Extension è previsto per giugno 2020.  Per ulteriori informazioni, consulta [Migrazione dall’SDK per file multimediali standalone ad Adobe Launch - iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **Questa fine del supporto influisce sull’SDK per FireTV e AndroidTV? &#x200B;**

   Sì, per FireTV e AndroidTV, l’implementazione consigliata consiste nella migrazione alle estensioni di Media Analytics.  Il supporto per AEP SDK e il supporto per Media Analytics Extension è previsto per giugno 2020.  Per ulteriori informazioni, consultate [Migrazione dall’SDK per file multimediali standalone ad Adobe Launch - Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).
