---
title: Batch test your LUIS app - Language Understanding
titleSuffix: Azure Cognitive Services
description: Use batch testing to continuously work on your application to refine it and improve its language understanding.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 07/06/2018
ms.author: diberry
ms.openlocfilehash: 6c621d3cfc56b20511b16d014f7925cb92ccc279
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868857"
---
# <a name="batch-testing-in-luis"></a><span data-ttu-id="bc75b-103">Batch testing in LUIS</span><span class="sxs-lookup"><span data-stu-id="bc75b-103">Batch testing in LUIS</span></span>

<span data-ttu-id="bc75b-104">Batch testing validates your [active](luis-concept-version.md#active-version) trained model to measure its prediction accuracy.</span><span class="sxs-lookup"><span data-stu-id="bc75b-104">Batch testing validates your [active](luis-concept-version.md#active-version) trained model to measure its prediction accuracy.</span></span> <span data-ttu-id="bc75b-105">A batch test helps you view the accuracy of each intent and entity in your current trained model in a chart.</span><span class="sxs-lookup"><span data-stu-id="bc75b-105">A batch test helps you view the accuracy of each intent and entity in your current trained model in a chart.</span></span> <span data-ttu-id="bc75b-106">Review the batch test results to take appropriate action to improve accuracy, such as adding more example utterances to an intent if your app frequently fails to identify the correct intent.</span><span class="sxs-lookup"><span data-stu-id="bc75b-106">Review the batch test results to take appropriate action to improve accuracy, such as adding more example utterances to an intent if your app frequently fails to identify the correct intent.</span></span>

## <a name="group-data-for-batch-test"></a><span data-ttu-id="bc75b-107">Group data for batch test</span><span class="sxs-lookup"><span data-stu-id="bc75b-107">Group data for batch test</span></span>
<span data-ttu-id="bc75b-108">It is important that utterances used for batch testing are new to LUIS.</span><span class="sxs-lookup"><span data-stu-id="bc75b-108">It is important that utterances used for batch testing are new to LUIS.</span></span> <span data-ttu-id="bc75b-109">If you have a dataset of utterances, divide the utterances into three sets: utterances added to an intent, utterances received from the published endpoint, and utterances used to batch test LUIS after it is trained.</span><span class="sxs-lookup"><span data-stu-id="bc75b-109">If you have a dataset of utterances, divide the utterances into three sets: utterances added to an intent, utterances received from the published endpoint, and utterances used to batch test LUIS after it is trained.</span></span> 

## <a name="a-dataset-of-utterances"></a><span data-ttu-id="bc75b-110">A dataset of utterances</span><span class="sxs-lookup"><span data-stu-id="bc75b-110">A dataset of utterances</span></span>
<span data-ttu-id="bc75b-111">Submit a batch file of utterances, known as a *dataset*, for batch testing.</span><span class="sxs-lookup"><span data-stu-id="bc75b-111">Submit a batch file of utterances, known as a *dataset*, for batch testing.</span></span> <span data-ttu-id="bc75b-112">The dataset is a JSON-formatted file containing a maximum of 1,000 labeled **non-duplicate** utterances.</span><span class="sxs-lookup"><span data-stu-id="bc75b-112">The dataset is a JSON-formatted file containing a maximum of 1,000 labeled **non-duplicate** utterances.</span></span> <span data-ttu-id="bc75b-113">You can test up to 10 datasets in an app.</span><span class="sxs-lookup"><span data-stu-id="bc75b-113">You can test up to 10 datasets in an app.</span></span> <span data-ttu-id="bc75b-114">If you need to test more, delete a dataset and then add a new one.</span><span class="sxs-lookup"><span data-stu-id="bc75b-114">If you need to test more, delete a dataset and then add a new one.</span></span>

|<span data-ttu-id="bc75b-115">**Rules**</span><span class="sxs-lookup"><span data-stu-id="bc75b-115">**Rules**</span></span>|
|--|
|<span data-ttu-id="bc75b-116">\*No duplicate utterances</span><span class="sxs-lookup"><span data-stu-id="bc75b-116">\*No duplicate utterances</span></span>|
|<span data-ttu-id="bc75b-117">No hierarchical entity children</span><span class="sxs-lookup"><span data-stu-id="bc75b-117">No hierarchical entity children</span></span>|
|<span data-ttu-id="bc75b-118">1000 utterances or less</span><span class="sxs-lookup"><span data-stu-id="bc75b-118">1000 utterances or less</span></span>|

<span data-ttu-id="bc75b-119">\*Duplicates are considered exact string matches, not matches that are tokenized first.</span><span class="sxs-lookup"><span data-stu-id="bc75b-119">\*Duplicates are considered exact string matches, not matches that are tokenized first.</span></span> 

## <a name="entities-allowed-in-batch-tests"></a><span data-ttu-id="bc75b-120">Entities allowed in batch tests</span><span class="sxs-lookup"><span data-stu-id="bc75b-120">Entities allowed in batch tests</span></span>
<span data-ttu-id="bc75b-121">Entities include simple, hierarchical parents, and composite.</span><span class="sxs-lookup"><span data-stu-id="bc75b-121">Entities include simple, hierarchical parents, and composite.</span></span> <span data-ttu-id="bc75b-122">All entities of these types appear in the batch test entities filter even if there are no corresponding entities in the batch file.</span><span class="sxs-lookup"><span data-stu-id="bc75b-122">All entities of these types appear in the batch test entities filter even if there are no corresponding entities in the batch file.</span></span>


<a name="json-file-with-no-duplicates"></a>
<a name="example-batch-file"></a>
## <a name="batch-file-format"></a><span data-ttu-id="bc75b-123">Batch file format</span><span class="sxs-lookup"><span data-stu-id="bc75b-123">Batch file format</span></span>
<span data-ttu-id="bc75b-124">The batch file consists of utterances.</span><span class="sxs-lookup"><span data-stu-id="bc75b-124">The batch file consists of utterances.</span></span> <span data-ttu-id="bc75b-125">Each utterance must have an expected intent prediction along with any [machine-learned entities](luis-concept-entity-types.md#types-of-entities) you expect to be detected.</span><span class="sxs-lookup"><span data-stu-id="bc75b-125">Each utterance must have an expected intent prediction along with any [machine-learned entities](luis-concept-entity-types.md#types-of-entities) you expect to be detected.</span></span> 

<span data-ttu-id="bc75b-126">The  following is an example of a batch file with proper syntax:</span><span class="sxs-lookup"><span data-stu-id="bc75b-126">The  following is an example of a batch file with proper syntax:</span></span>

```JSON
[
  {
    "text": "Are there any janitorial jobs currently open?",
    "intent": "GetJobInformation",
    "entities": 
    [
        {
            "entity": "Job",
            "startPos": 14,
            "endPos": 23
        }
    ]
  },
  {
    "text": "I would like a fullstack typescript programming with azure job",
    "intent": "GetJobInformation",
    "entities": 
    [
        {
            "entity": "Job",
            "startPos": 15,
            "endPos": 46
        }
    ]
  },
  {
    "text": "Is there a database position open in Los Colinas?",
    "intent": "GetJobInformation",
    "entities": 
    [
        {
            "entity": "Job",
            "startPos": 11,
            "endPos": 18
        }
    ]
  },
  {
    "text": "Please find database jobs open today in Seattle",
    "intent": "GetJobInformation",
    "entities": 
    [
        {
            "entity": "Job",
            "startPos": 12,
            "endPos": 19
        }
    ]
  }
]
```

## <a name="batch-syntax-template"></a><span data-ttu-id="bc75b-127">Batch syntax template</span><span class="sxs-lookup"><span data-stu-id="bc75b-127">Batch syntax template</span></span>

<span data-ttu-id="bc75b-128">Use the following template to start your batch file:</span><span class="sxs-lookup"><span data-stu-id="bc75b-128">Use the following template to start your batch file:</span></span>

```JSON
[
  {
    "text": "example utterance goes here",
    "intent": "intent name goes here",
    "entities": 
    [
        {
            "entity": "entity name 1 goes here",
            "startPos": 14,
            "endPos": 23
        },
        {
            "entity": "entity name 2 goes here",
            "startPos": 14,
            "endPos": 23
        }
    ]
  }
]
```

<span data-ttu-id="bc75b-129">The batch file uses the **startPos** and **endPos** properties to note the beginning and end of an entity.</span><span class="sxs-lookup"><span data-stu-id="bc75b-129">The batch file uses the **startPos** and **endPos** properties to note the beginning and end of an entity.</span></span> <span data-ttu-id="bc75b-130">The values are zero-based and should not begin or end on a space.</span><span class="sxs-lookup"><span data-stu-id="bc75b-130">The values are zero-based and should not begin or end on a space.</span></span> 

<span data-ttu-id="bc75b-131">This is different from the query logs, which use startIndex and endIndex properties.</span><span class="sxs-lookup"><span data-stu-id="bc75b-131">This is different from the query logs, which use startIndex and endIndex properties.</span></span> 


## <a name="common-errors-importing-a-batch"></a><span data-ttu-id="bc75b-132">Common errors importing a batch</span><span class="sxs-lookup"><span data-stu-id="bc75b-132">Common errors importing a batch</span></span>
<span data-ttu-id="bc75b-133">Common errors include:</span><span class="sxs-lookup"><span data-stu-id="bc75b-133">Common errors include:</span></span> 

> * <span data-ttu-id="bc75b-134">More than 1,000 utterances</span><span class="sxs-lookup"><span data-stu-id="bc75b-134">More than 1,000 utterances</span></span>
> * <span data-ttu-id="bc75b-135">An utterance JSON object that doesn't have an entities property</span><span class="sxs-lookup"><span data-stu-id="bc75b-135">An utterance JSON object that doesn't have an entities property</span></span>
> * <span data-ttu-id="bc75b-136">Word(s) labeled in multiple entities</span><span class="sxs-lookup"><span data-stu-id="bc75b-136">Word(s) labeled in multiple entities</span></span>

## <a name="batch-test-state"></a><span data-ttu-id="bc75b-137">Batch test state</span><span class="sxs-lookup"><span data-stu-id="bc75b-137">Batch test state</span></span>
<span data-ttu-id="bc75b-138">LUIS tracks the state of each dataset's last test.</span><span class="sxs-lookup"><span data-stu-id="bc75b-138">LUIS tracks the state of each dataset's last test.</span></span> <span data-ttu-id="bc75b-139">This includes the size (number of utterances in the batch), last run date, and last result (number of successfully predicted utterances).</span><span class="sxs-lookup"><span data-stu-id="bc75b-139">This includes the size (number of utterances in the batch), last run date, and last result (number of successfully predicted utterances).</span></span>

<a name="sections-of-the-results-chart"></a>
## <a name="batch-test-results"></a><span data-ttu-id="bc75b-140">Batch test results</span><span class="sxs-lookup"><span data-stu-id="bc75b-140">Batch test results</span></span>
<span data-ttu-id="bc75b-141">The batch test result is a scatter graph, known as an error matrix.</span><span class="sxs-lookup"><span data-stu-id="bc75b-141">The batch test result is a scatter graph, known as an error matrix.</span></span> <span data-ttu-id="bc75b-142">This graph is a 4-way comparison of the utterances in the file and the current model's predicted intent and entities.</span><span class="sxs-lookup"><span data-stu-id="bc75b-142">This graph is a 4-way comparison of the utterances in the file and the current model's predicted intent and entities.</span></span> 

<span data-ttu-id="bc75b-143">Data points on the **False Positive** and **False Negative** sections indicate errors, which should be investigated.</span><span class="sxs-lookup"><span data-stu-id="bc75b-143">Data points on the **False Positive** and **False Negative** sections indicate errors, which should be investigated.</span></span> <span data-ttu-id="bc75b-144">If all data points are on the **True Positive** and **True Negative** sections, then your app's accuracy is perfect on this dataset.</span><span class="sxs-lookup"><span data-stu-id="bc75b-144">If all data points are on the **True Positive** and **True Negative** sections, then your app's accuracy is perfect on this dataset.</span></span>

![Four sections of chart](./media/luis-concept-batch-test/chart-sections.png)

<span data-ttu-id="bc75b-146">This chart helps you find utterances that LUIS predicts incorrectly based on its current training.</span><span class="sxs-lookup"><span data-stu-id="bc75b-146">This chart helps you find utterances that LUIS predicts incorrectly based on its current training.</span></span> <span data-ttu-id="bc75b-147">The results are displayed per region of the chart.</span><span class="sxs-lookup"><span data-stu-id="bc75b-147">The results are displayed per region of the chart.</span></span> <span data-ttu-id="bc75b-148">Select individual points on the graph to review the utterance information or select region name to review utterance results in that region.</span><span class="sxs-lookup"><span data-stu-id="bc75b-148">Select individual points on the graph to review the utterance information or select region name to review utterance results in that region.</span></span>

![Batch testing](./media/luis-concept-batch-test/batch-testing.png)

## <a name="errors-in-the-results"></a><span data-ttu-id="bc75b-150">Errors in the results</span><span class="sxs-lookup"><span data-stu-id="bc75b-150">Errors in the results</span></span>
<span data-ttu-id="bc75b-151">Errors in the batch test indicate intents that are not predicted as noted in the batch file.</span><span class="sxs-lookup"><span data-stu-id="bc75b-151">Errors in the batch test indicate intents that are not predicted as noted in the batch file.</span></span> <span data-ttu-id="bc75b-152">Errors are indicated in the two red sections of the chart.</span><span class="sxs-lookup"><span data-stu-id="bc75b-152">Errors are indicated in the two red sections of the chart.</span></span> 

<span data-ttu-id="bc75b-153">The false positive section indicates that an utterance matched an intent or entity when it shouldn't have.</span><span class="sxs-lookup"><span data-stu-id="bc75b-153">The false positive section indicates that an utterance matched an intent or entity when it shouldn't have.</span></span> <span data-ttu-id="bc75b-154">The false negative indicates an utterance did not match an intent or entity when it should have.</span><span class="sxs-lookup"><span data-stu-id="bc75b-154">The false negative indicates an utterance did not match an intent or entity when it should have.</span></span> 

## <a name="fixing-batch-errors"></a><span data-ttu-id="bc75b-155">Fixing batch errors</span><span class="sxs-lookup"><span data-stu-id="bc75b-155">Fixing batch errors</span></span>
<span data-ttu-id="bc75b-156">If there are errors in the batch testing, you can either add more utterances to an intent, and/or label more utterances with the entity to help LUIS make the discrimination between intents.</span><span class="sxs-lookup"><span data-stu-id="bc75b-156">If there are errors in the batch testing, you can either add more utterances to an intent, and/or label more utterances with the entity to help LUIS make the discrimination between intents.</span></span> <span data-ttu-id="bc75b-157">If you have added utterances, and labeled them, and still get prediction errors in batch testing, consider adding a [phrase list](luis-concept-feature.md) feature with domain-specific vocabulary to help LUIS learn faster.</span><span class="sxs-lookup"><span data-stu-id="bc75b-157">If you have added utterances, and labeled them, and still get prediction errors in batch testing, consider adding a [phrase list](luis-concept-feature.md) feature with domain-specific vocabulary to help LUIS learn faster.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bc75b-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc75b-158">Next steps</span></span>

* <span data-ttu-id="bc75b-159">Learn how to [test a batch](luis-how-to-batch-test.md)</span><span class="sxs-lookup"><span data-stu-id="bc75b-159">Learn how to [test a batch](luis-how-to-batch-test.md)</span></span>
