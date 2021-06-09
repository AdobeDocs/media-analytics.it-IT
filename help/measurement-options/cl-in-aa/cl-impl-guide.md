---
title: Guida all’implementazione di Custom Link
description: null
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
exl-id: ee6f931a-ef80-4ebe-8ccb-cdbf970516e6
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 3%

---

# Guida all’implementazione di Custom Link{#custom-link-implementation-guide}

Il tracciamento video personalizzato utilizza il tracciamento manuale dei collegamenti tramite codice di collegamento personalizzato in Analytics `appMeasurement`.
Nella maggior parte dei casi, il tracciamento video con collegamenti video personalizzati viene utilizzato su piattaforme e dispositivi in cui è necessaria una misurazione video minima.

* In JavaScript: la funzione `s.tl()`
* Nelle App Mobile: [trackAction() Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/actions.html), [trackAction() iOS](https://docs.adobe.com/content/help/en/mobile-services/ios/analytics-ios/actions.html), [trackAction() OTT](/help/sdk-implement/analytics-with-ott/track-app-actions.md)
* Nell’API di inserimento dati: [tag linktype](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## Requisiti

* Accesso a eventi e dati API del lettore video
* Possibilità di aggiungere script se si utilizza Analytics SDK
* Possibilità di aggiungere beacon di tracciamento (script personalizzati o codice fisso) se si utilizza l’API di inserimento dati

## Metadati

* I metadati possono essere aggiunti a qualsiasi chiamata di tracciamento come parte dei dati del collegamento
* Ricorda di aggiornare `linkTrackVars` e `linkTrackEvents`

```javascript
/* Call on video complete */

if (e.type == "ended") {  
    s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15';
    s.linkTrackEvents = 'event3';
    s.prop10 = mediaName;
    s.eVar10 = mediaName;
    s.eVar12 = "video";
    s.eVar13 = document.title;
    s.eVar15 = mediaPlayerName;
    s.events = 'event3';
    s.tl(this,'o','Video Complete');
};
```

## Perché utilizzare il collegamento personalizzato

* Sono necessari prerequisiti minimi
* Funziona su qualsiasi piattaforma, incluso senza script
* Eventuali calcoli, ad esempio il tempo trascorso o i quartili, devono essere calcolati in uno script personalizzato
* Molto semplice senza librerie o script nascosti
* Controllo totale su ogni aspetto dei dati video

## JavaScript di esempio per il lettore HTML5

```javascript
<script type="text/javascript">
  myvideo = document.getElementById('movie');
  myvideo.addEventListener('play',myHandler,false);
  myvideo.addEventListener('seeked',myHandler,false);
  myvideo.addEventListener('seeking',myHandler,false);
  myvideo.addEventListener('pause',myHandler,false);
  myvideo.addEventListener('ended',myHandler,false);

  function myHandler(e) {
      var video = document.getElementsByTagName('video')[0];
      var mediaName="13502979:Sailing";
      var mediaLength = video.duration;
      var mediaPlayerName = "HTML5 Player";
      /*Define video offset*/
      if (video.currentTime > 0) {
          mediaOffset = Math.floor(video.currentTime);
      } else {
          mediaOffset = 0;
      };
      /*Call on video start*/
      if (e.type == "play") {
          if (mediaOffset == 0) {
              console.log(mediaPlayerName +
                ' -> start -> playhead: ' +  
                Math.floor(video.currentTime));
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15';
              s.linkTrackEvents='event2';
              s.prop10=mediaName;
              s.eVar10=mediaName;
              s.eVar12="video";
              s.eVar13=document.title;
              s.eVar15=mediaPlayerName;
              s.events='event2';
              s.tl(this,'o','Video Start');
          }
      };

      /*Call on video pause*/
      if (e.type == "pause") {
          console.log(mediaPlayerName +' -> pause -> playhead: ' + Math.floor(video.currentTime));
          if (video.currentTime != video.duration) {
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15';
              s.linkTrackEvents='event7';
              s.prop10=mediaName;
              s.eVar10=mediaName;
              s.eVar12="video";
              s.eVar13=document.title;
              s.eVar15=mediaPlayerName;
              s.events='event7';
              s.tl(this,'o','Video Pause');
          }
      };

      /*Call on video complete*/
      if (e.type == "ended") {
          console.log(mediaPlayerName +
            ' -> ended -> playhead: ' +
            Math.floor(video.currentTime));
          s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15';
          s.linkTrackEvents = 'event3';
          s.prop10= m ediaName;
          s.eVar10=mediaName;
          s.eVar12="video";
          s.eVar13=document.title;
          s.eVar15=mediaPlayerName;
          s.events='event3';
          s.tl(this,'o','Video Complete');
      };
  };
</script>
```
