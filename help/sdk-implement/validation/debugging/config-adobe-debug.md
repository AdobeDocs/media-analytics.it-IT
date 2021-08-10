---
title: Configurazione di Adobe Debug
description: '"Scopri come configurare Adobe Debug, che può essere utilizzato per risolvere i problemi relativi alle implementazioni Media SDK."'
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
exl-id: 48ad3f23-f36d-44f3-b8d9-b0b3a2ee06bc
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 41023be25308092a1b3e7c40bad2d8085429a0bc
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 2%

---

# Configurazione di Adobe Debug{#configure-adobe-debug}

## Accesso al debug Adobe {#accessing-adobe-debug}

Per accedere ad Adobe Debug:

1. Vai a [Experience Cloud](https://www.marketing.adobe.com/) e crea un nuovo utente Adobe Experience Cloud.

   >[!TIP]
   >
   >Questo login non è lo stesso nome utente/password che usi per accedere ad Adobe Analytics.

1. Dopo aver creato un account di Experience Cloud, contatta il tuo rappresentante Adobe per richiedere l&#39;accesso ad Adobe Debug.
1. Dopo aver concesso l&#39;accesso, vai su [https://debug.adobe.com](https://debug.adobe.com) e utilizza le tue credenziali Experience Cloud per accedere.

   ![](assets/adobe-debug-login.png)

   I browser supportati per questo strumento sono:
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer versioni 9-11

I browser consigliati sono le versioni più recenti di Chrome e Firefox.

## Debug proxy {#debug-proxy}

Scarica e configura il proxy di debug:

1. Scarica l&#39;app Debug Proxy in [Download app.](https://debug.adobe.com/#/downloads)

   I sistemi operativi supportati sono:
   * OS X 10.7 a 64 bit o superiore
   * Windows 7.1 a 64 bit o superiore

   ![](assets/debug-proxy-app.png)

1. Il server proxy di debug verrà eseguito sul computer locale sulla porta 33284 e verrà impostato come proxy di sistema.

   Potrebbe essere necessario regolare le impostazioni del browser in base al sistema operativo e al browser.

## Scarica e installa il certificato SSL sul desktop o sulle app {#download-and-install-sSL-desktop}

La prima volta che esegui Adobe Debug, verrà generato un certificato SSL univoco. Se supporti il traffico HTTPS tra desktop e/o app, devi scaricare e installare il nostro certificato SSL.

Scarica e installa il certificato SSL:

1. Dopo aver installato e avviato Adobe Debug, passa a [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) e scarica la certificazione.
1. Importa certificato

   **Mac OS**
   1. Fare doppio clic sul certificato CA principale per aprirlo in Accesso Portachiavi.
   1. Il certificato CA radice viene visualizzato nell&#39;accesso.
   1. Sposta (trascina) il certificato CA radice nel sistema.
   1. È necessario copiare il certificato in System per assicurarsi che sia attendibile per tutti gli utenti e i processi di sistema locali.
   1. Aprire il certificato CA principale, espandere Trust, selezionare Sempre attendibile e salvare le modifiche.

   **Windows**
   1. Completare una delle procedure seguenti:

      * [Aggiunta di certificati all&#39;archivio Autorità di certificazione radice attendibili per un computer locale](https://technet.microsoft.com/en-us/library/cc754841.aspx#BKMK_addlocal)
   1. Per Firefox, completa la procedura in [Installazione del certificato principale in Mozilla Firefox.](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)

      Potrebbe essere necessario chiudere e riaprire Firefox per visualizzare la modifica.
   **Dispositivi iOS**
   1. Imposta il tuo dispositivo iOS per utilizzare Adobe Debug come proxy HTTP facendo clic su **[!UICONTROL Settings app]** **>** **[!UICONTROL Wifi settings]**.

   1. In Safari, vai a [Debug.](https://proxy.debug.adobe.com/ssl)

      In Safari verrà richiesto di installare il certificato SSL.




## Installa il certificato SSL per il dispositivo mobile {#install-sSL-for-mobile-device}

Se mancano le chiamate HTTPS in Adobe Debug, devi installare il certificato SSL per Adobe Debug sul dispositivo mobile.

### iOS

Per installare il certificato SSL su un dispositivo iOS:

1. Sul tuo laptop, accendi il proxy di debug e vai a [Debug Adobe.](https://debug.adobe.com)
1. Completa i seguenti passaggi sul tuo dispositivo iOS:
   1. Ruotare il dispositivo in modalità aereo.
   1. Selezionare lo stesso segnale Wi-Fi utilizzato dal portatile.
   1. Sul laptop, imposta manualmente l&#39;IP e la porta mostrati nell&#39;app Debug Proxy.
   1. Apri una finestra del browser Apple Safari.
   1. Vai a [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Scarica e installa il certificato SSL.

1. Sul laptop, avvia la sessione di debug di Adobe.
1. Avvia il test sul dispositivo iOS.

### Android

Per installare il certificato SSL su un dispositivo Android:

1. Sul laptop, accendi il proxy di debug e vai a [Debug Adobe.](https://debug.adobe.com)
1. Completa i seguenti passaggi sul tuo dispositivo Android:
   1. Impostare il dispositivo su Modalità aeroplano.
   1. Selezionare lo stesso segnale Wi-Fi utilizzato dal portatile.
   1. Sul laptop, imposta manualmente l&#39;IP e la porta mostrati nell&#39;app Debug Proxy.
   1. Apri una finestra del browser.
   1. Vai a [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Scarica e installa il certificato SSL.

1. Sul laptop, avvia la sessione di debug di Adobe.
1. Avvia il test sul dispositivo Android.
