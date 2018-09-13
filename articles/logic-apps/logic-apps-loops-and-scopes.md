---
title: Create loops and scopes, or debatch data in workflows - Azure Logic Apps | Microsoft Docs
description: Create loops to iterate through data, group actions into scopes, or debatch data to start more workflows in Azure Logic Apps.
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: ''
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: jehollan
ms.openlocfilehash: 63ac171494e13f4451d585c3b704727eeed94fab
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555059"
---
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="a874a-103">Logic Apps Loops, Scopes, and Debatching</span><span class="sxs-lookup"><span data-stu-id="a874a-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="a874a-104">Logic Apps provides a number of ways to work with arrays, collections, batches, and loops within a workflow.</span><span class="sxs-lookup"><span data-stu-id="a874a-104">Logic Apps provides a number of ways to work with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="a874a-105">ForEach loop and arrays</span><span class="sxs-lookup"><span data-stu-id="a874a-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="a874a-106">Logic Apps allows you to loop over a set of data and perform an action for each item.</span><span class="sxs-lookup"><span data-stu-id="a874a-106">Logic Apps allows you to loop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="a874a-107">This is possible via the `foreach` action.</span><span class="sxs-lookup"><span data-stu-id="a874a-107">This is possible via the `foreach` action.</span></span>  <span data-ttu-id="a874a-108">In the designer, you can specify to add a for each loop.</span><span class="sxs-lookup"><span data-stu-id="a874a-108">In the designer, you can specify to add a for each loop.</span></span>  <span data-ttu-id="a874a-109">After selecting the array you wish to iterate over, you can begin adding actions.</span><span class="sxs-lookup"><span data-stu-id="a874a-109">After selecting the array you wish to iterate over, you can begin adding actions.</span></span>  <span data-ttu-id="a874a-110">Currently you are limited to only one action per foreach loop, but this restriction will be lifted in the coming weeks.</span><span class="sxs-lookup"><span data-stu-id="a874a-110">Currently you are limited to only one action per foreach loop, but this restriction will be lifted in the coming weeks.</span></span>  <span data-ttu-id="a874a-111">Once within the loop you can begin to specify what should occur at each value of the array.</span><span class="sxs-lookup"><span data-stu-id="a874a-111">Once within the loop you can begin to specify what should occur at each value of the array.</span></span>

<span data-ttu-id="a874a-112">If using code-view, you can specify a for each loop like below.</span><span class="sxs-lookup"><span data-stu-id="a874a-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="a874a-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span><span class="sxs-lookup"><span data-stu-id="a874a-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

``` json
{
    "email_filter": {
        "type": "query",
        "inputs": {
            "from": "@triggerBody()['emails']",
            "where": "@contains(item()['email'], 'microsoft.com')"
        }
    },
    "forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "actions": {
            "send_email": {
                "type": "ApiConnection",
                "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                },
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                },
                }
            }
        },
        "runAfter":{
            "email_filter": [ "Succeeded" ]
        }
    }
}
```
  
  <span data-ttu-id="a874a-114">A `foreach` action can iterate over arrays up to 5,000 rows.</span><span class="sxs-lookup"><span data-stu-id="a874a-114">A `foreach` action can iterate over arrays up to 5,000 rows.</span></span>  <span data-ttu-id="a874a-115">Each iteration will execute in parallel by default.</span><span class="sxs-lookup"><span data-stu-id="a874a-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="a874a-116">Sequential ForEach loops</span><span class="sxs-lookup"><span data-stu-id="a874a-116">Sequential ForEach loops</span></span>

