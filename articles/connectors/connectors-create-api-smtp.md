---
title: SMTP | Microsoft Docs
description: Create logic apps with Azure App service. Connect to SMTP to send email.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: deonhe
ms.openlocfilehash: 6b61217806a8274343f73d3335d5413633b0d28b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662815"
---
# <a name="get-started-with-the-smtp-connector"></a><span data-ttu-id="023b8-104">Get started with the SMTP connector</span><span class="sxs-lookup"><span data-stu-id="023b8-104">Get started with the SMTP connector</span></span>
<span data-ttu-id="023b8-105">Connect to SMTP to send email.</span><span class="sxs-lookup"><span data-stu-id="023b8-105">Connect to SMTP to send email.</span></span>

<span data-ttu-id="023b8-106">To use [any connector](apis-list.md), you first need to create a logic app.</span><span class="sxs-lookup"><span data-stu-id="023b8-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="023b8-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="023b8-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-smtp"></a><span data-ttu-id="023b8-108">Connect to SMTP</span><span class="sxs-lookup"><span data-stu-id="023b8-108">Connect to SMTP</span></span>
<span data-ttu-id="023b8-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span><span class="sxs-lookup"><span data-stu-id="023b8-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="023b8-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span><span class="sxs-lookup"><span data-stu-id="023b8-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="023b8-111">For example, in order to connect to SMTP, you first need an SMTP *connection*.</span><span class="sxs-lookup"><span data-stu-id="023b8-111">For example, in order to connect to SMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="023b8-112">To create a connection, you would need to provide the credentials you normally use to access the service you wish to connect to.</span><span class="sxs-lookup"><span data-stu-id="023b8-112">To create a connection, you would need to provide the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="023b8-113">So, in the SMTP example, you would need the credentials to your connection name, SMTP server address, and user login information in order to create the connection to SMTP.</span><span class="sxs-lookup"><span data-stu-id="023b8-113">So, in the SMTP example, you would need the credentials to your connection name, SMTP server address, and user login information in order to create the connection to SMTP.</span></span> [<span data-ttu-id="023b8-114">Learn more about connections</span><span class="sxs-lookup"><span data-stu-id="023b8-114">Learn more about connections</span></span>]()  

