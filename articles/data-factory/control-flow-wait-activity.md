---
title: Wait activity in Azure Data Factory | Microsoft Docs
description: The Wait activity pauses the execution of the pipeline for the specified period.
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
ms.date: 01/10/2018
ms.author: shlo
ms.openlocfilehash: 74a5d687535915fab7d518faaf916b98ab262c4b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871267"
---
# <a name="wait-activity-in-azure-data-factory"></a><span data-ttu-id="1caea-103">Wait activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1caea-103">Wait activity in Azure Data Factory</span></span>
<span data-ttu-id="1caea-104">When you use a Wait activity in a pipeline, the pipeline waits for the specified period of time before continuing with execution of subsequent activities.</span><span class="sxs-lookup"><span data-stu-id="1caea-104">When you use a Wait activity in a pipeline, the pipeline waits for the specified period of time before continuing with execution of subsequent activities.</span></span> 

## <a name="syntax"></a><span data-ttu-id="1caea-105">Syntax</span><span class="sxs-lookup"><span data-stu-id="1caea-105">Syntax</span></span>

```json
{
    "name": "MyWaitActivity",
    "type": "Wait",
    "typeProperties": {
        "waitTimeInSeconds": 1
    }
}

```

## <a name="type-properties"></a><span data-ttu-id="1caea-106">Type properties</span><span class="sxs-lookup"><span data-stu-id="1caea-106">Type properties</span></span>

<span data-ttu-id="1caea-107">Property</span><span class="sxs-lookup"><span data-stu-id="1caea-107">Property</span></span> | <span data-ttu-id="1caea-108">Description</span><span class="sxs-lookup"><span data-stu-id="1caea-108">Description</span></span> | <span data-ttu-id="1caea-109">Allowed values</span><span class="sxs-lookup"><span data-stu-id="1caea-109">Allowed values</span></span> | <span data-ttu-id="1caea-110">Required</span><span class="sxs-lookup"><span data-stu-id="1caea-110">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="1caea-111">name</span><span class="sxs-lookup"><span data-stu-id="1caea-111">name</span></span> | <span data-ttu-id="1caea-112">Name of the `Wait` activity.</span><span class="sxs-lookup"><span data-stu-id="1caea-112">Name of the `Wait` activity.</span></span> | <span data-ttu-id="1caea-113">String</span><span class="sxs-lookup"><span data-stu-id="1caea-113">String</span></span> | <span data-ttu-id="1caea-114">Yes</span><span class="sxs-lookup"><span data-stu-id="1caea-114">Yes</span></span>
<span data-ttu-id="1caea-115">type</span><span class="sxs-lookup"><span data-stu-id="1caea-115">type</span></span> | <span data-ttu-id="1caea-116">Must be set to **Wait**.</span><span class="sxs-lookup"><span data-stu-id="1caea-116">Must be set to **Wait**.</span></span> | <span data-ttu-id="1caea-117">String</span><span class="sxs-lookup"><span data-stu-id="1caea-117">String</span></span> | <span data-ttu-id="1caea-118">Yes</span><span class="sxs-lookup"><span data-stu-id="1caea-118">Yes</span></span>
<span data-ttu-id="1caea-119">waitTimeInSeconds</span><span class="sxs-lookup"><span data-stu-id="1caea-119">waitTimeInSeconds</span></span> | <span data-ttu-id="1caea-120">The number of seconds that the pipeline waits before continuing with the processing.</span><span class="sxs-lookup"><span data-stu-id="1caea-120">The number of seconds that the pipeline waits before continuing with the processing.</span></span> | <span data-ttu-id="1caea-121">Integer</span><span class="sxs-lookup"><span data-stu-id="1caea-121">Integer</span></span> | <span data-ttu-id="1caea-122">Yes</span><span class="sxs-lookup"><span data-stu-id="1caea-122">Yes</span></span>

## <a name="example"></a><span data-ttu-id="1caea-123">Example</span><span class="sxs-lookup"><span data-stu-id="1caea-123">Example</span></span>

