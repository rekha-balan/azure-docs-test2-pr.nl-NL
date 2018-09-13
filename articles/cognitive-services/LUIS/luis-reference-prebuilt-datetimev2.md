---
title: LUIS Prebuilt entities datetimeV2 reference - Azure| Microsoft Docs
titleSuffix: Azure
description: This article has datetimeV2 prebuilt entity information in Language Understanding (LUIS).
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 06/20/2018
ms.author: diberry
ms.openlocfilehash: 13f62e98a33aac51eae86d5ce1b802d4701ef3f6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869352"
---
# <a name="datetimev2-entity"></a><span data-ttu-id="af40b-103">DatetimeV2 entity</span><span class="sxs-lookup"><span data-stu-id="af40b-103">DatetimeV2 entity</span></span>

<span data-ttu-id="af40b-104">The **datetimeV2** prebuilt entity extracts date and time values.</span><span class="sxs-lookup"><span data-stu-id="af40b-104">The **datetimeV2** prebuilt entity extracts date and time values.</span></span> <span data-ttu-id="af40b-105">These values resolve in a standardized format for client programs to consume.</span><span class="sxs-lookup"><span data-stu-id="af40b-105">These values resolve in a standardized format for client programs to consume.</span></span> <span data-ttu-id="af40b-106">When an utterance has a date or time that isn't complete, LUIS includes _both past and future values_ in the endpoint response.</span><span class="sxs-lookup"><span data-stu-id="af40b-106">When an utterance has a date or time that isn't complete, LUIS includes _both past and future values_ in the endpoint response.</span></span> <span data-ttu-id="af40b-107">Because this entity is already trained, you do not need to add example utterances containing datetimeV2 to the application intents.</span><span class="sxs-lookup"><span data-stu-id="af40b-107">Because this entity is already trained, you do not need to add example utterances containing datetimeV2 to the application intents.</span></span> 

## <a name="types-of-datetimev2"></a><span data-ttu-id="af40b-108">Types of datetimeV2</span><span class="sxs-lookup"><span data-stu-id="af40b-108">Types of datetimeV2</span></span>
<span data-ttu-id="af40b-109">DatetimeV2 is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-DateTime.yaml) Github repository</span><span class="sxs-lookup"><span data-stu-id="af40b-109">DatetimeV2 is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-DateTime.yaml) Github repository</span></span>

