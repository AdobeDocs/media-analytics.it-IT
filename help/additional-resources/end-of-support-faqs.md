---
title: Informazioni sulle domande frequenti relative alla fine del supporto dell’SDK di Media Analytics
description: Questo argomento include le domande frequenti sulla fine del supporto per gli SDK Media Analytics.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 76%

---

# Domande frequenti su Mobile SDK di Media Analytics relative alla fine del supporto

Con la fine del supporto per gli SDK per dispositivi mobili versione 4, il 31 agosto 2021, Adobe ha anche terminato il supporto per gli SDK per dispositivi mobili di Media Analytics per iOS e Android. (Questo non include Media Analytics SDK for web (JS) e piattaforme OTT come Chromecast e Roku, che sono ancora supportate.)

Ciò significa che Adobe non fornisce più correzioni, aggiornamenti relativi al sistema operativo o supporto per il SDK mobile di Media Analytics. Durante la migrazione ai nuovi SDK Experience Platform, tieni presente che le [Estensioni Media Analytics](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) devono essere implementate per abilitare la raccolta multimediale Adobe Streaming.


## Le 5 cose più importanti da sapere

1. Gli SDK per dispositivi mobili v4 non sono più supportati a partire dal 31 agosto 2021. Esegui la migrazione agli SDK per dispositivi mobili di Adobe Experience Platform (AEP) per iOS e Android.

1. L’implementazione di Analytics for Streaming Media richiede l’SDK di AEP Mobile e l’utilizzo delle estensioni Analytics e Media Analytics. A partire dal 1° settembre 2021, è necessario utilizzare i nuovi SDK e le estensioni AEP Mobile.  Le estensioni di Media Analytics sono configurate tramite i Tag di Adobe (raccolta dati). Per ulteriori informazioni, consulta [Migrazione da Media SDK autonomo ad Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md)

1. Lo sviluppo delle funzioni è terminato per gli SDK Media Analytics per iOS e Android. Le nuove funzioni introdotte a partire dall’autunno 2019 vengono abilitate utilizzando le estensioni Media Analytics e l’API Media Collection.

1. Gli SDK Roku e Chromecast rimangono disponibili per i clienti Analytics per Streaming Media. Gli SDK Roku e Chromecast continueranno a essere migliorati e supportati come SDK autonomi. Se utilizzi l’SDK JS per Media Analytics, puoi continuare a utilizzare l’SDK autonomo o abilitare l’estensione Media Analytics tramite Adobe Data Collection (in precedenza Adobe Launch).

Per eventuali domande, contatta il tuo Account Team di Adobe.

## Domande frequenti

1. **Il supporto per gli SDK Roku e Chromecast sarà interessato?**

   No.  Gli SDK Roku e Chromecast continueranno a essere supportati come SDK autonomi per il momento.

1. **Questa modifica influisce sulle implementazioni dell’SDK JS di Media Analytics?**

   No.  I clienti che utilizzano l’SDK JS per Media Analytics possono continuare a utilizzare l’SDK o abilitarlo tramite Adobe Launch.

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
