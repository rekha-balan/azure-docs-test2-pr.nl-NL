---
title: Examples & scenarios - Azure Logic Apps | Microsoft Docs
description: Review logic apps examples for common scenarios
services: logic-apps
author: jeffhollan
manager: anneta
editor: ''
documentationcenter: .net,nodejs,java
ms.assetid: e06311bc-29eb-49df-9273-1f05bbb2395c
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 03/14/2017
ms.author: jehollan
ms.openlocfilehash: dcf089d680249d0a2f9d748b315076d91c8c78e8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551678"
---
# <a name="examples-and-common-scenarios-for-azure-logic-apps"></a><span data-ttu-id="369ba-103">Examples and common scenarios for Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="369ba-103">Examples and common scenarios for Azure Logic Apps</span></span>

<span data-ttu-id="369ba-104">To help you learn more about the many patterns and capabilities in Azure Logic Apps, here are common examples and scenarios.</span><span class="sxs-lookup"><span data-stu-id="369ba-104">To help you learn more about the many patterns and capabilities in Azure Logic Apps, here are common examples and scenarios.</span></span>

## <a name="key-scenarios-for-logic-apps"></a><span data-ttu-id="369ba-105">Key scenarios for logic apps</span><span class="sxs-lookup"><span data-stu-id="369ba-105">Key scenarios for logic apps</span></span>

<span data-ttu-id="369ba-106">Azure Logic Apps provides resilient orchestration and integration for different services.</span><span class="sxs-lookup"><span data-stu-id="369ba-106">Azure Logic Apps provides resilient orchestration and integration for different services.</span></span> <span data-ttu-id="369ba-107">The Logic Apps service is "serverless", so you don't have to worry about scale or instances - all you have to do is define the workflow (trigger and actions).</span><span class="sxs-lookup"><span data-stu-id="369ba-107">The Logic Apps service is "serverless", so you don't have to worry about scale or instances - all you have to do is define the workflow (trigger and actions).</span></span> <span data-ttu-id="369ba-108">The underlying platform handles scale, availability, and performance.</span><span class="sxs-lookup"><span data-stu-id="369ba-108">The underlying platform handles scale, availability, and performance.</span></span> <span data-ttu-id="369ba-109">Any scenario where you need to coordinate multiple actions, especially across multiple systems, is a great use case for Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="369ba-109">Any scenario where you need to coordinate multiple actions, especially across multiple systems, is a great use case for Azure Logic Apps.</span></span> <span data-ttu-id="369ba-110">Here are some patterns and examples.</span><span class="sxs-lookup"><span data-stu-id="369ba-110">Here are some patterns and examples.</span></span>

## <a name="respond-to-triggers-and-extend-actions"></a><span data-ttu-id="369ba-111">Respond to triggers and extend actions</span><span class="sxs-lookup"><span data-stu-id="369ba-111">Respond to triggers and extend actions</span></span>

<span data-ttu-id="369ba-112">Every logic app begins with a trigger.</span><span class="sxs-lookup"><span data-stu-id="369ba-112">Every logic app begins with a trigger.</span></span> <span data-ttu-id="369ba-113">For example, your workflow can start with a schedule event, a manual invocation, or an event from an external system, such as the "when a file is added to an FTP server" trigger.</span><span class="sxs-lookup"><span data-stu-id="369ba-113">For example, your workflow can start with a schedule event, a manual invocation, or an event from an external system, such as the "when a file is added to an FTP server" trigger.</span></span> <span data-ttu-id="369ba-114">Azure Logic Apps currently supports over 100 ready-to-use connectors, ranging from on-premises SAP to Azure Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="369ba-114">Azure Logic Apps currently supports over 100 ready-to-use connectors, ranging from on-premises SAP to Azure Cognitive Services.</span></span> <span data-ttu-id="369ba-115">For systems and services that might not have published connectors, you can also extend logic apps.</span><span class="sxs-lookup"><span data-stu-id="369ba-115">For systems and services that might not have published connectors, you can also extend logic apps.</span></span>