<span data-ttu-id="a874a-117">To enable a foreach loop to execute sequentially, the `Sequential` operation option should be added.</span><span class="sxs-lookup"><span data-stu-id="a874a-117">To enable a foreach loop to execute sequentially, the `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="a874a-118">Until loop</span><span class="sxs-lookup"><span data-stu-id="a874a-118">Until loop</span></span>
  
  <span data-ttu-id="a874a-119">You can perform an action or series of actions until a condition is met.</span><span class="sxs-lookup"><span data-stu-id="a874a-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="a874a-120">The most common scenario for this is calling an endpoint until you get the response you are looking for.</span><span class="sxs-lookup"><span data-stu-id="a874a-120">The most common scenario for this is calling an endpoint until you get the response you are looking for.</span></span>  <span data-ttu-id="a874a-121">In the designer, you can specify to add an until loop.</span><span class="sxs-lookup"><span data-stu-id="a874a-121">In the designer, you can specify to add an until loop.</span></span>  <span data-ttu-id="a874a-122">After adding actions inside the loop, you can set the exit condition, as well as the loop limits.</span><span class="sxs-lookup"><span data-stu-id="a874a-122">After adding actions inside the loop, you can set the exit condition, as well as the loop limits.</span></span>  <span data-ttu-id="a874a-123">There is a 1 minute delay between loop cycles.</span><span class="sxs-lookup"><span data-stu-id="a874a-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="a874a-124">If using code-view, you can specify an until loop like below.</span><span class="sxs-lookup"><span data-stu-id="a874a-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="a874a-125">This is an example of calling an HTTP endpoint until the response body has the value 'Completed'.</span><span class="sxs-lookup"><span data-stu-id="a874a-125">This is an example of calling an HTTP endpoint until the response body has the value 'Completed'.</span></span>  <span data-ttu-id="a874a-126">It will complete when either</span><span class="sxs-lookup"><span data-stu-id="a874a-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="a874a-127">HTTP Response has status of 'Completed'</span><span class="sxs-lookup"><span data-stu-id="a874a-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="a874a-128">It has tried for 1 hour</span><span class="sxs-lookup"><span data-stu-id="a874a-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="a874a-129">It has looped 100 times</span><span class="sxs-lookup"><span data-stu-id="a874a-129">It has looped 100 times</span></span>
  
  ``` json
  {
      "until_successful":{
        "type": "until",
        "expression": "@equals(actions('http')['status'], 'Completed')",
        "limit": {
            "count": 100,
            "timeout": "PT1H"
        },
        "actions": {
            "create_resource": {
                "type": "http",
                "inputs": {
                    "url": "http://provisionRseource.com",
                    "body": {
                        "resourceId": "@triggerBody()"
                    }
                }
            }
        }
      }
  }
  ```
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="a874a-130">SplitOn and debatching</span><span class="sxs-lookup"><span data-stu-id="a874a-130">SplitOn and debatching</span></span>

<span data-ttu-id="a874a-131">Sometimes a trigger may receive an array of items that you want to debatch and start a workflow per item.</span><span class="sxs-lookup"><span data-stu-id="a874a-131">Sometimes a trigger may receive an array of items that you want to debatch and start a workflow per item.</span></span>  <span data-ttu-id="a874a-132">This can be accomplished via the `spliton` command.</span><span class="sxs-lookup"><span data-stu-id="a874a-132">This can be accomplished via the `spliton` command.</span></span>  <span data-ttu-id="a874a-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span><span class="sxs-lookup"><span data-stu-id="a874a-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="a874a-134">SplitOn can only be added to a trigger.</span><span class="sxs-lookup"><span data-stu-id="a874a-134">SplitOn can only be added to a trigger.</span></span>  <span data-ttu-id="a874a-135">This can be manually configured or overridden in definition code-view.</span><span class="sxs-lookup"><span data-stu-id="a874a-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="a874a-136">Currently SplitOn can debatch arrays up to 5,000 items.</span><span class="sxs-lookup"><span data-stu-id="a874a-136">Currently SplitOn can debatch arrays up to 5,000 items.</span></span>  <span data-ttu-id="a874a-137">You cannot have a `spliton` and also implement the synchronous response pattern.</span><span class="sxs-lookup"><span data-stu-id="a874a-137">You cannot have a `spliton` and also implement the synchronous response pattern.</span></span>  <span data-ttu-id="a874a-138">Any workflow called that has a `response` action in addition to `spliton` will run asynchronously and send an immediate `202 Accepted` response.</span><span class="sxs-lookup"><span data-stu-id="a874a-138">Any workflow called that has a `response` action in addition to `spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="a874a-139">SplitOn can be specified in code-view as the following example.</span><span class="sxs-lookup"><span data-stu-id="a874a-139">SplitOn can be specified in code-view as the following example.</span></span>  <span data-ttu-id="a874a-140">This receives an array of items and debatches on each row.</span><span class="sxs-lookup"><span data-stu-id="a874a-140">This receives an array of items and debatches on each row.</span></span>

```
{
    "myDebatchTrigger": {
        "type": "Http",
        "inputs": {
            "url": "http://getNewCustomers",
        },
        "recurrence": {
            "frequencey": "Second",
            "interval": 15
        },
        "spliton": "@triggerBody()['rows']"
    }
}
```

## <a name="scopes"></a><span data-ttu-id="a874a-141">Scopes</span><span class="sxs-lookup"><span data-stu-id="a874a-141">Scopes</span></span>

<span data-ttu-id="a874a-142">It is possible to group a series of actions together using a scope.</span><span class="sxs-lookup"><span data-stu-id="a874a-142">It is possible to group a series of actions together using a scope.</span></span>  <span data-ttu-id="a874a-143">This is particularly useful for implementing exception handling.</span><span class="sxs-lookup"><span data-stu-id="a874a-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="a874a-144">In the designer you can add a new scope, and begin adding any actions inside of it.</span><span class="sxs-lookup"><span data-stu-id="a874a-144">In the designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="a874a-145">You can define scopes in code-view like the following:</span><span class="sxs-lookup"><span data-stu-id="a874a-145">You can define scopes in code-view like the following:</span></span>


```
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```