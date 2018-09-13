---
title: Connectors for Azure Logic Apps | Microsoft Docs
description: Automate workflows with connectors for Azure Logic Apps, including built-in, managed, on-premises, integration account, and enterprise connectors
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.suite: integration
ms.topic: article
ms.date: 08/23/2018
ms.openlocfilehash: 6b31882ec3916e60ac7dc7b8117328176abef1b4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44791315"
---
# <a name="connectors-for-azure-logic-apps"></a><span data-ttu-id="2ddb8-103">Connectors for Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="2ddb8-103">Connectors for Azure Logic Apps</span></span>

<span data-ttu-id="2ddb8-104">Connectors play an integral part when you create automated workflows with Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-104">Connectors play an integral part when you create automated workflows with Azure Logic Apps.</span></span> <span data-ttu-id="2ddb8-105">By using connectors in your logic apps, you expand the capabilities for your on-premises and cloud apps to perform tasks with the data that you create and already have.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-105">By using connectors in your logic apps, you expand the capabilities for your on-premises and cloud apps to perform tasks with the data that you create and already have.</span></span> 

<span data-ttu-id="2ddb8-106">While Logic Apps offers [~200+ connectors](https://docs.microsoft.com/connectors), this article describes popular and more commonly used connectors that are successfully used by thousands of apps and millions of executions for processing data and information.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-106">While Logic Apps offers [~200+ connectors](https://docs.microsoft.com/connectors), this article describes popular and more commonly used connectors that are successfully used by thousands of apps and millions of executions for processing data and information.</span></span> <span data-ttu-id="2ddb8-107">Connectors are available as either built-ins or managed connectors.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-107">Connectors are available as either built-ins or managed connectors.</span></span> 

> [!NOTE]
> <span data-ttu-id="2ddb8-108">For the full list of connectors and each connector's reference information, such as actions, any triggers, and limits, you can find the full list under the [Connectors overview](https://docs.microsoft.com/connectors).</span><span class="sxs-lookup"><span data-stu-id="2ddb8-108">For the full list of connectors and each connector's reference information, such as actions, any triggers, and limits, you can find the full list under the [Connectors overview](https://docs.microsoft.com/connectors).</span></span>

* <span data-ttu-id="2ddb8-109">[**Built-ins**](#built-ins): These built-in actions and triggers help you create logic apps that run on custom schedules, communicate with other endpoints, receive and respond to requests, and call Azure functions, Azure API Apps (Web Apps), your own APIs managed and published with Azure API Management, and nested logic apps that can receive requests.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-109">[**Built-ins**](#built-ins): These built-in actions and triggers help you create logic apps that run on custom schedules, communicate with other endpoints, receive and respond to requests, and call Azure functions, Azure API Apps (Web Apps), your own APIs managed and published with Azure API Management, and nested logic apps that can receive requests.</span></span> <span data-ttu-id="2ddb8-110">You can also use built-in actions that help you organize and control your logic app's workflow, and also work with data.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-110">You can also use built-in actions that help you organize and control your logic app's workflow, and also work with data.</span></span>

* <span data-ttu-id="2ddb8-111">**Managed connectors**: These connectors provide triggers and actions for accessing other services and systems.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-111">**Managed connectors**: These connectors provide triggers and actions for accessing other services and systems.</span></span> <span data-ttu-id="2ddb8-112">Some connectors require that you first create connections that are managed by Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-112">Some connectors require that you first create connections that are managed by Azure Logic Apps.</span></span> <span data-ttu-id="2ddb8-113">Managed connectors are organized into these groups:</span><span class="sxs-lookup"><span data-stu-id="2ddb8-113">Managed connectors are organized into these groups:</span></span>

  |   |   |
  |---|---|
  | [<span data-ttu-id="2ddb8-114">**Managed API connectors**</span><span class="sxs-lookup"><span data-stu-id="2ddb8-114">**Managed API connectors**</span></span>](#managed-api-connectors) | <span data-ttu-id="2ddb8-115">Create logic apps that use services such as Azure Blob Storage, Office 365, Dynamics, Power BI, OneDrive, Salesforce, SharePoint Online, and many more.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-115">Create logic apps that use services such as Azure Blob Storage, Office 365, Dynamics, Power BI, OneDrive, Salesforce, SharePoint Online, and many more.</span></span> | 
  | [<span data-ttu-id="2ddb8-116">**On-premises connectors**</span><span class="sxs-lookup"><span data-stu-id="2ddb8-116">**On-premises connectors**</span></span>](#on-premises-connectors) | <span data-ttu-id="2ddb8-117">After you install and set up the [on-premises data gateway][gateway-doc], these connectors help your logic apps access on-premises systems such as SQL Server, SharePoint Server, Oracle DB, file shares, and others.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-117">After you install and set up the [on-premises data gateway][gateway-doc], these connectors help your logic apps access on-premises systems such as SQL Server, SharePoint Server, Oracle DB, file shares, and others.</span></span> | 
  | [<span data-ttu-id="2ddb8-118">**Integration account connectors**</span><span class="sxs-lookup"><span data-stu-id="2ddb8-118">**Integration account connectors**</span></span>](#integration-account-connectors) | <span data-ttu-id="2ddb8-119">Available when you create and pay for an integration account, these connectors transform and validate XML, encode and decode flat files, and process business-to-business (B2B) messages with AS2, EDIFACT, and X12 protocols.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-119">Available when you create and pay for an integration account, these connectors transform and validate XML, encode and decode flat files, and process business-to-business (B2B) messages with AS2, EDIFACT, and X12 protocols.</span></span> | 
  | [<span data-ttu-id="2ddb8-120">**Enterprise connectors**</span><span class="sxs-lookup"><span data-stu-id="2ddb8-120">**Enterprise connectors**</span></span>](#enterprise-connectors) | <span data-ttu-id="2ddb8-121">Provide access to enterprise systems such as SAP and IBM MQ for an additional cost.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-121">Provide access to enterprise systems such as SAP and IBM MQ for an additional cost.</span></span> |
  ||| 

  <span data-ttu-id="2ddb8-122">For example, if you're using Microsoft BizTalk Server, your logic apps can connect to and communicate with your BizTalk Server by using the [BizTalk Server connector](#on-premises-connectors).</span><span class="sxs-lookup"><span data-stu-id="2ddb8-122">For example, if you're using Microsoft BizTalk Server, your logic apps can connect to and communicate with your BizTalk Server by using the [BizTalk Server connector](#on-premises-connectors).</span></span> 
  <span data-ttu-id="2ddb8-123">You can then extend or perform BizTalk-like operations in your logic apps by using the [integration account connectors](#integration-account-connectors).</span><span class="sxs-lookup"><span data-stu-id="2ddb8-123">You can then extend or perform BizTalk-like operations in your logic apps by using the [integration account connectors](#integration-account-connectors).</span></span> 

> [!NOTE] 
> <span data-ttu-id="2ddb8-124">For the full list of connectors and each connector's reference information, such as actions and any triggers, which are defined by a Swagger description, plus any limits, you can find the full list under the [Connectors overview](/connectors/).</span><span class="sxs-lookup"><span data-stu-id="2ddb8-124">For the full list of connectors and each connector's reference information, such as actions and any triggers, which are defined by a Swagger description, plus any limits, you can find the full list under the [Connectors overview](/connectors/).</span></span> <span data-ttu-id="2ddb8-125">For pricing information, see [Logic Apps pricing details](https://azure.microsoft.com/pricing/details/logic-apps/) and the [Logic Apps pricing model](../logic-apps/logic-apps-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="2ddb8-125">For pricing information, see [Logic Apps pricing details](https://azure.microsoft.com/pricing/details/logic-apps/) and the [Logic Apps pricing model](../logic-apps/logic-apps-pricing.md).</span></span> 

<a name="built-ins"></a>

## <a name="built-ins"></a><span data-ttu-id="2ddb8-126">Built-ins</span><span class="sxs-lookup"><span data-stu-id="2ddb8-126">Built-ins</span></span>

<span data-ttu-id="2ddb8-127">Logic Apps provides built-in triggers and actions so you can create schedule-based workflows, help your logic apps communicate with other apps and services, control the workflow through your logic apps, and manage or manipulate data.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-127">Logic Apps provides built-in triggers and actions so you can create schedule-based workflows, help your logic apps communicate with other apps and services, control the workflow through your logic apps, and manage or manipulate data.</span></span> 

|   |   |   |   | 
|---|---|---|---| 
| <span data-ttu-id="2ddb8-128">[![API icon][schedule-icon]<br/>**Schedule**][recurrence-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-128">[![API icon][schedule-icon]<br/>**Schedule**][recurrence-doc]</span></span> | <span data-ttu-id="2ddb8-129">- Run your logic app on a specified schedule, ranging from basic to complex recurrences, with the **Recurrence** trigger.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-129">- Run your logic app on a specified schedule, ranging from basic to complex recurrences, with the **Recurrence** trigger.</span></span> <p><span data-ttu-id="2ddb8-130">- Pause your logic app for a specified duration with the **Delay** action.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-130">- Pause your logic app for a specified duration with the **Delay** action.</span></span> <p><span data-ttu-id="2ddb8-131">- Pause your logic app until the specified date and time with the **Delay until** action.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-131">- Pause your logic app until the specified date and time with the **Delay until** action.</span></span> | <span data-ttu-id="2ddb8-132">[![API icon][http-icon]<br/>**HTTP**][http-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-132">[![API icon][http-icon]<br/>**HTTP**][http-doc]</span></span> | <span data-ttu-id="2ddb8-133">Communicate with any endpoint over HTTP with both triggers and actions for HTTP, HTTP + Swagger, and HTTP + Webhook.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-133">Communicate with any endpoint over HTTP with both triggers and actions for HTTP, HTTP + Swagger, and HTTP + Webhook.</span></span> | 
| <span data-ttu-id="2ddb8-134">[![API icon][http-request-icon]<br/>**Request**][http-request-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-134">[![API icon][http-request-icon]<br/>**Request**][http-request-doc]</span></span> | <span data-ttu-id="2ddb8-135">- Make your logic app callable from other apps or services, trigger on Event Grid resource events, or trigger on responses to Azure Security Center alerts with the **Request** trigger.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-135">- Make your logic app callable from other apps or services, trigger on Event Grid resource events, or trigger on responses to Azure Security Center alerts with the **Request** trigger.</span></span> <p><span data-ttu-id="2ddb8-136">- Send responses to an app or service with the **Response** action.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-136">- Send responses to an app or service with the **Response** action.</span></span> | <span data-ttu-id="2ddb8-137">[![API icon][batch-icon]<br/>**Batch**][batch-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-137">[![API icon][batch-icon]<br/>**Batch**][batch-doc]</span></span> | <span data-ttu-id="2ddb8-138">- Process messages in batches with the **Batch messages** trigger.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-138">- Process messages in batches with the **Batch messages** trigger.</span></span> <p><span data-ttu-id="2ddb8-139">- Call logic apps that have existing batch triggers with the **Send messages to batch** action.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-139">- Call logic apps that have existing batch triggers with the **Send messages to batch** action.</span></span> | 
| <span data-ttu-id="2ddb8-140">[![API icon][azure-functions-icon]<br/>**Azure Functions**][azure-functions-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-140">[![API icon][azure-functions-icon]<br/>**Azure Functions**][azure-functions-doc]</span></span> | <span data-ttu-id="2ddb8-141">Call Azure functions that run custom code snippets (C# or Node.js) from your logic apps.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-141">Call Azure functions that run custom code snippets (C# or Node.js) from your logic apps.</span></span> | <span data-ttu-id="2ddb8-142">[![API icon][azure-api-management-icon]</br>**Azure API Management**][azure-api-management-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-142">[![API icon][azure-api-management-icon]</br>**Azure API Management**][azure-api-management-doc]</span></span> | <span data-ttu-id="2ddb8-143">Call triggers and actions defined by your own APIs that you manage and publish with Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-143">Call triggers and actions defined by your own APIs that you manage and publish with Azure API Management.</span></span> | 
| <span data-ttu-id="2ddb8-144">[![API icon][azure-app-services-icon]<br/>**Azure App Services**][azure-app-services-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-144">[![API icon][azure-app-services-icon]<br/>**Azure App Services**][azure-app-services-doc]</span></span> | <span data-ttu-id="2ddb8-145">Call Azure API Apps, or Web Apps, hosted on Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-145">Call Azure API Apps, or Web Apps, hosted on Azure App Service.</span></span> <span data-ttu-id="2ddb8-146">The triggers and actions defined by these apps appear like any other first-class triggers and actions when Swagger is included.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-146">The triggers and actions defined by these apps appear like any other first-class triggers and actions when Swagger is included.</span></span> | <span data-ttu-id="2ddb8-147">[![API icon][azure-logic-apps-icon]<br/>**Azure<br/>Logic Apps**][nested-logic-app-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-147">[![API icon][azure-logic-apps-icon]<br/>**Azure<br/>Logic Apps**][nested-logic-app-doc]</span></span> | <span data-ttu-id="2ddb8-148">Call other logic apps that start with a Request trigger.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-148">Call other logic apps that start with a Request trigger.</span></span> | 
||||| 

### <a name="control-workflow"></a><span data-ttu-id="2ddb8-149">Control workflow</span><span class="sxs-lookup"><span data-stu-id="2ddb8-149">Control workflow</span></span>

<span data-ttu-id="2ddb8-150">Here are built-in actions for structuring and controlling the actions in your logic app's workflow:</span><span class="sxs-lookup"><span data-stu-id="2ddb8-150">Here are built-in actions for structuring and controlling the actions in your logic app's workflow:</span></span>

|   |   |   |   | 
|---|---|---|---| 
| <span data-ttu-id="2ddb8-151">[![Built-in Icon][condition-icon]<br/>**Condition**][condition-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-151">[![Built-in Icon][condition-icon]<br/>**Condition**][condition-doc]</span></span> | <span data-ttu-id="2ddb8-152">Evaluate a condition and run different actions based on whether the condition is true or false.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-152">Evaluate a condition and run different actions based on whether the condition is true or false.</span></span> | <span data-ttu-id="2ddb8-153">[![Built-in Icon][for-each-icon]</br>**For each**][for-each-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-153">[![Built-in Icon][for-each-icon]</br>**For each**][for-each-doc]</span></span> | <span data-ttu-id="2ddb8-154">Perform the same actions on every item in an array.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-154">Perform the same actions on every item in an array.</span></span> | 
| <span data-ttu-id="2ddb8-155">[![Built-in Icon][scope-icon]<br/>**Scope**][scope-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-155">[![Built-in Icon][scope-icon]<br/>**Scope**][scope-doc]</span></span> | <span data-ttu-id="2ddb8-156">Group actions into *scopes*, which get their own status after the actions in the scope finish running.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-156">Group actions into *scopes*, which get their own status after the actions in the scope finish running.</span></span> | <span data-ttu-id="2ddb8-157">[![Built-in Icon][switch-icon]</br>**Switch**][switch-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-157">[![Built-in Icon][switch-icon]</br>**Switch**][switch-doc]</span></span> | <span data-ttu-id="2ddb8-158">Group actions into *cases*, which are assigned unique values except for the default case.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-158">Group actions into *cases*, which are assigned unique values except for the default case.</span></span> <span data-ttu-id="2ddb8-159">Run only that case whose assigned value matches the result from an expression, object, or token.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-159">Run only that case whose assigned value matches the result from an expression, object, or token.</span></span> <span data-ttu-id="2ddb8-160">If no matches exist, run the default case.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-160">If no matches exist, run the default case.</span></span> | 
| <span data-ttu-id="2ddb8-161">[![Built-in Icon][terminate-icon]<br/>**Terminate**][terminate-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-161">[![Built-in Icon][terminate-icon]<br/>**Terminate**][terminate-doc]</span></span> | <span data-ttu-id="2ddb8-162">Stop an actively running logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-162">Stop an actively running logic app workflow.</span></span> | <span data-ttu-id="2ddb8-163">[![Built-in Icon][until-icon]<br/>**Until**][until-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-163">[![Built-in Icon][until-icon]<br/>**Until**][until-doc]</span></span> | <span data-ttu-id="2ddb8-164">Repeat actions until the specified condition is true or some state has changed.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-164">Repeat actions until the specified condition is true or some state has changed.</span></span> | 
||||| 

### <a name="manage-or-manipulate-data"></a><span data-ttu-id="2ddb8-165">Manage or manipulate data</span><span class="sxs-lookup"><span data-stu-id="2ddb8-165">Manage or manipulate data</span></span>

<span data-ttu-id="2ddb8-166">Here are built-in actions for working with data outputs and their formats:</span><span class="sxs-lookup"><span data-stu-id="2ddb8-166">Here are built-in actions for working with data outputs and their formats:</span></span>  

|   |   | 
|---|---| 
| <span data-ttu-id="2ddb8-167">![Built-in Icon][data-operations-icon]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-167">![Built-in Icon][data-operations-icon]</span></span><br/><span data-ttu-id="2ddb8-168">**Data Operations**</span><span class="sxs-lookup"><span data-stu-id="2ddb8-168">**Data Operations**</span></span> | <span data-ttu-id="2ddb8-169">Perform operations with data:</span><span class="sxs-lookup"><span data-stu-id="2ddb8-169">Perform operations with data:</span></span> <p><span data-ttu-id="2ddb8-170">- **Compose**: Create a single output from multiple inputs with various types.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-170">- **Compose**: Create a single output from multiple inputs with various types.</span></span> <br><span data-ttu-id="2ddb8-171">- **Create CSV table**: Create a comma-separated-value (CSV) table from an array with JSON objects.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-171">- **Create CSV table**: Create a comma-separated-value (CSV) table from an array with JSON objects.</span></span> <br><span data-ttu-id="2ddb8-172">- **Create HTML table**: Create an HTML table from an array with JSON objects.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-172">- **Create HTML table**: Create an HTML table from an array with JSON objects.</span></span> <br><span data-ttu-id="2ddb8-173">- **Filter array**: Create an array from items in another array that meet your criteria.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-173">- **Filter array**: Create an array from items in another array that meet your criteria.</span></span> <br><span data-ttu-id="2ddb8-174">- **Join**: Create a string from all items in an array and separate those items with the specified delimiter.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-174">- **Join**: Create a string from all items in an array and separate those items with the specified delimiter.</span></span> <br><span data-ttu-id="2ddb8-175">- **Parse JSON**: Create user-friendly tokens from properties and their values in JSON content so you can use those properties in your workflow.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-175">- **Parse JSON**: Create user-friendly tokens from properties and their values in JSON content so you can use those properties in your workflow.</span></span> <br><span data-ttu-id="2ddb8-176">- **Select**: Create an array with JSON objects by transforming items or values in another array and mapping those items to specified properties.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-176">- **Select**: Create an array with JSON objects by transforming items or values in another array and mapping those items to specified properties.</span></span> | 
| <span data-ttu-id="2ddb8-177">![Built-in Icon][date-time-icon]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-177">![Built-in Icon][date-time-icon]</span></span><br/><span data-ttu-id="2ddb8-178">**Date Time**</span><span class="sxs-lookup"><span data-stu-id="2ddb8-178">**Date Time**</span></span> | <span data-ttu-id="2ddb8-179">Perform operations with timestamps:</span><span class="sxs-lookup"><span data-stu-id="2ddb8-179">Perform operations with timestamps:</span></span> <p><span data-ttu-id="2ddb8-180">- **Add to time**: Add the specified number of units to a timestamp.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-180">- **Add to time**: Add the specified number of units to a timestamp.</span></span> <br><span data-ttu-id="2ddb8-181">- **Convert time zone**: Convert a timestamp from the source time zone to the target time zone.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-181">- **Convert time zone**: Convert a timestamp from the source time zone to the target time zone.</span></span> <br><span data-ttu-id="2ddb8-182">- **Current time**: Return the current timestamp as a string.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-182">- **Current time**: Return the current timestamp as a string.</span></span> <br><span data-ttu-id="2ddb8-183">- **Get future time**: Return the current timestamp plus the specified time units.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-183">- **Get future time**: Return the current timestamp plus the specified time units.</span></span> <br><span data-ttu-id="2ddb8-184">- **Get past time**: Return the current timestamp minus the specified time units.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-184">- **Get past time**: Return the current timestamp minus the specified time units.</span></span> <br><span data-ttu-id="2ddb8-185">- **Subtract from time**: Subtract a number of time units from a timestamp.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-185">- **Subtract from time**: Subtract a number of time units from a timestamp.</span></span> |
| <span data-ttu-id="2ddb8-186">[![Built-in Icon][variables-icon]<br/>**Variables**][variables-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-186">[![Built-in Icon][variables-icon]<br/>**Variables**][variables-doc]</span></span> | <span data-ttu-id="2ddb8-187">Perform operations with variables:</span><span class="sxs-lookup"><span data-stu-id="2ddb8-187">Perform operations with variables:</span></span> <p><span data-ttu-id="2ddb8-188">- **Append to array variable**: Insert a value as the last item in an array stored by a variable.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-188">- **Append to array variable**: Insert a value as the last item in an array stored by a variable.</span></span> <br><span data-ttu-id="2ddb8-189">- **Append to string variable**: Insert a value as the last character in a string stored by a variable.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-189">- **Append to string variable**: Insert a value as the last character in a string stored by a variable.</span></span> <br><span data-ttu-id="2ddb8-190">- **Decrement variable**: Decrease a variable by a constant value.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-190">- **Decrement variable**: Decrease a variable by a constant value.</span></span> <br><span data-ttu-id="2ddb8-191">- **Increment variable**: Increase a variable by a constant value.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-191">- **Increment variable**: Increase a variable by a constant value.</span></span> <br><span data-ttu-id="2ddb8-192">- **Initialize variable**: Create a variable and declare its data type and initial value.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-192">- **Initialize variable**: Create a variable and declare its data type and initial value.</span></span> <br><span data-ttu-id="2ddb8-193">- **Set variable**: Assign a different value to an existing variable.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-193">- **Set variable**: Assign a different value to an existing variable.</span></span> |
|  |  | 

<a name="managed-api-connectors"></a>

## <a name="managed-api-connectors"></a><span data-ttu-id="2ddb8-194">Managed API connectors</span><span class="sxs-lookup"><span data-stu-id="2ddb8-194">Managed API connectors</span></span>

<span data-ttu-id="2ddb8-195">Here are the more popular connectors for automating tasks, processes, and workflows with these services or systems:</span><span class="sxs-lookup"><span data-stu-id="2ddb8-195">Here are the more popular connectors for automating tasks, processes, and workflows with these services or systems:</span></span>

|   |   |   |   | 
|---|---|---|---| 
| <span data-ttu-id="2ddb8-196">[![API icon][azure-service-bus-icon]<br/>**Azure Service Bus**][azure-service-bus-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-196">[![API icon][azure-service-bus-icon]<br/>**Azure Service Bus**][azure-service-bus-doc]</span></span> | <span data-ttu-id="2ddb8-197">Manage asynchronous messages, sessions, and topic subscriptions with the most commonly used connector in Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-197">Manage asynchronous messages, sessions, and topic subscriptions with the most commonly used connector in Logic Apps.</span></span> | <span data-ttu-id="2ddb8-198">[![API icon][sql-server-icon]<br/>**SQL Server**][sql-server-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-198">[![API icon][sql-server-icon]<br/>**SQL Server**][sql-server-doc]</span></span> | <span data-ttu-id="2ddb8-199">Connect to your SQL Server on premises or an Azure SQL Database in the cloud so you can manage records, run stored procedures, or perform queries.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-199">Connect to your SQL Server on premises or an Azure SQL Database in the cloud so you can manage records, run stored procedures, or perform queries.</span></span> | 
| <span data-ttu-id="2ddb8-200">[![API icon][office-365-outlook-icon]<br/>**Office 365<br/>Outlook**][office-365-outlook-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-200">[![API icon][office-365-outlook-icon]<br/>**Office 365<br/>Outlook**][office-365-outlook-doc]</span></span> | <span data-ttu-id="2ddb8-201">Connect to your Office 365 email account so you can create and manage emails, tasks, calendar events and meetings, contacts, requests, and more.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-201">Connect to your Office 365 email account so you can create and manage emails, tasks, calendar events and meetings, contacts, requests, and more.</span></span> | <span data-ttu-id="2ddb8-202">[![API icon][azure-blob-storage-icon]<br/>**Azure Blob<br/>Storage**][azure-blob-storage-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-202">[![API icon][azure-blob-storage-icon]<br/>**Azure Blob<br/>Storage**][azure-blob-storage-doc]</span></span> | <span data-ttu-id="2ddb8-203">Connect to your storage account so you can create and manage blob content.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-203">Connect to your storage account so you can create and manage blob content.</span></span> | 
| <span data-ttu-id="2ddb8-204">[![API icon][sftp-icon]<br/>**SFTP**][sftp-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-204">[![API icon][sftp-icon]<br/>**SFTP**][sftp-doc]</span></span> | <span data-ttu-id="2ddb8-205">Connect to SFTP servers you can access from the internet so you can work with your files and folders.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-205">Connect to SFTP servers you can access from the internet so you can work with your files and folders.</span></span> | <span data-ttu-id="2ddb8-206">[![API icon][sharepoint-online-icon]<br/>**SharePoint<br/>Online**][sharepoint-online-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-206">[![API icon][sharepoint-online-icon]<br/>**SharePoint<br/>Online**][sharepoint-online-doc]</span></span> | <span data-ttu-id="2ddb8-207">Connect to SharePoint Online so you can manage files, attachments, folders, and more.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-207">Connect to SharePoint Online so you can manage files, attachments, folders, and more.</span></span> | 
| <span data-ttu-id="2ddb8-208">[![API icon][dynamics-365-icon]<br/>**Dynamics 365<br/>CRM Online**][dynamics-365-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-208">[![API icon][dynamics-365-icon]<br/>**Dynamics 365<br/>CRM Online**][dynamics-365-doc]</span></span> | <span data-ttu-id="2ddb8-209">Connect to your Dynamics 365 account so you can create and manage records, items, and more.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-209">Connect to your Dynamics 365 account so you can create and manage records, items, and more.</span></span> | <span data-ttu-id="2ddb8-210">[![API icon][ftp-icon]<br/>**FTP**][ftp-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-210">[![API icon][ftp-icon]<br/>**FTP**][ftp-doc]</span></span> | <span data-ttu-id="2ddb8-211">Connect to FTP servers you can access from the internet so you can work with your files and folders.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-211">Connect to FTP servers you can access from the internet so you can work with your files and folders.</span></span> | 
| <span data-ttu-id="2ddb8-212">[![API icon][salesforce-icon]<br/>**Salesforce**][salesforce-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-212">[![API icon][salesforce-icon]<br/>**Salesforce**][salesforce-doc]</span></span> | <span data-ttu-id="2ddb8-213">Connect to your Salesforce account so you can create and manage items such as records, jobs, objects, and more.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-213">Connect to your Salesforce account so you can create and manage items such as records, jobs, objects, and more.</span></span> | <span data-ttu-id="2ddb8-214">[![API icon][twitter-icon]<br/>**Twitter**][twitter-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-214">[![API icon][twitter-icon]<br/>**Twitter**][twitter-doc]</span></span> | <span data-ttu-id="2ddb8-215">Connect to your Twitter account so you can manage tweets, followers, your timeline, and more.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-215">Connect to your Twitter account so you can manage tweets, followers, your timeline, and more.</span></span> <span data-ttu-id="2ddb8-216">Save your tweets to SQL, Excel, or SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-216">Save your tweets to SQL, Excel, or SharePoint.</span></span> | 
| <span data-ttu-id="2ddb8-217">[![API icon][azure-event-hubs-icon]<br/>**Azure Event Hubs**][azure-event-hubs-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-217">[![API icon][azure-event-hubs-icon]<br/>**Azure Event Hubs**][azure-event-hubs-doc]</span></span> | <span data-ttu-id="2ddb8-218">Consume and publish events through an Event Hub.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-218">Consume and publish events through an Event Hub.</span></span> <span data-ttu-id="2ddb8-219">For example, get output from your logic app with Event Hubs, and then send that output to a real-time analytics provider.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-219">For example, get output from your logic app with Event Hubs, and then send that output to a real-time analytics provider.</span></span> | <span data-ttu-id="2ddb8-220">[![API icon][azure-event-grid-icon]<br/>**Azure Event**</br>**Grid**][azure-event-grid-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-220">[![API icon][azure-event-grid-icon]<br/>**Azure Event**</br>**Grid**][azure-event-grid-doc]</span></span> | <span data-ttu-id="2ddb8-221">Monitor events published by an Event Grid, for example, when Azure resources or third-party resources change.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-221">Monitor events published by an Event Grid, for example, when Azure resources or third-party resources change.</span></span> | 
||||| 

<a name="on-premises-connectors"></a>

## <a name="on-premises-connectors"></a><span data-ttu-id="2ddb8-222">On-premises connectors</span><span class="sxs-lookup"><span data-stu-id="2ddb8-222">On-premises connectors</span></span> 

<span data-ttu-id="2ddb8-223">Here are some commonly used connectors that provide access to data and resources in on-premises systems.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-223">Here are some commonly used connectors that provide access to data and resources in on-premises systems.</span></span> <span data-ttu-id="2ddb8-224">Before you can create a connection to an on-premises system, you must first [download, install, and set up an on-premises data gateway][gateway-doc].</span><span class="sxs-lookup"><span data-stu-id="2ddb8-224">Before you can create a connection to an on-premises system, you must first [download, install, and set up an on-premises data gateway][gateway-doc].</span></span> <span data-ttu-id="2ddb8-225">This gateway provides a secure communication channel without having to set up the necessary network infrastructure.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-225">This gateway provides a secure communication channel without having to set up the necessary network infrastructure.</span></span> 

|   |   |   |   |   | 
|---|---|---|---|---| 
| <span data-ttu-id="2ddb8-226">![API icon][biztalk-server-icon]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-226">![API icon][biztalk-server-icon]</span></span><br/><span data-ttu-id="2ddb8-227">**BizTalk**</span><span class="sxs-lookup"><span data-stu-id="2ddb8-227">**BizTalk**</span></span></br> <span data-ttu-id="2ddb8-228">**Server**</span><span class="sxs-lookup"><span data-stu-id="2ddb8-228">**Server**</span></span> | <span data-ttu-id="2ddb8-229">[![API icon][file-system-icon]<br/>**File</br> System**][file-system-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-229">[![API icon][file-system-icon]<br/>**File</br> System**][file-system-doc]</span></span> | <span data-ttu-id="2ddb8-230">[![API icon][ibm-db2-icon]<br/>**IBM DB2**][ibm-db2-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-230">[![API icon][ibm-db2-icon]<br/>**IBM DB2**][ibm-db2-doc]</span></span> | <span data-ttu-id="2ddb8-231">[![API icon][ibm-informix-icon]<br/>**IBM**</br> **Informix**][ibm-informix-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-231">[![API icon][ibm-informix-icon]<br/>**IBM**</br> **Informix**][ibm-informix-doc]</span></span> | <span data-ttu-id="2ddb8-232">![API icon][mysql-icon]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-232">![API icon][mysql-icon]</span></span><br/><span data-ttu-id="2ddb8-233">**MySQL**</span><span class="sxs-lookup"><span data-stu-id="2ddb8-233">**MySQL**</span></span> | 
| <span data-ttu-id="2ddb8-234">[![API icon][oracle-db-icon]<br/>**Oracle DB**][oracle-db-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-234">[![API icon][oracle-db-icon]<br/>**Oracle DB**][oracle-db-doc]</span></span> | <span data-ttu-id="2ddb8-235">![API icon][postgre-sql-icon]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-235">![API icon][postgre-sql-icon]</span></span><br/><span data-ttu-id="2ddb8-236">**PostgreSQL**</span><span class="sxs-lookup"><span data-stu-id="2ddb8-236">**PostgreSQL**</span></span> | <span data-ttu-id="2ddb8-237">[![API icon][sharepoint-server-icon]<br/>**SharePoint</br> Server**][sharepoint-server-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-237">[![API icon][sharepoint-server-icon]<br/>**SharePoint</br> Server**][sharepoint-server-doc]</span></span> | <span data-ttu-id="2ddb8-238">[![API icon][sql-server-icon]<br/>**SQL</br> Server**][sql-server-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-238">[![API icon][sql-server-icon]<br/>**SQL</br> Server**][sql-server-doc]</span></span> | <span data-ttu-id="2ddb8-239">![API icon][teradata-icon]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-239">![API icon][teradata-icon]</span></span><br/><span data-ttu-id="2ddb8-240">**Teradata**</span><span class="sxs-lookup"><span data-stu-id="2ddb8-240">**Teradata**</span></span> | 
||||| 

<a name="integration-account-connectors"></a>

## <a name="integration-account-connectors"></a><span data-ttu-id="2ddb8-241">Integration account connectors</span><span class="sxs-lookup"><span data-stu-id="2ddb8-241">Integration account connectors</span></span> 

<span data-ttu-id="2ddb8-242">Here are connectors for building business-to-business (B2B) solutions with your logic apps when you create and pay for an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md), which is available through the Enterprise Integration Pack (EIP) in Azure.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-242">Here are connectors for building business-to-business (B2B) solutions with your logic apps when you create and pay for an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md), which is available through the Enterprise Integration Pack (EIP) in Azure.</span></span> <span data-ttu-id="2ddb8-243">With this account, you can create and store B2B artifacts such as trading partners, agreements, maps, schemas, certificates, and so on.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-243">With this account, you can create and store B2B artifacts such as trading partners, agreements, maps, schemas, certificates, and so on.</span></span> <span data-ttu-id="2ddb8-244">To use these artifacts, associate your logic apps with your integration account.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-244">To use these artifacts, associate your logic apps with your integration account.</span></span> <span data-ttu-id="2ddb8-245">If you currently use BizTalk Server, these connectors might seem familiar already.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-245">If you currently use BizTalk Server, these connectors might seem familiar already.</span></span>

|   |   |   |   | 
|---|---|---|---| 
| <span data-ttu-id="2ddb8-246">[![API icon][as2-icon]<br/>**AS2</br> decoding**][as2-decode-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-246">[![API icon][as2-icon]<br/>**AS2</br> decoding**][as2-decode-doc]</span></span> | <span data-ttu-id="2ddb8-247">[![API icon][as2-icon]<br/>**AS2</br> encoding**][as2-encode-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-247">[![API icon][as2-icon]<br/>**AS2</br> encoding**][as2-encode-doc]</span></span> | <span data-ttu-id="2ddb8-248">[![API icon][edifact-icon]<br/>**EDIFACT</br> decoding**][edifact-decode-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-248">[![API icon][edifact-icon]<br/>**EDIFACT</br> decoding**][edifact-decode-doc]</span></span> | <span data-ttu-id="2ddb8-249">[![API icon][edifact-icon]<br/>**EDIFACT</br> encoding**][edifact-encode-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-249">[![API icon][edifact-icon]<br/>**EDIFACT</br> encoding**][edifact-encode-doc]</span></span> | 
| <span data-ttu-id="2ddb8-250">[![API icon][flat-file-decode-icon]<br/>**Flat file</br> decoding**][flat-file-decode-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-250">[![API icon][flat-file-decode-icon]<br/>**Flat file</br> decoding**][flat-file-decode-doc]</span></span> | <span data-ttu-id="2ddb8-251">[![API icon][flat-file-encode-icon]<br/>**Flat file</br> encoding**][flat-file-encode-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-251">[![API icon][flat-file-encode-icon]<br/>**Flat file</br> encoding**][flat-file-encode-doc]</span></span> | <span data-ttu-id="2ddb8-252">[![API icon][integration-account-icon]<br/>**Integration<br/>account**][integration-account-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-252">[![API icon][integration-account-icon]<br/>**Integration<br/>account**][integration-account-doc]</span></span> | <span data-ttu-id="2ddb8-253">[![API icon][liquid-icon]<br/>**Liquid**</br>**transforms**][json-liquid-transform-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-253">[![API icon][liquid-icon]<br/>**Liquid**</br>**transforms**][json-liquid-transform-doc]</span></span> | 
| <span data-ttu-id="2ddb8-254">[![API icon][x12-icon]<br/>**X12</br> decoding**][x12-decode-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-254">[![API icon][x12-icon]<br/>**X12</br> decoding**][x12-decode-doc]</span></span> | <span data-ttu-id="2ddb8-255">[![API icon][x12-icon]<br/>**X12</br> encoding**][x12-encode-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-255">[![API icon][x12-icon]<br/>**X12</br> encoding**][x12-encode-doc]</span></span> | <span data-ttu-id="2ddb8-256">[![API icon][xml-transform-icon]<br/>**XML**</br>**transforms**][xml-transform-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-256">[![API icon][xml-transform-icon]<br/>**XML**</br>**transforms**][xml-transform-doc]</span></span> | <span data-ttu-id="2ddb8-257">[![API icon][xml-validate-icon]<br/>**XML <br/>validation**][xml-validate-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-257">[![API icon][xml-validate-icon]<br/>**XML <br/>validation**][xml-validate-doc]</span></span> |  
||||| 

<a name="enterprise-connectors"></a>

## <a name="enterprise-connectors"></a><span data-ttu-id="2ddb8-258">Enterprise connectors</span><span class="sxs-lookup"><span data-stu-id="2ddb8-258">Enterprise connectors</span></span>

<span data-ttu-id="2ddb8-259">Your logic apps can access enterprise systems, such as SAP and IBM MQ:</span><span class="sxs-lookup"><span data-stu-id="2ddb8-259">Your logic apps can access enterprise systems, such as SAP and IBM MQ:</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="2ddb8-260">[![API icon][ibm-mq-icon]<br/>**IBM MQ**][ibm-mq-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-260">[![API icon][ibm-mq-icon]<br/>**IBM MQ**][ibm-mq-doc]</span></span> | <span data-ttu-id="2ddb8-261">[![API icon][sap-icon]<br/>**SAP**][sap-connector-doc]</span><span class="sxs-lookup"><span data-stu-id="2ddb8-261">[![API icon][sap-icon]<br/>**SAP**][sap-connector-doc]</span></span> |
||| 

## <a name="more-about-triggers-and-actions"></a><span data-ttu-id="2ddb8-262">More about triggers and actions</span><span class="sxs-lookup"><span data-stu-id="2ddb8-262">More about triggers and actions</span></span>

<span data-ttu-id="2ddb8-263">Some connectors provide *triggers* that notify your logic app when specific events happen.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-263">Some connectors provide *triggers* that notify your logic app when specific events happen.</span></span> <span data-ttu-id="2ddb8-264">So when these events happen, the trigger creates and runs an instance of your logic app.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-264">So when these events happen, the trigger creates and runs an instance of your logic app.</span></span> <span data-ttu-id="2ddb8-265">For example, the FTP connector provides a "When a file is added or modified" trigger that starts your logic app when a file gets updated.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-265">For example, the FTP connector provides a "When a file is added or modified" trigger that starts your logic app when a file gets updated.</span></span> 

<span data-ttu-id="2ddb8-266">Logic Apps provides these kinds of triggers:</span><span class="sxs-lookup"><span data-stu-id="2ddb8-266">Logic Apps provides these kinds of triggers:</span></span>  

* <span data-ttu-id="2ddb8-267">*Polling triggers*: These triggers poll your service at a specified frequency and checks for new data.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-267">*Polling triggers*: These triggers poll your service at a specified frequency and checks for new data.</span></span> 

  <span data-ttu-id="2ddb8-268">When new data is available, a new instance of your logic app gets created and runs with the data that's passed in as input.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-268">When new data is available, a new instance of your logic app gets created and runs with the data that's passed in as input.</span></span> 

* <span data-ttu-id="2ddb8-269">*Push triggers*: These triggers listen for new data at an endpoint or for an event to happen, which creates and runs new instance of your logic app.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-269">*Push triggers*: These triggers listen for new data at an endpoint or for an event to happen, which creates and runs new instance of your logic app.</span></span>

* <span data-ttu-id="2ddb8-270">*Recurrence trigger*: This trigger creates and runs an instance of your logic app based on a specified schedule.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-270">*Recurrence trigger*: This trigger creates and runs an instance of your logic app based on a specified schedule.</span></span>

<span data-ttu-id="2ddb8-271">Connectors also provide *actions* that perform tasks in your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-271">Connectors also provide *actions* that perform tasks in your logic app's workflow.</span></span> <span data-ttu-id="2ddb8-272">For example, your logic app can read data and use this data in later steps of your logic app.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-272">For example, your logic app can read data and use this data in later steps of your logic app.</span></span> <span data-ttu-id="2ddb8-273">More specifically, your logic app can find customer data from a SQL database, and process this data later in your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-273">More specifically, your logic app can find customer data from a SQL database, and process this data later in your logic app's workflow.</span></span> 

<span data-ttu-id="2ddb8-274">For more about triggers and actions, see the [Connectors overview](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ddb8-274">For more about triggers and actions, see the [Connectors overview](connectors-overview.md).</span></span> 

## <a name="custom-apis-and-connectors"></a><span data-ttu-id="2ddb8-275">Custom APIs and connectors</span><span class="sxs-lookup"><span data-stu-id="2ddb8-275">Custom APIs and connectors</span></span> 

<span data-ttu-id="2ddb8-276">To call APIs that run custom code or aren't available as connectors, you can extend the Logic Apps platform by [creating custom API Apps](../logic-apps/logic-apps-create-api-app.md).</span><span class="sxs-lookup"><span data-stu-id="2ddb8-276">To call APIs that run custom code or aren't available as connectors, you can extend the Logic Apps platform by [creating custom API Apps](../logic-apps/logic-apps-create-api-app.md).</span></span> <span data-ttu-id="2ddb8-277">You can also [create custom connectors](../logic-apps/custom-connector-overview.md) for *any* REST or SOAP-based APIs, which make those APIs available to any logic app in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-277">You can also [create custom connectors](../logic-apps/custom-connector-overview.md) for *any* REST or SOAP-based APIs, which make those APIs available to any logic app in your Azure subscription.</span></span>
<span data-ttu-id="2ddb8-278">To make custom API Apps or connectors public for anyone to use in Azure, you can [submit connectors for Microsoft certification](../logic-apps/custom-connector-submit-certification.md).</span><span class="sxs-lookup"><span data-stu-id="2ddb8-278">To make custom API Apps or connectors public for anyone to use in Azure, you can [submit connectors for Microsoft certification](../logic-apps/custom-connector-submit-certification.md).</span></span>

## <a name="get-support"></a><span data-ttu-id="2ddb8-279">Get support</span><span class="sxs-lookup"><span data-stu-id="2ddb8-279">Get support</span></span>

* <span data-ttu-id="2ddb8-280">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="2ddb8-280">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

* <span data-ttu-id="2ddb8-281">To submit or vote on ideas for Azure Logic Apps and connectors, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="2ddb8-281">To submit or vote on ideas for Azure Logic Apps and connectors, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

* <span data-ttu-id="2ddb8-282">Are the docs missing articles or details you think are important?</span><span class="sxs-lookup"><span data-stu-id="2ddb8-282">Are the docs missing articles or details you think are important?</span></span> <span data-ttu-id="2ddb8-283">If yes, you can help by adding to the existing articles or by writing your own.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-283">If yes, you can help by adding to the existing articles or by writing your own.</span></span> <span data-ttu-id="2ddb8-284">The documentation is open source and hosted on GitHub.</span><span class="sxs-lookup"><span data-stu-id="2ddb8-284">The documentation is open source and hosted on GitHub.</span></span> <span data-ttu-id="2ddb8-285">Get started at the Azure documentation's [GitHub repository](https://github.com/Microsoft/azure-docs).</span><span class="sxs-lookup"><span data-stu-id="2ddb8-285">Get started at the Azure documentation's [GitHub repository](https://github.com/Microsoft/azure-docs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2ddb8-286">Next steps</span><span class="sxs-lookup"><span data-stu-id="2ddb8-286">Next steps</span></span>

* <span data-ttu-id="2ddb8-287">Find the [connectors' full list](https://docs.microsoft.com/connectors)</span><span class="sxs-lookup"><span data-stu-id="2ddb8-287">Find the [connectors' full list](https://docs.microsoft.com/connectors)</span></span>
* [<span data-ttu-id="2ddb8-288">Create your first logic app</span><span class="sxs-lookup"><span data-stu-id="2ddb8-288">Create your first logic app</span></span>](../logic-apps/quickstart-create-first-logic-app-workflow.md)
* [<span data-ttu-id="2ddb8-289">Create custom connectors for logic apps</span><span class="sxs-lookup"><span data-stu-id="2ddb8-289">Create custom connectors for logic apps</span></span>](https://docs.microsoft.com/connectors/custom-connectors/)
* [<span data-ttu-id="2ddb8-290">Create custom APIs for logic apps</span><span class="sxs-lookup"><span data-stu-id="2ddb8-290">Create custom APIs for logic apps</span></span>](../logic-apps/logic-apps-create-api-app.md)

<!--Misc doc links-->
[gateway-doc]: ../logic-apps/logic-apps-gateway-connection.md "Connect to data sources on-premises from logic apps with on-premises data gateway"

<!--Built-ins doc links-->
[azure-functions-doc]: ../logic-apps/logic-apps-azure-functions.md "Integrate logic apps with Azure Functions"
[azure-api-management-doc]: ../api-management/get-started-create-service-instance.md "Create an Azure API Management service instance for managing and publishing your APIs"
[azure-app-services-doc]: ../logic-apps/logic-apps-custom-hosted-api.md "Integrate logic apps with App Service API Apps"
[azure-service-bus-doc]: ./connectors-create-api-servicebus.md "Send messages from Service Bus Queues and Topics and receive messages from Service Bus Queues and Subscriptions"
[batch-doc]: ../logic-apps/logic-apps-batch-process-send-receive-messages.md "Process messages in groups, or as batches"
[condition-doc]: ../logic-apps/logic-apps-control-flow-conditional-statement.md "Evaluate a condition and run different actions based on whether the condition is true or false"
[delay-doc]: ./connectors-native-delay.md "Perform delayed actions"
[for-each-doc]: ../logic-apps/logic-apps-control-flow-loops.md#foreach-loop "Perform the same actions on every item in an array"
[http-doc]: ./connectors-native-http.md "Make HTTP calls with the HTTP connector"
[http-request-doc]: ./connectors-native-reqres.md "Add actions for HTTP requests and responses to your logic apps"
[http-response-doc]: ./connectors-native-reqres.md "Add actions for HTTP requests and responses to your logic apps"
[http-swagger-doc]: ./connectors-native-http-swagger.md "Make HTTP calls with HTTP + Swagger connector"
[http-webook-doc]: ./connectors-native-webhook.md "Add HTTP webhook actions and triggers to your logic apps"
[nested-logic-app-doc]: ../logic-apps/logic-apps-http-endpoint.md "Integrate logic apps with nested workflows"
[query-doc]: ./connectors-native-query.md "Select and filter arrays with the Query action"
[recurrence-doc]:  ./connectors-native-recurrence.md "Trigger recurring actions for logic apps"
[scope-doc]: ../logic-apps/logic-apps-control-flow-run-steps-group-scopes.md "Organize actions into groups, which get their own status after the actions in group finish running" 
[switch-doc]: ../logic-apps/logic-apps-control-flow-switch-statement.md "Organize actions into cases, which are assigned unique values. Run only the case whose value matches the result from an expression, object, or token. If no matches exist, run the default case"
[terminate-doc]: ../logic-apps/logic-apps-workflow-actions-triggers.md#terminate-action "Stop or cancel an actively running workflow for your logic app"
[until-doc]: ../logic-apps/logic-apps-control-flow-loops.md#until-loop "Repeat actions until the specified condition is true or some state has changed"
[variables-doc]: ../logic-apps/logic-apps-create-variables-store-values.md "Perform operations with variables, such as initialize, set, increment, decrement, and append to string or array variable"

<!--Managed API doc links-->
[azure-blob-storage-doc]: ./connectors-create-api-azureblobstorage.md "Manage files in your blob container with Azure blob storage connector"
[azure-event-grid-doc]: ../event-grid/monitor-virtual-machine-changes-event-grid-logic-app.md " Monitor events published by an Event Grid, for example, when Azure resources or third-party resources change"
[azure-event-hubs-doc]: ./connectors-create-api-azure-event-hubs.md "Connect to Azure Event Hubs. Receive and send events between logic apps and Event Hubs"
[box-doc]: ./connectors-create-api-box.md "Connect to Box. Upload, get, delete, list your files, and more"
[dropbox-doc]: ./connectors-create-api-dropbox.md "Connect to Dropbox. Upload, get, delete, list your files, and more"
[dynamics-365-doc]: ./connectors-create-api-crmonline.md "Connect to Dynamics CRM Online so you can work with CRM Online data"
[facebook-doc]: ./connectors-create-api-facebook.md "Connect to Facebook. Post to a timeline, get a page feed, and more"
[file-system-doc]: ../logic-apps/logic-apps-using-file-connector.md "Connect to an on-premises file system"
[ftp-doc]: ./connectors-create-api-ftp.md "Connect to an FTP / FTPS server for FTP tasks, like uploading, getting, deleting files, and more"
[github-doc]: ./connectors-create-api-github.md "Connect to GitHub and track issues"
[google-calendar-doc]: ./connectors-create-api-googlecalendar.md "Connects to Google Calendar and can manage calendar."
[google-drive-doc]: ./connectors-create-api-googledrive.md "Connect to GoogleDrive so you can work with your data"
[google-sheets-doc]: ./connectors-create-api-googlesheet.md "Connect to Google Sheets so you can modify your sheets"
[google-tasks-doc]: ./connectors-create-api-googletasks.md "Connects to Google Tasks so you can manage your tasks"
[ibm-db2-doc]: ./connectors-create-api-db2.md "Connect to IBM DB2 in the cloud or on-premises. Update a row, get a table, and more"
[ibm-informix-doc]: ./connectors-create-api-informix.md "Connect to Informix in the cloud or on-premises. Read a row, list the tables, and more"
[ibm-mq-doc]: ./connectors-create-api-mq.md "Connect to IBM MQ on-premises or in Azure to send and receive messages"
[instagram-doc]: ./connectors-create-api-instagram.md "Connect to Instagram. Trigger or act on events"
[mailchimp-doc]: ./connectors-create-api-mailchimp.md "Connect to your MailChimp account. Manage and automate mails"
[mandrill-doc]: ./connectors-create-api-mandrill.md "Connect to Mandrill for communication"
[microsoft-translator-doc]: ./connectors-create-api-microsofttranslator.md "Connect to Microsoft Translator. Translate text, detect languages, and more" 
[office-365-outlook-doc]: ./connectors-create-api-office365-outlook.md "Connect to your Office 365 account. Send and receive emails, manage your calendar and contacts, and more"
[office-365-users-doc]: ./connectors-create-api-office365-users.md 
[office-365-video-doc]: ./connectors-create-api-office365-video.md "Get video info, video lists and channels, and playback URLs for Office 365 videos"
[onedrive-doc]: ./connectors-create-api-onedrive.md "Connect to your personal Microsoft OneDrive. Upload, delete, list files, and more"
[onedrive-for-business-doc]: ./connectors-create-api-onedriveforbusiness.md "Connect to your business Microsoft OneDrive. Upload, delete, list your files, and more"
[oracle-db-doc]: ./connectors-create-api-oracledatabase.md "Connect to an Oracle database to add, insert, delete rows, and more"
[outlook.com-doc]: ./connectors-create-api-outlook.md "Connect to your Outlook mailbox. Manage your email, calendars, contacts, and more"
[project-online-doc]: ./connectors-create-api-projectonline.md "Connect to Microsoft Project Online. Manage your projects, tasks, resources, and more"
[rss-doc]: ./connectors-create-api-rss.md "Publish and retrieve feed items, trigger operations when a new item is published to an RSS feed."
[salesforce-doc]: ./connectors-create-api-salesforce.md "Connect to your Salesforce account. Manage accounts, leads, opportunities, and more"
[sap-connector-doc]: ../logic-apps/logic-apps-using-sap-connector.md "Connect to an on-premises SAP system"
[sendgrid-doc]: ./connectors-create-api-sendgrid.md "Connect to SendGrid. Send email and manage recipient lists"
[sftp-doc]: ./connectors-create-api-sftp.md "Connect to your SFTP account. Upload, get, delete files, and more"
[sharepoint-server-doc]: ./connectors-create-api-sharepointserver.md "Connect to SharePoint on-premises server. Manage documents, list items, and more"
[sharepoint-online-doc]: ./connectors-create-api-sharepointonline.md "Connect to SharePoint Online. Manage documents, list items, and more"
[slack-doc]: ./connectors-create-api-slack.md "Connect to Slack and post messages to Slack channels"
[smtp-doc]: ./connectors-create-api-smtp.md "Connect to an SMTP server and send email with attachments"
[sparkpost-doc]: ./connectors-create-api-sparkpost.md "Connects to SparkPost for communication"
[sql-server-doc]: ./connectors-create-api-sqlazure.md "Connect to Azure SQL Database or SQL Server. Create, update, get, and delete entries in a SQL database table."
[trello-doc]: ./connectors-create-api-trello.md "Connect to Trello. Manage your projects and organize anything with anyone"
[twilio-doc]: ./connectors-create-api-twilio.md "Connect to Twilio. Send and get messages, get available numbers, manage incoming phone numbers, and more"
[twitter-doc]: ./connectors-create-api-twitter.md "Connect to Twitter. Get timelines, post tweets, and more"
[wunderlist-doc]: ./connectors-create-api-wunderlist.md "Connect to Wunderlist. Manage your tasks and to-do lists, keep your life in sync, and more"
[yammer-doc]: ./connectors-create-api-yammer.md "Connect to Yammer. Post messages, get new messages, and more"
[youtube-doc]: ./connectors-create-api-youtube.md "Connect to YouTube. Manage your videos and channels"

<!--Enterprise Intregation Pack doc links-->
[as2-doc]: ../logic-apps/logic-apps-enterprise-integration-as2.md "Learn about enterprise integration AS2."
[as2-decode-doc]: ../logic-apps/logic-apps-enterprise-integration-as2-decode.md "Learn about enterprise integration AS2 decode"
[as2-encode-doc]:../logic-apps/logic-apps-enterprise-integration-as2-encode.md "Learn about enterprise integration AS2 encode"
[edifact-decode-doc]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-decode.md "Learn about enterprise integration EDIFACT decode"
[edifact-encode-doc]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-encode.md "Learn about enterprise integration EDIFACT encode"
[flat-file-decode-doc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Learn about enterprise integration flat file."
[flat-file-encode-doc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Learn about enterprise integration flat file."
[integration-account-doc]: ../logic-apps/logic-apps-enterprise-integration-metadata.md "Look up schemas, maps, partners, and more in your integration account"
[json-liquid-transform-doc]: ../logic-apps/logic-apps-enterprise-integration-liquid-transform.md "Learn about JSON transformations with Liquid"
[x12-doc]: ../logic-apps/logic-apps-enterprise-integration-x12.md "Learn about enterprise integration X12"
[x12-decode-doc]: ../logic-apps/logic-apps-enterprise-integration-X12-decode.md "Learn about enterprise integration X12 decode"
[x12-encode-doc]: ../logic-apps/logic-apps-enterprise-integration-X12-encode.md "Learn about enterprise integration X12 encode"
[xml-transform-doc]: ../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about enterprise integration transforms."
[xml-validate-doc]: ../logic-apps/logic-apps-enterprise-integration-xml-validation.md "Learn about enterprise integration XML validation."

<!-- Built-ins icons -->
[azure-api-management-icon]: ./media/apis-list/azure-api-management.png
[azure-app-services-icon]: ./media/apis-list/azure-app-services.png
[azure-functions-icon]: ./media/apis-list/azure-functions.png
[azure-logic-apps-icon]: ./media/apis-list/azure-logic-apps.png
[batch-icon]: ./media/apis-list/batch.png
[condition-icon]: ./media/apis-list/condition.png
[data-operations-icon]: ./media/apis-list/data-operations.png
[date-time-icon]: ./media/apis-list/date-time.png
[for-each-icon]: ./media/apis-list/for-each-loop.png
[http-icon]: ./media/apis-list/http.png
[http-request-icon]: ./media/apis-list/request.png
[http-response-icon]: ./media/apis-list/response.png
[http-swagger-icon]: ./media/apis-list/http-swagger.png
[http-webhook-icon]: ./media/apis-list/http-webhook.png
[schedule-icon]: ./media/apis-list/recurrence.png
[scope-icon]: ./media/apis-list/scope.png
[switch-icon]: ./media/apis-list/switch.png
[terminate-icon]: ./media/apis-list/terminate.png
[until-icon]: ./media/apis-list/until.png
[variables-icon]: ./media/apis-list/variables.png

<!--Managed API icons-->
[appfigures-icon]: ./media/apis-list/appfigures.png
[asana-icon]: ./media/apis-list/asana.png
[azure-automation-icon]: ./media/apis-list/azure-automation.png
[azure-blob-storage-icon]: ./media/apis-list/azure-blob-storage.png
[azure-cognitive-services-text-analytics-icon]: ./media/apis-list/azure-cognitive-services-text-analytics.png
[azure-data-lake-icon]: ./media/apis-list/azure-data-lake.png
[azure-document-db-icon]: ./media/apis-list/azure-document-db.png
[azure-event-grid-icon]: ./media/apis-list/azure-event-grid.png
[azure-event-grid-publish-icon]: ./media/apis-list/azure-event-grid-publish.png
[azure-event-hubs-icon]: ./media/apis-list/azure-event-hubs.png
[azure-ml-icon]: ./media/apis-list/azure-ml.png
[azure-queues-icon]: ./media/apis-list/azure-queues.png
[azure-resource-manager-icon]: ./media/apis-list/azure-resource-manager.png
[azure-service-bus-icon]: ./media/apis-list/azure-service-bus.png
[basecamp-3-icon]: ./media/apis-list/basecamp.png
[bitbucket-icon]: ./media/apis-list/bitbucket.png
[bitly-icon]: ./media/apis-list/bitly.png
[biztalk-server-icon]: ./media/apis-list/biztalk.png
[blogger-icon]: ./media/apis-list/blogger.png
[box-icon]: ./media/apis-list/box.png
[campfire-icon]: ./media/apis-list/campfire.png
[common-data-service-icon]: ./media/apis-list/common-data-service.png
[dropbox-icon]: ./media/apis-list/dropbox.png
[dynamics-365-icon]: ./media/apis-list/dynamics-crm-online.png
[dynamics-365-financials-icon]: ./media/apis-list/dynamics-365-financials.png
[dynamics-365-operations-icon]: ./media/apis-list/dynamics-365-operations.png
[easy-redmine-icon]: ./media/apis-list/easyredmine.png
[facebook-icon]: ./media/apis-list/facebook.png
[file-system-icon]: ./media/apis-list/file-system.png
[ftp-icon]: ./media/apis-list/ftp.png
[github-icon]: ./media/apis-list/github.png
[google-calendar-icon]: ./media/apis-list/google-calendar.png
[google-drive-icon]: ./media/apis-list/google-drive.png
[google-sheets-icon]: ./media/apis-list/google-sheet.png
[google-tasks-icon]: ./media/apis-list/google-tasks.png
[hipchat-icon]: ./media/apis-list/hipchat.png
[ibm-db2-icon]: ./media/apis-list/ibm-db2.png
[ibm-informix-icon]: ./media/apis-list/ibm-informix.png
[ibm-mq-icon]: ./media/apis-list/ibm-mq.png
[insightly-icon]: ./media/apis-list/insightly.png
[instagram-icon]: ./media/apis-list/instagram.png
[instapaper-icon]: ./media/apis-list/instapaper.png
[jira-icon]: ./media/apis-list/jira.png
[mailchimp-icon]: ./media/apis-list/mailchimp.png
[mandrill-icon]: ./media/apis-list/mandrill.png
[microsoft-translator-icon]: ./media/apis-list/microsoft-translator.png
[mysql-icon]: ./media/apis-list/mysql.png
[office-365-outlook-icon]: ./media/apis-list/office-365.png
[office-365-users-icon]: ./media/apis-list/office-365-users.png
[office-365-video-icon]: ./media/apis-list/office-365-video.png
[onedrive-icon]: ./media/apis-list/onedrive.png
[onedrive-for-business-icon]: ./media/apis-list/onedrive-business.png
[oracle-db-icon]: ./media/apis-list/oracle-db.png
[outlook.com-icon]: ./media/apis-list/outlook.png
[pagerduty-icon]: ./media/apis-list/pagerduty.png
[pinterest-icon]: ./media/apis-list/pinterest.png
[postgre-sql-icon]: ./media/apis-list/postgre-sql.png
[project-online-icon]: ./media/apis-list/projecton-line.png
[redmine-icon]: ./media/apis-list/redmine.png
[rss-icon]: ./media/apis-list/rss.png
[salesforce-icon]: ./media/apis-list/salesforce.png
[sap-icon]: ./media/apis-list/sap.png
[send-grid-icon]: ./media/apis-list/sendgrid.png
[sftp-icon]: ./media/apis-list/sftp.png
[sharepoint-online-icon]: ./media/apis-list/sharepoint-online.png
[sharepoint-server-icon]: ./media/apis-list/sharepoint-server.png
[slack-icon]: ./media/apis-list/slack.png
[smartsheet-icon]: ./media/apis-list/smartsheet.png
[smtp-icon]: ./media/apis-list/smtp.png
[sparkpost-icon]: ./media/apis-list/sparkpost.png
[sql-server-icon]: ./media/apis-list/sql.png
[teradata-icon]: ./media/apis-list/teradata.png
[todoist-icon]: ./media/apis-list/todoist.png
[trello-icon]: ./media/apis-list/trello.png
[twilio-icon]: ./media/apis-list/twilio.png
[twitter-icon]: ./media/apis-list/twitter.png
[vimeo-icon]: ./media/apis-list/vimeo.png
[visual-studio-team-services-icon]: ./media/apis-list/visual-studio-team-services.png
[wordpress-icon]: ./media/apis-list/wordpress.png
[wunderlist-icon]: ./media/apis-list/wunderlist.png
[yammer-icon]: ./media/apis-list/yammer.png
[youtube-icon]: ./media/apis-list/youtube.png

<!-- Enterprise Integration Pack icons -->
[as2-icon]: ./media/apis-list/as2.png
[edifact-icon]: ./media/apis-list/edifact.png
[flat-file-encode-icon]: ./media/apis-list/flat-file-encoding.png
[flat-file-decode-icon]: ./media/apis-list/flat-file-decoding.png
[integration-account-icon]: ./media/apis-list/integration-account.png
[liquid-icon]: ./media/apis-list/liquid-transform.png
[x12-icon]: ./media/apis-list/x12.png
[xml-validate-icon]: ./media/apis-list/xml-validation.png
[xml-transform-icon]: ./media/apis-list/xsl-transform.png