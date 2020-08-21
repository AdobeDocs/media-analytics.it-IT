---
title: Configurazione di Adobe Debug
description: In questo argomento viene descritto come configurare  Debug Adobe, che potete utilizzare per risolvere eventuali problemi di implementazione di Media SDK.
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
translation-type: tm+mt
source-git-commit: f0f04ffab851999becb2b7771eef36ad7477c9f3
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 2%

---


# Configurazione di Adobe Debug{#configure-adobe-debug}

## Accesso al debug  Adobe {#accessing-adobe-debug}

Per accedere  Debug Adobe:

1. Vai a [Experience Cloud ](https://www.marketing.adobe.com) e create un nuovo utente Adobe Experience Cloud.

   >[!TIP]
   >
   >Questo login non è lo stesso nome utente/password usato per accedere  Adobe Analytics.

1. Dopo aver creato un account  Experience Cloud, contattate il rappresentante  Adobe per richiedere l&#39;accesso  Debug Adobe.
1. Dopo aver concesso l&#39;accesso, andate a [https://debug.adobe.com](https://debug.adobe.com) e utilizzate le credenziali  Experience Cloud per effettuare l&#39;accesso.

   ![](assets/adobe-debug-login.png)

   I browser supportati per questo strumento sono:
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer versioni 9-11

I browser consigliati sono le versioni più recenti di Chrome e Firefox.

## Debug proxy {#debug-proxy}

Scaricate e configurate il proxy di debug:

1. Scarica l&#39;app Debug Proxy in [Download delle app.](https://debug.adobe.com/#/downloads)

   I sistemi operativi supportati sono:
   * OS X 10.7 a 64 bit o superiore
   * Windows 7.1 a 64 bit o superiore

   ![](assets/debug-proxy-app.png)

1. Il server proxy di debug verrà eseguito sul computer locale sulla porta 33284 e verrà impostato come proxy di sistema.

   Potrebbe essere necessario regolare l&#39;impostazione del browser in base al sistema operativo e al browser.

## Scaricare e installare il certificato SSL sul desktop o sulle app {#download-and-install-sSL-desktop}

La prima volta che eseguite  Adobe Debug, verrà generato un certificato SSL univoco. Se supportate il traffico HTTPS tra desktop e/o app, dovete scaricare e installare il nostro certificato SSL.

Scaricate e installate il certificato SSL:

1. Dopo  Adobe di debug installato e avviato, andate a [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) e scaricare la certificazione.
1. Importare il certificato

   **Mac OS**
   1. Fare doppio clic sul certificato CA principale per aprirlo in Accesso portachiavi.
   1. Il certificato CA radice viene visualizzato nel login.
   1. Sposta (trascina) il certificato CA radice nel sistema.
   1. È necessario copiare il certificato nel sistema per assicurarsi che sia affidabile da parte di tutti gli utenti e i processi del sistema locale.
   1. Aprire il certificato CA principale, espandere Trust, selezionare Always Trust e salvare le modifiche.

   **Windows**
   1. Completare una delle procedure seguenti:

      * [Aggiunta di certificati all&#39;archivio Autorità di certificazione radice attendibili per un computer locale](https://technet.microsoft.com/en-us/library/cc754841.aspx#BKMK_addlocal)
   1. Per Firefox, completare la procedura in [Installazione del certificato radice in Mozilla Firefox.](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)

      Potrebbe essere necessario chiudere e riaprire Firefox per visualizzare la modifica.
   **Dispositivi iOS**
   1. Impostate il dispositivo iOS in modo che utilizzi  Debug Adobe come proxy HTTP facendo clic su **[!UICONTROL Settings app]** **>** **[!UICONTROL Wifi settings]**.

   1. In Safari, vai a [Debug.](https://proxy.debug.adobe.com/ssl)

      Safari chiederà di installare il certificato SSL.




## Installare il certificato SSL per il dispositivo mobile {#install-sSL-for-mobile-device}

Se  Debug Adobe mancano le chiamate HTTPS, è necessario installare il certificato SSL per  Debug Adobe sul dispositivo mobile.

### iOS

Per installare il certificato SSL su un dispositivo iOS:

1. Sul computer portatile, accendere il proxy di debug e passare a [ Debug Adobe.](https://debug.adobe.com)
1. Completa i seguenti passaggi sul dispositivo iOS:
   1. Ruotare il dispositivo in modalità aereo.
   1. Selezionare lo stesso segnale Wi-Fi utilizzato dal notebook.
   1. Sul notebook, impostate manualmente l&#39;IP e la porta visualizzate nell&#39;app Debug Proxy.
   1. Aprite una finestra del browser Apple Safari.
   1. Vai a [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Scaricate e installate il certificato SSL.

1. Sul computer portatile, avvia la sessione di debug  Adobe.
1. Avvia il test sul dispositivo iOS.

### Android

Per installare il certificato SSL su un dispositivo Android:

1. Sul computer portatile, accendi il proxy di debug e passa a [ Debug Adobe.](https://debug.adobe.com)
1. Completa i seguenti passaggi sul dispositivo Android:
   1. Impostate il dispositivo sulla modalità Aereo.
   1. Selezionare lo stesso segnale Wi-Fi utilizzato dal notebook.
   1. Sul notebook, impostate manualmente l&#39;IP e la porta visualizzate nell&#39;app Debug Proxy.
   1. Aprite una finestra del browser.
   1. Vai a [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Scaricate e installate il certificato SSL.

1. Sul computer portatile, avvia la sessione di debug  Adobe.
1. Avviate il test sul dispositivo Android.

