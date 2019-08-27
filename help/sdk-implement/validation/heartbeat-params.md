---
seo-title: Descrizioni dei parametri Heartbeat
title: Descrizioni dei parametri Heartbeat
uuid: e 9 ddda 32-0952-43 d 0-a 702-49 f 5 b 1 bfd 8 cf
translation-type: tm+mt
source-git-commit: 10a5d921953339bef1cde2f802eb9ce0cb1bbe4b

---


# Descrizioni dei parametri di Media Analytics (heartbeats){#heartbeat-parameter-descriptions}

Elenco dei parametri di Media Analytics che Adobe raccoglie e elabora sul server di Media Analytics (heartbeats):

## Tutti gli eventi

| Nome | Origine dati |  Descrizione  |
| ---  | --- | --- |
| s: evento: type | Media SDK | (Obbligatorio)<br/><br/>Il tipo di evento tracciato. Tipi di evento: <ul> <li> s: evento: type = start </li> <li> s: evento: type = complete </li> <li> s: evento: type = chapter_ start </li> <li> s: evento: type = chapter_ complete </li> <li> s: evento: type = buffer </li> <li> s: evento: type = pause </li> <li> s: evento: type = resume </li> <li> s: evento: type = bitrate_ change </li> <li> s: evento: type = aa_ start </li> <li> s: evento: type = stall </li> <li> s: evento: type = end </li> </ul> |
| l: evento: prev_ ts | Media SDK | (Obbligatorio)<br/><br/>La marca temporale dell'ultimo evento dello stesso tipo in questa sessione. Il valore è -1. |
| l: evento: ts | Media SDK | (Obbligatorio)<br/><br/>La marca temporale dell'evento. |
| l: evento: duration | Media SDK | (Obbligatorio)<br/><br/>Questo valore viene impostato internamente (in millisecondi) da Media SDK, non dal lettore. Viene utilizzato per calcolare il tempo trascorso sul retro. Ad esempio: a. media. totaltimeplayviene calcolato come somma della durata di tutti i heartbebeat Play (type = play) generati. <br/>*Nota:* Questo parametro è impostato su 0 per determinati eventi perché sono "eventi di modifica dello stato" (ad es., type = complete, type = chapter_ complete o type = bitrate_ change.) |
| l: evento: playhead | Videoinfo | (Obbligatorio)<br/><br/>Quando l'evento è stato registrato, l'indicatore di riproduzione si trovava all'interno della risorsa attualmente attiva (principale o annuncio). |
| s: evento: sid | Media SDK | (Obbligatorio)<br/><br/>L'ID sessione (una stringa generata in modo casuale). Tutti gli eventi in una determinata sessione (video + ads) devono essere identici. |
| l: risorse: duration/l: risorse: length <br/>(rinominata dalla durata della lunghezza) | Videoinfo | (Obbligatorio)<br/><br/>Lunghezza della risorsa video della risorsa principale. |
| s: risorse: editore | Mediaheartbeatconfig | (Obbligatorio)<br/><br/>L'editore della risorsa. |
| s: risorse: video_ id | Videoinfo | (Obbligatorio)<br/><br/>Un ID che identifica in modo univoco il video nel catalogo dell'editore. |
| s: risorse: type | Media SDK | (Obbligatorio)<br/><br/>Il tipo di risorsa (principale o annuncio). |
| s: stream: type | Videoinfo | (Obbligatorio)<br/><br/>Il tipo di flusso. Può essere uno dei seguenti: <ul> <li> live </li> <li> vod </li> <li> linear </li> </ul> |
| s: utente: id | Oggetto di configurazione per dispositivi mobili, misurazione dell'app visitorid | (Facoltativo) L<br/><br/>'ID visitatore impostato dall'utente. |
| s: utente: aid | Experience Cloud Organizzazione | (Facoltativo)<br/><br/>Il valore ID visitatore di Analytics dell'utente. |
| s: utente: mid | Experience Cloud Organizzazione | (Obbligatorio)<br/><br/>Il valore ID visitatore di Experience Cloud dell'utente. |
| s: cuser: customer_ user_ ids_ x | Mediaheartbeatconfig | (Facoltativo)<br/><br/>Tutti gli ID utente cliente impostati su Audience Manager. |
| l: aam: loc_ hint | Mediaheartbeatconfig | (Richiesti)<br/><br/>I dati AAM inviati su ciascun payload dopo aa_ start |
| s: aam: blob | Mediaheartbeatconfig | (Richiesti)<br/><br/>I dati AAM inviati su ciascun payload dopo aa_ start |
| s: sc: rsid | ID report Report (o ID) | (Obbligatorio)<br/><br/>RSID di Adobe Analytics dove è necessario inviare i rapporti. |
| s: sc: tracking_ server | Mediaheartbeatconfig | (Obbligatorio)<br/><br/>Server di tracciamento Adobe Analytics. |
| h: sc: ssl | Mediaheartbeatconfig | (Obbligatorio)<br/><br/>Se il traffico è sopra HTTPS (se è impostato su 1) o su HTTP (impostato su 0). |
| s: sp: ovp | Mediaheartbeatconfig | (Facoltativo)<br/><br/>Impostare su «primetime» per i lettori Primetime, o l'OVP effettivo per altri lettori. |
| s: sp: sdk | Mediaheartbeatconfig | (Obbligatorio)<br/><br/>Stringa della versione OVP. |
| s: sp: player_ name | Videoinfo | (Obbligatorio)<br/><br/>Nome del lettore video (il software del lettore effettivo utilizzato per identificare il lettore). |
| s: sp: canale | Mediaheartbeatconfig | (Facoltativo)<br/><br/>Il canale in cui l'utente sta visualizzando il contenuto. Per un'app mobile, il nome dell'app. Per un sito Web, il nome del dominio. |
| s: sp: hb_ version | Media SDK | (Obbligatorio)<br/><br/>Il numero di versione della libreria Media SDK che emette la chiamata. |
| l: stream: bitrate | Qosinfo | (Obbligatorio)<br/><br/>Il valore corrente del bitrate di streaming (in bps). |

