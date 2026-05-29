---
title: Migrare i tipi di pubblico al nuovo tipo di dati Adobe Analytics for Streaming Media
description: Scopri come migrare i tipi di pubblico al nuovo tipo di dati Adobe Analytics for Streaming Media
feature: Streaming Media
role: User, Admin, Developer
exl-id: 67e67a4b-bd61-4247-93b7-261bd348d29b
TQID: https://experienceleague.adobe.com/Y-Y-xWKm-zOzaQm8kMbgGx8r6BTNLl-Q5AltlF5v7aA
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 759
ht-degree: 1%

---

# Migra Customer Journey Analytics per utilizzare i nuovi campi per contenuti multimediali in streaming

In questo documento viene descritto come aggiornare una configurazione di Customer Journey Analytics che utilizza il tipo di dati di Adobe Streaming Media Services denominato &quot;Media&quot; per utilizzare il nuovo tipo di dati corrispondente denominato &quot;[Media Reporting Details](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;.

## Migra Customer Journey Analytics

Per eseguire la migrazione di un&#39;installazione di Customer Journey Analytics dal vecchio tipo di dati denominato &quot;Media&quot; al nuovo tipo di dati denominato &quot;[Media Reporting Details](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;, è necessario aggiornare le seguenti impostazioni che utilizzano il vecchio tipo di dati:

* Visualizzazioni dati

* Campi derivati

### Eseguire la migrazione delle visualizzazioni dati

Per migrare le visualizzazioni dati al nuovo tipo di dati:

1. Individua tutte le visualizzazioni dati utilizzando il tipo di dati &quot;Media&quot; obsoleto. In tutti i campi il percorso inizia con `media.mediaTimed`.

1. Esegui una delle operazioni seguenti:

   * In tali visualizzazioni dati, inserisci i campi dal nuovo tipo di dati &quot;Dettagli report multimediali&quot;.

   * Creare un campo derivato che utilizza il nuovo tipo di dati &quot;Dettagli di Media Reporting&quot;, se è impostato, o che utilizza il vecchio tipo di dati &quot;Media&quot; se non è impostato il tipo di dati &quot;Dettagli di Media Reporting&quot;.

### Migra campi derivati

Per migrare i campi derivati al nuovo tipo di dati:

1. Individua tutti i campi derivati utilizzando il tipo di dati &quot;Media&quot; obsoleto. Si tratta di tutti i campi derivati che contengono campi il cui percorso inizia con `media.mediaTimed`.

1. Sostituisci tutti i vecchi campi nel campo derivato con il nuovo campo corrispondente da &quot;Media Reporting Details&quot;.

Vedere il parametro [ID contenuto](/help/reporting/dimensions/content.md) e le altre variabili dei contenuti multimediali in streaming documentate in [Servizi multimediali in streaming](/help/media-overview.md) per eseguire la mappatura tra i campi precedenti e i nuovi campi. Il vecchio percorso di campo si trova nella proprietà &quot;Percorso campo XDM&quot;, mentre il nuovo percorso di campo si trova nella proprietà &quot;Percorso campo XDM per reporting&quot;.

![Percorsi di campo XDM vecchi e nuovi](assets/field-paths-updated.jpeg)

## Esempio

Per seguire più facilmente le linee guida per la migrazione, considera l’esempio seguente che contiene una visualizzazione dati con campi del vecchio tipo di dati &quot;Media&quot; obsoleto. In questa visualizzazione dati, devi aggiungere i nuovi campi corrispondenti.

### Aggiornare la visualizzazione dati

Per aggiornare la visualizzazione dati, puoi utilizzare una delle seguenti opzioni:

#### Opzione 1

1. Individua una metrica o una dimensione che utilizza il vecchio campo del tipo di dati obsoleto.

   ![Percorso campo precedente nella visualizzazione dati](assets/old-field-data-view.jpeg)

1. Controlla il nuovo campo corrispondente nell&#39;articolo [Offset capitolo](/help/reporting/dimensions/chapter-offset.md).

1. Individua il nuovo campo corrispondente nella visualizzazione dati.

   ![Nuovo percorso campo nella visualizzazione dati](assets/new-field-data-view.jpeg)

1. Trascina il nuovo campo nella metrica o dimensione.

1. Ripeti questo processo per tutte le metriche e le dimensioni che utilizzano campi del tipo di dati &quot;Media&quot; obsoleto.

#### Opzione 2

Questa opzione crea un campo derivato che seleziona il valore dal campo precedente o il valore dal nuovo campo in base al quale esiste un campo per un evento specifico. Questo campo derivato sostituisce il vecchio tipo di dati &quot;Media&quot; in tutti i progetti in cui viene utilizzato.

Se si desidera creare un campo derivato per il &quot;Nome capitolo&quot; che utilizza il nuovo tipo di dati &quot;Dettagli di Media Reporting&quot;, se è impostato, o che utilizza il vecchio tipo di dati &quot;Media&quot; se il tipo di dati &quot;Dettagli di Media Reporting&quot; non è impostato:

1. Trascinare una clausola &quot;Case When&quot; nei campi derivati.

   ![Personalizzare il nuovo campo per creare una visualizzazione dati](assets/create-derived-field2.jpeg)

1. Compilare la clausola [!UICONTROL **If**] utilizzando il valore del **Percorso campo XDM per reporting**, come illustrato nella pagina [Nome capitolo](/help/reporting/dimensions/chapter-name.md).

   ![Nome capitolo](assets/chapter-name.jpeg)

   ![Nome capitolo](assets/chapter-name2.jpeg)

   ![Condizione campo derivato](assets/derived-field-condition.jpeg)

   ![Nome capitolo campo derivato](assets/derived-field-chapter-name.jpeg)

1. Popola il valore di fallback utilizzando il vecchio campo del tipo di dati &quot;Media&quot; obsoleto.

   ![Valore di fallback](assets/fallback-value.jpeg)

   ![Valore di fallback](assets/fallback-value2.jpeg)

   Definizione finale del campo derivato.

   ![Campo derivato completato](assets/derived-field-complete.jpeg)

1. Per aggiornare i campi derivati, individuare un campo derivato che utilizza i campi obsoleti (percorso che inizia con `media.mediaTimed`).

   ![campo derivato](assets/old-derived-field.jpeg)

1. Passa il puntatore del mouse sul campo derivato che desideri aggiornare, quindi seleziona l&#39;icona [!UICONTROL **Modifica**].

1. Individuare tutti i campi del vecchio tipo di dati (percorso che inizia con `media.mediaTimed`) e sostituirli con il nuovo campo corrispondente.

   ![Individua campo con tipo di dati precedente](assets/locate-fields-with-old-datatype.jpeg)

1. Controlla il nuovo campo corrispondente nell&#39;articolo [Nome contenuto](/help/reporting/dimensions/content-name.md).

1. Sostituire il campo precedente con il nuovo campo.

   ![Nuovo campo](assets/derived-field-new.jpeg)

1. Ripeti questo processo per tutti i campi derivati utilizzando i campi del vecchio tipo di dati &quot;Media&quot; obsoleto.

   La migrazione della configurazione di CJA è stata completata.
