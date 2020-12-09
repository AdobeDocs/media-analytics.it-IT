---
title: Domande frequenti relative alla fine del supporto per l’SDK di Media Analytics
description: Questo argomento include domande frequenti sulla fine del supporto per gli SDK di Media Analytics.
translation-type: tm+mt
source-git-commit: dfffcf1e1d815ca178e0bdba881d973d60fe1631
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---


# Domande frequenti relative alla fine del supporto per l’SDK di Media Analytics

Con la fine del supporto per gli SDK della versione 4 per dispositivi mobili il 31 agosto 2021,  Adobe interromperà anche il supporto per gli SDK di Media Analytics per iOS e Android. Dopo il 31 agosto 2021,  Adobe non fornirà correzioni, aggiornamenti relativi al sistema operativo o supporto per l’SDK di Media Analytics.  Durante il processo di migrazione a questi nuovi SDK per Experienci Platform , tenete presente che le [estensioni Media Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) devono essere implementate per abilitare  Adobe Analytics per gli elementi multimediali in streaming.

## Le 5 cose più importanti da sapere

1. Gli SDK di Mobile v4 non saranno più supportati dopo il 31 agosto 2021. Esegui la migrazione agli SDK per dispositivi mobili Adobe Experience Platform (AEP) per iOS e Android. Per ulteriori informazioni, consultate [Versione 4 SDK per dispositivi mobili - Domande frequenti sulla fine del supporto](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq).

1. L’implementazione di Analytics per Streaming Media richiede l’SDK di AEP Mobile e l’utilizzo delle estensioni Analytics e Media Analytics. A partire dal 1 settembre 2021, è necessario utilizzare i nuovi SDK AEP Mobile e le nuove estensioni.  Le estensioni Media Analytics sono configurate tramite  lancio Adobe.  Per ulteriori informazioni, consultate [Migrazione dall&#39;SDK per file multimediali indipendenti al lancio  Adobe](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. Lo sviluppo di funzioni è terminato per gli SDK di Media Analytics per iOS e Android.  Le nuove funzioni introdotte a partire dall’autunno 2019 sono abilitate utilizzando le estensioni Media Analytics e l’API Media Collection.

1. Gli SDK Roku e Chromecast rimangono disponibili per i clienti Analytics per lo streaming dei file multimediali. Gli SDK Roku e Chromecast continueranno a essere migliorati e supportati come SDK standalone.  Se utilizzate l’SDK JS per Media Analytics, potete continuare a utilizzare l’SDK autonomo o attivare l’estensione Media Analytics tramite  lancio del Adobe.

1. Prima del 1° settembre 2021,  Adobe può, a sua discrezione, elaborare nuove correzioni per problemi di forte impatto tecnico o di esposizione delle imprese. In base all&#39;input del cliente,  Adobe determinerà il grado di impatto e di esposizione e le attività che ne derivano.

Per qualsiasi domanda, contattate il vostro responsabile del successo  Adobe.

## Domande frequenti

1. **Il supporto per gli SDK Roku e Chromecast verrà influenzato? &#x200B;**

   No.  Gli SDK Roku e Chromecast continueranno a essere supportati come SDK standalone per il momento. &#x200B;
&#x200B;
1. **La modifica interesserà le implementazioni dell&#39;SDK JS di Media Analytics? &#x200B;**

   No.  I clienti che utilizzano l’SDK JS per Media Analytics possono continuare a utilizzare l’SDK o attivarlo tramite  lancio Adobe.
&#x200B;
1. **Qual è il livello di sforzo per migrare alle estensioni Media Analytics &#x200B;?**

   LOE dipende dall’implementazione di ciascun cliente, quindi varia.  Dopo aver esaminato la documentazione sulla migrazione riportata di seguito, consulta e/o l’assistenza clienti per ulteriore assistenza.

   [Estensioni di Media Analytics: Migrazione Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Estensioni di Media Analytics: Migrazione iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Estensioni di Media Analytics: nuove implementazioni](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **È necessario disporre di Launch come sistema di gestione tag? Cosa succede se non si desidera utilizzare Launch?**

   Per l’uso delle app per dispositivi mobili, Launch non viene utilizzato come sistema di gestione tag, ma come sistema Web.  Per configurare le estensioni SDK è necessario utilizzare l&#39;interfaccia utente di Launch. Questa procedura è simile a quella utilizzata dall&#39;interfaccia utente di Mobile Services del  Adobe per configurare l&#39;SDK di Mobile v4. Per l&#39;installazione, l&#39;utilizzo di Launch offre istruzioni di installazione personalizzate in base all&#39;estensione scelta.

1. **Questa fine del supporto influisce sull’SDK per tvOS?**

   Sì, per tvOS (versione 10+) l&#39;implementazione consigliata consiste nella migrazione alle estensioni di Media Analytics.  Per ulteriori informazioni, consultate [Migrazione dall&#39;SDK per file multimediali standalone al lancio  Adobe - iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **Questa fine del supporto influisce sull’SDK per FireTV e AndroidTV? &#x200B;**

   Sì, per FireTV e AndroidTV, l’implementazione consigliata consiste nella migrazione alle estensioni di Media Analytics.  Per ulteriori informazioni, consultate [Migrazione dall&#39;SDK per file multimediali standalone al lancio  Adobe - Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).