## Eventi errore

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| s: evento: source | Media SDK | (Obbligatorio)<br/><br/>L'origine dell'errore, player-interno o applicazione. |
| s: evento: id | Media SDK | (Obbligatorio)<br/><br/>L'ID errore identifica l'errore in modo univoco. |

## Eventi annunci

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| s: risorse: ad_ id | Adinfo | (Obbligatorio)<br/><br/>Il nome dell'annuncio. |
| s: risorse: ad_ sid | Media SDK | (Obbligatorio)<br/><br/>Un identificatore univoco generato da Media SDK, aggiunto a tutti gli hit ad hoc. |
| s: risorse: pod_ id | Media SDK | (Obbligatorio)<br/><br/>ID contenitore all'interno del video. Questo valore viene calcolato automaticamente in base alla formula seguente: <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| s: risorse: pod_ position | Adbreakinfo | (Obbligatorio)<br/><br/>Indice dell'annuncio all'interno del contenitore (il primo ad ha indice 0, il secondo ad indice 1, ecc.). |
| s: risorse: resolver | Adbreakinfo | (Obbligatorio)<br/><br/>Il resolver. |
| s: meta: custom_ ad_ metadata. x | Mediaheartbeat | (Facoltativo)<br/><br/>I metadati degli annunci personalizzati. |

## Eventi capitolo

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| s: stream: chapter_ sid | Media SDK | (Obbligatorio)<br/><br/>L'identificatore univoco associato all'istanza di riproduzione del capitolo. <br/> **Nota:** Un capitolo può essere riprodotto più volte a causa di operazioni di ricerca eseguite dall'utente. |
| s: stream: chapter_ name | Chapterinfo | (Facoltativo)<br/><br/>Il nome è descrittivo (ovvero, leggibile dall'uomo). |
| s: stream: chapter_ id | Media SDK | (Obbligatorio)<br/><br/>L'ID univoco del capitolo. Questo valore viene calcolato automaticamente in base alla formula seguente: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| l: stream: chapter_ pos | Chapterinfo | (Obbligatorio)<br/><br/>L'indice del capitolo nell'elenco dei capitoli (a partire da 1). |
| l: stream: chapter_ offset | Chapterinfo | (Obbligatorio) L<br/><br/>'offset del capitolo (espresso in secondi) all'interno del contenuto principale, escludendo gli annunci. |
| l: stream: chapter_ length | Chapterinfo | (Obbligatorio)<br/><br/>La durata del capitolo (espressa in secondi). |
| s: meta: custom_ chapter_ metadata. x | Chapterinfo | (Facoltativo)<br/><br/>Metadati dei capitoli personalizzati. |

## Evento fine sessione

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| s: evento: type = end | Media SDK | (Obbligatorio) <br/><br/>`end``close` |

