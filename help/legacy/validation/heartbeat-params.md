---
title: Descrizioni dei parametri Heartbeat
description: Approfondisci i parametri heartbeat che Adobe raccoglie ed elabora sul server Media Analytics (heartbeat).
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
exl-id: ffa67b5e-ee54-4a5b-8064-decd108f944b
feature: "Streaming Media, Variables"
role: User, Admin, Data Engineer
source-git-commit: 70900e305c3ed7a2be4069c6f296d56f1f6e0966
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 99%

---

# Descrizioni dei parametri di Media Analytics (heartbeat){#heartbeat-parameter-descriptions}

Elenco dei parametri di Media Analytics che Adobe raccoglie ed elabora sul server Media Analytics (heartbeat):

## Tutti gli eventi

| Nome | Origine dati |  Descrizione  |
| ---  | --- | --- |
| `s:event:type` | Media SDK | (Obbligatorio)<br/><br/>Il tipo di evento tracciato. Tipi di evento: <ul> <li> s:event:type=start </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | Media SDK | (Obbligatorio)<br/><br/>La marca temporale dell’ultimo evento dello stesso tipo in questa sessione. Il valore è -1. |
| `l:event:ts` | Media SDK | (Obbligatorio)<br/><br/>La marca temporale dell’evento. |
| `l:event:duration` | Media SDK | (Obbligatorio)<br/><br/>Questo valore viene impostato internamente (in millisecondi) da Media SDK, non dal lettore. Viene utilizzato per calcolare il tempo impiegato dalle metriche sul back-end. Ad esempio: a.media.totalTimePlayed viene calcolato come somma della durata di tutti gli heartbeat Play (type=play) generati. <br/>*Nota:* questo parametro è impostato su 0 per alcuni eventi perché si tratta di “eventi di modifica dello stato” (ad esempio, type=complete, type=chapter_complete o type=bitrate_change.) |
| `l:event:playhead` | VideoInfo | (Obbligatorio)<br/><br/>La testina di riproduzione si trovava all’interno della risorsa attiva (principale o annuncio) nel momento in cui l’evento è stato registrato. |
| `s:event:sid` | Media SDK | (Obbligatorio)<br/><br/>L’ID sessione (una stringa generata in modo casuale). Tutti gli eventi in una determinata sessione (video + annunci) devono essere gli stessi. |
| `l:asset:duration` / `l:asset:length` <br/>(rinominato dalla durata della lunghezza) | VideoInfo | (Obbligatorio)<br/><br/>La lunghezza della risorsa video della risorsa principale. |
| `s:asset:publisher` | MediaHeartbeatConfig | (Obbligatorio)<br/><br/>L’editore della risorsa. |
| `s:asset:video_id` | VideoInfo | (Obbligatorio)<br/><br/>Un ID che identifica il video in modo univoco nel catalogo dell’editore. |
| `s:asset:type` | Media SDK | (Obbligatorio)<br/><br/>Il tipo di risorsa (principale o annuncio). |
| `s:stream:type` | VideoInfo | (Obbligatorio)<br/><br/>Il tipo di flusso. Può essere uno dei seguenti: <ul> <li> live </li> <li> vod </li> <li> lineare </li> </ul> |
| `s:user:id` | Oggetto di configurazione per dispositivi mobili, misurazione app VisitorID | (Facoltativo)<br/><br/>L’ID visitatore impostato in modo specifico per l’utente. |
| `s:user:aid` | Organizzazione Experience Cloud | (Facoltativo)<br/><br/>Il valore ID visitatore di Analytics dell’utente. |
| `s:user:mid` | Organizzazione Experience Cloud | (Obbligatorio)<br/><br/>Il valore ID visitatore di Experience Cloud dell’utente. |
| `s:cuser:customer_user_ids_x` | MediaHeartbeatConfig | (Facoltativo)<br/><br/>Tutti gli ID utente del cliente impostati su Audience Manager. |
| `l:aam:loc_hint` | MediaHeartbeatConfig | (Obbligatorio)<br/><br/>Dati AAM inviati su ciascun payload dopo aa_start |
| `s:aam:blob` | MediaHeartbeatConfig | (Obbligatorio)<br/><br/>Dati AAM inviati su ciascun payload dopo aa_start |
| `s:sc:rsid` | ID suite di rapporti (o ID) | (Obbligatorio)<br/><br/>RSID Adobe Analytics a cui devono essere inviati i rapporti. |
| `s:sc:tracking_server` | MediaHeartbeatConfig | (Obbligatorio)<br/><br/>Server di tracciamento Adobe Analytics. |
| `h:sc:ssl` | MediaHeartbeatConfig | (Obbligatorio)<br/><br/>Se il traffico si trova su HTTPS (se impostato su 1) o su HTTP (se impostato su 0). |
| `s:sp:ovp` | MediaHeartbeatConfig | (Facoltativo)<br/><br/>Impostare su “primetime” per i lettori Primetime o OVP effettivo per gli altri lettori. |
| `s:sp:sdk` | MediaHeartbeatConfig | (Obbligatorio)<br/><br/>Stringa della versione OVP. |
| `s:sp:player_name` | VideoInfo | (Obbligatorio)<br/><br/>Nome del lettore video (l’effettivo software del lettore utilizzato per identificare il lettore). |
| `s:sp:channel` | MediaHeartbeatConfig | (Facoltativo)<br/><br/>Il canale in cui l’utente sta guardando il contenuto. Per un’app mobile, il nome dell’app. Per un sito web, il nome di dominio. |
| `s:sp:hb_version` | Media SDK | (Obbligatorio)<br/><br/>Il numero di versione della libreria Media SDK che emette la chiamata. |
| `l:stream:bitrate` | QoSInfo | (Obbligatorio)<br/><br/>Il valore corrente del bitrate del flusso (in bps). |

