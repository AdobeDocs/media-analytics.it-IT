---
title: Invio di dati QoE
description: Scopri come inviare eventi con una chiave JSON qoeData.
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '55'
ht-degree: 100%

---

# Invio di dati QoE {#sending-qoe-data}

Ogni evento può essere decorato con una chiave JSON aggiuntiva denominata `qoeData`, posizionata accanto alla chiave `params` nel corpo della richiesta JSON.

>[!NOTE]
>
>Controlla gli [schemi di convalida JSON](mc-api-validate-reqs.md) per verificare i tipi di parametri e se sono obbligatori o facoltativi.