* [<span data-ttu-id="369ba-116">Tutorial: Build an AI-powered social dashboard in minutes with Logic Apps and Power BI</span><span class="sxs-lookup"><span data-stu-id="369ba-116">Tutorial: Build an AI-powered social dashboard in minutes with Logic Apps and Power BI</span></span>](http://aka.ms/logicappsdemo)
* [<span data-ttu-id="369ba-117">Create custom triggers or actions</span><span class="sxs-lookup"><span data-stu-id="369ba-117">Create custom triggers or actions</span></span>](../logic-apps/logic-apps-create-api-app.md)
* [<span data-ttu-id="369ba-118">Set up long-running actions for workflow runs</span><span class="sxs-lookup"><span data-stu-id="369ba-118">Set up long-running actions for workflow runs</span></span>](../logic-apps/logic-apps-create-api-app.md)
* [<span data-ttu-id="369ba-119">Respond to external events and actions with webhooks</span><span class="sxs-lookup"><span data-stu-id="369ba-119">Respond to external events and actions with webhooks</span></span>](../logic-apps/logic-apps-create-api-app.md)
* [<span data-ttu-id="369ba-120">Call, trigger, or nest workflows with synchronous responses to HTTP requests</span><span class="sxs-lookup"><span data-stu-id="369ba-120">Call, trigger, or nest workflows with synchronous responses to HTTP requests</span></span>](logic-apps-http-endpoint.md)
* [<span data-ttu-id="369ba-121">Tutorial: Respond to Twilio SMS webhooks and send a text response</span><span class="sxs-lookup"><span data-stu-id="369ba-121">Tutorial: Respond to Twilio SMS webhooks and send a text response</span></span>](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)

## <a name="error-handling-logging-and-control-flow-capabilities"></a><span data-ttu-id="369ba-122">Error handling, logging, and control flow capabilities</span><span class="sxs-lookup"><span data-stu-id="369ba-122">Error handling, logging, and control flow capabilities</span></span>

<span data-ttu-id="369ba-123">Logic apps include rich capabilities for advanced control flow, like conditions, switches, loops, and scopes.</span><span class="sxs-lookup"><span data-stu-id="369ba-123">Logic apps include rich capabilities for advanced control flow, like conditions, switches, loops, and scopes.</span></span> <span data-ttu-id="369ba-124">To ensure resilient solutions, you can also implement error and exception handling in your workflows.</span><span class="sxs-lookup"><span data-stu-id="369ba-124">To ensure resilient solutions, you can also implement error and exception handling in your workflows.</span></span> <span data-ttu-id="369ba-125">For notification and diagnostic logs for workflow run status, Azure Logic Apps also provides monitoring and alerts.</span><span class="sxs-lookup"><span data-stu-id="369ba-125">For notification and diagnostic logs for workflow run status, Azure Logic Apps also provides monitoring and alerts.</span></span>

* [<span data-ttu-id="369ba-126">Perform different actions with switch statements</span><span class="sxs-lookup"><span data-stu-id="369ba-126">Perform different actions with switch statements</span></span>](logic-apps-switch-case.md)
* [<span data-ttu-id="369ba-127">Process items in arrays and collections with loops and batches in logic apps</span><span class="sxs-lookup"><span data-stu-id="369ba-127">Process items in arrays and collections with loops and batches in logic apps</span></span>](logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="369ba-128">Author error and exception handling in a workflow</span><span class="sxs-lookup"><span data-stu-id="369ba-128">Author error and exception handling in a workflow</span></span>](logic-apps-exception-handling.md)
* [<span data-ttu-id="369ba-129">Configure Azure Alerts and diagnostics</span><span class="sxs-lookup"><span data-stu-id="369ba-129">Configure Azure Alerts and diagnostics</span></span>](logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="369ba-130">Use case: How a healthcare company uses logic app exception handling for HL7 FHIR workflows</span><span class="sxs-lookup"><span data-stu-id="369ba-130">Use case: How a healthcare company uses logic app exception handling for HL7 FHIR workflows</span></span>](logic-apps-scenario-error-and-exception-handling.md)

## <a name="deploy-and-manage-logic-apps"></a><span data-ttu-id="369ba-131">Deploy and manage logic apps</span><span class="sxs-lookup"><span data-stu-id="369ba-131">Deploy and manage logic apps</span></span>

<span data-ttu-id="369ba-132">You can fully develop and deploy logic apps with Visual Studio, Visual Studio Team Services, or any other source control and automated build tools.</span><span class="sxs-lookup"><span data-stu-id="369ba-132">You can fully develop and deploy logic apps with Visual Studio, Visual Studio Team Services, or any other source control and automated build tools.</span></span> <span data-ttu-id="369ba-133">To support deployment for workflows and dependent connections in a resource template, logic apps use Azure resource deployment templates.</span><span class="sxs-lookup"><span data-stu-id="369ba-133">To support deployment for workflows and dependent connections in a resource template, logic apps use Azure resource deployment templates.</span></span> <span data-ttu-id="369ba-134">Visual Studio tools automatically generate these templates, which you can check in to source control for versioning.</span><span class="sxs-lookup"><span data-stu-id="369ba-134">Visual Studio tools automatically generate these templates, which you can check in to source control for versioning.</span></span>

* [<span data-ttu-id="369ba-135">Create an automated deployment template</span><span class="sxs-lookup"><span data-stu-id="369ba-135">Create an automated deployment template</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="369ba-136">Build and deploy logic apps from Visual Studio</span><span class="sxs-lookup"><span data-stu-id="369ba-136">Build and deploy logic apps from Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="369ba-137">Monitor the health of your logic apps</span><span class="sxs-lookup"><span data-stu-id="369ba-137">Monitor the health of your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a><span data-ttu-id="369ba-138">Content types, conversions, and transformations within a run</span><span class="sxs-lookup"><span data-stu-id="369ba-138">Content types, conversions, and transformations within a run</span></span>

<span data-ttu-id="369ba-139">You can access, convert, and transform multiple content types by using the many functions in the Azure Logic Apps [workflow definition language](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="369ba-139">You can access, convert, and transform multiple content types by using the many functions in the Azure Logic Apps [workflow definition language](http://aka.ms/logicappsdocs).</span></span> <span data-ttu-id="369ba-140">For example, you can convert between a string, JSON, and XML with the `@json()` and `@xml()` workflow expressions.</span><span class="sxs-lookup"><span data-stu-id="369ba-140">For example, you can convert between a string, JSON, and XML with the `@json()` and `@xml()` workflow expressions.</span></span> <span data-ttu-id="369ba-141">The Logic Apps engine preserves content types to support content transfer in a lossless manner between services.</span><span class="sxs-lookup"><span data-stu-id="369ba-141">The Logic Apps engine preserves content types to support content transfer in a lossless manner between services.</span></span>

* <span data-ttu-id="369ba-142">[Handle non-JSON content types](../logic-apps/logic-apps-content-type.md), like `application/xml`, `application/octet-stream`, and `multipart/formdata`</span><span class="sxs-lookup"><span data-stu-id="369ba-142">[Handle non-JSON content types](../logic-apps/logic-apps-content-type.md), like `application/xml`, `application/octet-stream`, and `multipart/formdata`</span></span>
* [<span data-ttu-id="369ba-143">How workflow expressions work in logic apps</span><span class="sxs-lookup"><span data-stu-id="369ba-143">How workflow expressions work in logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="369ba-144">Reference: Azure Logic Apps workflow definition language</span><span class="sxs-lookup"><span data-stu-id="369ba-144">Reference: Azure Logic Apps workflow definition language</span></span>](http://aka.ms/logicappsdocs)

## <a name="other-integrations-and-capabilities"></a><span data-ttu-id="369ba-145">Other integrations and capabilities</span><span class="sxs-lookup"><span data-stu-id="369ba-145">Other integrations and capabilities</span></span>

<span data-ttu-id="369ba-146">Logic apps also offer integration with many services, like Azure Functions, Azure API Management, Azure App Services, and custom HTTP endpoints, for example, REST and SOAP.</span><span class="sxs-lookup"><span data-stu-id="369ba-146">Logic apps also offer integration with many services, like Azure Functions, Azure API Management, Azure App Services, and custom HTTP endpoints, for example, REST and SOAP.</span></span>

* [<span data-ttu-id="369ba-147">Create a real-time social dashboard with Azure Serverless</span><span class="sxs-lookup"><span data-stu-id="369ba-147">Create a real-time social dashboard with Azure Serverless</span></span>](logic-apps-scenario-social-serverless.md)
* [<span data-ttu-id="369ba-148">Call Azure Functions from logic apps</span><span class="sxs-lookup"><span data-stu-id="369ba-148">Call Azure Functions from logic apps</span></span>](../logic-apps/logic-apps-azure-functions.md)
* [<span data-ttu-id="369ba-149">Scenario: Trigger logic apps with Azure Functions</span><span class="sxs-lookup"><span data-stu-id="369ba-149">Scenario: Trigger logic apps with Azure Functions</span></span>](logic-apps-scenario-function-sb-trigger.md)
* [<span data-ttu-id="369ba-150">Blog: Call SOAP endpoints from logic apps</span><span class="sxs-lookup"><span data-stu-id="369ba-150">Blog: Call SOAP endpoints from logic apps</span></span>](https://blogs.msdn.microsoft.com/logicapps/2016/04/07/using-soap-services-with-logic-apps/)

## <a name="next-steps"></a><span data-ttu-id="369ba-151">Next Steps</span><span class="sxs-lookup"><span data-stu-id="369ba-151">Next Steps</span></span>

- [<span data-ttu-id="369ba-152">Handle errors and exceptions in logic apps</span><span class="sxs-lookup"><span data-stu-id="369ba-152">Handle errors and exceptions in logic apps</span></span>](logic-apps-exception-handling.md)
- [<span data-ttu-id="369ba-153">Author workflow definitions with the workflow definition language</span><span class="sxs-lookup"><span data-stu-id="369ba-153">Author workflow definitions with the workflow definition language</span></span>](logic-apps-author-definitions.md)
- [<span data-ttu-id="369ba-154">Submit your comments, questions, feedback, or suggestions for how can we improve Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="369ba-154">Submit your comments, questions, feedback, or suggestions for how can we improve Azure Logic Apps</span></span>](https://feedback.azure.com/forums/287593-logic-apps)