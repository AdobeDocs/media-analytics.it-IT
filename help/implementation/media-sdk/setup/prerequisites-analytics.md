---
title: Prerequisiti per le implementazioni basate solo su Adobe Analytics
description: Scopri i prerequisiti per l’utilizzo del componente aggiuntivo Adobe Analytics for Streaming Media per le implementazioni basate solo su Adobe Analytics
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
TQID: https://experienceleague.adobe.com/falbDtUtqAMtmtQs2jLpEvUKmwvATotVu8njuTNZ09k
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdb
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 243
ht-degree: 9%

---

# Prerequisiti per le implementazioni basate solo su Adobe Analytics

I prerequisiti descritti in questa sezione sono specifici per l’implementazione del componente aggiuntivo Adobe Analytics for Streaming Media per le implementazioni basate solo su Adobe Analytics (quando non si utilizza Edge).

1. **Completare i prerequisiti generali**<br>
Che tu implementi i servizi di streaming multimediale per le implementazioni basate solo su Adobe Analytics o su Edge, accertati di soddisfare i [prerequisiti generali](/help/getting-started/prereqs.md).

1. **Conferma di disporre di un&#39;implementazione Adobe Analytics**<br>
Quando si implementa il componente aggiuntivo Adobe Analytics for Streaming Media per un’implementazione solo di Analytics, è necessaria anche un’implementazione di base di Adobe Analytics. Per ulteriori informazioni, consulta [Implementare Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=it).

1. **Ottieni l&#39;URL del server di tracciamento dei contenuti multimediali**<br>
Chiedi al tuo rappresentante Adobe Analytics l’URL del server di tracciamento dei contenuti multimediali. Questo è l&#39;URL `collection-api-server` per Mobile SDK, JavaScript SDK e il server di tracciamento non-collection-api per Roku. I nomi di dominio per l’implementazione API sono: `[your_namespace].hb-api.omtrdc.net`.

1. **Scarica il Media SDK corrente o implementa le estensioni richieste**<br>
A seconda del percorso di implementazione, [scarica il SDK](/help/getting-started/download-sdks.md) corrente per piattaforme web, mobili o over-the-top. È necessario implementare le estensioni richieste per abilitare il componente aggiuntivo Adobe Analytics for Streaming Media.

1. **Abilita rapporti Adobe Analytics**<br>
Per abilitare i rapporti in Analytics e visualizzare il contenuto e i dati degli annunci che stai raccogliendo, devi abilitare i rapporti in Analytics. Consulta [Abilitazione di rapporti multimediali](/help/reporting/media-reports-enable.md).
