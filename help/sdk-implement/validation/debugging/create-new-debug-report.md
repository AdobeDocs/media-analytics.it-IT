---
title: Creazione di un nuovo report di debug
description: Scopri come creare un nuovo report di debug.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 5%

---

# Crea un nuovo report di debug{#create-a-new-debug-report}

Per creare un nuovo report di debug:

1. In [!UICONTROL Create New Debug Report] seleziona quanto segue:

   ![](assets/create-new-debug-report.png)

1. Compila i campi con le seguenti informazioni:

   * **Denomina il report**  - Inserisci il nome e la data del lettore in modo da poter tenere traccia del lettore durante la certificazione e mantenere i marchi e le piattaforme separati.
   * **Adobe Analytics**

      * [!UICONTROL User Name] e  [!UICONTROL Shared Secret] - Questi campi sono facoltativi, ma puoi aggiungere le credenziali API dei servizi web ad Adobe Debug per visualizzare i nomi delle variabili e le impostazioni delle variabili per la suite di rapporti.

         Puoi accedere a in uno dei seguenti modi:

         * [!UICONTROL Analytics > Admin > Company Settings > Web Services]
         * [!UICONTROL Analytics > Admin > User Management > Users > Individual User Settings] Per creare una credenziale API dei servizi Web per un nuovo utente, in  [!UICONTROL User Management], aggiungi l’utente al gruppo di utenti  **Web Service** Access .
      * [!UICONTROL Default Endpoint] - I dati in questo campo sono forniti dall&#39;Adobe e non possono essere modificati.
      * [!UICONTROL Extra Endpoint] - Aggiungi  `CNAMES`, se li utilizzi, per il server di tracciamento come  `metrics.companyname.com`
   * **Video Heartbeat (Media Analytics)**

      * [!UICONTROL Default Endpoint] - I dati in questo campo sono forniti dall&#39;Adobe e non possono essere modificati.
      * [!UICONTROL Extra Endpoint] - Aggiungi  `CNAMES`, se li utilizzi, per il server di tracciamento, ad esempio  `metrics.companyname.com`.
