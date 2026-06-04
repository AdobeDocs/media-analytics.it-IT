---
title: Migrare i profili ai nuovi campi di Streaming Media
description: Scopri come migrare i profili ai nuovi campi di Streaming Media
feature: Streaming Media
role: User, Admin, Developer
exl-id: 0f75e594-5216-4ac1-91bd-fa89ab4b2110
TQID: https://experienceleague.adobe.com/c1WHnEeZnI3PP6aO40pDHpJCi2Z0ERiNY8lCj4wyMiU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 92e1a77339d29b0ef7ec8adc76817b2ac61ee900
workflow-type: tm+mt
source-wordcount: 522
ht-degree: 0%

---

# Migrare i profili ai nuovi campi dei contenuti multimediali in streaming

Questo documento descrive il processo di migrazione del servizio di filtro profili esistente sopra i flussi di raccolta dati di Adobe abilitati per Adobe Analytics per i dati multimediali in streaming. La migrazione converte il servizio di filtro dei profili dall&#39;utilizzo del tipo di dati Adobe Streaming Media Services denominato &quot;Media&quot; per l&#39;utilizzo del nuovo tipo di dati corrispondente denominato &quot;[Media Reporting Details](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;.

## Migrare i profili

Per migrare il filtro dei profili dal vecchio tipo di dati denominato &quot;Media&quot; al nuovo tipo di dati denominato &quot;[Media Reporting Details](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;, è necessario modificare le regole di filtro dei profili esistenti:

1. In Adobe Experience Platform, nella sezione **[!UICONTROL Sources]**, vai alla scheda **[!UICONTROL Dataflows]**.

1. Individua il flusso di dati responsabile dell’importazione di dati multimediali in streaming da Adobe Analytics a Adobe Experience Platform tramite Raccolta dati di Adobe.

1. Selezionare **[!UICONTROL Update dataflow]** per modificare l&#39;impostazione del filtro profili sostituendo ogni regola personalizzata contenente un campo obsoleto con il nuovo campo corrispondente del nuovo oggetto XDM.

1. Individua i filtri contenenti i campi dell’oggetto &quot;Media&quot; obsoleto.

1. Aggiungi questi filtri aggiungendo campi dal nuovo oggetto &quot;Dettagli di Media Reporting&quot;.

1. Utilizza un operatore OR tra i due campi;

1. Verifica che i profili funzionino ancora come previsto.

Vedere il parametro [ID contenuto](/help/reporting/dimensions/content.md) e le altre variabili dei contenuti multimediali in streaming documentate in [Servizi multimediali in streaming](/help/media-overview.md) per eseguire la mappatura tra i campi precedenti e i nuovi campi. Il vecchio percorso di campo si trova nella proprietà &quot;Percorso campo XDM&quot;, mentre il nuovo percorso di campo si trova nella proprietà &quot;Percorso campo XDM per reporting&quot;.

## Esempio

Per seguire più facilmente le linee guida per la migrazione, considera il seguente flusso di dati di esempio che contiene una singola regola di filtro del profilo. In questo caso, poiché esiste una sola regola, è necessario applicare le linee guida sulla migrazione una sola volta.

1. In Adobe Experience Platform, nella sezione **[!UICONTROL Sources]**, vai alla scheda **[!UICONTROL Dataflows]**.

1.Individua il flusso di dati responsabile dell’importazione di dati multimediali in streaming da Adobe Analytics a Adobe Experience Platform tramite Adobe Analytics.

1. Selezionare **[!UICONTROL Update dataflow]** per accedere all&#39;interfaccia utente di modifica, come illustrato nell&#39;immagine seguente.

   ![Profilo flusso di dati AEP](../../assets/aep-dataflow-profile.jpeg)

1. Selezionare **[!UICONTROL Next]** per passare alla scheda Filtro.

   ![Scheda filtro flusso di dati di AEP](../../assets/aep-dataflow-filtering-profile.jpeg)

1. Nella scheda **[!UICONTROL Filtering]**, identificare le regole di filtro che si basano sui campi `media.mediaTimed`.

   ![Regole filtro flusso di dati di AEP](../../assets/dataflow-filtering-rules-profile.jpeg)


   Per ogni filtro che utilizza l&#39;oggetto media.mediaTimed, trovare il corrispondente nell&#39;oggetto `mediaReporting` utilizzando le variabili di Streaming Media documentate in [Streaming Media Services](/help/media-overview.md) per eseguire la mappatura tra i vecchi campi e i nuovi campi. Il vecchio percorso di campo si trova nella proprietà &quot;Percorso campo XDM&quot;, mentre il nuovo percorso di campo si trova nella proprietà &quot;Percorso campo XDM per reporting&quot;. Ad esempio, per [Media Starts](/help/reporting/metrics/media-starts.md), il corrispondente per `media.mediaTimed.impressions.value` è `xdm.mediaReporting.sessionDetails.isViewed`.

   ![Campi XDM nuovi e precedenti](../../assets/xdm-fields-new-and-old.jpeg)

1. Trascina il campo `mediaReporting` rilevante nella regola di filtro e utilizza l&#39;operatore OR tra le due regole. Aggiungi la stessa regola di quella esistente quando utilizzi il nuovo campo.

   ![Aggiungi regole filtro](../../assets/add-filter-rules.jpeg)

1. Seleziona **[!UICONTROL Next]** per salvare le modifiche.
