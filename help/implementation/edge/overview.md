---
title: Panoramica sull’implementazione di Edge
description: Imposta lo schema, il set di dati e lo stream di dati di Adobe Experience Platform necessari per raccogliere i dati multimediali in streaming tramite Edge Network.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 4%

---

# Panoramica sull’implementazione di Edge

L’Edge Network di Adobe Experience Platform consente di inviare dati destinati a più prodotti a un singolo endpoint, che inoltra le informazioni appropriate a ciascun prodotto. Questo è il modo consigliato per implementare Streaming Media Collection ed è l’unico approccio che supporta sia Adobe Analytics che Customer Journey Analytics da una singola implementazione.

A differenza dell’approccio legacy di Media SDK, che richiedeva strumenti specifici per ogni soluzione Adobe, un’implementazione Edge utilizza un modello di dati XDM condiviso e un singolo stream di dati. I dati scorrono da SDK o API a Edge Network, che li indirizza quindi a qualsiasi prodotto Adobe configurato nel flusso di dati (Analytics, CJA, AJO o RTCDP). Ciò significa che il passaggio a un altro prodotto o l’aggiunta di prodotti a valle in un secondo momento non richiede la ristrumentazione degli eventi multimediali.

Indipendentemente dal codebase utilizzato, devi prima completare la configurazione della piattaforma descritta in questa pagina: crea uno schema, crea un set di dati e configura un flusso di dati.

## Prerequisiti

1. **Completare i prerequisiti generali.** Consulta i [prerequisiti generali](/help/getting-started/prereqs.md).

1. **Conferma una soluzione Adobe compatibile.** È necessaria un&#39;implementazione funzionante di almeno uno dei seguenti elementi:
   * [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=it): la destinazione di reporting principale per i dati multimediali basati su Edge
   * [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=it): supportato insieme o al posto di CJA tramite lo stesso flusso di dati
   * [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=it) o [Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html): aggiungi il servizio **[!UICONTROL Adobe Experience Platform]** allo stream di dati durante la configurazione di uno di questi

## Configurare lo schema in Adobe Experience Platform

Per standardizzare la raccolta dei dati tra le applicazioni che utilizzano Adobe Experience Platform, Adobe ha creato lo standard Experience Data Model (XDM) aperto e documentato pubblicamente.