> [!NOTE]
> <span data-ttu-id="1caea-124">This section provides JSON definitions and sample PowerShell commands to run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="1caea-124">This section provides JSON definitions and sample PowerShell commands to run the pipeline.</span></span> <span data-ttu-id="1caea-125">For a walkthrough with step-by-step instructions to create a Data Factory pipeline by using Azure PowerShell and JSON definitions, see [tutorial: create a data factory by using Azure PowerShell](quickstart-create-data-factory-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1caea-125">For a walkthrough with step-by-step instructions to create a Data Factory pipeline by using Azure PowerShell and JSON definitions, see [tutorial: create a data factory by using Azure PowerShell](quickstart-create-data-factory-powershell.md).</span></span>

### <a name="pipeline-with-wait-activity"></a><span data-ttu-id="1caea-126">Pipeline with Wait activity</span><span class="sxs-lookup"><span data-stu-id="1caea-126">Pipeline with Wait activity</span></span>
<span data-ttu-id="1caea-127">In this example, the pipeline has two activities: **Until** and **Wait**.</span><span class="sxs-lookup"><span data-stu-id="1caea-127">In this example, the pipeline has two activities: **Until** and **Wait**.</span></span> <span data-ttu-id="1caea-128">The Wait activity is configured to wait for one second.</span><span class="sxs-lookup"><span data-stu-id="1caea-128">The Wait activity is configured to wait for one second.</span></span> <span data-ttu-id="1caea-129">The pipeline runs the Web activity in a loop with one second waiting time between each run.</span><span class="sxs-lookup"><span data-stu-id="1caea-129">The pipeline runs the Web activity in a loop with one second waiting time between each run.</span></span> 

```json
{
    "name": "DoUntilPipeline",
    "properties": {
        "activities": [
            {
                "type": "Until",
                "typeProperties": {
                    "expression": {
                        "value": "@equals('Failed', coalesce(body('MyUnauthenticatedActivity')?.status, actions('MyUnauthenticatedActivity')?.status, 'null'))",
                        "type": "Expression"
                    },
                    "timeout": "00:00:01",
                    "activities": [
                        {
                            "name": "MyUnauthenticatedActivity",
                            "type": "WebActivity",
                            "typeProperties": {
                                "method": "get",
                                "url": "https://www.fake.com/",
                                "headers": {
                                    "Content-Type": "application/json"
                                }
                            },
                            "dependsOn": [
                                {
                                    "activity": "MyWaitActivity",
                                    "dependencyConditions": [ "Succeeded" ]
                                }
                            ]
                        },
                        {
                            "type": "Wait",
                            "typeProperties": {
                                "waitTimeInSeconds": 1
                            },
                            "name": "MyWaitActivity"
                        }
                    ]
                },
                "name": "MyUntilActivity"
            }
        ]
    }
}

```

## <a name="next-steps"></a><span data-ttu-id="1caea-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="1caea-130">Next steps</span></span>
<span data-ttu-id="1caea-131">See other control flow activities supported by Data Factory:</span><span class="sxs-lookup"><span data-stu-id="1caea-131">See other control flow activities supported by Data Factory:</span></span> 

- [<span data-ttu-id="1caea-132">If Condition Activity</span><span class="sxs-lookup"><span data-stu-id="1caea-132">If Condition Activity</span></span>](control-flow-if-condition-activity.md)
- [<span data-ttu-id="1caea-133">Execute Pipeline Activity</span><span class="sxs-lookup"><span data-stu-id="1caea-133">Execute Pipeline Activity</span></span>](control-flow-execute-pipeline-activity.md)
- [<span data-ttu-id="1caea-134">For Each Activity</span><span class="sxs-lookup"><span data-stu-id="1caea-134">For Each Activity</span></span>](control-flow-for-each-activity.md)
- [<span data-ttu-id="1caea-135">Get Metadata Activity</span><span class="sxs-lookup"><span data-stu-id="1caea-135">Get Metadata Activity</span></span>](control-flow-get-metadata-activity.md)
- [<span data-ttu-id="1caea-136">Lookup Activity</span><span class="sxs-lookup"><span data-stu-id="1caea-136">Lookup Activity</span></span>](control-flow-lookup-activity.md)
- [<span data-ttu-id="1caea-137">Web Activity</span><span class="sxs-lookup"><span data-stu-id="1caea-137">Web Activity</span></span>](control-flow-web-activity.md)
- [<span data-ttu-id="1caea-138">Until Activity</span><span class="sxs-lookup"><span data-stu-id="1caea-138">Until Activity</span></span>](control-flow-until-activity.md)
