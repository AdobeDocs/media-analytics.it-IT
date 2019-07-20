---
seo-title: Configurare Adobe Debug
title: Configurare Adobe Debug
uuid: e 416458 d-f 23 c -41 ce -8 d 99-fa 5076 c 455 f 0
translation-type: tm+mt
source-git-commit: 5ff3566fae2c1df559341057fafdd289774e4b2f

---


# Configure Adobe Debug{#configure-adobe-debug}

## Accessing Adobe Debug {#section_AF81E7AD331E41FFA371AB9DA924BFBB}

Per accedere ad Adobe Debug:

1. Go to [Experience Cloud](https://www.marketing.adobe.com) and create a new Adobe Experience Cloud user.

   >[!TIP]
   >
   >Questo login non è lo stesso nome utente e password che utilizzate per accedere ad Adobe Analytics.

1. Dopo aver ottenuto un account Experience Cloud, contatta il tuo rappresentante Adobe per richiedere l'accesso ad Adobe Debug.
1. After access has been granted, go to [https://debug.adobe.com](https://debug.adobe.com) and use your Experience Cloud credentials to log in.

   ![](assets/adobe-debug-login.png)

   I browser supportati per questo strumento sono:
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer versione 9-11

I browser consigliati sono le versioni più recenti di Chrome e Firefox.

## Debug Proxy {#section_8D3493B8426B46DEB9CD7E2ABD785D66}

Scarica e configura il proxy Debug:

1. Download the Debug Proxy app at [App Downloads.](https://debug.adobe.com/#/downloads)

   I sistemi operativi supportati sono:
   * OS X 10.7 a 64 bit o superiore
   * Windows 7.1 a 64 bit o superiore
   ![](assets/debug-proxy-app.png)

1. Il server debug proxy viene eseguito sul computer locale sulla porta 33284 e verrà impostato come proxy di sistema.

   Potrebbe essere necessario regolare le impostazioni del browser in base al sistema operativo e al browser.

## Download and install the SSL Certificate on desktop or apps {#section_2F9547E301CB413299A67BD59AFBEE0D}

La prima volta che eseguite Adobe Debug, viene generato un certificato SSL univoco. Se supportate il traffico HTTPS su computer desktop e/o app, dovete scaricare e installare il nostro certificato SSL.

Scaricate e installate il certificato SSL:

1. After Adobe Debug has been installed and started, go to [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) and download the certification.
1. Importare il certificato

   **Mac OS**
   1. Fate doppio clic sul certificato CA principale per aprirlo in Keychain Access.
   1. Il certificato CA principale viene visualizzato al momento del login.
   1. Spostate (trascinate) il certificato CA principale sul sistema.
   1. È necessario copiare il certificato nel sistema per assicurarsi che sia affidabile da parte di tutti gli utenti e dei processi locali del sistema.
   1. Aprire il certificato CA principale, espandere Confidence, selezionare Always Trust (Considera sempre attendibile) e salvare le modifiche.
   **Windows**
   1. Completa una delle procedure seguenti:

      * [Aggiunta di certificati allo store Trusted Root Certification Authority per un computer locale](https://technet.microsoft.com/en-us/library/cc754841.aspx#BKMK_addlocal)
<!--        * [How To Import a Trusted Root Certification Authority In Windows 7/Vista/XP](https://www.sqlservermart.com/HowTo/Windows_Import_Certificate.aspx) You might need to quit and reopen your browser to see the change.
-->

    1. Per Firefox, completa la procedura in [Installing root certificate in Mozilla Firefox (Installazione del certificato principale in Mozilla Firefox).](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)
    
    You might need to quit and reopen Firefox to see the change.
    
    ** Dispositivi iOS**
    1. Impostate il dispositivo iOS per utilizzare Adobe Debug come proxy HTTP facendo clic su** [! UICONTROL Settings app]**** &gt;**** [! UICONTROL Wifi settings]**.
    
    1. In Safari, andate a [Debug.](https://proxy.debug.adobe.com/ssl)
    
    Safari will prompt you to install the SSL certificate.

## Install the SSL certificate for your mobile device {#section_F2A3336F482C43E2ABEA742AD5CCACCA}

Se mancano le chiamate HTTPS in Adobe Debug, devi installare il certificato SSL per Adobe Debug sul dispositivo mobile.

### App

Per installare il certificato SSL su un dispositivo iOS:

1. On your laptop, turn on the Debug Proxy, and go to [Adobe Debug.](https://debug.adobe.com)
1. Completa i seguenti passaggi sul dispositivo iOS:
   1. Passate alla modalità aereo.
   1. Selezionate lo stesso segnale Wi-Fi utilizzato dal laptop.
   1. Nel portatile, imposta manualmente l'IP e la porta mostrati nell'app Debug Proxy.
   1. Aprite una finestra browser Apple Safari.
   1. Go to [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Scaricate e installate il certificato SSL.

1. Sul laptop, avvia la sessione Adobe Debug.
1. Avviate il test sul dispositivo iOS.

### Android

Per installare il certificato SSL su un dispositivo Android:

1. On your laptop turn on the Debug Proxy and go to [Adobe Debug.](https://debug.adobe.com)
1. Completa i passaggi seguenti sul dispositivo Android:
   1. Impostate il dispositivo su Modalità aereo.
   1. Selezionate lo stesso segnale Wi-Fi utilizzato dal laptop.
   1. Nel portatile, imposta manualmente l'IP e la porta mostrati nell'app Debug Proxy.
   1. Aprite una finestra del browser.
   1. Go to [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Scaricate e installate il certificato SSL.

1. Sul laptop, avvia la sessione Adobe Debug.
1. Avviate il test sul dispositivo Android.

