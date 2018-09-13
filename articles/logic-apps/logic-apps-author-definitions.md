---
title: Define workflows with JSON - Azure Logic Apps | Microsoft Docs
description: How to write workflow definitions in JSON for logic apps
author: jeffhollan
manager: anneta
editor: ''
services: logic-apps
documentationcenter: ''
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: c071a7b9090599293fbc6a5f070c7cc0543a80a3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564728"
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="6849d-103">Create workflow definitions for logic apps using JSON</span><span class="sxs-lookup"><span data-stu-id="6849d-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="6849d-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span><span class="sxs-lookup"><span data-stu-id="6849d-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="6849d-105">If you haven't already, first review [how to create your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6849d-105">If you haven't already, first review [how to create your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="6849d-106">Also, see the [full reference for the Workflow Definition Language](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="6849d-106">Also, see the [full reference for the Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="6849d-107">Repeat steps over a list</span><span class="sxs-lookup"><span data-stu-id="6849d-107">Repeat steps over a list</span></span>

<span data-ttu-id="6849d-108">To iterate through an array that has up to 10,000 items and perform an action for each item, use the [foreach type](logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="6849d-108">To iterate through an array that has up to 10,000 items and perform an action for each item, use the [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="6849d-109">Handle failures if something goes wrong</span><span class="sxs-lookup"><span data-stu-id="6849d-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="6849d-110">Usually, you want to include a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span><span class="sxs-lookup"><span data-stu-id="6849d-110">Usually, you want to include a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="6849d-111">This example gets data from various places, but if the call fails, we want to POST a message somewhere so we can track down that failure later:</span><span class="sxs-lookup"><span data-stu-id="6849d-111">This example gets data from various places, but if the call fails, we want to POST a message somewhere so we can track down that failure later:</span></span>  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "postToErrorMessageQueue": {
      "type": "ApiConnection",
      "inputs": "...",
      "runAfter": {
        "readData": [
          "Failed"
        ]
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="6849d-112">To specify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use the `runAfter` property, for example, to specify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span><span class="sxs-lookup"><span data-stu-id="6849d-112">To specify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use the `runAfter` property, for example, to specify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="6849d-113">Finally, because this example now handles the error, we no longer mark the run as `Failed`.</span><span class="sxs-lookup"><span data-stu-id="6849d-113">Finally, because this example now handles the error, we no longer mark the run as `Failed`.</span></span> <span data-ttu-id="6849d-114">Because we added the step for handling this failure in this example, the run has `Succeeded` although one step `Failed`.</span><span class="sxs-lookup"><span data-stu-id="6849d-114">Because we added the step for handling this failure in this example, the run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="6849d-115">Execute two or more steps in parallel</span><span class="sxs-lookup"><span data-stu-id="6849d-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="6849d-116">To run multiple actions in parallel, the `runAfter` property must be equivalent at runtime.</span><span class="sxs-lookup"><span data-stu-id="6849d-116">To run multiple actions in parallel, the `runAfter` property must be equivalent at runtime.</span></span> 

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "kind": "http",
      "type": "Request"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="6849d-117">In this example, both `branch1` and `branch2` are set to run after `readData`.</span><span class="sxs-lookup"><span data-stu-id="6849d-117">In this example, both `branch1` and `branch2` are set to run after `readData`.</span></span> <span data-ttu-id="6849d-118">As a result, both branches run in parallel.</span><span class="sxs-lookup"><span data-stu-id="6849d-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="6849d-119">The timestamp for both branches is identical.</span><span class="sxs-lookup"><span data-stu-id="6849d-119">The timestamp for both branches is identical.</span></span>

![Parallel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="6849d-121">Join two parallel branches</span><span class="sxs-lookup"><span data-stu-id="6849d-121">Join two parallel branches</span></span>

<span data-ttu-id="6849d-122">You can join two actions that are set to run in parallel by adding items to the `runAfter` property as in the previous example.</span><span class="sxs-lookup"><span data-stu-id="6849d-122">You can join two actions that are set to run in parallel by adding items to the `runAfter` property as in the previous example.</span></span>

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-04-01-preview/workflowdefinition.json#",
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {}
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "join": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "branch1": [
          "Succeeded"
        ],
        "branch2": [
          "Succeeded"
        ]
      }
    }
  },
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "Http",
      "inputs": {
        "schema": {}
      }
    }
  },
  "contentVersion": "1.0.0.0",
  "outputs": {}
}
```

![Parallel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-author-definitions/join.png)

## <a name="map-list-items-to-a-different-configuration"></a><span data-ttu-id="6849d-124">Map list items to a different configuration</span><span class="sxs-lookup"><span data-stu-id="6849d-124">Map list items to a different configuration</span></span>

<span data-ttu-id="6849d-125">Next, let's say that we want to get different content based on the value of a property.</span><span class="sxs-lookup"><span data-stu-id="6849d-125">Next, let's say that we want to get different content based on the value of a property.</span></span> <span data-ttu-id="6849d-126">We can create a map of values to destinations as a parameter:</span><span class="sxs-lookup"><span data-stu-id="6849d-126">We can create a map of values to destinations as a parameter:</span></span>  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "specialCategories": {
      "defaultValue": [
        "science",
        "google",
        "microsoft",
        "robots",
        "NSA"
      ],
      "type": "Array"
    },
    "destinationMap": {
      "defaultValue": {
        "science": "http://www.nasa.gov",
        "microsoft": "https://www.microsoft.com/en-us/default.aspx",
        "google": "https://www.google.com",
        "robots": "https://en.wikipedia.org/wiki/Robot",
        "NSA": "https://www.nsa.gov/"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "http"
    }
  },
  "actions": {
    "getArticles": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "https://ajax.googleapis.com/ajax/services/feed/load?v=1.0&q=http://feeds.wired.com/wired/index"
      }
    },
    "forEachArticle": {
      "type": "foreach",
      "foreach": "@body('getArticles').responseData.feed.entries",
      "actions": {
        "ifGreater": {
          "type": "if",
          "expression": "@greater(length(intersection(item().categories, parameters('specialCategories'))), 0)",
          "actions": {
            "getSpecialPage": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('destinationMap')[first(intersection(item().categories, parameters('specialCategories')))]"
              }
            }
          }
        }
      },
      "runAfter": {
        "getArticles": [
          "Succeeded"
        ]
      }
    }
  }
}
```