### <a name="create-a-connection-to-smtp"></a><span data-ttu-id="023b8-115">Create a connection to SMTP</span><span class="sxs-lookup"><span data-stu-id="023b8-115">Create a connection to SMTP</span></span>
> [!INCLUDE [Steps to create a connection to SMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="023b8-116">Use an SMTP trigger</span><span class="sxs-lookup"><span data-stu-id="023b8-116">Use an SMTP trigger</span></span>
<span data-ttu-id="023b8-117">A trigger is an event that can be used to start the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="023b8-117">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="023b8-118">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="023b8-118">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="023b8-119">In this example, because SMTP does not have a trigger of its own, we'll use the **Salesforce - When an object is created** trigger.</span><span class="sxs-lookup"><span data-stu-id="023b8-119">In this example, because SMTP does not have a trigger of its own, we'll use the **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="023b8-120">This trigger will activate when a new object is created in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="023b8-120">This trigger will activate when a new object is created in Salesforce.</span></span> <span data-ttu-id="023b8-121">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via the SMTP connector with a notification of the new lead being created.</span><span class="sxs-lookup"><span data-stu-id="023b8-121">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via the SMTP connector with a notification of the new lead being created.</span></span>

1. <span data-ttu-id="023b8-122">Enter *salesforce* in the search box on the logic apps designer then select the **Salesforce - When an object is created** trigger.</span><span class="sxs-lookup"><span data-stu-id="023b8-122">Enter *salesforce* in the search box on the logic apps designer then select the **Salesforce - When an object is created** trigger.</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="023b8-123">The **When an object is created** control is displayed.</span><span class="sxs-lookup"><span data-stu-id="023b8-123">The **When an object is created** control is displayed.</span></span>
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="023b8-124">Select the **Object Type** then select *Lead* from the list of objects.</span><span class="sxs-lookup"><span data-stu-id="023b8-124">Select the **Object Type** then select *Lead* from the list of objects.</span></span> <span data-ttu-id="023b8-125">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="023b8-125">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="023b8-126">The trigger has been created.</span><span class="sxs-lookup"><span data-stu-id="023b8-126">The trigger has been created.</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="023b8-127">Use an SMTP action</span><span class="sxs-lookup"><span data-stu-id="023b8-127">Use an SMTP action</span></span>
<span data-ttu-id="023b8-128">An action is an operation carried out by the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="023b8-128">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="023b8-129">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="023b8-129">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="023b8-130">Now that the trigger has been added, follow these steps to add an SMTP action that will occur when a new lead is created in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="023b8-130">Now that the trigger has been added, follow these steps to add an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="023b8-131">Select **+ New Step** to add the action you would like to take when a new lead is created.</span><span class="sxs-lookup"><span data-stu-id="023b8-131">Select **+ New Step** to add the action you would like to take when a new lead is created.</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="023b8-132">Select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="023b8-132">Select **Add an action**.</span></span> <span data-ttu-id="023b8-133">This opens the search box where you can search for any action you would like to take.</span><span class="sxs-lookup"><span data-stu-id="023b8-133">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="023b8-134">Enter *smtp* to search for actions related to SMTP.</span><span class="sxs-lookup"><span data-stu-id="023b8-134">Enter *smtp* to search for actions related to SMTP.</span></span>  
4. <span data-ttu-id="023b8-135">Select **SMTP - Send Email** as the action to take when the new lead is created.</span><span class="sxs-lookup"><span data-stu-id="023b8-135">Select **SMTP - Send Email** as the action to take when the new lead is created.</span></span> <span data-ttu-id="023b8-136">The action control block opens.</span><span class="sxs-lookup"><span data-stu-id="023b8-136">The action control block opens.</span></span> <span data-ttu-id="023b8-137">You will have to establish your smtp connection in the designer block if you have not done so previously.</span><span class="sxs-lookup"><span data-stu-id="023b8-137">You will have to establish your smtp connection in the designer block if you have not done so previously.</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="023b8-138">Input your desired email information in the **SMTP - Send Email** block.</span><span class="sxs-lookup"><span data-stu-id="023b8-138">Input your desired email information in the **SMTP - Send Email** block.</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="023b8-139">Save your work in order to activate your workflow.</span><span class="sxs-lookup"><span data-stu-id="023b8-139">Save your work in order to activate your workflow.</span></span>  

## <a name="technical-details"></a><span data-ttu-id="023b8-140">Technical details</span><span class="sxs-lookup"><span data-stu-id="023b8-140">Technical details</span></span>
<span data-ttu-id="023b8-141">Here are the details about the triggers, actions and responses that this connection supports:</span><span class="sxs-lookup"><span data-stu-id="023b8-141">Here are the details about the triggers, actions and responses that this connection supports:</span></span>

## <a name="smtp-triggers"></a><span data-ttu-id="023b8-142">SMTP triggers</span><span class="sxs-lookup"><span data-stu-id="023b8-142">SMTP triggers</span></span>
<span data-ttu-id="023b8-143">SMTP has no triggers.</span><span class="sxs-lookup"><span data-stu-id="023b8-143">SMTP has no triggers.</span></span> 

## <a name="smtp-actions"></a><span data-ttu-id="023b8-144">SMTP actions</span><span class="sxs-lookup"><span data-stu-id="023b8-144">SMTP actions</span></span>
<span data-ttu-id="023b8-145">SMTP has the following action:</span><span class="sxs-lookup"><span data-stu-id="023b8-145">SMTP has the following action:</span></span>

| <span data-ttu-id="023b8-146">Action</span><span class="sxs-lookup"><span data-stu-id="023b8-146">Action</span></span> | <span data-ttu-id="023b8-147">Description</span><span class="sxs-lookup"><span data-stu-id="023b8-147">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="023b8-148">Send Email</span><span class="sxs-lookup"><span data-stu-id="023b8-148">Send Email</span></span>](connectors-create-api-smtp.md#send-email) |<span data-ttu-id="023b8-149">This operation sends an email to one or more recipients.</span><span class="sxs-lookup"><span data-stu-id="023b8-149">This operation sends an email to one or more recipients.</span></span> |

### <a name="action-details"></a><span data-ttu-id="023b8-150">Action details</span><span class="sxs-lookup"><span data-stu-id="023b8-150">Action details</span></span>
<span data-ttu-id="023b8-151">Here are the details for the action of this connector, along with its responses:</span><span class="sxs-lookup"><span data-stu-id="023b8-151">Here are the details for the action of this connector, along with its responses:</span></span>

### <a name="send-email"></a><span data-ttu-id="023b8-152">Send Email</span><span class="sxs-lookup"><span data-stu-id="023b8-152">Send Email</span></span>
<span data-ttu-id="023b8-153">This operation sends an email to one or more recipients.</span><span class="sxs-lookup"><span data-stu-id="023b8-153">This operation sends an email to one or more recipients.</span></span> 

| <span data-ttu-id="023b8-154">Property Name</span><span class="sxs-lookup"><span data-stu-id="023b8-154">Property Name</span></span> | <span data-ttu-id="023b8-155">Display Name</span><span class="sxs-lookup"><span data-stu-id="023b8-155">Display Name</span></span> | <span data-ttu-id="023b8-156">Description</span><span class="sxs-lookup"><span data-stu-id="023b8-156">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="023b8-157">To</span><span class="sxs-lookup"><span data-stu-id="023b8-157">To</span></span> |<span data-ttu-id="023b8-158">To</span><span class="sxs-lookup"><span data-stu-id="023b8-158">To</span></span> |<span data-ttu-id="023b8-159">Specify email addresses separated by semicolons like recipient1@domain.com;recipient2@domain.com</span><span class="sxs-lookup"><span data-stu-id="023b8-159">Specify email addresses separated by semicolons like recipient1@domain.com;recipient2@domain.com</span></span> |
| <span data-ttu-id="023b8-160">CC</span><span class="sxs-lookup"><span data-stu-id="023b8-160">CC</span></span> |<span data-ttu-id="023b8-161">cc</span><span class="sxs-lookup"><span data-stu-id="023b8-161">cc</span></span> |<span data-ttu-id="023b8-162">Specify email addresses separated by semicolons like recipient1@domain.com;recipient2@domain.com</span><span class="sxs-lookup"><span data-stu-id="023b8-162">Specify email addresses separated by semicolons like recipient1@domain.com;recipient2@domain.com</span></span> |
| <span data-ttu-id="023b8-163">Subject</span><span class="sxs-lookup"><span data-stu-id="023b8-163">Subject</span></span> |<span data-ttu-id="023b8-164">Subject</span><span class="sxs-lookup"><span data-stu-id="023b8-164">Subject</span></span> |<span data-ttu-id="023b8-165">Email subject</span><span class="sxs-lookup"><span data-stu-id="023b8-165">Email subject</span></span> |
| <span data-ttu-id="023b8-166">Body</span><span class="sxs-lookup"><span data-stu-id="023b8-166">Body</span></span> |<span data-ttu-id="023b8-167">Body</span><span class="sxs-lookup"><span data-stu-id="023b8-167">Body</span></span> |<span data-ttu-id="023b8-168">Email body</span><span class="sxs-lookup"><span data-stu-id="023b8-168">Email body</span></span> |
| <span data-ttu-id="023b8-169">From</span><span class="sxs-lookup"><span data-stu-id="023b8-169">From</span></span> |<span data-ttu-id="023b8-170">From</span><span class="sxs-lookup"><span data-stu-id="023b8-170">From</span></span> |<span data-ttu-id="023b8-171">Email address of sender like sender@domain.com</span><span class="sxs-lookup"><span data-stu-id="023b8-171">Email address of sender like sender@domain.com</span></span> |
| <span data-ttu-id="023b8-172">IsHtml</span><span class="sxs-lookup"><span data-stu-id="023b8-172">IsHtml</span></span> |<span data-ttu-id="023b8-173">Is Html</span><span class="sxs-lookup"><span data-stu-id="023b8-173">Is Html</span></span> |<span data-ttu-id="023b8-174">Send the email as HTML (true/false)</span><span class="sxs-lookup"><span data-stu-id="023b8-174">Send the email as HTML (true/false)</span></span> |
| <span data-ttu-id="023b8-175">Bcc</span><span class="sxs-lookup"><span data-stu-id="023b8-175">Bcc</span></span> |<span data-ttu-id="023b8-176">bcc</span><span class="sxs-lookup"><span data-stu-id="023b8-176">bcc</span></span> |<span data-ttu-id="023b8-177">Specify email addresses separated by semicolons like recipient1@domain.com;recipient2@domain.com</span><span class="sxs-lookup"><span data-stu-id="023b8-177">Specify email addresses separated by semicolons like recipient1@domain.com;recipient2@domain.com</span></span> |
| <span data-ttu-id="023b8-178">Importance</span><span class="sxs-lookup"><span data-stu-id="023b8-178">Importance</span></span> |<span data-ttu-id="023b8-179">Importance</span><span class="sxs-lookup"><span data-stu-id="023b8-179">Importance</span></span> |<span data-ttu-id="023b8-180">Importance of the email (High, Normal, or Low)</span><span class="sxs-lookup"><span data-stu-id="023b8-180">Importance of the email (High, Normal, or Low)</span></span> |
| <span data-ttu-id="023b8-181">ContentData</span><span class="sxs-lookup"><span data-stu-id="023b8-181">ContentData</span></span> |<span data-ttu-id="023b8-182">Attachments Content Data</span><span class="sxs-lookup"><span data-stu-id="023b8-182">Attachments Content Data</span></span> |<span data-ttu-id="023b8-183">Content data (base64 encoded for streams and as-is for string)</span><span class="sxs-lookup"><span data-stu-id="023b8-183">Content data (base64 encoded for streams and as-is for string)</span></span> |
| <span data-ttu-id="023b8-184">ContentType</span><span class="sxs-lookup"><span data-stu-id="023b8-184">ContentType</span></span> |<span data-ttu-id="023b8-185">Attachments Content Type</span><span class="sxs-lookup"><span data-stu-id="023b8-185">Attachments Content Type</span></span> |<span data-ttu-id="023b8-186">Content type</span><span class="sxs-lookup"><span data-stu-id="023b8-186">Content type</span></span> |
| <span data-ttu-id="023b8-187">ContentTransferEncoding</span><span class="sxs-lookup"><span data-stu-id="023b8-187">ContentTransferEncoding</span></span> |<span data-ttu-id="023b8-188">Attachments Content Transfer Encoding</span><span class="sxs-lookup"><span data-stu-id="023b8-188">Attachments Content Transfer Encoding</span></span> |<span data-ttu-id="023b8-189">Content Transfer Encoding (base64 or none)</span><span class="sxs-lookup"><span data-stu-id="023b8-189">Content Transfer Encoding (base64 or none)</span></span> |
| <span data-ttu-id="023b8-190">FileName</span><span class="sxs-lookup"><span data-stu-id="023b8-190">FileName</span></span> |<span data-ttu-id="023b8-191">Attachments File Name</span><span class="sxs-lookup"><span data-stu-id="023b8-191">Attachments File Name</span></span> |<span data-ttu-id="023b8-192">File name</span><span class="sxs-lookup"><span data-stu-id="023b8-192">File name</span></span> |
| <span data-ttu-id="023b8-193">ContentId</span><span class="sxs-lookup"><span data-stu-id="023b8-193">ContentId</span></span> |<span data-ttu-id="023b8-194">Attachments Content ID</span><span class="sxs-lookup"><span data-stu-id="023b8-194">Attachments Content ID</span></span> |<span data-ttu-id="023b8-195">Content id</span><span class="sxs-lookup"><span data-stu-id="023b8-195">Content id</span></span> |

<span data-ttu-id="023b8-196">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="023b8-196">An \* indicates that a property is required</span></span>

## <a name="http-responses"></a><span data-ttu-id="023b8-197">HTTP responses</span><span class="sxs-lookup"><span data-stu-id="023b8-197">HTTP responses</span></span>
<span data-ttu-id="023b8-198">The actions and triggers above can return one or more of the following HTTP status codes:</span><span class="sxs-lookup"><span data-stu-id="023b8-198">The actions and triggers above can return one or more of the following HTTP status codes:</span></span> 

| <span data-ttu-id="023b8-199">Name</span><span class="sxs-lookup"><span data-stu-id="023b8-199">Name</span></span> | <span data-ttu-id="023b8-200">Description</span><span class="sxs-lookup"><span data-stu-id="023b8-200">Description</span></span> |
| --- | --- |
| <span data-ttu-id="023b8-201">200</span><span class="sxs-lookup"><span data-stu-id="023b8-201">200</span></span> |<span data-ttu-id="023b8-202">OK</span><span class="sxs-lookup"><span data-stu-id="023b8-202">OK</span></span> |
| <span data-ttu-id="023b8-203">202</span><span class="sxs-lookup"><span data-stu-id="023b8-203">202</span></span> |<span data-ttu-id="023b8-204">Accepted</span><span class="sxs-lookup"><span data-stu-id="023b8-204">Accepted</span></span> |
| <span data-ttu-id="023b8-205">400</span><span class="sxs-lookup"><span data-stu-id="023b8-205">400</span></span> |<span data-ttu-id="023b8-206">Bad Request</span><span class="sxs-lookup"><span data-stu-id="023b8-206">Bad Request</span></span> |
| <span data-ttu-id="023b8-207">401</span><span class="sxs-lookup"><span data-stu-id="023b8-207">401</span></span> |<span data-ttu-id="023b8-208">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="023b8-208">Unauthorized</span></span> |
| <span data-ttu-id="023b8-209">403</span><span class="sxs-lookup"><span data-stu-id="023b8-209">403</span></span> |<span data-ttu-id="023b8-210">Forbidden</span><span class="sxs-lookup"><span data-stu-id="023b8-210">Forbidden</span></span> |
| <span data-ttu-id="023b8-211">404</span><span class="sxs-lookup"><span data-stu-id="023b8-211">404</span></span> |<span data-ttu-id="023b8-212">Not Found</span><span class="sxs-lookup"><span data-stu-id="023b8-212">Not Found</span></span> |
| <span data-ttu-id="023b8-213">500</span><span class="sxs-lookup"><span data-stu-id="023b8-213">500</span></span> |<span data-ttu-id="023b8-214">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="023b8-214">Internal Server Error.</span></span> <span data-ttu-id="023b8-215">Unknown error occurred.</span><span class="sxs-lookup"><span data-stu-id="023b8-215">Unknown error occurred.</span></span> |
| <span data-ttu-id="023b8-216">default</span><span class="sxs-lookup"><span data-stu-id="023b8-216">default</span></span> |<span data-ttu-id="023b8-217">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="023b8-217">Operation Failed.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="023b8-218">Next steps</span><span class="sxs-lookup"><span data-stu-id="023b8-218">Next steps</span></span>
[<span data-ttu-id="023b8-219">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="023b8-219">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)









