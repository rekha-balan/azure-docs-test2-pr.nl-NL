---
title: CalcHistogram method in the Academic Knowledge API | Microsoft Docs
description: Use the CalcHistogram method to calculate the distribution of attribute values for a set of paper entities in Microsoft Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.component: academic-knowledge
ms.topic: article
ms.date: 03/27/2017
ms.author: alch
ms.openlocfilehash: e0b773fb9791ee638c8cfdbbc9dca40543e50ec0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827307"
---
# <a name="calchistogram-method"></a>CalcHistogram Method

The **calchistogram** REST API is used to calculate the distribution of attribute values for a set of paper entities.          


**REST endpoint:**
```
https:// westus.api.cognitive.microsoft.com/academic/v1.0/calchistogram?
``` 
<br>
  
## <a name="request-parameters"></a>Request Parameters

Name  |Value | Required?  |Description
-----------|----------|--------|----------
**expr**    |Text string | Yes  |A query expression that specifies the entities over which to calculate histograms.
**model** |Text string | No |Select the name of the model that you wish to query.  Currently, the value defaults to *latest*.
**attributes** | Text string | No<br>default: | A comma-delimited list that specifies the attribute values that are included in the response. Attribute names are case-sensitive.
**count** |Number | No<br>Default: 10 |Number of results to return.
**offset**  |Number | No<br>Default: 0 |Index of the first result to return.
<br>
## <a name="response-json"></a>Response (JSON)
Name | Description
--------|---------
**expr**  |The expr parameter from the request.
**num_entities** | Total number of matching entities.
**histograms** |  An array of histograms, one for each attribute specified in the request.
**histograms[x].attribute** | Name of the attribute over which the histogram was computed.
**histograms[x].distinct_values** | Number of distinct values among matching entities for this attribute.
**histograms[x].total_count** | Total number of value instances among matching entities for this attribute.
**histograms[x].histogram** | Histogram data for this attribute.
**histograms[x].histogram[y].value** |  A value for the attribute.
**histograms[x].histogram[y].logprob**  |Total natural log probability of matching entities with this attribute value.
**histograms[x].histogram[y].count**  |Number of matching entities with this attribute value.
**aborted** | True if the request timed out.

 <br>
#### <a name="example"></a>Example:
```
https:// westus.api.cognitive.microsoft.com/academic/v1.0/calchistogram?expr=And(Composite(AA.AuN=='jaime teevan'),Y>2012)&attributes=Y,F.FN&count=4
```
<br>In this example, in order to generate a histogram of the count of publications by year for a particular author since 2010, we can first generate the query expression using the **interpret** API with query string: *papers by jaime teevan after 2012*.

```
https:// westus.api.cognitive.microsoft.com/academic/v1.0/interpret?query=papers by jaime teevan after 2012
```
<br>The expression in the first interpretation that is returned from the interpret API is *And(Composite(AA.AuN=='jaime teevan'),Y>2012)*.
<br>This expression value is then passed in to the **calchistogram** API. The *attributes=Y,F.FN* parameter indicates that the distributions of paper counts should be by Year and Field of Study, e.g.:
```
https:// westus.api.cognitive.microsoft.com/academic/v1.0/calchistogram?expr=And(Composite(AA.AuN=='jaime teevan'),Y>2012)&attributes=Y,F.FN&count=4
```
<br>The response to this request first indicates that there are 37 papers that match the query expression.  For the *Year* attribute, there are 3 distinct values, one for each year after 2012 (i.e. 2013, 2014, and 2015) as specified in the query.  The total paper count over the 3 distinct values is 37.  For each *Year*, the histogram shows the value, total natural log probability, and count of matching entities.     

The histogram for *Field of Study* shows that there are 34 distinct fields of study. As a paper may be associated with multiple fields of study, the total count (53) can be larger than the number of matching entities.  Although there are 34 distinct values, the response only includes the top 4 because of the *count=4* parameter.

```JSON
{
  "expr": "And(Composite(AA.AuN=='jaime teevan'),Y>2012)",
  "num_entities": 37,
  "histograms": [
    {
      "attribute": "Y",
      "distinct_values": 3,
      "total_count": 37,
      "histogram": [
        {
          "value": 2014,
          "logprob": -15.753,
          "count": 15
        },
        {
          "value": 2013,
          "logprob": -15.805,
          "count": 12
        },
        {
          "value": 2015,
          "logprob": -16.035,
          "count": 10
        }
      ]
    },
    {
      "attribute": "F.FN",
      "distinct_values": 34,
      "total_count": 53,
      "histogram": [
        {
          "value": "crowdsourcing",
          "logprob": -15.258,
          "count": 9
        },
        {
          "value": "information retrieval",
          "logprob": -16.002,
          "count": 4
        },
        {
          "value": "personalization",
          "logprob": -16.226,
          "count": 3
        },
        {
          "value": "mobile search",
          "logprob": -17.228,
          "count": 2
        }
      ]
    }
  ]
}
```
