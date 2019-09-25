---
seo-title: Creare un nuovo rapporto Debug
title: Creare un nuovo rapporto Debug
uuid: 438fde3d-98f9-46d1-9672-75d204361568
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# Creare un nuovo rapporto Debug{#create-a-new-debug-report}

Per creare un nuovo rapporto di debug:

1. In [!UICONTROL Create New Debug Report] select the following:

   ![](assets/create-new-debug-report.png)

1. Compila i campi con le seguenti informazioni:

   * **Denominate il report** - Immettete il nome e la data del lettore in modo da poter monitorare facilmente il lettore durante la certificazione e mantenere i marchi e le piattaforme separati.
   * **Adobe Analytics**

      * [!UICONTROL User Name] e [!UICONTROL Shared Secret] - Questi campi sono facoltativi, ma puoi aggiungere le credenziali API dei servizi Web ad Adobe Debug per visualizzare i nomi delle variabili e le impostazioni delle variabili per la suite di rapporti.

         Potete accedere in uno dei seguenti modi:

         * [!UICONTROL Analytics > Admin > Company Settings > Web Services]
         * [!UICONTROL Analytics > Admin > User Management > Users > Individual User Settings] Per creare una credenziale API di servizi Web per un nuovo utente, in [!UICONTROL User Management], aggiungere l'utente al gruppo di utenti **Web Service Access** .
      * [!UICONTROL Default Endpoint] - I dati in questo campo vengono forniti da Adobe e non possono essere modificati.
      * [!UICONTROL Extra Endpoint] - Aggiungi `CNAMES`, se li usi, per il server di tracciamento come `metrics.companyname.com`
   * **Video Heartbeat (Media Analytics)**

      * [!UICONTROL Default Endpoint] - I dati in questo campo vengono forniti da Adobe e non possono essere modificati.
      * [!UICONTROL Extra Endpoint] - Aggiungi `CNAMES`, se li utilizzi, al server di tracciamento, ad esempio `metrics.companyname.com`.



