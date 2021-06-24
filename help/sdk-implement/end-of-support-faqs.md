---
title: Informazioni sulle domande frequenti relative alla fine del supporto dell’SDK di Media Analytics
description: Questo argomento include le domande frequenti sulla fine del supporto per gli SDK Media Analytics.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 1%

---

# Domande frequenti sull’SDK di Media Analytics relative alla fine del supporto

Con la fine del supporto per gli SDK per dispositivi mobili versione 4, il 31 agosto 2021, Adobe terminerà anche il supporto per gli SDK Media Analytics per iOS e Android. Dopo il 31 agosto 2021, Adobe non fornirà correzioni, aggiornamenti relativi al sistema operativo o supporto per l’SDK di Media Analytics.  Durante il processo di migrazione a questi nuovi SDK di Experience Platform, ricorda che le [estensioni Media Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) devono essere implementate per abilitare Adobe Analytics for Streaming Media.

## Le 5 cose più importanti da sapere

1. Gli SDK per dispositivi mobili v4 non saranno più supportati dopo il 31 agosto 2021. Esegui la migrazione agli SDK per dispositivi mobili Adobe Experience Platform (AEP) per iOS e Android. Per ulteriori informazioni, consulta le [domande frequenti relative alla fine del supporto degli SDK per dispositivi mobili versione 4](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq).

1. L’implementazione di Analytics for Streaming Media richiede l’SDK di AEP Mobile e l’utilizzo delle estensioni Analytics e Media Analytics. A partire dal 1° settembre 2021, è necessario utilizzare i nuovi SDK e le estensioni AEP Mobile.  Le estensioni Media Analytics sono configurate tramite Adobe Launch.  Per ulteriori informazioni, consulta [Migrazione dall’SDK per contenuti multimediali indipendenti all’Adobe Launch](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. Lo sviluppo delle funzioni è terminato per gli SDK Media Analytics per iOS e Android.  Le nuove funzioni introdotte a partire da Autunno 2019 vengono abilitate utilizzando le estensioni Media Analytics e l’API Media Collection.

1. Gli SDK Roku e Chromecast rimangono disponibili per i clienti di Analytics per Streaming Media. Gli SDK Roku e Chromecast continueranno a essere migliorati e supportati come SDK autonomi.  Se utilizzi l’SDK JS per Media Analytics, puoi continuare a utilizzare l’SDK autonomo o abilitare l’estensione Media Analytics tramite Adobe Launch.

1. Prima del 1° settembre 2021, l&#39;Adobe può, a sua esclusiva discrezione, elaborare nuove correzioni per problemi di forte impatto tecnico o di esposizione delle imprese. In base all&#39;input del cliente, l&#39;Adobe determinerà il grado di impatto e di esposizione e le attività che ne derivano.

Per qualsiasi domanda, contatta il tuo Adobe Customer Success Manager.

## Domande frequenti

1. **Il supporto per gli SDK Roku e Chromecast sarà interessato? &#x200B;**

   No.  Gli SDK Roku e Chromecast continueranno a essere supportati come SDK autonomi per il momento. &#x200B;
&#x200B;
1. **Questa modifica influisce sulle implementazioni dell’SDK JS di Media Analytics? &#x200B;**

   No.  I clienti che utilizzano l’SDK JS per Media Analytics possono continuare a utilizzare l’SDK o abilitarlo tramite Adobe Launch.
&#x200B;
1. **Qual è il livello di impegno per la migrazione alle estensioni Media Analytics? &#x200B;**

   LOE dipende dall’implementazione di ciascun cliente, quindi varia.  Dopo aver esaminato la documentazione sulla migrazione riportata di seguito, rivolgiti alla consulenza e/o all’assistenza clienti per richiedere supporto aggiuntivo.

   [Estensioni di Media Analytics: Migrazione Android](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Estensioni di Media Analytics: Migrazione iOS](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Estensioni di Media Analytics: nuove implementazioni](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **È necessario disporre di Launch come sistema di gestione dei tag? Cosa succede se non voglio utilizzare Launch?**

   Per il caso d’uso dell’app mobile, Launch non viene utilizzato come sistema di gestione dei tag come per il web.  Per configurare le estensioni SDK è necessario utilizzare l’interfaccia utente di Launch. È simile a come utilizzi l’interfaccia utente di Adobe Mobile Services per configurare l’SDK per dispositivi mobili v4. Per l’installazione, l’utilizzo di Launch offre istruzioni di installazione personalizzate in base all’estensione scelta.

1. **Questa fine del supporto influisce sull&#39;SDK per tvOS?**

   Sì, per tvOS (versione 10+) l&#39;implementazione consigliata consiste nella migrazione alle estensioni Media Analytics.  Per ulteriori informazioni, consulta [Migrazione dall’SDK di Media autonomo ad Adobe Launch - iOS](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **Questa fine del supporto influisce sull’SDK per FireTV e AndroidTV? &#x200B;**

   Sì, per FireTV e AndroidTV, l’implementazione consigliata è quella di migrare alle estensioni Media Analytics.  Per ulteriori informazioni, consulta [Migrazione dall’SDK di Media autonomo ad Adobe Launch - Android](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).