## Eventi di errore

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| `s:event:source` | Media SDK | (Obbligatorio)<br/><br/>Origine dell’errore, interno del lettore o a livello di applicazione. |
| `s:event:id` | Media SDK | (Obbligatorio)<br/><br/>ID errore per identificare l’errore in modo univoco. |

## Eventi annuncio

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| `s:asset:ad_id` | AdInfo | (Obbligatorio)<br/><br/>Nome dell’annuncio. |
| `s:asset:ad_sid` | Media SDK | (Obbligatorio)<br/><br/>Identificatore univoco generato da Media SDK, aggiunto a tutti i ping relativi agli annunci. |
| `s:asset:pod_id` | Media SDK | (Obbligatorio)<br/><br/>ID del pod all’interno del video. Questo valore viene calcolato automaticamente in base alla formula seguente: <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| `s:asset:pod_position` | AdBreakInfo | (Obbligatorio)<br/><br/>Indice dell’annuncio all’interno del pod (il primo annuncio ha l’indice uguale a 0, il secondo ha l’indice uguale a 1, ecc.). |
| `s:asset:resolver` | AdBreakInfo | (Obbligatorio)<br/><br/>Il resolver dell’annuncio |
| `s:meta:custom_ad_metadata.x` | MediaHeartbeat | (Facoltativo)<br/><br/>Metadati dell’annuncio personalizzati. |

## Capitolo Eventi

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| `s:stream:chapter_sid` | Media SDK | (Obbligatorio)<br/><br/>Identificatore univoco associato all’istanza di riproduzione del capitolo.<br/> **Nota:** un capitolo può essere riprodotto più volte a causa delle operazioni di ricerca eseguite dall’utente. |
| `s:stream:chapter_name` | ChapterInfo | (Facoltativo)<br/><br/>Il nome del capitolo è descrittivo (cioè leggibile da un utente). |
| `s:stream:chapter_id` | Media SDK | (Obbligatorio)<br/><br/>ID univoco del capitolo. Questo valore viene calcolato automaticamente in base alla formula seguente: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| `l:stream:chapter_pos` | ChapterInfo | (Obbligatorio)<br/><br/>Indice del capitolo che si trova nell’elenco dei capitoli (partendo da 1). |
| `l:stream:chapter_offset` | ChapterInfo | (Obbligatorio)<br/><br/>Offset del capitolo (espresso in secondi) all’interno del contenuto principale, esclusi gli annunci. |
| `l:stream:chapter_length` | ChapterInfo | (Obbligatorio)<br/><br/>La durata del capitolo (espressa in secondi). |
| `s:meta:custom_chapter_metadata.x` | ChapterInfo | (Facoltativo)<br/><br/>Metadati del capitolo personalizzati. |

## Evento fine sessione

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| `s:event:type=end` | Media SDK | (Obbligatorio)<br/><br/> Il `end` `close` |
