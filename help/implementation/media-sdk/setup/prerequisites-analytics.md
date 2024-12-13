---
title: Prerequisiti per le implementazioni basate solo su Adobe Analytics
description: Informazioni sui prerequisiti per l’utilizzo di Streaming Media Collection con implementazioni basate solo su Adobe Analytics
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 40%

---

# Prerequisiti per le implementazioni basate solo su Adobe Analytics

I prerequisiti descritti in questa sezione sono specifici per l’implementazione di Streaming Media Collection con implementazioni basate solo su Adobe Analytics (quando non si utilizza Edge).

1. **Completare i prerequisiti generali**<br>
Che tu implementi la raccolta di file multimediali in streaming per le implementazioni basate solo su Adobe Analytics o per quelle basate su Edge, accertati di soddisfare i [prerequisiti generali](/help/getting-started/prereqs.md).

1. **Conferma di disporre di un&#39;implementazione Adobe Analytics**<br>
Quando si implementa Streaming Media Collection con un’implementazione solo Analytics, è necessaria anche un’implementazione di base di Adobe Analytics. Per ulteriori informazioni, consulta [Implementare Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=it).

1. **Ottieni l’URL del server di tracciamento dei contenuti multimediali**<br>
Chiedi al tuo rappresentante Adobe Analytics l’URL del server di tracciamento dei contenuti multimediali. Questo è l&#39;URL `collection-api-server` per Mobile SDK, JavaScript SDK e il server di tracciamento non-collection-api per Roku. I nomi di dominio per l’implementazione API sono: `[your_namespace].hb-api.omtrdc.net`.

1. **Scarica il Media SDK corrente o implementa le estensioni richieste**<br>
A seconda del percorso di implementazione, [scarica l’SDK corrente](/help/getting-started/download-sdks.md) per piattaforme web, mobili o over-the-top. Per abilitare i percorsi delle estensioni di Streaming Media Collection, è necessario implementare le estensioni richieste.

1. **Abilita i rapporti di Adobe Analytics**<br>
Per abilitare i rapporti in Analytics e visualizzare il contenuto e i dati degli annunci che stai raccogliendo, è necessario abilitare i rapporti in Analytics. Consulta [Abilitazione di rapporti multimediali](/help/reporting/media-reports-enable.md).
