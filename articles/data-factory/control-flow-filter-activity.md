---
title: Filter activity in Azure Data Factory | Microsoft Docs
description: The Filter activity filters the inputs.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/04/2018
ms.author: shlo
ms.openlocfilehash: b3b26869a84b8519ced19a4c93a6d39d6ed20f9b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966429"
---
# <a name="filter-activity-in-azure-data-factory"></a><span data-ttu-id="3482f-103">Filter activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3482f-103">Filter activity in Azure Data Factory</span></span>
<span data-ttu-id="3482f-104">You can use a Filter activity in a pipeline to apply a filter expression to an input array.</span><span class="sxs-lookup"><span data-stu-id="3482f-104">You can use a Filter activity in a pipeline to apply a filter expression to an input array.</span></span> 

## <a name="syntax"></a><span data-ttu-id="3482f-105">Syntax</span><span class="sxs-lookup"><span data-stu-id="3482f-105">Syntax</span></span>

```json
{
    "name": "MyFilterActivity",
    "type": "filter",
    "typeProperties": {
        "condition": "<condition>",
        "items": "<input array>"
    }
}
```

## <a name="type-properties"></a><span data-ttu-id="3482f-106">Type properties</span><span class="sxs-lookup"><span data-stu-id="3482f-106">Type properties</span></span>

<span data-ttu-id="3482f-107">Property</span><span class="sxs-lookup"><span data-stu-id="3482f-107">Property</span></span> | <span data-ttu-id="3482f-108">Description</span><span class="sxs-lookup"><span data-stu-id="3482f-108">Description</span></span> | <span data-ttu-id="3482f-109">Allowed values</span><span class="sxs-lookup"><span data-stu-id="3482f-109">Allowed values</span></span> | <span data-ttu-id="3482f-110">Required</span><span class="sxs-lookup"><span data-stu-id="3482f-110">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="3482f-111">name</span><span class="sxs-lookup"><span data-stu-id="3482f-111">name</span></span> | <span data-ttu-id="3482f-112">Name of the `Filter` activity.</span><span class="sxs-lookup"><span data-stu-id="3482f-112">Name of the `Filter` activity.</span></span> | <span data-ttu-id="3482f-113">String</span><span class="sxs-lookup"><span data-stu-id="3482f-113">String</span></span> | <span data-ttu-id="3482f-114">Yes</span><span class="sxs-lookup"><span data-stu-id="3482f-114">Yes</span></span>
<span data-ttu-id="3482f-115">type</span><span class="sxs-lookup"><span data-stu-id="3482f-115">type</span></span> | <span data-ttu-id="3482f-116">Must be set to **filter**.</span><span class="sxs-lookup"><span data-stu-id="3482f-116">Must be set to **filter**.</span></span> | <span data-ttu-id="3482f-117">String</span><span class="sxs-lookup"><span data-stu-id="3482f-117">String</span></span> | <span data-ttu-id="3482f-118">Yes</span><span class="sxs-lookup"><span data-stu-id="3482f-118">Yes</span></span>
<span data-ttu-id="3482f-119">condition</span><span class="sxs-lookup"><span data-stu-id="3482f-119">condition</span></span> | <span data-ttu-id="3482f-120">Condition to be used for filtering the input.</span><span class="sxs-lookup"><span data-stu-id="3482f-120">Condition to be used for filtering the input.</span></span> | <span data-ttu-id="3482f-121">Expression</span><span class="sxs-lookup"><span data-stu-id="3482f-121">Expression</span></span> | <span data-ttu-id="3482f-122">Yes</span><span class="sxs-lookup"><span data-stu-id="3482f-122">Yes</span></span>
<span data-ttu-id="3482f-123">items</span><span class="sxs-lookup"><span data-stu-id="3482f-123">items</span></span> | <span data-ttu-id="3482f-124">Input array on which filter should be applied.</span><span class="sxs-lookup"><span data-stu-id="3482f-124">Input array on which filter should be applied.</span></span> | <span data-ttu-id="3482f-125">Expression</span><span class="sxs-lookup"><span data-stu-id="3482f-125">Expression</span></span> | <span data-ttu-id="3482f-126">Yes</span><span class="sxs-lookup"><span data-stu-id="3482f-126">Yes</span></span>

