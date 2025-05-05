---
title: Acquisiire i dati del rapporto JSON sui visualizzatori simultanei
description: Acquisiire i dati del rapporto JSON sui visualizzatori simultanei
uuid: 9168f114-2459-4951-a06c-57b735d09dc0
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 100%

---


# Acquisiire i dati del rapporto JSON sui visualizzatori simultanei{#get-concurrent-viewers-json-report-data}

Puoi acquisire i dati del rapporto sui visualizzatori simultanei utilizzando la _*versione 1.4*_ delle API di Analytics.
* [API di Analytics](https://github.com/AdobeDocs/analytics-1.4-apis)
* [Swagger](https://adobedocs.github.io/analytics-1.4-apis/swagger-docs.html#/Report/Report.Get)

1. Filtra i dati utilizzando qualsiasi segmento generato nell’interfaccia utente. Per filtrare secondo un ID di contenuto specifico, crea un nuovo segmento.
1. Imposta `elements` -> `id` nel corpo della richiesta su `videoconcurrentviewers`.
1. Richiedi una quantità sufficiente di dati. Per garantire che non vi siano lacune nei dati, Adobe consiglia 3200 punti di dati.

   * L’intervallo di dati specificato nel rapporto raccoglie tutti i dati del visualizzatore simultaneo _nel momento in cui termina la sessione video._
Quindi devi tenere conto delle sessioni che iniziano in un giorno e terminano dopo la mezzanotte (cioè il giorno successivo).

   * Richiedi più di una giornata di dati, ma nella tua analisi _*utilizza solo il primo giorno dei dati.*_

Un esempio di payload di richiesta per questo scenario sarà simile al seguente:

```
{
  "reportDescription":{
    "reportSuiteID":"[YOUR_RSID]",
    "dateFrom":"2018-07-01",
    "dateTo":"2018-07-02",
    "metrics":[
      {
        "id":"instances"
      }
    ],
    "elements":[
      {
        "id":"videoconcurrentviewers",
        "top":"3200"
      }
    ],
    "segments":[
      {
        "id":"s1234_58ca4fc7e4b0abc238707bb9"                                         
      }
    ],
    "sortBy":"instances",
    "locale":"en_US"
  }
}
```

<!--
You can extract the concurrent viewers report data using the Experience Cloud API Explorer as follows. 

1. Navigate to: [https://www.adobe.io.](https://www.adobe.io)
1. Select and enter the following information in the API Explorer form:

    * **API -** Select "Report".
    * **Method -** Select "Queue".
    * **Environment -** Select your data center.
    * Request JSON - Specify the following:

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html?lang=it)
        
        * `dateTo` - End date of the report.         
        
          >[!NOTE]
          >
          >The maximum time period supported is two days.

        * `dateFrom` - Start date of the report.
        * `elements : id` - Set to `"videoconcurrentviewers"`
        
        * `elements : top` - Specify the number of entries to be returned.

      Sample request body:

      ```    
      {
          "reportDescription": {
              "reportSuiteID": "[Your Report Suite ID]",
              "dateTo": "2017-09-07",
              "dateFrom": "2017-09-07"
              "metrics": [
                  {
                      "id": "instances"
                  }
              ],
              "elements": [
                  {
                      "id": "videoconcurrentviewers",
                      "top": 2880
                  }
              ]
              "locale": "en_US"
          }
      }
      
      ```

      >[!TIP]
      >
      >Some sessions are ended on the next day, and at that point the data will be available for reporting. In that case the best approach is to select 2 days (2880 minutes) of data, and use only the data for the first day (1440 minutes).

1. Click **Get Response**.

   In the Response field, you should get a `reportID`.
1. In the form, change **Method** to "Get".
1. Enter the value of the `reportID` you received in Step 3, and click **Get Response**.

   The concurrent viewers report data, in JSON format, is presented in the Response field.
   
   For example:
   
   ![](assets/api_helper_2.png) 

   ![](assets/api_helper_1.png)

-->
