---
title: Scenario - Trigger logic apps with Azure Functions and Azure Service Bus | Microsoft Docs
description: Create functions that trigger logic apps by using Azure Functions and Azure Service Bus
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.reviewer: jehollan, klam, LADocs
ms.topic: article
ms.assetid: 19cbd921-7071-4221-ab86-b44d0fc0ecef
ms.date: 08/25/2018
ms.openlocfilehash: 8d6f2ecaec7bf7ae7e4415ccd60fc6ec3ff487f3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805693"
---
# <a name="scenario-trigger-logic-apps-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="0056a-103">Scenario: Trigger logic apps with Azure Functions and Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="0056a-103">Scenario: Trigger logic apps with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="0056a-104">You can use Azure Functions to create a trigger for a logic app when you need to deploy a long-running listener or task.</span><span class="sxs-lookup"><span data-stu-id="0056a-104">You can use Azure Functions to create a trigger for a logic app when you need to deploy a long-running listener or task.</span></span> <span data-ttu-id="0056a-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span><span class="sxs-lookup"><span data-stu-id="0056a-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0056a-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0056a-106">Prerequisites</span></span>

* <span data-ttu-id="0056a-107">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0056a-107">An Azure subscription.</span></span> <span data-ttu-id="0056a-108">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="0056a-108">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> 

* <span data-ttu-id="0056a-109">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="0056a-109">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span> 

