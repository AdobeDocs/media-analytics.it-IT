---
title: Migrare i tipi di pubblico al nuovo tipo di dati Adobe Analytics for Streaming Media
description: Scopri come migrare i tipi di pubblico al nuovo tipo di dati Adobe Analytics for Streaming Media
feature: Streaming Media
role: User, Admin, Developer
exl-id: 5664bf56-b228-430a-944c-faaab55fa108
TQID: https://experienceleague.adobe.com/TqsfcR2JgxVjDNx3-CBBa9n6pwvuGk9JgQ--DvWeHg0
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 516
ht-degree: 0%

---

# Migrare i tipi di pubblico ai nuovi campi dei contenuti multimediali in streaming

In questo documento viene descritto come eseguire la migrazione di un pubblico che utilizza campi del tipo di dati di Adobe Streaming Media Services denominato &quot;Media&quot; per utilizzare il nuovo tipo di dati corrispondente denominato &quot;[Media Reporting Details](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;.

## Migrare un pubblico

Per migrare un pubblico dal vecchio tipo di dati denominato &quot;Media&quot; al nuovo tipo di dati denominato &quot;[Dettagli report multimediali](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;, è necessario modificare il pubblico e in ogni regola sostituire il vecchio campo dal tipo di dati obsoleto con il nuovo campo corrispondente del nuovo tipo di dati:

1. Individua le regole contenenti i campi del tipo di dati &quot;Media&quot; obsoleto. Questi sono tutti i campi che iniziano con il percorso, `media.mediaTimed`.

1. Duplica tali regole utilizzando i campi del nuovo tipo di dati &quot;[Dettagli report multimediali](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;.

1. Mantieni entrambe le regole attive finché non verifichi che i tipi di pubblico funzionino come previsto.

1. Rimuovi le regole che contengono campi dal tipo di dati &quot;Contenuto multimediale&quot; obsoleto.

1. Verifica che i tipi di pubblico funzionino ancora come previsto.

Vedere il parametro [ID contenuto](/help/reporting/dimensions/content.md) e le altre variabili dei contenuti multimediali in streaming documentate in [Servizi multimediali in streaming](/help/media-overview.md) per eseguire la mappatura tra i campi precedenti e i nuovi campi. Il vecchio percorso di campo si trova nella proprietà &quot;Percorso campo XDM&quot;, mentre il nuovo percorso di campo si trova nella proprietà &quot;Percorso campo XDM per reporting&quot;.

![Percorsi di campo XDM vecchi e nuovi](assets/field-paths-updated.jpeg)

## Esempio

Per seguire più facilmente le linee guida per la migrazione, considera l’esempio seguente che contiene un pubblico con una singola regola. Poiché il pubblico dispone di una singola regola, è necessario applicare le linee guida per la migrazione una sola volta.

1. Seleziona il pulsante [!UICONTROL **Modifica pubblico**] nell&#39;angolo superiore destro.

1. Individua le regole configurate per il pubblico.

   ![Modifica pubblico](assets/audience-edit.jpeg)

   ![Modifica pubblico](assets/audience-edit2.jpeg)

1. Seleziona la regola per aprirne la configurazione.

   ![Modifica pubblico](assets/audience-edit3.jpeg)

1. (Facoltativo) Per visualizzare il percorso del campo utilizzato nella regola, seleziona il pulsante Info accanto al nome del campo.

   ![Modifica pubblico](assets/audience-edit4.jpeg)

1. Identifica il nome del campo (in questo caso &quot;Media Starts&quot;).

   ![Modifica pubblico](assets/audience-edit5.jpeg)

1. Vedi le variabili dei contenuti multimediali in streaming documentate in [Servizi multimediali in streaming](/help/media-overview.md) per la mappatura tra i campi precedenti. Il vecchio percorso di campo si trova nella proprietà &quot;Percorso campo XDM&quot;, mentre il nuovo percorso di campo si trova nella proprietà &quot;Percorso campo XDM per reporting&quot;. Ad esempio, per il parametro [Media Starts](/help/reporting/metrics/media-starts.md), il corrispondente per `media.mediaTimed.impressions.value` è `xdm.mediaReporting.sessionDetails.isViewed`.

   ![Percorso XDM aggiornato](assets/updated-xdm-path.jpeg)

1. Aggiungi la stessa regola di quella esistente utilizzando il nuovo campo.

   ![Aggiungi regola](assets/add-rule.jpeg)

   ![Aggiungi regola](assets/add-rule2.jpeg)

   ![Aggiungi regola](assets/add-rule3.jpeg)

1. Seleziona [!UICONTROL **Salva**] per salvare il pubblico. Puoi mantenere questa configurazione per il tempo necessario a verificare che il pubblico funzioni ancora come previsto.

1. Al termine della convalida, rimuovi il campo precedente, quindi seleziona [!UICONTROL **Salva**] per salvare il pubblico.

   ![Aggiungi regola](assets/add-rule4.jpeg)

1. Convalida di nuovo il pubblico.

   Il processo di migrazione del pubblico è stato completato.
