---
title: Informazioni sulle domande frequenti relative alla fine del supporto dell’SDK di Media Analytics
description: Questo argomento include le domande frequenti sulla fine del supporto per gli SDK Media Analytics.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/qfM2-x6s-SPf4gw2FpLlg7mPI-h-xZ3Y1TeeVALn3fQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdbid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 639
ht-degree: 62%

---

# Domande frequenti su Mobile SDK di Media Analytics relative alla fine del supporto

Con la fine del supporto per gli SDK per dispositivi mobili versione 4, il 31 agosto 2021, Adobe ha anche terminato il supporto per gli SDK per dispositivi mobili di Media Analytics per iOS e Android. (Questo non include Media Analytics SDK for web (JS) e piattaforme OTT come Chromecast e Roku, che sono ancora supportate.)

Ciò significa che Adobe non fornisce più correzioni, aggiornamenti relativi al sistema operativo o supporto per il SDK mobile di Media Analytics. Durante la migrazione ai nuovi SDK di Experience Platform, tieni presente che le [Estensioni di Media Analytics](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) devono essere implementate per abilitare i servizi multimediali in streaming di Adobe.


## Le 5 cose più importanti da sapere

1. Gli SDK per dispositivi mobili v4 non sono più supportati a partire dal 31 agosto 2021. Esegui la migrazione agli SDK per dispositivi mobili Adobe Experience Platform (AEP) per iOS e Android.

1. Un’implementazione di Adobe Streaming Media Services richiede AEP Mobile SDK e l’utilizzo delle estensioni Analytics e Media Analytics. A partire dal 1° settembre 2021, dovresti utilizzare i nuovi SDK e le estensioni per dispositivi mobili di AEP.  Le estensioni di Media Analytics sono configurate tramite i Tag di Adobe (raccolta dati). Per ulteriori informazioni, consulta [Migrazione da Media SDK autonomo ad Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md)

1. Lo sviluppo delle funzioni è terminato per gli SDK Media Analytics per iOS e Android. Le nuove funzioni introdotte a partire dall’autunno 2019 vengono abilitate utilizzando le estensioni Media Analytics e l’API Media Collection.

1. Gli SDK Roku e Chromecast rimangono disponibili per il cliente con il componente aggiuntivo Adobe Analytics for Streaming Media e il componente aggiuntivo Customer Journey Analytics Streaming Media Collection. Gli SDK Roku e Chromecast continueranno a essere migliorati e supportati come SDK autonomi. Se utilizzi l’SDK JS per Media Analytics, puoi continuare a utilizzare l’SDK autonomo o abilitare l’estensione Media Analytics tramite Adobe Data Collection (in precedenza Adobe Launch).

Per eventuali domande, contatta il team del tuo account Adobe.

## Domande frequenti

1. **Il supporto per gli SDK Roku e Chromecast sarà interessato?**

   No.  Gli SDK Roku e Chromecast continueranno a essere supportati come SDK autonomi per il momento&#x200B;.
&#x200B;
1. **Questa modifica influisce sulle implementazioni dell’SDK JS di Media Analytics?**

   No.  I clienti che utilizzano JS SDK per Media Analytics possono continuare a utilizzare SDK o abilitarlo tramite Adobe Launch.
&#x200B;
1. **Qual è il livello di impegno per la migrazione alle estensioni Media Analytics?**

   LOE dipende dall’implementazione di ciascun cliente, quindi varia.  Dopo aver esaminato la documentazione sulla migrazione riportata di seguito, rivolgiti alla consulenza e/o all’assistenza clienti per richiedere un supporto aggiuntivo.

   [Estensioni di Media Analytics: migrazione Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

   [Estensioni di Media Analytics: migrazione iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Estensioni di Media Analytics: nuove implementazioni](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

1. **È necessario disporre di Launch come sistema di gestione dei tag? Cosa succede se non voglio utilizzare Launch?**

   Per il caso d’uso dell’app mobile, Launch non viene utilizzato come sistema di gestione dei tag come avviene per il web. Per configurare le estensioni SDK è necessario utilizzare l’interfaccia utente di Launch. È simile a come utilizzi l’interfaccia utente di Adobe Mobile Services per configurare l’SDK per dispositivi mobili v4. Per l’installazione, l’utilizzo di Launch offre istruzioni di installazione personalizzate in base all’estensione scelta.

1. **Questa fine del supporto influisce sull’SDK per tvOS?**

   Sì, per tvOS (versione 10+) l’implementazione consigliata consiste nella migrazione alle estensioni Media Analytics. Per ulteriori informazioni, consulta [Migrazione da Media SDK autonomo ad Adobe Launch - iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md).

1. **Questa fine del supporto influisce sull’SDK per Fire TV e Android TV?**

   Sì, per Fire TV e Android TV, l’implementazione consigliata consiste nella migrazione alle estensioni Media Analytics. Per ulteriori informazioni, consulta [Migrazione da Media SDK autonomo ad Adobe Launch - Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md).