## <a name="example-json"></a><span data-ttu-id="af40b-110">Example JSON</span><span class="sxs-lookup"><span data-stu-id="af40b-110">Example JSON</span></span> 
<span data-ttu-id="af40b-111">The following example JSON response has a `datetimeV2` entity with a subtype of `datetime`.</span><span class="sxs-lookup"><span data-stu-id="af40b-111">The following example JSON response has a `datetimeV2` entity with a subtype of `datetime`.</span></span> <span data-ttu-id="af40b-112">For examples of other types of datetimeV2 entities, see [Subtypes of datetimeV2](#subtypes-of-datetimev2)</a>.</span><span class="sxs-lookup"><span data-stu-id="af40b-112">For examples of other types of datetimeV2 entities, see [Subtypes of datetimeV2](#subtypes-of-datetimev2)</a>.</span></span>

```JSON
"entities": [
  {
    "entity": "8am on may 2nd 2017",
    "type": "builtin.datetimeV2.datetime",
    "startIndex": 15,
    "endIndex": 30,
    "resolution": {
      "values": [
        {
          "timex": "2017-05-02T08",
          "type": "datetime",
          "value": "2017-05-02 08:00:00"
        }
      ]
    }
  }
]
  ```

## <a name="json-property-descriptions"></a><span data-ttu-id="af40b-113">JSON property descriptions</span><span class="sxs-lookup"><span data-stu-id="af40b-113">JSON property descriptions</span></span>

|<span data-ttu-id="af40b-114">Property name</span><span class="sxs-lookup"><span data-stu-id="af40b-114">Property name</span></span> |<span data-ttu-id="af40b-115">Property type and description</span><span class="sxs-lookup"><span data-stu-id="af40b-115">Property type and description</span></span>|
|---|---|
|<span data-ttu-id="af40b-116">Entity</span><span class="sxs-lookup"><span data-stu-id="af40b-116">Entity</span></span>|<span data-ttu-id="af40b-117">**string** - Text extracted from the utterance with type of date, time, date range, or time range.</span><span class="sxs-lookup"><span data-stu-id="af40b-117">**string** - Text extracted from the utterance with type of date, time, date range, or time range.</span></span>|
|<span data-ttu-id="af40b-118">type</span><span class="sxs-lookup"><span data-stu-id="af40b-118">type</span></span>|<span data-ttu-id="af40b-119">**string** - One of the [subtypes of datetimeV2](#subtypes-of-datetimev2)</span><span class="sxs-lookup"><span data-stu-id="af40b-119">**string** - One of the [subtypes of datetimeV2](#subtypes-of-datetimev2)</span></span>
|<span data-ttu-id="af40b-120">startIndex</span><span class="sxs-lookup"><span data-stu-id="af40b-120">startIndex</span></span>|<span data-ttu-id="af40b-121">**int** - The index in the utterance at which the entity begins.</span><span class="sxs-lookup"><span data-stu-id="af40b-121">**int** - The index in the utterance at which the entity begins.</span></span>|
|<span data-ttu-id="af40b-122">endIndex</span><span class="sxs-lookup"><span data-stu-id="af40b-122">endIndex</span></span>|<span data-ttu-id="af40b-123">**int** - The index in the utterance at which the entity ends.</span><span class="sxs-lookup"><span data-stu-id="af40b-123">**int** - The index in the utterance at which the entity ends.</span></span>|
|<span data-ttu-id="af40b-124">resolution</span><span class="sxs-lookup"><span data-stu-id="af40b-124">resolution</span></span>|<span data-ttu-id="af40b-125">Has a `values` array that has one, two, or four [values of resolution](#values-of-resolution).</span><span class="sxs-lookup"><span data-stu-id="af40b-125">Has a `values` array that has one, two, or four [values of resolution](#values-of-resolution).</span></span>|
|<span data-ttu-id="af40b-126">end</span><span class="sxs-lookup"><span data-stu-id="af40b-126">end</span></span>|<span data-ttu-id="af40b-127">The end value of a time, or date range, in the same format as `value`.</span><span class="sxs-lookup"><span data-stu-id="af40b-127">The end value of a time, or date range, in the same format as `value`.</span></span> <span data-ttu-id="af40b-128">Only used if `type` is `daterange`, `timerange`, or `datetimerange`</span><span class="sxs-lookup"><span data-stu-id="af40b-128">Only used if `type` is `daterange`, `timerange`, or `datetimerange`</span></span>|

## <a name="subtypes-of-datetimev2"></a><span data-ttu-id="af40b-129">Subtypes of datetimeV2</span><span class="sxs-lookup"><span data-stu-id="af40b-129">Subtypes of datetimeV2</span></span>

<span data-ttu-id="af40b-130">The **datetimeV2** prebuilt entity has the following subtypes, and examples of each are provided in the table that follows:</span><span class="sxs-lookup"><span data-stu-id="af40b-130">The **datetimeV2** prebuilt entity has the following subtypes, and examples of each are provided in the table that follows:</span></span>
* `date`
* `time`
* `daterange`
* `timerange`
* `datetimerange`
* `duration`
* `set`

## <a name="values-of-resolution"></a><span data-ttu-id="af40b-131">Values of resolution</span><span class="sxs-lookup"><span data-stu-id="af40b-131">Values of resolution</span></span>
* <span data-ttu-id="af40b-132">The array has one element if the date or time in the utterance is fully specified and unambiguous.</span><span class="sxs-lookup"><span data-stu-id="af40b-132">The array has one element if the date or time in the utterance is fully specified and unambiguous.</span></span>
* <span data-ttu-id="af40b-133">The array has two elements if the datetimeV2 value is ambiguous.</span><span class="sxs-lookup"><span data-stu-id="af40b-133">The array has two elements if the datetimeV2 value is ambiguous.</span></span> <span data-ttu-id="af40b-134">Ambiguity includes lack of specific year, time, or time range.</span><span class="sxs-lookup"><span data-stu-id="af40b-134">Ambiguity includes lack of specific year, time, or time range.</span></span> <span data-ttu-id="af40b-135">See [Ambiguous dates](#ambiguous-dates) for examples.</span><span class="sxs-lookup"><span data-stu-id="af40b-135">See [Ambiguous dates](#ambiguous-dates) for examples.</span></span> <span data-ttu-id="af40b-136">When the time is ambiguous for A.M.</span><span class="sxs-lookup"><span data-stu-id="af40b-136">When the time is ambiguous for A.M.</span></span> <span data-ttu-id="af40b-137">or P.M., both values are included.</span><span class="sxs-lookup"><span data-stu-id="af40b-137">or P.M., both values are included.</span></span>
* <span data-ttu-id="af40b-138">The array has four elements if the utterance has two elements with ambiguity.</span><span class="sxs-lookup"><span data-stu-id="af40b-138">The array has four elements if the utterance has two elements with ambiguity.</span></span> <span data-ttu-id="af40b-139">This ambiguity includes elements that have:</span><span class="sxs-lookup"><span data-stu-id="af40b-139">This ambiguity includes elements that have:</span></span>
  * <span data-ttu-id="af40b-140">A date or date range that is ambiguous as to year</span><span class="sxs-lookup"><span data-stu-id="af40b-140">A date or date range that is ambiguous as to year</span></span>
  * <span data-ttu-id="af40b-141">A time or time range that is ambiguous as to A.M.</span><span class="sxs-lookup"><span data-stu-id="af40b-141">A time or time range that is ambiguous as to A.M.</span></span> <span data-ttu-id="af40b-142">or P.M.</span><span class="sxs-lookup"><span data-stu-id="af40b-142">or P.M.</span></span> <span data-ttu-id="af40b-143">For example, 3:00 April 3rd.</span><span class="sxs-lookup"><span data-stu-id="af40b-143">For example, 3:00 April 3rd.</span></span>

<span data-ttu-id="af40b-144">Each element of the `values` array may have the following fields:</span><span class="sxs-lookup"><span data-stu-id="af40b-144">Each element of the `values` array may have the following fields:</span></span> 

|<span data-ttu-id="af40b-145">Property name</span><span class="sxs-lookup"><span data-stu-id="af40b-145">Property name</span></span>|<span data-ttu-id="af40b-146">Property description</span><span class="sxs-lookup"><span data-stu-id="af40b-146">Property description</span></span>|
|--|--|
|<span data-ttu-id="af40b-147">timex</span><span class="sxs-lookup"><span data-stu-id="af40b-147">timex</span></span>|<span data-ttu-id="af40b-148">time, date, or date range expressed in TIMEX format that follows the [ISO 8601 standard](https://en.wikipedia.org/wiki/ISO_8601) and the TIMEX3 attributes for annotation using the TimeML language.</span><span class="sxs-lookup"><span data-stu-id="af40b-148">time, date, or date range expressed in TIMEX format that follows the [ISO 8601 standard](https://en.wikipedia.org/wiki/ISO_8601) and the TIMEX3 attributes for annotation using the TimeML language.</span></span> <span data-ttu-id="af40b-149">This annotation is described in the [TIMEX guidelines](http://www.timeml.org/tempeval2/tempeval2-trial/guidelines/timex3guidelines-072009.pdf).</span><span class="sxs-lookup"><span data-stu-id="af40b-149">This annotation is described in the [TIMEX guidelines](http://www.timeml.org/tempeval2/tempeval2-trial/guidelines/timex3guidelines-072009.pdf).</span></span>|
|<span data-ttu-id="af40b-150">type</span><span class="sxs-lookup"><span data-stu-id="af40b-150">type</span></span>|<span data-ttu-id="af40b-151">The subtype, which can be one of the following items: datetime, date, time, daterange, timerange, datetimerange, duration, set.</span><span class="sxs-lookup"><span data-stu-id="af40b-151">The subtype, which can be one of the following items: datetime, date, time, daterange, timerange, datetimerange, duration, set.</span></span>|
|<span data-ttu-id="af40b-152">value</span><span class="sxs-lookup"><span data-stu-id="af40b-152">value</span></span>|<span data-ttu-id="af40b-153">**Optional.**</span><span class="sxs-lookup"><span data-stu-id="af40b-153">**Optional.**</span></span> <span data-ttu-id="af40b-154">A datetime object in the Format yyyy:MM:dd  (date), HH:mm:ss (time) yyyy:MM:dd HH:mm:ss (datetime).</span><span class="sxs-lookup"><span data-stu-id="af40b-154">A datetime object in the Format yyyy:MM:dd  (date), HH:mm:ss (time) yyyy:MM:dd HH:mm:ss (datetime).</span></span> <span data-ttu-id="af40b-155">If `type` is `duration`, the value is the number of seconds (duration)</span><span class="sxs-lookup"><span data-stu-id="af40b-155">If `type` is `duration`, the value is the number of seconds (duration)</span></span> <br/> <span data-ttu-id="af40b-156">Only used if `type` is `datetime` or `date`, `time`, or \`duration.</span><span class="sxs-lookup"><span data-stu-id="af40b-156">Only used if `type` is `datetime` or `date`, `time`, or \`duration.</span></span>|

## <a name="valid-date-values"></a><span data-ttu-id="af40b-157">Valid date values</span><span class="sxs-lookup"><span data-stu-id="af40b-157">Valid date values</span></span>

<span data-ttu-id="af40b-158">The **datetimeV2** supports dates between the following ranges:</span><span class="sxs-lookup"><span data-stu-id="af40b-158">The **datetimeV2** supports dates between the following ranges:</span></span>

| <span data-ttu-id="af40b-159">Min</span><span class="sxs-lookup"><span data-stu-id="af40b-159">Min</span></span> | <span data-ttu-id="af40b-160">Max</span><span class="sxs-lookup"><span data-stu-id="af40b-160">Max</span></span> |
|----------|-------------|
| <span data-ttu-id="af40b-161">1st January 1900</span><span class="sxs-lookup"><span data-stu-id="af40b-161">1st January 1900</span></span>   | <span data-ttu-id="af40b-162">31st December 2099</span><span class="sxs-lookup"><span data-stu-id="af40b-162">31st December 2099</span></span> |

## <a name="ambiguous-dates"></a><span data-ttu-id="af40b-163">Ambiguous dates</span><span class="sxs-lookup"><span data-stu-id="af40b-163">Ambiguous dates</span></span>

<span data-ttu-id="af40b-164">If the date can be in the past or future, LUIS provides both values.</span><span class="sxs-lookup"><span data-stu-id="af40b-164">If the date can be in the past or future, LUIS provides both values.</span></span> <span data-ttu-id="af40b-165">An example is an utterance that includes the month and date without the year.</span><span class="sxs-lookup"><span data-stu-id="af40b-165">An example is an utterance that includes the month and date without the year.</span></span>  

<span data-ttu-id="af40b-166">For example, given the utterance "May 2nd":</span><span class="sxs-lookup"><span data-stu-id="af40b-166">For example, given the utterance "May 2nd":</span></span>
* <span data-ttu-id="af40b-167">If today's date is May 3rd 2017, LUIS provides both "2017-05-02" and "2018-05-02" as values.</span><span class="sxs-lookup"><span data-stu-id="af40b-167">If today's date is May 3rd 2017, LUIS provides both "2017-05-02" and "2018-05-02" as values.</span></span> 
* <span data-ttu-id="af40b-168">When today's date is May 1st 2017, LUIS provides both "2016-05-02" and "2017-05-02" as values.</span><span class="sxs-lookup"><span data-stu-id="af40b-168">When today's date is May 1st 2017, LUIS provides both "2016-05-02" and "2017-05-02" as values.</span></span>

<span data-ttu-id="af40b-169">The following example shows the resolution of the entity "may 2nd".</span><span class="sxs-lookup"><span data-stu-id="af40b-169">The following example shows the resolution of the entity "may 2nd".</span></span> <span data-ttu-id="af40b-170">This resolution assumes that today's date is a date between May 2nd 2017 and May 1st 2018.</span><span class="sxs-lookup"><span data-stu-id="af40b-170">This resolution assumes that today's date is a date between May 2nd 2017 and May 1st 2018.</span></span>
<span data-ttu-id="af40b-171">Fields with `X` in the `timex` field are parts of the date that aren't explicitly specified in the utterance.</span><span class="sxs-lookup"><span data-stu-id="af40b-171">Fields with `X` in the `timex` field are parts of the date that aren't explicitly specified in the utterance.</span></span>

```JSON
  "entities": [
    {
      "entity": "may 2nd",
      "type": "builtin.datetimeV2.date",
      "startIndex": 0,
      "endIndex": 6,
      "resolution": {
        "values": [
          {
            "timex": "XXXX-05-02",
            "type": "date",
            "value": "2017-05-02"
          },
          {
            "timex": "XXXX-05-02",
            "type": "date",
            "value": "2018-05-02"
          }
        ]
      }
    }
  ]
```

## <a name="date-range-resolution-examples-for-numeric-date"></a><span data-ttu-id="af40b-172">Date range resolution examples for numeric date</span><span class="sxs-lookup"><span data-stu-id="af40b-172">Date range resolution examples for numeric date</span></span>

<span data-ttu-id="af40b-173">The `datetimeV2` entity extracts date and time ranges.</span><span class="sxs-lookup"><span data-stu-id="af40b-173">The `datetimeV2` entity extracts date and time ranges.</span></span> <span data-ttu-id="af40b-174">The `start` and `end` fields specify the beginning and end of the range.</span><span class="sxs-lookup"><span data-stu-id="af40b-174">The `start` and `end` fields specify the beginning and end of the range.</span></span> <span data-ttu-id="af40b-175">For the utterance "May 2nd to May 5th", LUIS provides **daterange** values for both the current year and the next year.</span><span class="sxs-lookup"><span data-stu-id="af40b-175">For the utterance "May 2nd to May 5th", LUIS provides **daterange** values for both the current year and the next year.</span></span> <span data-ttu-id="af40b-176">In the `timex` field, the `XXXX` values indicate the ambiguity of the year.</span><span class="sxs-lookup"><span data-stu-id="af40b-176">In the `timex` field, the `XXXX` values indicate the ambiguity of the year.</span></span> <span data-ttu-id="af40b-177">`P3D` indicates the time period is three days long.</span><span class="sxs-lookup"><span data-stu-id="af40b-177">`P3D` indicates the time period is three days long.</span></span>

```JSON
"entities": [
    {
      "entity": "may 2nd to may 5th",
      "type": "builtin.datetimeV2.daterange",
      "startIndex": 0,
      "endIndex": 17,
      "resolution": {
        "values": [
          {
            "timex": "(XXXX-05-02,XXXX-05-05,P3D)",
            "type": "daterange",
            "start": "2017-05-02",
            "end": "2017-05-05"
          },
          {
            "timex": "(XXXX-05-02,XXXX-05-05,P3D)",
            "type": "daterange",
            "start": "2018-05-02",
            "end": "2018-05-05"
          }
        ]
      }
    }
  ]
```

## <a name="date-range-resolution-examples-for-day-of-week"></a><span data-ttu-id="af40b-178">Date range resolution examples for day of week</span><span class="sxs-lookup"><span data-stu-id="af40b-178">Date range resolution examples for day of week</span></span>

<span data-ttu-id="af40b-179">The following example shows how LUIS uses **datetimeV2** to resolve the utterance "Tuesday to Thursday".</span><span class="sxs-lookup"><span data-stu-id="af40b-179">The following example shows how LUIS uses **datetimeV2** to resolve the utterance "Tuesday to Thursday".</span></span> <span data-ttu-id="af40b-180">In this example, the current date is June 19th.</span><span class="sxs-lookup"><span data-stu-id="af40b-180">In this example, the current date is June 19th.</span></span> <span data-ttu-id="af40b-181">LUIS includes **daterange** values for both of the date ranges that precede and follow the current date.</span><span class="sxs-lookup"><span data-stu-id="af40b-181">LUIS includes **daterange** values for both of the date ranges that precede and follow the current date.</span></span>

```JSON
  "entities": [
    {
      "entity": "tuesday to thursday",
      "type": "builtin.datetimeV2.daterange",
      "startIndex": 0,
      "endIndex": 19,
      "resolution": {
        "values": [
          {
            "timex": "(XXXX-WXX-2,XXXX-WXX-4,P2D)",
            "type": "daterange",
            "start": "2017-06-13",
            "end": "2017-06-15"
          },
          {
            "timex": "(XXXX-WXX-2,XXXX-WXX-4,P2D)",
            "type": "daterange",
            "start": "2017-06-20",
            "end": "2017-06-22"
          }
        ]
      }
    }
  ]
```
## <a name="ambiguous-time"></a><span data-ttu-id="af40b-182">Ambiguous time</span><span class="sxs-lookup"><span data-stu-id="af40b-182">Ambiguous time</span></span>
<span data-ttu-id="af40b-183">The values array has two time elements if the time, or time range is ambiguous.</span><span class="sxs-lookup"><span data-stu-id="af40b-183">The values array has two time elements if the time, or time range is ambiguous.</span></span> <span data-ttu-id="af40b-184">When there's an ambiguous time, values have both the A.M.</span><span class="sxs-lookup"><span data-stu-id="af40b-184">When there's an ambiguous time, values have both the A.M.</span></span> <span data-ttu-id="af40b-185">and P.M.</span><span class="sxs-lookup"><span data-stu-id="af40b-185">and P.M.</span></span> <span data-ttu-id="af40b-186">times.</span><span class="sxs-lookup"><span data-stu-id="af40b-186">times.</span></span>

## <a name="time-range-resolution-example"></a><span data-ttu-id="af40b-187">Time range resolution example</span><span class="sxs-lookup"><span data-stu-id="af40b-187">Time range resolution example</span></span>

<span data-ttu-id="af40b-188">The following example shows how LUIS uses **datetimeV2** to resolve the utterance that has a time range.</span><span class="sxs-lookup"><span data-stu-id="af40b-188">The following example shows how LUIS uses **datetimeV2** to resolve the utterance that has a time range.</span></span>

```
  "entities": [
    {
      "entity": "6pm to 7pm",
      "type": "builtin.datetimeV2.timerange",
      "startIndex": 0,
      "endIndex": 9,
      "resolution": {
        "values": [
          {
            "timex": "(T18,T19,PT1H)",
            "type": "timerange",
            "start": "18:00:00",
            "end": "19:00:00"
          }
        ]
      }
    }
  ]
```

## <a name="deprecated-prebuilt-datetime"></a><span data-ttu-id="af40b-189">Deprecated prebuilt datetime</span><span class="sxs-lookup"><span data-stu-id="af40b-189">Deprecated prebuilt datetime</span></span>

<span data-ttu-id="af40b-190">The `datetime` prebuilt entity is deprecated and replaced by **datetimeV2**.</span><span class="sxs-lookup"><span data-stu-id="af40b-190">The `datetime` prebuilt entity is deprecated and replaced by **datetimeV2**.</span></span> 

<span data-ttu-id="af40b-191">To replace `datetime` with `datetimeV2` in your LUIS app, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="af40b-191">To replace `datetime` with `datetimeV2` in your LUIS app, complete the following steps:</span></span>

1. <span data-ttu-id="af40b-192">Open the **Entities** pane of the LUIS web interface.</span><span class="sxs-lookup"><span data-stu-id="af40b-192">Open the **Entities** pane of the LUIS web interface.</span></span> 
2. <span data-ttu-id="af40b-193">Delete the **datetime** prebuilt entity.</span><span class="sxs-lookup"><span data-stu-id="af40b-193">Delete the **datetime** prebuilt entity.</span></span>
3. <span data-ttu-id="af40b-194">Click **Add prebuilt entity**</span><span class="sxs-lookup"><span data-stu-id="af40b-194">Click **Add prebuilt entity**</span></span>
4. <span data-ttu-id="af40b-195">Select **datetimeV2** and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="af40b-195">Select **datetimeV2** and click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af40b-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="af40b-196">Next steps</span></span>

<span data-ttu-id="af40b-197">Learn about the [dimension](luis-reference-prebuilt-dimension.md), [email](luis-reference-prebuilt-email.md) entities, and [number](luis-reference-prebuilt-number.md).</span><span class="sxs-lookup"><span data-stu-id="af40b-197">Learn about the [dimension](luis-reference-prebuilt-dimension.md), [email](luis-reference-prebuilt-email.md) entities, and [number](luis-reference-prebuilt-number.md).</span></span> 