* <span data-ttu-id="0056a-110">Before you can create an Azure function, [create a function app](../azure-functions/functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0056a-110">Before you can create an Azure function, [create a function app](../azure-functions/functions-create-function-app-portal.md).</span></span>

## <a name="create-logic-app"></a><span data-ttu-id="0056a-111">Create logic app</span><span class="sxs-lookup"><span data-stu-id="0056a-111">Create logic app</span></span>

<span data-ttu-id="0056a-112">In this example, you have a function running for each logic app that needs to be triggered.</span><span class="sxs-lookup"><span data-stu-id="0056a-112">In this example, you have a function running for each logic app that needs to be triggered.</span></span> <span data-ttu-id="0056a-113">First, create a logic app that has an HTTP request trigger.</span><span class="sxs-lookup"><span data-stu-id="0056a-113">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="0056a-114">The function calls that endpoint whenever a queue message is received.</span><span class="sxs-lookup"><span data-stu-id="0056a-114">The function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="0056a-115">Sign in to the [Azure portal](https://portal.azure.com), and create blank logic app.</span><span class="sxs-lookup"><span data-stu-id="0056a-115">Sign in to the [Azure portal](https://portal.azure.com), and create blank logic app.</span></span> 

   <span data-ttu-id="0056a-116">If you're new to logic apps, review [Quickstart: Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="0056a-116">If you're new to logic apps, review [Quickstart: Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>

1. <span data-ttu-id="0056a-117">In the search box, enter "http request".</span><span class="sxs-lookup"><span data-stu-id="0056a-117">In the search box, enter "http request".</span></span> <span data-ttu-id="0056a-118">Under the triggers list, select this trigger: **When a HTTP request is received**</span><span class="sxs-lookup"><span data-stu-id="0056a-118">Under the triggers list, select this trigger: **When a HTTP request is received**</span></span>

   ![Select trigger](./media/logic-apps-scenario-function-sb-trigger/when-http-request-received-trigger.png)

1. <span data-ttu-id="0056a-120">For the **Request** trigger, you can optionally enter a JSON schema for use with the queue message.</span><span class="sxs-lookup"><span data-stu-id="0056a-120">For the **Request** trigger, you can optionally enter a JSON schema for use with the queue message.</span></span> <span data-ttu-id="0056a-121">JSON schemas help the Logic App Designer understand the structure of the input data and makes outputs easier for you to select throughout the workflow.</span><span class="sxs-lookup"><span data-stu-id="0056a-121">JSON schemas help the Logic App Designer understand the structure of the input data and makes outputs easier for you to select throughout the workflow.</span></span> 

   <span data-ttu-id="0056a-122">To specify a schema, enter the schema in the **Request Body JSON Schema** box, for example:</span><span class="sxs-lookup"><span data-stu-id="0056a-122">To specify a schema, enter the schema in the **Request Body JSON Schema** box, for example:</span></span> 

   ![Specify JSON schema](./media/logic-apps-scenario-function-sb-trigger/when-http-request-received-trigger-schema.png)

   <span data-ttu-id="0056a-124">If you don't have a schema, but you have a sample payload in JSON format, you can generate a schema from that payload.</span><span class="sxs-lookup"><span data-stu-id="0056a-124">If you don't have a schema, but you have a sample payload in JSON format, you can generate a schema from that payload.</span></span>

   1. <span data-ttu-id="0056a-125">In the Request trigger, choose **Use sample payload to generate schema**.</span><span class="sxs-lookup"><span data-stu-id="0056a-125">In the Request trigger, choose **Use sample payload to generate schema**.</span></span>

   1. <span data-ttu-id="0056a-126">Under **Enter or paste a sample JSON payload**, enter your sample payload, and then choose **Done**.</span><span class="sxs-lookup"><span data-stu-id="0056a-126">Under **Enter or paste a sample JSON payload**, enter your sample payload, and then choose **Done**.</span></span>
      
      ![Enter sample payload](./media/logic-apps-scenario-function-sb-trigger/enter-sample-payload.png)

   <span data-ttu-id="0056a-128">This sample payload generates this schema that appears in the trigger:</span><span class="sxs-lookup"><span data-stu-id="0056a-128">This sample payload generates this schema that appears in the trigger:</span></span>

   ```json
   {
      "type": "object",
      "properties": {
         "address": {
            "type": "object",
            "properties": {
               "number": {
                  "type": "integer"
               },
               "street": {
                  "type": "string"
               },
               "city": {
                  "type": "string"
               },
               "postalCode": {
                  "type": "integer"
               },
               "country": {
                  "type": "string"
               }
            }
         }
      }
   }
   ```

1. <span data-ttu-id="0056a-129">Add any other actions you want to happen after receiving the queue message.</span><span class="sxs-lookup"><span data-stu-id="0056a-129">Add any other actions you want to happen after receiving the queue message.</span></span> 

   <span data-ttu-id="0056a-130">For example, you can send an email with the Office 365 Outlook connector.</span><span class="sxs-lookup"><span data-stu-id="0056a-130">For example, you can send an email with the Office 365 Outlook connector.</span></span>

1. <span data-ttu-id="0056a-131">Save your logic app, which generates the callback URL for the trigger in this logic app.</span><span class="sxs-lookup"><span data-stu-id="0056a-131">Save your logic app, which generates the callback URL for the trigger in this logic app.</span></span> <span data-ttu-id="0056a-132">This URL appears in the **HTTP POST URL** property.</span><span class="sxs-lookup"><span data-stu-id="0056a-132">This URL appears in the **HTTP POST URL** property.</span></span>

   ![Generated callback URL for trigger](./media/logic-apps-scenario-function-sb-trigger/callback-URL-for-trigger.png)

## <a name="create-azure-function"></a><span data-ttu-id="0056a-134">Create Azure function</span><span class="sxs-lookup"><span data-stu-id="0056a-134">Create Azure function</span></span>

<span data-ttu-id="0056a-135">Next, create the function that acts as the trigger and listens to the queue.</span><span class="sxs-lookup"><span data-stu-id="0056a-135">Next, create the function that acts as the trigger and listens to the queue.</span></span> 

1. <span data-ttu-id="0056a-136">In the Azure portal, open and expand your function app, if not already open.</span><span class="sxs-lookup"><span data-stu-id="0056a-136">In the Azure portal, open and expand your function app, if not already open.</span></span> 

1. <span data-ttu-id="0056a-137">Under your function app name, expand **Functions**.</span><span class="sxs-lookup"><span data-stu-id="0056a-137">Under your function app name, expand **Functions**.</span></span> <span data-ttu-id="0056a-138">On the **Functions** pane, choose **New function**.</span><span class="sxs-lookup"><span data-stu-id="0056a-138">On the **Functions** pane, choose **New function**.</span></span> <span data-ttu-id="0056a-139">Select this template: **Service Bus Queue trigger - C#**</span><span class="sxs-lookup"><span data-stu-id="0056a-139">Select this template: **Service Bus Queue trigger - C#**</span></span>
   
   ![Select Azure Functions portal](./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png)

1. <span data-ttu-id="0056a-141">Provide a name for your trigger, and then configure the connection to the Service Bus queue, which uses the Azure Service Bus SDK `OnMessageReceive()` listener.</span><span class="sxs-lookup"><span data-stu-id="0056a-141">Provide a name for your trigger, and then configure the connection to the Service Bus queue, which uses the Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>

1. <span data-ttu-id="0056a-142">Write a basic function to call the previously created logic app endpoint by using the queue message as a trigger, for example:</span><span class="sxs-lookup"><span data-stu-id="0056a-142">Write a basic function to call the previously created logic app endpoint by using the queue message as a trigger, for example:</span></span> 
   
   ```CSharp
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

   <span data-ttu-id="0056a-143">This example uses the `application/json` message content type, but you can change this type as necessary.</span><span class="sxs-lookup"><span data-stu-id="0056a-143">This example uses the `application/json` message content type, but you can change this type as necessary.</span></span>

1. <span data-ttu-id="0056a-144">To test the function, add a queue message by using a tool such as the [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="0056a-144">To test the function, add a queue message by using a tool such as the [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> 

   <span data-ttu-id="0056a-145">The logic app triggers immediately after the function receives the message.</span><span class="sxs-lookup"><span data-stu-id="0056a-145">The logic app triggers immediately after the function receives the message.</span></span>

## <a name="get-support"></a><span data-ttu-id="0056a-146">Get support</span><span class="sxs-lookup"><span data-stu-id="0056a-146">Get support</span></span>

* <span data-ttu-id="0056a-147">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="0056a-147">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="0056a-148">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="0056a-148">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