<span data-ttu-id="6849d-127">In this case, we first get a list of articles.</span><span class="sxs-lookup"><span data-stu-id="6849d-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="6849d-128">Based on the category that was defined as a parameter, the second step uses a map to look up the URL for getting the content.</span><span class="sxs-lookup"><span data-stu-id="6849d-128">Based on the category that was defined as a parameter, the second step uses a map to look up the URL for getting the content.</span></span>

<span data-ttu-id="6849d-129">Some times to note here:</span><span class="sxs-lookup"><span data-stu-id="6849d-129">Some times to note here:</span></span> 

*   <span data-ttu-id="6849d-130">The [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether the category matches one of the known defined categories.</span><span class="sxs-lookup"><span data-stu-id="6849d-130">The [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether the category matches one of the known defined categories.</span></span>

*   <span data-ttu-id="6849d-131">After we get the category, we can pull the item from the map using square brackets: `parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="6849d-131">After we get the category, we can pull the item from the map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="6849d-132">Process strings</span><span class="sxs-lookup"><span data-stu-id="6849d-132">Process strings</span></span>

<span data-ttu-id="6849d-133">You can use various functions to manipulate strings.</span><span class="sxs-lookup"><span data-stu-id="6849d-133">You can use various functions to manipulate strings.</span></span> <span data-ttu-id="6849d-134">For example, suppose we have a string that we want to pass to a system, but we aren't confident about proper handling for character encoding.</span><span class="sxs-lookup"><span data-stu-id="6849d-134">For example, suppose we have a string that we want to pass to a system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="6849d-135">One option is to base64 encode this string.</span><span class="sxs-lookup"><span data-stu-id="6849d-135">One option is to base64 encode this string.</span></span> <span data-ttu-id="6849d-136">However, to avoid escaping in a URL, we are going to replace a few characters.</span><span class="sxs-lookup"><span data-stu-id="6849d-136">However, to avoid escaping in a URL, we are going to replace a few characters.</span></span> 

<span data-ttu-id="6849d-137">We also want a substring of the order's name because the first five characters are not used.</span><span class="sxs-lookup"><span data-stu-id="6849d-137">We also want a substring of the order's name because the first five characters are not used.</span></span>

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1",
        "orderer": "NAME=St�ph�n__�?�i?ian�"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{replace(replace(base64(substring(parameters('order').orderer,5,sub(length(parameters('order').orderer), 5) )),'+','-') ,'/' ,'_' )}"
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="6849d-138">Working from inside to outside:</span><span class="sxs-lookup"><span data-stu-id="6849d-138">Working from inside to outside:</span></span>

1. <span data-ttu-id="6849d-139">Get the [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for the orderer's name, so we get back the total number of characters.</span><span class="sxs-lookup"><span data-stu-id="6849d-139">Get the [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for the orderer's name, so we get back the total number of characters.</span></span>

2. <span data-ttu-id="6849d-140">Subtract 5 because we want a shorter string.</span><span class="sxs-lookup"><span data-stu-id="6849d-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="6849d-141">Actually, take the [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span><span class="sxs-lookup"><span data-stu-id="6849d-141">Actually, take the [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="6849d-142">We start at index `5` and go the remainder of the string.</span><span class="sxs-lookup"><span data-stu-id="6849d-142">We start at index `5` and go the remainder of the string.</span></span>

4. <span data-ttu-id="6849d-143">Convert this substring to a [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span><span class="sxs-lookup"><span data-stu-id="6849d-143">Convert this substring to a [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="6849d-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `+` characters with `-` characters.</span><span class="sxs-lookup"><span data-stu-id="6849d-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="6849d-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `/` characters with `_` characters.</span><span class="sxs-lookup"><span data-stu-id="6849d-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="6849d-146">Work with Date Times</span><span class="sxs-lookup"><span data-stu-id="6849d-146">Work with Date Times</span></span>

<span data-ttu-id="6849d-147">Date Times can be useful, particularly when you are trying to pull data from a data source that doesn't naturally support *triggers*.</span><span class="sxs-lookup"><span data-stu-id="6849d-147">Date Times can be useful, particularly when you are trying to pull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="6849d-148">You can also use Date Times for finding how long various steps are taking.</span><span class="sxs-lookup"><span data-stu-id="6849d-148">You can also use Date Times for finding how long various steps are taking.</span></span>

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{parameters('order').id}"
      }
    },
    "ifTimingWarning": {
      "type": "If",
      "expression": "@less(actions('order').startTime,addseconds(utcNow(),-1))",
      "actions": {
        "timingWarning": {
          "type": "Http",
          "inputs": {
            "method": "GET",
            "uri": "http://www.example.com/?recordLongOrderTime=@{parameters('order').id}&currentTime=@{utcNow('r')}"
          }
        }
      },
      "runAfter": {
        "order": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="6849d-149">In this example, we extract the `startTime` from the previous step.</span><span class="sxs-lookup"><span data-stu-id="6849d-149">In this example, we extract the `startTime` from the previous step.</span></span> <span data-ttu-id="6849d-150">Then we get the current time, and subtract one second:</span><span class="sxs-lookup"><span data-stu-id="6849d-150">Then we get the current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="6849d-151">You can use other units of time, like `minutes` or `hours`.</span><span class="sxs-lookup"><span data-stu-id="6849d-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="6849d-152">Finally, we can compare these two values.</span><span class="sxs-lookup"><span data-stu-id="6849d-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="6849d-153">If the first value is less than the second value, then more than one second has passed since the order was first placed.</span><span class="sxs-lookup"><span data-stu-id="6849d-153">If the first value is less than the second value, then more than one second has passed since the order was first placed.</span></span>

<span data-ttu-id="6849d-154">To format dates, we can use string formatters.</span><span class="sxs-lookup"><span data-stu-id="6849d-154">To format dates, we can use string formatters.</span></span> <span data-ttu-id="6849d-155">For example, to get the RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="6849d-155">For example, to get the RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="6849d-156">To learn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="6849d-156">To learn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="6849d-157">Deployment parameters for different environments</span><span class="sxs-lookup"><span data-stu-id="6849d-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="6849d-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span><span class="sxs-lookup"><span data-stu-id="6849d-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="6849d-159">For example, you might use the same definition in all these environments but use different databases.</span><span class="sxs-lookup"><span data-stu-id="6849d-159">For example, you might use the same definition in all these environments but use different databases.</span></span> <span data-ttu-id="6849d-160">Likewise, you might want to use the same definition across different regions for high availability but want each logic app instance to talk to that region's database.</span><span class="sxs-lookup"><span data-stu-id="6849d-160">Likewise, you might want to use the same definition across different regions for high availability but want each logic app instance to talk to that region's database.</span></span>
<span data-ttu-id="6849d-161">This scenario differs from taking parameters at *runtime* where instead, you should use the `trigger()` function as in the previous example.</span><span class="sxs-lookup"><span data-stu-id="6849d-161">This scenario differs from taking parameters at *runtime* where instead, you should use the `trigger()` function as in the previous example.</span></span>

<span data-ttu-id="6849d-162">You can start with a basic definition like this example:</span><span class="sxs-lookup"><span data-stu-id="6849d-162">You can start with a basic definition like this example:</span></span>

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "uri": {
            "type": "string"
        }
    },
    "triggers": {
        "request": {
          "type": "request",
          "kind": "http"
        }
    },
    "actions": {
        "readData": {
            "type": "Http",
            "inputs": {
                "method": "GET",
                "uri": "@parameters('uri')"
            }
        }
    },
    "outputs": {}
}
```

<span data-ttu-id="6849d-163">In the actual `PUT` request for the logic apps, you can provide the parameter `uri`.</span><span class="sxs-lookup"><span data-stu-id="6849d-163">In the actual `PUT` request for the logic apps, you can provide the parameter `uri`.</span></span> <span data-ttu-id="6849d-164">Because a default value no longer exists, the logic app payload requires this parameter:</span><span class="sxs-lookup"><span data-stu-id="6849d-164">Because a default value no longer exists, the logic app payload requires this parameter:</span></span>

```
{
    "properties": {},
        "definition": {
          // Use the definition from above here
        },
        "parameters": {
            "connection": {
                "value": "https://my.connection.that.is.per.enviornment"
            }
        }
    },
    "location": "westus"
}
``` 

<span data-ttu-id="6849d-165">In each environment, you can provide a different value for the `connection` parameter.</span><span class="sxs-lookup"><span data-stu-id="6849d-165">In each environment, you can provide a different value for the `connection` parameter.</span></span> 

<span data-ttu-id="6849d-166">For all the options that you have for creating and managing logic apps, see the [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span><span class="sxs-lookup"><span data-stu-id="6849d-166">For all the options that you have for creating and managing logic apps, see the [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 


