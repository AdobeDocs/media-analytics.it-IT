---
title: Descrizioni dei parametri Heartbeat
description: Esplora i parametri heartbeat che Adobe raccoglie ed elabora sul server Media Analytics (heartbeat).
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
exl-id: ffa67b5e-ee54-4a5b-8064-decd108f944b
feature: '"Media Analytics, variabili"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 5%

---

# Descrizioni dei parametri di Media Analytics (heartbeat){#heartbeat-parameter-descriptions}

Elenco dei parametri di Media Analytics che Adobe raccoglie ed elabora sul server Media Analytics (heartbeat):

## Tutti gli eventi

| Nome | Origine dati |  Descrizione  |
| ---  | --- | --- |
| s:event:type | Media SDK | (Obbligatorio)<br/><br/>Il tipo di evento da tracciare. Tipi di evento: <ul> <li> s:event:type=start </li> <li> s:event:type=complete </li> <li> s:event:type=capitolo_start </li> <li> s:event:type=capitolo_complete </li> <li> s:event:type=buffer </li> <li> s:event:type=pause </li> <li> s:event:type=curriculum </li> <li> s:event:type=bitrate_change </li> <li> s:event:type=aa_start </li> <li> s:event:type=stall </li> <li> s:event:type=end </li> </ul> |
| l:event:prev_ts | Media SDK | (Obbligatorio)<br/><br/>La marca temporale dell&#39;ultimo evento dello stesso tipo in questa sessione. Il valore è -1. |
| l:event:ts | Media SDK | (Obbligatorio)<br/><br/>La marca temporale dell&#39;evento. |
| l:event:durata | Media SDK | (Obbligatorio)<br/><br/>Questo valore viene impostato internamente (in millisecondi) dall&#39;SDK Media, non dal lettore. Viene utilizzato per calcolare il tempo impiegato dalle metriche sul backend. Ad esempio: a.media.totalTimePlayed viene calcolato come somma della durata di tutti gli heartbeat Play (type=play) generati. <br/>*Nota:* questo parametro è impostato su 0 per alcuni eventi perché si tratta di &quot;eventi di modifica dello stato&quot; (ad esempio, type=complete, type=capitolo_complete, o type=bitrate_change.) |
| l:event:testina di riproduzione | VideoInfo | (Obbligatorio)<br/><br/>L&#39;indicatore di riproduzione si trovava all&#39;interno della risorsa attualmente attiva (principale o annuncio), quando l&#39;evento è stato registrato. |
| s:event:sid | Media SDK | (Obbligatorio)<br/><br/>L&#39;ID sessione (una stringa generata in modo casuale). Tutti gli eventi in una determinata sessione (video + annunci) devono essere gli stessi. |
| l:asset:durata / l:asset:lunghezza <br/>(rinominata in base alla durata della lunghezza) | VideoInfo | (Obbligatorio)<br/><br/>La lunghezza della risorsa video della risorsa principale. |
| s:asset:editore | MediaHeartbeatConfig | (Obbligatorio)<br/><br/>L’editore della risorsa. |
| s:asset:video_id | VideoInfo | (Obbligatorio)<br/><br/>Un ID che identifica il video in modo univoco nel catalogo dell&#39;editore. |
| s:asset:type | Media SDK | (Obbligatorio)<br/><br/>Il tipo di risorsa (principale o annuncio). |
| s:stream:type | VideoInfo | (Obbligatorio)<br/><br/>Il tipo di flusso. Può essere uno dei seguenti: <ul> <li> live </li> <li> vago </li> <li> lineare </li> </ul> |
| s:user:id | Oggetto di configurazione per dispositivi mobili, misurazione app VisitorID | (Facoltativo)<br/><br/>L&#39;ID visitatore impostato specificamente dall&#39;utente. |
| s:user:aid | Organizzazione Experience Cloud | (Facoltativo)<br/><br/>Valore ID visitatore di Analytics dell&#39;utente. |
| s:user:mid | Organizzazione Experience Cloud | (Obbligatorio)<br/><br/>Valore ID visitatore Experience Cloud dell&#39;utente. |
| s:cuser:customer_user_ids_x | MediaHeartbeatConfig | (Facoltativo)<br/><br/>Tutti gli ID utente cliente impostati sull&#39;Audience Manager. |
| l:aam:loc_hint | MediaHeartbeatConfig | (Obbligatorio)<br/><br/>AAM dati inviati su ciascun payload dopo aa_start |
| s:aam:blob | MediaHeartbeatConfig | (Obbligatorio)<br/><br/>AAM dati inviati su ciascun payload dopo aa_start |
| s:sc:rsid | ID suite di rapporti (o ID) | (Obbligatorio)<br/><br/>Adobe Analytics RSID dove devono essere inviati i rapporti. |
| s:sc:tracking_server | MediaHeartbeatConfig | (Obbligatorio)<br/><br/>Server di tracciamento Adobe Analytics. |
| h:sc:ssl | MediaHeartbeatConfig | (Obbligatorio)<br/><br/>Se il traffico si trova su HTTPS (se impostato su 1) o su HTTP (se impostato su 0). |
| s:sp:ovp | MediaHeartbeatConfig | (Facoltativo)<br/><br/>Impostare su &quot;primetime&quot; per i lettori Primetime o l&#39;OVP effettiva per gli altri lettori. |
| s:sp:sdk | MediaHeartbeatConfig | (Obbligatorio)<br/><br/>Stringa della versione OVP. |
| s:sp:nome_lettore | VideoInfo | (Obbligatorio)<br/><br/>Nome del lettore video (l&#39;effettivo software utilizzato per identificare il lettore). |
| s:sp:canale | MediaHeartbeatConfig | (Facoltativo)<br/><br/>Il canale in cui l&#39;utente sta guardando il contenuto. Per un’app mobile, il nome dell’app. Per un sito web, il nome di dominio. |
| s:sp:hb_version | Media SDK | (Obbligatorio)<br/><br/>Il numero di versione della libreria Media SDK che emette la chiamata . |
| l:stream:bitrate | QoSInfo | (Obbligatorio)<br/><br/>Il valore corrente del bitrate del flusso (in bps). |

## Eventi di errore

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| s:event:sorgente | Media SDK | (Obbligatorio)<br/><br/>Origine dell&#39;errore, interno del lettore o a livello di applicazione. |
| s:event:id | Media SDK | (Obbligatorio)<br/><br/>ID errore, identifica l&#39;errore in modo univoco. |

## Eventi annuncio

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| s:asset:ad_id | AdInfo | (Obbligatorio)<br/><br/>Il nome dell&#39;annuncio. |
| s:asset:ad_sid | Media SDK | (Obbligatorio)<br/><br/>Un identificatore univoco generato dall&#39;SDK Media, aggiunto a tutti i ping relativi agli annunci. |
| s:asset:pod_id | Media SDK | (Obbligatorio)<br/><br/>ID del contenitore all’interno del video. Questo valore viene calcolato automaticamente in base alla formula seguente: <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| s:asset:pod_position | AdBreakInfo | (Obbligatorio)<br/><br/>Indice dell&#39;annuncio all&#39;interno del pod (il primo annuncio ha l&#39;indice 0, il secondo ha l&#39;indice 1, ecc.). |
| s:asset:resolver | AdBreakInfo | (Obbligatorio)<br/><br/>Il risolutore di annunci. |
| s:meta:custom_ad_metadata.x | MediaHeartbeat | (Facoltativo)<br/><br/>I metadati personalizzati dell&#39;annuncio. |

## Capitolo Eventi

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| s:stream:capitolo_sid | Media SDK | (Obbligatorio)<br/><br/>Identificatore univoco associato all&#39;istanza di riproduzione del capitolo.  <br/> **Nota:** un capitolo può essere riprodotto più volte a causa di operazioni di ricerca eseguite dall&#39;utente. |
| s:stream:nome_capitolo | CapitoloInfo | (Facoltativo)<br/><br/>Nome descrittivo del capitolo (cioè leggibile dall&#39;utente). |
| s:stream:capitolo_id | Media SDK | (Obbligatorio)<br/><br/>ID univoco del capitolo. Questo valore viene calcolato automaticamente in base alla formula seguente: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| l:stream:capitolo_pos | CapitoloInfo | (Obbligatorio)<br/><br/>Indice del capitolo nell&#39;elenco dei capitoli (a partire da 1). |
| l:stream:capitolo_offset | CapitoloInfo | (Obbligatorio)<br/><br/>L&#39;offset del capitolo (espresso in secondi) all&#39;interno del contenuto principale, esclusi gli annunci. |
| l:stream:capitolo_length | CapitoloInfo | (Obbligatorio)<br/><br/>Durata del capitolo (espressa in secondi). |
| s:meta:custom_capitolo_metadata.x | CapitoloInfo | (Facoltativo)<br/><br/>Metadati capitolo personalizzati. |

## Evento fine sessione

| Nome | Origine dati | Descrizione   |
| ---  | --- | --- |
| s:event:type=end | Media SDK | (Obbligatorio)<br/><br/> Il `end` `close` |
