---
seo-title: Risoluzione della riproduzione principale tra annunci pubblicitari
title: Risoluzione della riproduzione principale tra annunci pubblicitari
uuid: 228 b 4812-c 23 e -40 c 8-ae 2 b-e 15 ca 69 b 0 bc 2
translation-type: tm+mt
source-git-commit: 8c20af925a1043c90b84d7d13021848725e05500

---


# Resolving main:play appearing between ads{#resolving-main-play-appearing-between-ads}

## PROBLEMA

In some ad tracking scenarios, you could encounter `main:play` calls occurring unexpectedly between the end of one ad and the start of the next ad. If the delay between the ad complete call and the next ad start call is greater than 250 milliseconds, the Media SDK will fall back to sending `main:play` calls. If this fallback to `main:play` occurs during a pre-roll ad break, the content start metric may be set early.

Uno spazio tra annunci come descritto in precedenza viene interpretato da Media SDK come contenuto principale, in quanto non ci si sovrappone ad alcun contenuto pubblicitario. In Media SDK non sono presenti informazioni di annunci pubblicitari, mentre il lettore è in stato di riproduzione. Se non sono presenti informazioni Ad e lo stato del lettore sta per essere riprodotto, l'SDK di Media SDK imposta la durata del vuoto verso il contenuto principale per impostazione predefinita. Non è possibile utilizzare la durata di riproduzione del credito per informazioni sull'annuncio null.

## IDENTIFICAZIONE

Quando usi Adobe Debug o un sniffer di pacchetti di rete come Charles, se vedi le seguenti chiamate Heartbeat in questo ordine durante un'interruzione di annunci precedente:

* Session Start: `s:event:type=start` &amp; `s:asset:type=main`
* Ad Start: `s:event:type=start` &amp; `s:asset:type=ad`
* Ad Play: `s:event:type=play` &amp; `s:asset:type=ad`
* Ad Complete: `s:event:type=complete` &amp; `s:asset:type=ad`
* Main Content Play: `s:event:type=play` &amp; `s:asset:type=main` **(unexpected)**

* Ad Start: `s:event:type=start` &amp; `s:asset:type=ad`
* Ad Play: `s:event:type=play` &amp; `s:asset:type=ad`
* Ad Complete: `s:event:type=complete` &amp; `s:asset:type=ad`
* Main Content Play: `s:event:type=play` &amp; `s:asset:type=main` **(expected)**

## RESOLUTION

***Ritardo nell'attivazione della chiamata Ad Complete.***

Handle the gap from within the player by calling `trackEvent:AdComplete` late for the first ad, followed immediately by `trackEvent:AdStart` for the second ad. The app should hold off on calling the `AdComplete` event after the first ad finishes. Make sure you call `trackEvent:AdComplete` for the last ad in the ad break. If the player can identify that the current ad asset is the final one in the ad break, call `trackEvent:AdComplete` immediately. Questa risoluzione darà luogo a meno di 1 secondi di tempo supplementare impiegato per essere attribuito all'unità di annunci precedente.

**All'avvio di un annuncio, incluso l'anteprima:**

* Create the `adBreak` object instance for the ad break; for example, `adBreakObject`.

* Chiamata `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**In ogni avvio di risorse pubblicitarie:**

* **Chiamata`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Invoca questa opzione solo se l'annuncio precedente non è stato completato. Consider a Boolean value to maintain an "`isinAd`" state for the previous ad.

* Create the ad object instance for the ad asset: for example, `adObject`.
* Populate the ad metadata, `adCustomMetadata`.
* Chiamata `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Call `trackPlay()` if this is the first ad in a pre-roll ad break.

**Per tutte le risorse pubblicitarie complete:**

* **Non effettuare una chiamata**

   >[!NOTE]
   >
   >If the application knows it is the last ad in the ad break, call `trackEvent:AdComplete` here and skip setting `trackEvent:AdComplete` in the `trackEvent:AdBreakComplete`

**On jump:**

* Chiamata `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**All'interruzione di annuncio completa:**

* **Chiamata`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >If this step is already performed above as part of the last `trackEvent:AdComplete` call then this can be skipped.

* Chiamata `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.