## <a name="example"></a><span data-ttu-id="3482f-127">Example</span><span class="sxs-lookup"><span data-stu-id="3482f-127">Example</span></span>

<span data-ttu-id="3482f-128">In this example, the pipeline has two activities: **Filter** and **ForEach**.</span><span class="sxs-lookup"><span data-stu-id="3482f-128">In this example, the pipeline has two activities: **Filter** and **ForEach**.</span></span> <span data-ttu-id="3482f-129">The Filter activity is configured to filter the input array for items with a value greater than 3.</span><span class="sxs-lookup"><span data-stu-id="3482f-129">The Filter activity is configured to filter the input array for items with a value greater than 3.</span></span> <span data-ttu-id="3482f-130">The ForEach activity then iterates over the filtered values and waits for the number of seconds specified by the current value.</span><span class="sxs-lookup"><span data-stu-id="3482f-130">The ForEach activity then iterates over the filtered values and waits for the number of seconds specified by the current value.</span></span>

```json
{
    "name": "PipelineName",
    "properties": {
        "activities": [{
                "name": "MyFilterActivity",
                "type": "filter",
                "typeProperties": {
                    "condition": "@greater(item(),3)",
                    "items": "@pipeline().parameters.inputs"
                }
            },
            {
                "name": "MyForEach",
                "type": "ForEach",
                "typeProperties": {
                    "isSequential": "false",
                    "batchCount": 1,
                    "items": "@activity('MyFilterActivity').output.value",
                    "activities": [{
                        "type": "Wait",
                        "typeProperties": {
                            "waitTimeInSeconds": "@item()"
                        },
                        "name": "MyWaitActivity"
                    }]
                },
                "dependsOn": [{
                    "activity": "MyFilterActivity",
                    "dependencyConditions": ["Succeeded"]
                }]
            }
        ],
        "parameters": {
            "inputs": {
                "type": "Array",
                "defaultValue": [1, 2, 3, 4, 5, 6]
            }
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="3482f-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="3482f-131">Next steps</span></span>
<span data-ttu-id="3482f-132">See other control flow activities supported by Data Factory:</span><span class="sxs-lookup"><span data-stu-id="3482f-132">See other control flow activities supported by Data Factory:</span></span> 

- [<span data-ttu-id="3482f-133">If Condition Activity</span><span class="sxs-lookup"><span data-stu-id="3482f-133">If Condition Activity</span></span>](control-flow-if-condition-activity.md)
- [<span data-ttu-id="3482f-134">Execute Pipeline Activity</span><span class="sxs-lookup"><span data-stu-id="3482f-134">Execute Pipeline Activity</span></span>](control-flow-execute-pipeline-activity.md)
- [<span data-ttu-id="3482f-135">For Each Activity</span><span class="sxs-lookup"><span data-stu-id="3482f-135">For Each Activity</span></span>](control-flow-for-each-activity.md)
- [<span data-ttu-id="3482f-136">Get Metadata Activity</span><span class="sxs-lookup"><span data-stu-id="3482f-136">Get Metadata Activity</span></span>](control-flow-get-metadata-activity.md)
- [<span data-ttu-id="3482f-137">Lookup Activity</span><span class="sxs-lookup"><span data-stu-id="3482f-137">Lookup Activity</span></span>](control-flow-lookup-activity.md)
- [<span data-ttu-id="3482f-138">Web Activity</span><span class="sxs-lookup"><span data-stu-id="3482f-138">Web Activity</span></span>](control-flow-web-activity.md)
- [<span data-ttu-id="3482f-139">Until Activity</span><span class="sxs-lookup"><span data-stu-id="3482f-139">Until Activity</span></span>](control-flow-until-activity.md)
