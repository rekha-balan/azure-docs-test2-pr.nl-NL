---
title: (deprecated) Azure Machine Learning Anomaly Detection Service | Microsoft Docs
description: (deprecated) Anomaly Detection Service is an example built with Microsoft Azure Machine Learning that detects anomalies in time series data with numerical values that are uniformly spaced in time.
services: machine-learning
documentationcenter: ''
author: alokkirpal
manager: jhubbard
editor: cgronlun
ms.service: machine-learning
ms.devlang: na
ms.topic: deprecated
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 01/18/2017
ms.author: alok
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 0421df90db36c9d901c4e880bf7d4b4802f2211d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551336"
---
# <a name="machine-learning-anomaly-detection-service-deprecated"></a>Machine Learning Anomaly Detection Service (deprecated)
> [!NOTE]
> You can now deploy this API into your Azure subscription using the new **signup** option in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2). See [Machine Learning Anomaly Detection API](machine-learning-apps-anomaly-detection-api.md) for more information.
> 
> The method described in this article of accessing the API through the Azure Datamarket has been deprecated.

## <a name="overview"></a>Overview
[Anomaly Detection API (Deprecated)](https://datamarket.azure.com/dataset/aml_labs/anomalydetection) is an example built with Azure Machine Learning that detects anomalies in time series data with numerical values that are uniformly spaced in time. 

This API can detect the following types of anomalous patterns in time series data:

* **Positive and negative trends**: For example, when monitoring memory usage in computing an upward trend may be of interest as it may be indicative of a memory leak,
* **Changes in the dynamic range of values**: For example, when monitoring the exceptions thrown by a cloud service, any changes in the dynamic range of values could indicate instability in the health of the service, and
* **Spikes and Dips**: For example, when monitoring the number of login failures in a service or number of checkouts in an e-commerce site, spikes or dips could indicate abnormal behavior.

These machine learning detectors track such changes in values over time and report ongoing changes in their values as anomaly scores. They do not require adhoc threshold tuning and their scores can be used to control false positive rate. The anomaly detection API is useful in several scenarios like service monitoring by tracking KPIs over time, usage monitoring through metrics such as number of searches, numbers of clicks, performance monitoring through counters like memory, CPU, file reads, etc. over time.

The Anomaly Detection offering comes with useful tools to get you started. 

* The [web application](http://anomalydetection-aml.azurewebsites.net/) helps you evaluate and visualize the results of anomaly detection APIs on your data. 
* The [sample code](http://adresultparser.codeplex.com/) shows how to programmatically access the API and parse the results in C#.

> [!NOTE]
> Try **IT Anomaly Insights solution** powered by [this API](https://datamarket.azure.com/dataset/aml_labs/anomalydetection)
> 
> To get this end to end solution deployed to your Azure subscription <a href="https://gallery.cortanaintelligence.com/Solution/Anomaly-Detection-Pre-Configured-Solution-1" target="_blank">**Start here >**</a>
> 
> 

## <a name="api-definition"></a>API Definition
The service provides a REST-based API over HTTPS that can be consumed in different ways including a web or mobile application, R, Python, Excel, etc.  You send your time series data to this service via a REST API call, and it runs a combination of the three anomaly types described above. The service runs on the Azure Machine Learning platform, which scales to your business needs seamlessly and provides SLAs.

### <a name="headers"></a>Headers
Ensure that you include the correct headers in your request, which should be as follows:

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

You can find your account key from your account in the [Azure Data Market](https://datamarket.azure.com/account/keys). 

### <a name="score-api"></a>Score API
The Score API is used for running anomaly detection on non-seasonal time series data. The API runs a number of anomaly detectors on the data and returns their anomaly scores. The figure below shows an example of anomalies that the Score API can detect. This time series has 2 distinct level changes, and 3 spikes. The red dots show the time at which the level change is detected, while the black dots show the detected spikes.

![Score API][1]

**URL**

    https://api.datamarket.azure.com/data.ashx/aml_labs/anomalydetection/v2/Score 

**Example request body**

In the request below, we send a time series (shown truncated) with data points from 3/1/2016 through 3/10/2016 and parameters of spike detectors to the API for detecting if any of these data points are anomalous. 

    {
      "data": [
        [ "9/21/2014 11:05:00 AM", "3" ],
        [ "9/21/2014 11:10:00 AM", "9.09" ],
        [ "9/21/2014 11:15:00 AM", "0" ]
      ],
      "params": {
        "tspikedetector.sensitivity": "3",
        "zspikedetector.sensitivity": "3",
        "trenddetector.sensitivity": "3.25",
        "bileveldetector.sensitivity": "3.25",
        "postprocess.tailRows": "2"
      }
    }

The response to this will be : 

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/aml_labs/anomalydetection/v2/$metadata#AnomalyDetection.FrontEndService.Models.AnomalyDetectionResult",
      "ADOutput":"{
        "ColumnNames":["Time","Data","TSpike","ZSpike","rpscore","rpalert","tscore","talert"],
        "ColumnTypes":["DateTime","Double","Double","Double","Double","Int32","Double","Int32"],
        "Values":[
          ["9/21/2014 11:10:00 AM","9.09","0","0","-1.07030497733224","0","-0.884548154298423","0"],
          ["9/21/2014 11:15:00 AM","0","0","0","-1.05186237440962","0","-1.173800281031","0"]
        ]
      }"
    }

### <a name="scorewithseasonality-api"></a>ScoreWithSeasonality API
The ScoreWithSeasonality API is used for running anomaly detection on time series that have seasonal patterns. This API is useful to detect deviations in seasonal patterns.  

The following figure shows an example of anomalies detected in a seasonal time series. The time series has one spike (the 1st black dot), two dips (the 2nd black dot and one at the end), and one level change (red dot). Note that both the dip in the middle of the time series and the level change are only discernable after seasonal components are removed from the series.

![Seasonality API][2]

**URL**

    https://api.datamarket.azure.com/data.ashx/aml_labs/anomalydetection/v2/ScoreWithSeasonality 

**Example request body**

In the request below, we send a time series (shown truncated) with data points from 3/1/2016 through 3/10/2016 and parameters to the API for detecting if any of these data points are anomalous. 

    {
      "data": [
        [ "9/21/2014 11:10:00 AM", "9" ],
        [ "9/21/2014 11:15:00 AM", "12" ],
        [ "9/21/2014 11:20:00 AM", "10" ]
      ],
      "params": {
        "preprocess.aggregationInterval": "0",
        "preprocess.aggregationFunc": "mean",
        "preprocess.replaceMissing": "lkv",
        "postprocess.tailRows": "1",
        "zspikedetector.sensitivity": "3",
        "tspikedetector.sensitivity": "3",
        "upleveldetector.sensitivity": "3.25",
        "bileveldetector.sensitivity": "3.25",
        "trenddetector.sensitivity": "3.25",
        "detectors.historywindow": "500",
        "seasonality.enable": "true",
        "seasonality.transform": "deseason",
        "seasonality.numSeasonality": "1"
      }
    }

The response to this will be: 

    {
        "odata.metadata": "https://api.datamarket.azure.com/data.ashx/aml_labs/anomalydetection/v2/$metadata#AnomalyDetection.FrontEndService.Models.AnomalyDetectionResult",
        "ADOutput": "{
            "ColumnNames":["Time","OriginalData","ProcessedData","TSpike","ZSpike","PScore","PAlert","RPScore","RPAlert","TScore","TAlert"],
              "ColumnTypes":["DateTime","Double","Double","Double","Double","Double","Int32","Double","Int32","Double","Int32"],
              "Values":[
                ["9/21/201411: 20: 00AM","10","10","0","0","-1.30229513613974","0","-1.30229513613974","0","-1.173800281031","0"]
              ]
        }"
    }

### <a name="detectors"></a>Detectors
The anomaly detection API supports detectors in 3 broad categories. Details on specific input parameters and outputs for each detector can be found in the following table.

| Detector Category | Detector | Description | Input Parameters | Outputs |
| --- | --- | --- | --- | --- |
| Spike Detectors |TSpike Detector |Detect spikes and dips based on far the values are from first and third quartiles |*tspikedetector.sensitivity:* takes integer value in the range 1-10, default: 3; Higher values will catch more extreme values thus making it less sensitive |TSpike: binary values – ‘1’ if a spike/dip is detected, ‘0’ otherwise |
| ZSpike Detector |Detect spikes and dips based on how far the datapoints are from their mean |*zspikedetector.sensitivity:* take integer value in the range 1-10, default: 3; Higher values will catch more extreme values making it less sensitive |ZSpike: binary values – ‘1’ if a spike/dip is detected, ‘0’ otherwise | |
| Slow Trend Detector |Slow Trend Detector |Detect slow positive trend as per the set sensitivity |*trenddetector.sensitivity:* threshold on detector score (default: 3.25, 3.25 – 5 is a reasonable range to select this from; The higher the less sensitive) |TScore: floating number representing anomaly score on trend |
| Level Change Detectors |Unidirectional Level Change Detector |Detect upward level change as per the set sensitivity |*upleveldetector.sensitivity:* threshold on detector score (default: 3.25, 3.25 – 5 is a reasonable range to select this from; The higher the less sensitive) |PScore: floating number representing anomaly score on upward level change |
| Bidirectional Level Change Detector |Detect both upward and downward level change as per the set sensitivity |*bileveldetector.sensitivity:* threshold on detector score (default: 3.25, 3.25 – 5 is a reasonable range to select this from; The higher the less sensitive) |RPScore: floating number representing anomaly score on upward and downward level change | |

### <a name="parameters"></a>Parameters
More detailed information on these input parameters is listed in the table below:

| Input Parameters | Description | Default Setting | Type | Valid Range | Suggested Range |
| --- | --- | --- | --- | --- | --- |
| preprocess.aggregationInterval |Aggregation interval in seconds for aggregating input time series |0 (no aggregation is performed) |integer |0: skip aggregation, > 0 otherwise |5 minutes to 1 day, time-series dependent |
| preprocess.aggregationFunc |Function used for aggregating data into the specified AggregationInterval |mean |enumerated |mean, sum, length |N/A |
| preprocess.replaceMissing |Values used to impute missing data |lkv (last known value) |enumerated |zero, lkv, mean |N/A |
| detectors.historyWindow |History (in # of data points) used for  anomaly score computation |500 |integer |10-2000 |Time-series dependent |
| upleveldetector.sensitivity |Sensitivity for upward level change detector. |3.25 |double |None |3.25-5(Lesser values mean more sensitive) |
| bileveldetector.sensitivity |Sensitivity for bidirectional level change detector. |3.25 |double |None |3.25-5(Lesser values mean more sensitive) |
| trenddetector.sensitivity |Sensitivity for positive trend detector. |3.25 |double |None |3.25-5(Lesser values mean more sensitive) |
| tspikedetector.sensitivity |Sensitivity for TSpike Detector |3 |integer |1-10 |3-5(Lesser values mean more sensitive) |
| zspikedetector.sensitivity |Sensitivity for ZSpike Detector |3 |integer |1-10 |3-5(Lesser values mean more sensitive) |
| seasonality.enable |Whether seasonality analysis is to be performed |true |boolean |true, false |Time-series dependent |
| seasonality.numSeasonality |Maximum number of periodic cycles to be detected |1 |integer |1, 2 |1-2 |
| seasonality.transform |Whether seasonal (and) trend components shall be removed before applying anomaly detection |deseason |enumerated |none, deseason, deseasontrend |N/A |
| postprocess.tailRows |Number of the latest data points to be kept in the output results |0 |integer |0 (keep all data points), or specify number of points to keep in results |N/A |

### <a name="output"></a>Output
The API runs all detectors on your time series data and returns anomaly scores and binary spike indicators for each point in time. The table below lists outputs from the API. 

| Outputs | Description |
| --- | --- |
| Time |Timestamps from raw data, or aggregated (and/or) imputed data if aggregation (and/or) missing data imputation is applied |
| OriginalData |Values from raw data, or aggregated (and/or) imputed data if aggregation (and/or) missing data imputation is applied |
| ProcessedData |Either of the following: <ul><li>Seasonally adjusted time series if significant seasonality has been detected and deseason option selected;</li><li>seasonally adjusted and detrended time series if significant seasonality has been detected and deseasontrend option selected</li><li>otherwise, this is the same as OriginalData</li> |
| TSpike |Binary indicator to indicate whether a spike is detected by TSpike Detector |
| ZSpike |Binary indicator to indicate whether a spike is detected by ZSpike Detector |
| Pscore |A floating number representing anomaly score on upward level change |
| Palert |1/0 value indicating there is an upward level change anomaly based on the input sensitivity |
| RPScore |A floating number representing anomaly score on bidirectional level change |
| RPAlert |1/0 value indicating there is a bidirectional level change anomaly based on the input sensitivity |
| TScore |A floating number representing anomaly score on positive trend |
| TAlert |1/0 value indicating there is a positive trend anomaly based on the input sensitivity |

This output can be parsed using a [simple parser](https://adresultparser.codeplex.com/) - it has sample code that shows how to connect to the API and parse the output. The anomalies detected can be visualized on a dashboard and/or passed on to human experts for corrective actions or integrated into ticketing systems.

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-apps-anomaly-detection/anomaly-detection-score.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-apps-anomaly-detection/anomaly-detection-seasonal.png






