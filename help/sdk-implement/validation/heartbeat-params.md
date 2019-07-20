---
seo-title: Descrizioni dei parametri Heartbeat
title: Descrizioni dei parametri Heartbeat
uuid: e 9 ddda 32-0952-43 d 0-a 702-49 f 5 b 1 bfd 8 cf
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# Heartbeat parameter descriptions{#heartbeat-parameter-descriptions}

Elenco di parametri heartbeat che Adobe raccoglie e elabora sul server heartbeat:

## Tutti gli eventi

| Nome | Obbligatorio / Facoltativo | Origine dati | Descrizione   |
| ---  | :---: | --- | --- |
| `s:event:type` | R | Media SDK | Il tipo di evento tracciato. Tipi di evento: <ul> <li> `s:event:type=start` </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | R | Media SDK | La marca temporale dell'ultimo evento dello stesso tipo in questa sessione. The value is `-1` |
| `l:event:ts` | R | Media SDK | Marca temporale dell'evento. |
| `l:event:duration` | R | Media SDK | Questo valore viene impostato internamente (in millisecondi) dalla libreria VHL, non dal lettore. Viene utilizzato per calcolare il tempo trascorso sul retro. For example `a.media.totalTimePlayed` `type=play` Note:  For some of the HB that are sent This parameter is set to 0 for certain events because they are "state change events" (e.g., `type=complete` `type=chapter_complete` `type=bitrate_change` |
| `l:event:playhead` | R | `VideoInfo` | L'indicatore di riproduzione si trovava all'interno della risorsa attualmente attiva (principale o ad) quando l'evento è stato registrato. |
| `s:event:sid` | R | Media SDK | L'ID sessione (una stringa generata in modo casuale). Tutti gli eventi in una determinata sessione (video + ads) devono essere identici. |
| `l:asset:duration / l:asset:length` (Rinominato da `length``duration` | R | `VideoInfo` | Lunghezza della risorsa video della risorsa principale. |
| `s:asset:publisher` | R | `MediaHeartbeatConfig` | Editore della risorsa. |
| `s:asset:video_id` | R | `VideoInfo` | Un ID che identifica in modo univoco il video nel catalogo dell'editore. |
| `s:asset:type` | R | Media SDK | Tipo di risorsa (principale o annuncio). |
| `s:stream:type` | R | `VideoInfo` | Il tipo di flusso. Può essere uno dei seguenti: <ul> <li> `live` </li> <li> `vod` </li> <li> `linear` </li> </ul>. |
| `s:user:id` | O | Oggetto di configurazione per dispositivi mobili, misurazione dell'app visitorid | L'ID visitatore impostato dall'utente. |
| `s:user:aid` | O | Experience Cloud Organizzazione | Il valore ID visitatore dell'utente. |
| `s:user:mid` | R | Experience Cloud Organizzazione | Il valore ID visitatore di Experience Cloud dell'utente. |
| `s:cuser:customer_user_ids_x` | O | `MediaHeartbeatConfig` | Tutti gli ID utente cliente impostati su Audience Manager. |
| `l:aam:loc_hint` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:aam:blob` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:sc:rsid` | R | ID report Report (o ID) | RSID sitecatalyst: i rapporti devono essere inviati. |
| `s:sc:tracking_server` | R | `MediaHeartbeatConfig` | Server di monitoraggio sitecatalyst. |
| `h:sc:ssl` | R | `MediaHeartbeatConfig` | Se il traffico si trova sopra HTTPS (se è impostato su 1) o su HTTP (impostato su 0). |
| `s:sp:ovp` | O | `MediaHeartbeatConfig` | Impostate su «primetime» per i lettori Primetime, o l'OVP effettivo per altri lettori. |
| `s:sp:sdk` | R | `MediaHeartbeatConfig` | Stringa della versione OVP. |
| `s:sp:player_name` | R | `VideoInfo` | Nome del lettore video (il software lettore effettivo utilizzato per identificare il lettore). |
| `s:sp:channel` | O | `MediaHeartbeatConfig` | Canale in cui l'utente sta visualizzando il contenuto. Per un'app mobile, il nome dell'app. Per un sito Web, il nome del dominio. |
| `s:sp:hb_version` | R | Media SDK | Il numero di versione della libreria videoheartbeat che emette la chiamata. |
| `l:stream:bitrate` | R | `QoSInfo` | Il valore corrente del bitrate di streaming (in bps). |

## Eventi errore

| Nome | Obbligatorio / Facoltativo | Origine dati | Descrizione   |
| ---  | :---: | --- | --- |
| `s:event:source` | R | Media SDK | L'origine dell'errore, player-interno o applicazione. |
| `s:event:id` | R | Media SDK | ID errore, identifica l'errore in modo univoco. |

## Eventi annunci

| Nome | Obbligatorio / Facoltativo | Origine dati | Descrizione   |
| ---  | :---: | --- | --- |
| `s:asset:ad_id` | R | `AdInfo` | Nome dell'annuncio. |
| `s:asset:ad_sid` | R | Media SDK | Un identificatore univoco generato da Media SDK, aggiunto a tutti gli hit ad hoc. |
| `s:asset:pod_id` | R | Media SDK | ID contenitore all'interno del video. This value is computed automatically based on the following formula: `MD5(video_id) + "_" + [pod index]` |
| `s:asset:pod_position` | R | `AdBreakInfo` | Indice dell'annuncio all'interno del contenitore (il primo ad ha indice 0, il secondo ad indice 1, ecc.). |
| `s:asset:resolver` | R | `AdBreakInfo` | Il resolver. |
| `s:meta:custom_ad_metadata.x` | O | `MediaHeartbeat` | Metadati annunci personalizzati. |

## Eventi capitolo

| Nome | Obbligatorio / Facoltativo | Origine dati | Descrizione   |
| ---  | :---: | --- | --- |
| `s:stream:chapter_sid` | R | Media SDK | L'identificatore univoco associato all'istanza di riproduzione del capitolo. Nota: Un capitolo può essere riprodotto più volte a causa di operazioni di ricerca eseguite dall'utente. |
| `s:stream:chapter_name` | O | `ChapterInfo` | Il titolo è descrittivo (ovvero, leggibile dall'uomo). |
| `s:stream:chapter_id` | R | Media SDK | L'ID univoco del capitolo. This value is computed automatically based on the following formula: `MD5(video_id) + "_" + chapter_pos` |
| `l:stream:chapter_pos` | R | `ChapterInfo` | Indice del capitolo nell'elenco dei capitoli (a partire da 1). |
| `l:stream:chapter_offset` | R | `ChapterInfo` | L'offset del capitolo (espresso in secondi) all'interno del contenuto principale, escludendo gli annunci. |
| `l:stream:chapter_length` | R | `ChapterInfo` | Durata del capitolo (espressa in secondi). |
| `s:meta:custom_chapter_metadata.x` | O | `ChapterInfo` | Metadati dei capitoli personalizzati. |

## Evento fine sessione

| Nome | Obbligatorio / Facoltativo | Origine dati | Descrizione   |
| ---  | :---: | --- | --- |
| `s:event:type=end` | R | Media SDK | L'opzione `end` `close` |

