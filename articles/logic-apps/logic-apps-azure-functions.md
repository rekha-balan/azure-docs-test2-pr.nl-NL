---
title: Custom code for Azure Logic Apps with Azure Functions | Microsoft Docs
description: Create and run custom code for Azure Logic Apps with Azure Functions
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: ''
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: jehollan
ms.openlocfilehash: dc8e14f77d7c4038f97687bf472cbd5581edca1c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660694"
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="f0553-103">Add and run custom code for logic apps through Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f0553-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="f0553-104">To run custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="f0553-104">To run custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="f0553-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span><span class="sxs-lookup"><span data-stu-id="f0553-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="f0553-106">Advanced formatting or compute of fields in logic apps</span><span class="sxs-lookup"><span data-stu-id="f0553-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="f0553-107">Perform calculations in a workflow.</span><span class="sxs-lookup"><span data-stu-id="f0553-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="f0553-108">Extend the logic app functionality with functions that are supported in C# or node.js</span><span class="sxs-lookup"><span data-stu-id="f0553-108">Extend the logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="f0553-109">Create custom functions for your logic apps</span><span class="sxs-lookup"><span data-stu-id="f0553-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="f0553-110">We recommend that you create a function in the Azure Functions portal, from the **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span><span class="sxs-lookup"><span data-stu-id="f0553-110">We recommend that you create a function in the Azure Functions portal, from the **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="f0553-111">The result creates an auto-populated a template that accepts `application/json` from a logic app.</span><span class="sxs-lookup"><span data-stu-id="f0553-111">The result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="f0553-112">Functions that you create from these templates are automatically detected and appear in the Logic App Designer under **Azure Functions in my region.**</span><span class="sxs-lookup"><span data-stu-id="f0553-112">Functions that you create from these templates are automatically detected and appear in the Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="f0553-113">In the Azure portal, on the **Integrate** pane for your function, your template should show that **Mode** set to **Webhook** and **Webhook type** is set to **Generic JSON**.</span><span class="sxs-lookup"><span data-stu-id="f0553-113">In the Azure portal, on the **Integrate** pane for your function, your template should show that **Mode** set to **Webhook** and **Webhook type** is set to **Generic JSON**.</span></span> 

<span data-ttu-id="f0553-114">Webhook functions accept a request and pass it into the method via a `data` variable.</span><span class="sxs-lookup"><span data-stu-id="f0553-114">Webhook functions accept a request and pass it into the method via a `data` variable.</span></span> <span data-ttu-id="f0553-115">You can access the properties of your payload by using dot notation like `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="f0553-115">You can access the properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="f0553-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="f0553-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like the following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="f0553-117">Call Azure Functions from logic apps</span><span class="sxs-lookup"><span data-stu-id="f0553-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="f0553-118">To list the containers in your subscription and select the function that you want to call, in Logic App Designer, click the **Actions** menu, and select from **Azure Functions in my Region**.</span><span class="sxs-lookup"><span data-stu-id="f0553-118">To list the containers in your subscription and select the function that you want to call, in Logic App Designer, click the **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="f0553-119">After you select the function, you are asked to specify an input payload object.</span><span class="sxs-lookup"><span data-stu-id="f0553-119">After you select the function, you are asked to specify an input payload object.</span></span> <span data-ttu-id="f0553-120">This object is the message that the logic app sends to the function and must be a JSON object.</span><span class="sxs-lookup"><span data-stu-id="f0553-120">This object is the message that the logic app sends to the function and must be a JSON object.</span></span> <span data-ttu-id="f0553-121">For example, if you want to pass in the **Last Modified** date from a Salesforce trigger, the function payload might look like this example:</span><span class="sxs-lookup"><span data-stu-id="f0553-121">For example, if you want to pass in the **Last Modified** date from a Salesforce trigger, the function payload might look like this example:</span></span>

![Last modified date][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="f0553-123">Trigger logic apps from a function</span><span class="sxs-lookup"><span data-stu-id="f0553-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="f0553-124">You can trigger a logic app from inside a function.</span><span class="sxs-lookup"><span data-stu-id="f0553-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="f0553-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="f0553-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="f0553-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST to the manual trigger URL with the payload that you want sent to the logic app.</span><span class="sxs-lookup"><span data-stu-id="f0553-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST to the manual trigger URL with the payload that you want sent to the logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="f0553-127">Create a function from Logic App Designer</span><span class="sxs-lookup"><span data-stu-id="f0553-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="f0553-128">You can also create a node.js webhook function from the designer.</span><span class="sxs-lookup"><span data-stu-id="f0553-128">You can also create a node.js webhook function from the designer.</span></span> <span data-ttu-id="f0553-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span><span class="sxs-lookup"><span data-stu-id="f0553-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="f0553-130">If you don't yet have a container, you need to create one from the [Azure Functions portal](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="f0553-130">If you don't yet have a container, you need to create one from the [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="f0553-131">Then select **Create New**.</span><span class="sxs-lookup"><span data-stu-id="f0553-131">Then select **Create New**.</span></span>  

<span data-ttu-id="f0553-132">To generate a template based on the data that you want to compute, specify the context object that you plan to pass into a function.</span><span class="sxs-lookup"><span data-stu-id="f0553-132">To generate a template based on the data that you want to compute, specify the context object that you plan to pass into a function.</span></span> <span data-ttu-id="f0553-133">This object must be a JSON object.</span><span class="sxs-lookup"><span data-stu-id="f0553-133">This object must be a JSON object.</span></span> <span data-ttu-id="f0553-134">For example, if you pass in the file content from an FTP action, the context payload looks like this example:</span><span class="sxs-lookup"><span data-stu-id="f0553-134">For example, if you pass in the file content from an FTP action, the context payload looks like this example:</span></span>

![Context payload][2]

> [!NOTE]
> <span data-ttu-id="f0553-136">Because this object wasn't cast as a string, the content is added directly to the JSON payload.</span><span class="sxs-lookup"><span data-stu-id="f0553-136">Because this object wasn't cast as a string, the content is added directly to the JSON payload.</span></span> <span data-ttu-id="f0553-137">However, an error occurs if the object is not a JSON token (that is, a string or a JSON object/array).</span><span class="sxs-lookup"><span data-stu-id="f0553-137">However, an error occurs if the object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="f0553-138">To cast the object as a string, add quotes as shown in the first illustration in this article.</span><span class="sxs-lookup"><span data-stu-id="f0553-138">To cast the object as a string, add quotes as shown in the first illustration in this article.</span></span>
> 

<span data-ttu-id="f0553-139">The designer then generates a function template that you can create inline.</span><span class="sxs-lookup"><span data-stu-id="f0553-139">The designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="f0553-140">Variables are pre-created based on the context that you plan to pass into the function.</span><span class="sxs-lookup"><span data-stu-id="f0553-140">Variables are pre-created based on the context that you plan to pass into the function.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-azure-functions/callfunction.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-azure-functions/createfunction.png


