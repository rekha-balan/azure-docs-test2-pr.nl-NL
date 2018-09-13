---
title: Scenario - Trigger logic apps with Azure Functions and Azure Service Bus | Microsoft Docs
description: Create a function to trigger a logic app by using Azure Functions and Azure Service Bus
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: ''
ms.assetid: 19cbd921-7071-4221-ab86-b44d0fc0ecef
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/23/2016
ms.author: jehollan
ms.openlocfilehash: 6cb1c2052e675417f1596d1efb62359208f6cbee
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563384"
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="9ed33-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="9ed33-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="9ed33-104">You can use Azure Functions to create a trigger for a logic app when you need to deploy a long-running listener or task.</span><span class="sxs-lookup"><span data-stu-id="9ed33-104">You can use Azure Functions to create a trigger for a logic app when you need to deploy a long-running listener or task.</span></span> <span data-ttu-id="9ed33-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span><span class="sxs-lookup"><span data-stu-id="9ed33-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-the-logic-app"></a><span data-ttu-id="9ed33-106">Build the logic app</span><span class="sxs-lookup"><span data-stu-id="9ed33-106">Build the logic app</span></span>
<span data-ttu-id="9ed33-107">In this example, you have a function running for each logic app that needs to be triggered.</span><span class="sxs-lookup"><span data-stu-id="9ed33-107">In this example, you have a function running for each logic app that needs to be triggered.</span></span> <span data-ttu-id="9ed33-108">First, create a logic app that has an HTTP request trigger.</span><span class="sxs-lookup"><span data-stu-id="9ed33-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="9ed33-109">The function calls that endpoint whenever a queue message is received.</span><span class="sxs-lookup"><span data-stu-id="9ed33-109">The function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="9ed33-110">Create a logic app.</span><span class="sxs-lookup"><span data-stu-id="9ed33-110">Create a logic app.</span></span>
2. <span data-ttu-id="9ed33-111">Select the **Manual - When an HTTP Request is Received** trigger.</span><span class="sxs-lookup"><span data-stu-id="9ed33-111">Select the **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="9ed33-112">Optionally, you can specify a JSON schema to use with the queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span><span class="sxs-lookup"><span data-stu-id="9ed33-112">Optionally, you can specify a JSON schema to use with the queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="9ed33-113">Paste the schema in the trigger.</span><span class="sxs-lookup"><span data-stu-id="9ed33-113">Paste the schema in the trigger.</span></span> <span data-ttu-id="9ed33-114">Schemas help the designer understand the shape of the data and flow properties more easily through the workflow.</span><span class="sxs-lookup"><span data-stu-id="9ed33-114">Schemas help the designer understand the shape of the data and flow properties more easily through the workflow.</span></span>
2. <span data-ttu-id="9ed33-115">Add any additional steps that you want to occur after a queue message is received.</span><span class="sxs-lookup"><span data-stu-id="9ed33-115">Add any additional steps that you want to occur after a queue message is received.</span></span> <span data-ttu-id="9ed33-116">For example, send an email via Office 365.</span><span class="sxs-lookup"><span data-stu-id="9ed33-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="9ed33-117">Save the logic app to generate the callback URL for the trigger to this logic app.</span><span class="sxs-lookup"><span data-stu-id="9ed33-117">Save the logic app to generate the callback URL for the trigger to this logic app.</span></span> <span data-ttu-id="9ed33-118">The URL appears on the trigger card.</span><span class="sxs-lookup"><span data-stu-id="9ed33-118">The URL appears on the trigger card.</span></span>

![The callback URL appears on the trigger card][1]

## <a name="build-the-function"></a><span data-ttu-id="9ed33-120">Build the function</span><span class="sxs-lookup"><span data-stu-id="9ed33-120">Build the function</span></span>
<span data-ttu-id="9ed33-121">Next, you must create a function that acts as the trigger and listens to the queue.</span><span class="sxs-lookup"><span data-stu-id="9ed33-121">Next, you must create a function that acts as the trigger and listens to the queue.</span></span>

1. <span data-ttu-id="9ed33-122">In the [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select the **ServiceBusQueueTrigger - C#** template.</span><span class="sxs-lookup"><span data-stu-id="9ed33-122">In the [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select the **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![Azure Functions portal][2]
2. <span data-ttu-id="9ed33-124">Configure the connection to the Service Bus queue, which uses the Azure Service Bus SDK `OnMessageReceive()` listener.</span><span class="sxs-lookup"><span data-stu-id="9ed33-124">Configure the connection to the Service Bus queue, which uses the Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="9ed33-125">Write a basic function to call the logic app endpoint (created earlier) by using the queue message as a trigger.</span><span class="sxs-lookup"><span data-stu-id="9ed33-125">Write a basic function to call the logic app endpoint (created earlier) by using the queue message as a trigger.</span></span> <span data-ttu-id="9ed33-126">Here's a full example of a function.</span><span class="sxs-lookup"><span data-stu-id="9ed33-126">Here's a full example of a function.</span></span> <span data-ttu-id="9ed33-127">The example uses an `application/json` message content type, but you can change this type as necessary.</span><span class="sxs-lookup"><span data-stu-id="9ed33-127">The example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
   ```
   using System;
   using System.Threading.Tasks;
   using System.Net.Http;
   using System.Text;
   
   private static string logicAppUri = @"https://prod-05.westus.logic.azure.com:443/.........";
   
   public static void Run(string myQueueItem, TraceWriter log)
   {
   
       log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
       using (var client = new HttpClient())
       {
           var response = client.PostAsync(logicAppUri, new StringContent(myQueueItem, Encoding.UTF8, "application/json")).Result;
       }
   }
   ```

<span data-ttu-id="9ed33-128">To test, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="9ed33-128">To test, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="9ed33-129">See the logic app fire immediately after the function receives the message.</span><span class="sxs-lookup"><span data-stu-id="9ed33-129">See the logic app fire immediately after the function receives the message.</span></span>

<!-- Image References -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png


