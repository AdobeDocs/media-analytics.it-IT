---
title: 'Creare un nuovo rapporto di debug '
description: Scopri come creare un nuovo rapporto di debug
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 100%

---

# Creare un nuovo rapporto di debug {#create-a-new-debug-report}

Per creare un nuovo rapporto di debug:

1. In [!UICONTROL Create New Debug Report], seleziona quanto segue:

   ![](assets/create-new-debug-report.png)

1. Compila i campi con le seguenti informazioni:

   * **Assegna un nome al rapporto**: inserisci il nome e la data del lettore in modo da poterlo tracciare facilmente durante la certificazione e mantenere i marchi e le piattaforme separati.
   * **Adobe Analytics**

      * [!UICONTROL User Name] e [!UICONTROL Shared Secret]: questi campi sono facoltativi, ma puoi aggiungere le credenziali API dei servizi Web ad Adobe Debug per visualizzare i nomi delle variabili e le relative impostazioni per la suite di rapporti.

        Puoi accedere in uno dei seguenti modi:

         * [!UICONTROL Analytics > Admin > Company Settings > Web Services]
         * [!UICONTROL Analytics > Admin > User Management > Users > Individual User Settings] Per creare una credenziale API di servizi Web per un nuovo utente, in [!UICONTROL User Management], aggiungi l’utente al gruppo di utenti dell’**Accesso al servizio Web**.

      * [!UICONTROL Default Endpoint]: i dati in questo campo sono forniti da Adobe e non possono essere modificati.
      * [!UICONTROL Extra Endpoint]: aggiungi `CNAMES`, se li utilizzi, per il server di tracciamento come `metrics.companyname.com`

   * **Video Heartbeat (Media Analytics)**

      * [!UICONTROL Default Endpoint]: i dati in questo campo sono forniti da Adobe e non possono essere modificati.
      * [!UICONTROL Extra Endpoint]: aggiungi `CNAMES`, se li utilizzi, per il server di tracciamento, ad esempio `metrics.companyname.com`.