1. In Adobe Experience Platform, iniziare a creare lo schema come descritto in [Creare e modificare gli schemi nell&#39;interfaccia utente](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en).

1. Nella pagina Dettagli schema, scegliere **[!UICONTROL Experience Event]** come classe base per lo schema.

   ![Gruppi di campi aggiunti](assets/schema-experience-event.png)

1. Seleziona **[!UICONTROL Next]**.

1. Specificare il nome e la descrizione dello schema, quindi selezionare **[!UICONTROL Finish]**.

1. Nell&#39;area **[!UICONTROL Composition]**, nella sezione **[!UICONTROL Field groups]**, selezionare **[!UICONTROL Add]**, quindi cercare e aggiungere i seguenti gruppi di campi allo schema:
   * `End User ID Details`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   Dopo aver aggiunto i gruppi di campi, questi vengono visualizzati nella sezione **[!UICONTROL Field groups]**:

   ![Gruppi di campi aggiunti](assets/schema-field-groups-added.png)

1. Seleziona **[!UICONTROL Save]** per salvare le modifiche.

1. (Facoltativo) Puoi nascondere alcuni campi dall’interfaccia utente dello schema. Questi campi sono campi di reporting calcolati dal server e compilati da Adobe nel backend, non vengono inviati da SDK o dall’API e non influiscono sulla raccolta dei dati. Nasconderli non ha alcun impatto funzionale; riduce solo il rumore visivo durante la navigazione nello schema nell’interfaccia utente di AEP. Questi campi fanno riferimento solo a quelli del gruppo di campi `MediaAnalytics Interaction Details`.

   +++ Espandi per visualizzare le istruzioni sui campi che puoi nascondere.

   1. Nell&#39;area **[!UICONTROL Structure]**, selezionare il campo `Media Collection Details`, quindi selezionare **[!UICONTROL Manage related fields]**.

      ![gestisci campi correlati](assets/manage-related-fields.png)

   1. Abilita l&#39;opzione a **[!UICONTROL Show display names for fields]**, quindi aggiorna lo schema come segue:

      * Nel campo `Media Collection Details` > `Advertising Details`, nascondi i seguenti campi di reporting: `Ad Completed`, `Ad Started` e `Ad Time Played`.

      * Nel campo `Media Collection Details` > `Advertising Pod Details`, nascondi il seguente campo di reporting: `Ad Break ID`

      * Nel campo `Media Collection Details` > `Chapter Details`, nascondere i seguenti campi di reporting: `Chapter Completed`, `Chapter ID`, `Chapter Started` e `Chapter Time Played`.

      * Nel campo `Media Collection Details`, nascondere il campo `List Of States`.

        ![nascondi stati raccolta file multimediali](assets/schema-hide-media-collection-states.png)

      * Nel campo `Media Collection Details` > `List Of States End` e `Media Collection Details` > `List Of States Start`, nascondi i seguenti campi di reporting: `Player State Count`, `Player State Set` e `Player State Time`.

        ![campi da nascondere](assets/schema-hide-listofstates.png)

      * Nel campo `Media Collection Details` > `Qoe Data Details`, nascondere i seguenti campi di reporting: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Impacted Streams`, `Buffer Events`, `Dropped Frame Impacted Streams`, `Drops Before Starts`, `Errors`, `External Error IDs`, `Error Impacted Streams`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Impacted Streams`, `Stalling Events`, `Total Buffer Duration` e `Total Stalling Duration`.

      * Nel campo `Media Collection Details` > `Session Details`, nascondere i seguenti campi di reporting: `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Content Completes`, `Chapter Count`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Segment Views`, `Media Downloaded Flag`, `Media Starts`, `Media Session ID`, `Media Session Server Timeout`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pev3`, `Pccr`, `Total Pause Duration`, `Unique Time Played` e `Video Segment`.

   1. Seleziona **[!UICONTROL Confirm]** per salvare le modifiche.

   1. Nell&#39;area **[!UICONTROL Structure]**, abilitare l&#39;opzione a **[!UICONTROL Show display names for fields]**, quindi selezionare il campo `List Of Media Collection Downloaded Content Events`.

   1. Selezionare **[!UICONTROL Manage related fields]**, quindi aggiornare lo schema come segue:

      * Nel campo `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details`, nascondi i seguenti campi di reporting: `Ad Completed`, `Ad Started` e `Ad Time Played`.

      * Nel campo `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details`, nascondi il seguente campo di reporting: `Ad Break ID`

      * Nel campo `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details`, nascondi i seguenti campi di reporting: `Chapter Completed`, `Chapter ID`, `Chapter Started` e `Chapter Time Played`.

      * Nel campo `List Of Media Collection Downloaded Content Events` > `Media Details`, nascondi il campo `List Of States`.

      * Nel campo `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` e `Media Collection Details` > `List Of States Start`, nascondi i seguenti campi di reporting: `Player State Count`, `Player State Set` e `Player State Time`.

      * Nel campo `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details`, nascondi i seguenti campi di reporting: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Events`, `Buffer Impacted Streams`, `Drops Before Starts`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Errors`, `External Error IDs`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`, `Stalling Impacted Streams`, `Total Buffer Duration` e `Total Stalling Duration`.

      * Nel campo `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details`, nascondere i seguenti campi di reporting: `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Content Completes`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Downloaded Flag`, `Media Segment Views`, `Media Session ID`, `Media Session Server Timeout`, `Media Starts`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pccr`, `Pev3`, `Total Pause Duration`, `Unique Time Played` e `Video Segment`.

      * Nel campo `List Of Media Collection Downloaded Content Events` > `Media Details`, nascondi il campo `Media Session ID`.

   1. Seleziona **[!UICONTROL Confirm]** per salvare le modifiche.

   1. Nell&#39;area **[!UICONTROL Structure]**, selezionare il campo `Media Reporting Details`, quindi selezionare **[!UICONTROL Manage related fields]**.

   1. Abilita l&#39;opzione a **[!UICONTROL Show display names for fields]**, quindi aggiorna lo schema come segue:

      * Nel campo `Media Reporting Details`, nascondere i campi seguenti: `Error Details`, `List Of States End`, `List of States Start` e `Media Session ID`.

   1. Seleziona **[!UICONTROL Confirm]** > **[!UICONTROL Save]** per salvare le modifiche.

   +++

1. (Facoltativo) Puoi aggiungere metadati personalizzati allo schema. Questo consente di includere metadati aggiuntivi definiti dall&#39;utente per esigenze o contesti specifici. Per ulteriori informazioni sui metadati personalizzati con l&#39;API di Media Edge, vedi [Supporto per metadati personalizzati](custom-metadata.md).

   +++ Espandi per visualizzare le istruzioni sull’aggiunta di metadati personalizzati allo schema.

   1. Individuare il nome tenant dell&#39;organizzazione selezionando **[!UICONTROL Account info]** > **[!UICONTROL Assigned orgs]** > [!UICONTROL _**nome organizzazione**_] > **[!UICONTROL tenant]**.

      I campi personalizzati vengono ricevuti tramite questo percorso. Ad esempio, nome tenant: _dcbl → percorso myCustomField: _dcbl.myCustomField.

   1. Aggiungi un gruppo di campi personalizzato allo schema multimediale definito.

      ![add-custom-metadata](assets/add-custom-metadata-fieldgroup.png)

   1. Aggiungi al gruppo di campi tutti i campi personalizzati di cui desideri tenere traccia.

      ![add-custom-metadata](assets/add-custom-fields.png)

   1. [Utilizza il percorso generato](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/fields/overview#type-specific-properties) per il campo personalizzato nel payload della richiesta.

      ![add-custom-metadata](assets/custom-fields-path.png)

   +++

## Creare un set di dati in Adobe Experience Platform

1. In Adobe Experience Platform, inizia a creare il set di dati come descritto nella [Guida dell&#39;interfaccia utente dei set di dati](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=it#create).

   Quando selezioni uno schema per il set di dati, scegli lo schema creato in precedenza.

## Configurare uno stream di dati in Adobe Experience Platform

1. Creare un nuovo stream di dati come descritto in [Configurare uno stream di dati](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en).

   Durante la creazione dello stream di dati, effettua le seguenti selezioni:

   * Nel campo **[!UICONTROL Event Schema]** selezionare lo schema creato in [Configurare lo schema in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform).

     >[!IMPORTANT]
     >
     >Selezionare **[!UICONTROL Save]**; non selezionare **[!UICONTROL Save and Add Mapping]**. La selezione di **[!UICONTROL Save and Add Mapping]** causa errori di mappatura per il campo Timestamp.

     ![Crea un flusso di dati e seleziona uno schema](assets/datastream-create-schema.png)

   * Aggiungi i servizi appropriati al flusso di dati in base alla soluzione Adobe. Per informazioni sull&#39;aggiunta di un servizio, vedere &quot;Aggiungere servizi a uno stream di dati&quot; in [Configurare uno stream di dati](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details).

      * **[!UICONTROL Adobe Analytics]** (se si utilizza Adobe Analytics): definire una suite di rapporti come descritto in [Creare una suite di rapporti](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite).

      * **[!UICONTROL Adobe Experience Platform]** (se si utilizza Customer Journey Analytics, Adobe Journey Optimizer o Real-Time Customer Data Platform)

     ![Aggiungi il servizio Adobe Analytics](assets/datastream-add-service.png)

   * Espandere **[!UICONTROL Advanced Options]**, quindi abilitare l&#39;opzione **[!UICONTROL Media Analytics]**.

     ![Opzione Media Analytics](assets/datastream-media-check.png)

## Scegli il metodo di implementazione

Con lo schema, il set di dati e lo stream di dati impostati, implementa una delle seguenti basi di codice per iniziare a inviare dati multimediali in streaming ad Edge Network. Ogni pagina descrive la configurazione specifica per i contenuti multimediali in streaming; il codice per evento e per variabile risiede in [Eventi](/help/implementation/events/overview.md) e [Variabili](/help/implementation/variables/overview.md).

Le implementazioni di **In-code** scrivono le chiamate SDK direttamente nel codice sorgente dell&#39;applicazione. **Utilizzo delle implementazioni Tags** utilizza [Tag Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home) che consente di configurare e distribuire le regole di tracciamento senza modificare il codice dell&#39;applicazione. Scegli quale approccio si adatta al flusso di lavoro di distribuzione.

| Codebase | In-code | Utilizzo dei tag |
|---|---|---|
| Web | [Web SDK](web-sdk.md) | [Estensione tag Web SDK](web-sdk-tags.md) |
| iOS | [iOS](ios.md) | [iOS (Tag)](ios-tags.md) |
| Android | [Android](android.md) | [Android (Tag)](android-tags.md) |
| Roku | [Edge Roku](roku.md) | — |
| API | [API Media Edge](media-edge-api.md) | — |

## Passaggio successivo

Dopo aver iniziato la raccolta dei dati, puoi configurare la generazione rapporti:

* [Configurare la generazione di rapporti per le implementazioni di Edge](/help/reporting/setup/edge-reporting.md) (Customer Journey Analytics)
* [Imposta il reporting per le implementazioni solo Analytics](/help/reporting/setup/analytics-reporting.md) (se lo stream di dati alimenta Adobe Analytics)

>[!MORELIKETHIS]
>
>* [Supporto metadati personalizzati](custom-metadata.md)
>* [Schema di reporting XDM](reporting-schema.md)
>* [Panoramica eventi](/help/implementation/events/overview.md)
