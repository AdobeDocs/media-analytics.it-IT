---
title: Descrizioni dei parametri Heartbeat
description: Elenco dei parametri heartbeat raccolti ed elaborati da Adobe sul server Media Analytics (heartbeat).
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Descrizioni dei parametri di Media Analytics (heartbeat){#heartbeat-parameter-descriptions}

Elenco dei parametri di Media Analytics raccolti ed elaborati da Adobe sul server Media Analytics (heartbeat):

## Tutti gli eventi

| Nome | Origine dati |  Descrizione  |
| ---  | --- | --- |
| s:event:type | Media SDK | (Obbligatorio)<br/><br/>Il tipo di evento di cui tenere traccia. Tipi di evento: <ul> <li> s:event:type=start </li> <li> s:event:type=complete </li> <li> s:event:type=Chapter_start </li> <li> s:event:type=Chapter_complete </li> <li> s:event:type=buffer </li> <li> s:event:type=pause </li> <li> s:event:type=curriculum </li> <li> s:event:type=bitrate_change </li> <li> s:event:type=aa_start </li> <li> s:event:type=stall </li> <li> s:event:type=end </li> </ul> |
| l:event:prev_ts | Media SDK | (Obbligatorio)<br/><br/>Timestamp dell'ultimo evento dello stesso tipo in questa sessione. Il valore è -1. |
| l:event:ts | Media SDK | (Obbligatorio)<br/><br/>Marca temporale dell'evento. |
| l:evento:durata | Media SDK | (Obbligatorio)<br/><br/>Questo valore viene impostato internamente (in millisecondi) dall’SDK di Media, non dal lettore. Viene utilizzato per calcolare il tempo trascorso dalle metriche sul backend. Ad esempio: a.media.totalTimePlayed viene calcolato come somma della durata di tutti i heartbeat Play (type=play) generati. <br/>** Nota: Questo parametro è impostato su 0 per alcuni eventi perché si tratta di "eventi di modifica dello stato" (ad esempio, type=complete, type=Chapter_complete o type=bitrate_change.) |
| l:event:playhead | VideoInfo | (Obbligatorio)<br/><br/>L'indicatore di riproduzione si trovava all'interno della risorsa attiva (principale o annuncio) al momento della registrazione dell'evento. |
| s:event:sid | Media SDK | (Obbligatorio)<br/><br/>ID sessione (una stringa generata in modo casuale). Tutti gli eventi in una determinata sessione (video + annunci) devono corrispondere. |
| l:risorsa:durata / l:risorsa:lunghezza <br/>(rinominata da durata lunghezza) | VideoInfo | (Obbligatorio)<br/><br/>Lunghezza della risorsa video principale. |
| s:risorsa:editore | MediaHeartbeatConfig | (Obbligatorio)<br/><br/>L’editore della risorsa. |
| s:asset:video_id | VideoInfo | (Obbligatorio)<br/><br/>Un ID che identifica in modo univoco il video nel catalogo dell'editore. |
| s:asset:type | Media SDK | (Obbligatorio)<br/><br/>Il tipo di risorsa (principale o annuncio). |
| s:stream:type | VideoInfo | (Obbligatorio)<br/><br/>Il tipo di flusso. Può essere uno dei seguenti: <ul> <li> live </li> <li> vod </li> <li> linear </li> </ul> |
| s:user:id | Oggetto Config per mobile, misurazione app VisitorID | (Facoltativo) ID visitatore impostato specificamente dall'<br/><br/>utente. |
| s:utente:aid | Organizzazione Experience Cloud | (Facoltativo)<br/><br/>Il valore ID visitatore di Analytics dell’utente. |
| s:utente:mid | Organizzazione Experience Cloud | (Obbligatorio)<br/><br/>Il valore ID visitatore Experience Cloud dell’utente. |
| s:cuser:customer_user_ids_x | MediaHeartbeatConfig | (Facoltativo)<br/><br/>Tutti gli ID utente cliente impostati su Audience Manager. |
| l:aam:loc_hint | MediaHeartbeatConfig | (Obbligatorio) Dati<br/><br/>AAM inviati su ogni payload dopo un_start |
| s:aam:blob | MediaHeartbeatConfig | (Obbligatorio) Dati<br/><br/>AAM inviati su ogni payload dopo un_start |
| s:sc:rsid | ID suite di rapporti (o ID) | (Obbligatorio)RSID di<br/><br/>Adobe Analytics in cui devono essere inviati i rapporti. |
| s:sc:tracking_server | MediaHeartbeatConfig | (Obbligatorio)Server di tracciamento<br/><br/>Adobe Analytics. |
| h:sc:ssl | MediaHeartbeatConfig | (Obbligatorio)<br/><br/>Indica se il traffico si trova su HTTPS (se impostato su 1) o su HTTP (se impostato su 0). |
| s:sp:ovp | MediaHeartbeatConfig | (Facoltativo)<br/><br/>Impostare su "primetime" per i lettori Primetime, o sull'OVP effettiva per altri lettori. |
| s:sp:sdk | MediaHeartbeatConfig | (Obbligatorio)<br/><br/>Stringa della versione OVP. |
| s:sp:player_name | VideoInfo | (Obbligatorio)Nome del lettore<br/><br/>video (il software del lettore utilizzato per identificare il lettore). |
| s:sp:channel | MediaHeartbeatConfig | (Facoltativo)<br/><br/>Canale in cui l'utente sta guardando il contenuto. Per un'app mobile, il nome dell'app. Per un sito Web, il nome del dominio. |
| s:sp:hb_version | Media SDK | (Obbligatorio)<br/><br/>Il numero di versione della libreria Media SDK che ha emesso la chiamata. |
| l:stream:bitrate | QoSInfo | (Obbligatorio)<br/><br/>Il valore corrente del bitrate del flusso (in bps). |

##  Eventi errore

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| s:event:source | Media SDK | (Obbligatorio)<br/><br/>L'origine dell'errore, interna al lettore o a livello di applicazione. |
| s:event:id | Media SDK | (Obbligatorio)ID<br/><br/>errore, che identifica l’errore in modo univoco. |

## Eventi annuncio

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| s:asset:ad_id | AdInfo | (Obbligatorio)<br/><br/>Il nome dell'annuncio. |
| s:asset:ad_sid | Media SDK | (Obbligatorio)<br/><br/>Un identificatore univoco generato da Media SDK, aggiunto a tutti i ping relativi agli annunci. |
| s:asset:pod_id | Media SDK | (Obbligatorio)ID<br/><br/>contenitore all’interno del video. Questo valore viene calcolato automaticamente in base alla seguente formula: <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| s:asset:pod_position | AdBreakInfo | (Obbligatorio)<br/><br/>Indice dell'annuncio all'interno del contenitore (il primo annuncio ha indice 0, il secondo ha indice 1, ecc.). |
| s:asset:resolver | AdBreakInfo | (Obbligatorio)<br/><br/>Il risolutore di annunci. |
| s:meta:custom_ad_metadata.x | MediaHeartbeat | (Facoltativo)<br/><br/>Metadati annuncio personalizzati. |

## Eventi capitolo

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| s:stream:capitolo_sid | Media SDK | (Obbligatorio)<br/><br/>Identificatore univoco associato all'istanza di riproduzione del capitolo.  <br/> **** Nota: Un capitolo può essere riprodotto più volte a causa delle operazioni di ricerca eseguite dall'utente. |
| s:stream:nome_capitolo | ChapterInfo | (Facoltativo)<br/><br/>Nome intuitivo (leggibile dall’uomo) del capitolo. |
| s:stream:capitolo_id | Media SDK | (Obbligatorio)<br/><br/>ID univoco del capitolo. Questo valore viene calcolato automaticamente in base alla seguente formula: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| l:stream:pos_capitolo | ChapterInfo | (Obbligatorio)<br/><br/>Indice del capitolo nell'elenco dei capitoli (a partire da 1). |
| l:stream:Chapter_offset | ChapterInfo | (Obbligatorio)<br/><br/>L'offset del capitolo (espresso in secondi) all'interno del contenuto principale, esclusi gli annunci. |
| l:stream:lunghezza_capitolo | ChapterInfo | (Obbligatorio)<br/><br/>Durata del capitolo (espressa in secondi). |
| s:meta:custom_Chapter_metadata.x | ChapterInfo | (Facoltativo) Metadati<br/><br/>personalizzati per i capitoli. |

## Evento fine sessione

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| s:event:type=end | Media SDK | (Obbligatorio)<br/><br/> Il `end``close` |

