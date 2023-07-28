---
title: Prerequisiti per le implementazioni basate solo su Adobe Analytics
description: Informazioni sui prerequisiti per l’utilizzo di Streaming Media con implementazioni basate solo su Adobe Analytics
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: c4d058ee82f4995f42bfe21c0442004f1f7ea4af
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 58%

---

# Prerequisiti per le implementazioni basate solo su Adobe Analytics

I prerequisiti descritti in questa sezione sono specifici per l’implementazione di Streaming Media con implementazioni basate solo su Adobe Analytics (quando non si utilizza Edge).

1. **Completare i prerequisiti generali**<br>
Che tu implementi Streaming Media per implementazioni basate solo su Adobe Analytics o Edge, assicurati di soddisfare i requisiti [prerequisiti generali](/help/getting-started/prereqs.md).

1. **Conferma di disporre di un’implementazione Adobe Analytics**<br>
Quando si implementano Streaming Media con un’implementazione solo Analytics, è necessaria anche un’implementazione di base di Adobe Analytics. Per ulteriori informazioni, consulta [Implementare Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=it).

1. **Ottieni l’URL del server di tracciamento dei contenuti multimediali**<br>
Chiedi al tuo rappresentante Adobe Analytics l’URL del server di tracciamento dei contenuti multimediali. Questo è l’ `collection-api-server` URL per Mobile SDK, SDK per JavaScript e il server di tracciamento non-collection-api per Roku. I nomi di dominio per l’implementazione API sono: `[your_namespace].hb-api.omtrdc.net`.

1. **Scarica il Media SDK corrente o implementa le estensioni richieste**<br>
A seconda del percorso di implementazione, [scarica l’SDK corrente](/help/getting-started/download-sdks.md) per piattaforme web, mobili o over-the-top. Per abilitare i percorsi di estensione di Adobe Analytics for Streaming Media, è necessario implementare le estensioni richieste.

1. **Abilita i rapporti di Adobe Analytics**<br>
Per abilitare i rapporti in Analytics e visualizzare il contenuto e i dati degli annunci che stai raccogliendo, è necessario abilitare i rapporti in Analytics. Consulta [Abilitazione di rapporti multimediali](/help/reporting/media-reports-enable.md).
