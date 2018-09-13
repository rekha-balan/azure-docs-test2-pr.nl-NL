---
title: SendGrid | Microsoft Docs
description: Create Logic apps with Azure App service. SendGrid Connection Provider lets you send email and manage recipient lists.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: bc4f1fc2-824c-4ed7-8de8-e82baff3b746
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: deonhe
ms.openlocfilehash: e30231bd576436ae69f4fa42d0e2ab312c3938d6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549547"
---
# <a name="get-started-with-the-sendgrid-connector"></a><span data-ttu-id="991d0-104">Get started with the SendGrid connector</span><span class="sxs-lookup"><span data-stu-id="991d0-104">Get started with the SendGrid connector</span></span>
<span data-ttu-id="991d0-105">SendGrid Connection Provider lets you send email and manage recipient lists.</span><span class="sxs-lookup"><span data-stu-id="991d0-105">SendGrid Connection Provider lets you send email and manage recipient lists.</span></span>

> [!NOTE]
> <span data-ttu-id="991d0-106">This version of the article applies to logic apps 2015-08-01-preview schema version.</span><span class="sxs-lookup"><span data-stu-id="991d0-106">This version of the article applies to logic apps 2015-08-01-preview schema version.</span></span> 
> 
> 

<span data-ttu-id="991d0-107">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="991d0-107">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="triggers-and-actions"></a><span data-ttu-id="991d0-108">Triggers and actions</span><span class="sxs-lookup"><span data-stu-id="991d0-108">Triggers and actions</span></span>
<span data-ttu-id="991d0-109">The SendGrid connector can be used as an action; it has trigger(s).</span><span class="sxs-lookup"><span data-stu-id="991d0-109">The SendGrid connector can be used as an action; it has trigger(s).</span></span> <span data-ttu-id="991d0-110">All connectors support data in JSON and XML formats.</span><span class="sxs-lookup"><span data-stu-id="991d0-110">All connectors support data in JSON and XML formats.</span></span> 

 <span data-ttu-id="991d0-111">The SendGrid connector has the following actions available.</span><span class="sxs-lookup"><span data-stu-id="991d0-111">The SendGrid connector has the following actions available.</span></span> <span data-ttu-id="991d0-112">There are no triggers.</span><span class="sxs-lookup"><span data-stu-id="991d0-112">There are no triggers.</span></span>

### <a name="sendgrid-actions"></a><span data-ttu-id="991d0-113">SendGrid actions</span><span class="sxs-lookup"><span data-stu-id="991d0-113">SendGrid actions</span></span>
<span data-ttu-id="991d0-114">You can take these action(s):</span><span class="sxs-lookup"><span data-stu-id="991d0-114">You can take these action(s):</span></span>

| <span data-ttu-id="991d0-115">Action</span><span class="sxs-lookup"><span data-stu-id="991d0-115">Action</span></span> | <span data-ttu-id="991d0-116">Description</span><span class="sxs-lookup"><span data-stu-id="991d0-116">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="991d0-117">SendEmail</span><span class="sxs-lookup"><span data-stu-id="991d0-117">SendEmail</span></span>](connectors-create-api-sendgrid.md#sendemail) |<span data-ttu-id="991d0-118">Sends an email using SendGrid API (Limited to 10,000 recipients)</span><span class="sxs-lookup"><span data-stu-id="991d0-118">Sends an email using SendGrid API (Limited to 10,000 recipients)</span></span> |
| [<span data-ttu-id="991d0-119">AddRecipientToList</span><span class="sxs-lookup"><span data-stu-id="991d0-119">AddRecipientToList</span></span>](connectors-create-api-sendgrid.md#addrecipienttolist) |<span data-ttu-id="991d0-120">Add an individual recipient to a recipient list</span><span class="sxs-lookup"><span data-stu-id="991d0-120">Add an individual recipient to a recipient list</span></span> |

## <a name="create-a-connection-to-sendgrid"></a><span data-ttu-id="991d0-121">Create a connection to SendGrid</span><span class="sxs-lookup"><span data-stu-id="991d0-121">Create a connection to SendGrid</span></span>
<span data-ttu-id="991d0-122">To create Logic apps with SendGrid, you must first create a **connection** then provide the details for the following properties:</span><span class="sxs-lookup"><span data-stu-id="991d0-122">To create Logic apps with SendGrid, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="991d0-123">Property</span><span class="sxs-lookup"><span data-stu-id="991d0-123">Property</span></span> | <span data-ttu-id="991d0-124">Required</span><span class="sxs-lookup"><span data-stu-id="991d0-124">Required</span></span> | <span data-ttu-id="991d0-125">Description</span><span class="sxs-lookup"><span data-stu-id="991d0-125">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="991d0-126">ApiKey</span><span class="sxs-lookup"><span data-stu-id="991d0-126">ApiKey</span></span> |<span data-ttu-id="991d0-127">Yes</span><span class="sxs-lookup"><span data-stu-id="991d0-127">Yes</span></span> |<span data-ttu-id="991d0-128">Provide Your SendGrid Api Key</span><span class="sxs-lookup"><span data-stu-id="991d0-128">Provide Your SendGrid Api Key</span></span> |

> [!INCLUDE [Steps to create a connection to SendGrid](../../includes/connectors-create-api-sendgrid.md)]
> 
> [!TIP]
> <span data-ttu-id="991d0-129">You can use this connection in other logic apps.</span><span class="sxs-lookup"><span data-stu-id="991d0-129">You can use this connection in other logic apps.</span></span>
> 
> 

<span data-ttu-id="991d0-130">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span><span class="sxs-lookup"><span data-stu-id="991d0-130">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span>

## <a name="reference-for-sendgrid"></a><span data-ttu-id="991d0-131">Reference for SendGrid</span><span class="sxs-lookup"><span data-stu-id="991d0-131">Reference for SendGrid</span></span>
<span data-ttu-id="991d0-132">Applies to version: 1.0</span><span class="sxs-lookup"><span data-stu-id="991d0-132">Applies to version: 1.0</span></span>

## <a name="sendemail"></a><span data-ttu-id="991d0-133">SendEmail</span><span class="sxs-lookup"><span data-stu-id="991d0-133">SendEmail</span></span>
<span data-ttu-id="991d0-134">Send email: Sends an email using SendGrid API (Limited to 10,000 recipients)</span><span class="sxs-lookup"><span data-stu-id="991d0-134">Send email: Sends an email using SendGrid API (Limited to 10,000 recipients)</span></span> 

```POST: /api/mail.send.json``` 

| <span data-ttu-id="991d0-135">Name</span><span class="sxs-lookup"><span data-stu-id="991d0-135">Name</span></span> | <span data-ttu-id="991d0-136">Data Type</span><span class="sxs-lookup"><span data-stu-id="991d0-136">Data Type</span></span> | <span data-ttu-id="991d0-137">Required</span><span class="sxs-lookup"><span data-stu-id="991d0-137">Required</span></span> | <span data-ttu-id="991d0-138">Located In</span><span class="sxs-lookup"><span data-stu-id="991d0-138">Located In</span></span> | <span data-ttu-id="991d0-139">Default Value</span><span class="sxs-lookup"><span data-stu-id="991d0-139">Default Value</span></span> | <span data-ttu-id="991d0-140">Description</span><span class="sxs-lookup"><span data-stu-id="991d0-140">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="991d0-141">request</span><span class="sxs-lookup"><span data-stu-id="991d0-141">request</span></span> | |<span data-ttu-id="991d0-142">yes</span><span class="sxs-lookup"><span data-stu-id="991d0-142">yes</span></span> |<span data-ttu-id="991d0-143">body</span><span class="sxs-lookup"><span data-stu-id="991d0-143">body</span></span> |<span data-ttu-id="991d0-144">none</span><span class="sxs-lookup"><span data-stu-id="991d0-144">none</span></span> |<span data-ttu-id="991d0-145">Email message to send</span><span class="sxs-lookup"><span data-stu-id="991d0-145">Email message to send</span></span> |

#### <a name="response"></a><span data-ttu-id="991d0-146">Response</span><span class="sxs-lookup"><span data-stu-id="991d0-146">Response</span></span>
| <span data-ttu-id="991d0-147">Name</span><span class="sxs-lookup"><span data-stu-id="991d0-147">Name</span></span> | <span data-ttu-id="991d0-148">Description</span><span class="sxs-lookup"><span data-stu-id="991d0-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="991d0-149">200</span><span class="sxs-lookup"><span data-stu-id="991d0-149">200</span></span> |<span data-ttu-id="991d0-150">OK</span><span class="sxs-lookup"><span data-stu-id="991d0-150">OK</span></span> |
| <span data-ttu-id="991d0-151">400</span><span class="sxs-lookup"><span data-stu-id="991d0-151">400</span></span> |<span data-ttu-id="991d0-152">Bad Request</span><span class="sxs-lookup"><span data-stu-id="991d0-152">Bad Request</span></span> |
| <span data-ttu-id="991d0-153">401</span><span class="sxs-lookup"><span data-stu-id="991d0-153">401</span></span> |<span data-ttu-id="991d0-154">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="991d0-154">Unauthorized</span></span> |
| <span data-ttu-id="991d0-155">403</span><span class="sxs-lookup"><span data-stu-id="991d0-155">403</span></span> |<span data-ttu-id="991d0-156">Forbidden</span><span class="sxs-lookup"><span data-stu-id="991d0-156">Forbidden</span></span> |
| <span data-ttu-id="991d0-157">404</span><span class="sxs-lookup"><span data-stu-id="991d0-157">404</span></span> |<span data-ttu-id="991d0-158">Not Found</span><span class="sxs-lookup"><span data-stu-id="991d0-158">Not Found</span></span> |
| <span data-ttu-id="991d0-159">429</span><span class="sxs-lookup"><span data-stu-id="991d0-159">429</span></span> |<span data-ttu-id="991d0-160">Too Many Request</span><span class="sxs-lookup"><span data-stu-id="991d0-160">Too Many Request</span></span> |
| <span data-ttu-id="991d0-161">500</span><span class="sxs-lookup"><span data-stu-id="991d0-161">500</span></span> |<span data-ttu-id="991d0-162">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="991d0-162">Internal Server Error.</span></span> <span data-ttu-id="991d0-163">Unknown error occured</span><span class="sxs-lookup"><span data-stu-id="991d0-163">Unknown error occured</span></span> |
| <span data-ttu-id="991d0-164">default</span><span class="sxs-lookup"><span data-stu-id="991d0-164">default</span></span> |<span data-ttu-id="991d0-165">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="991d0-165">Operation Failed.</span></span> |

## <a name="addrecipienttolist"></a><span data-ttu-id="991d0-166">AddRecipientToList</span><span class="sxs-lookup"><span data-stu-id="991d0-166">AddRecipientToList</span></span>
<span data-ttu-id="991d0-167">Add recipient to list: Add an individual recipient to a recipient list</span><span class="sxs-lookup"><span data-stu-id="991d0-167">Add recipient to list: Add an individual recipient to a recipient list</span></span> 

```POST: /v3/contactdb/lists/{listId}/recipients/{recipientId}``` 

| <span data-ttu-id="991d0-168">Name</span><span class="sxs-lookup"><span data-stu-id="991d0-168">Name</span></span> | <span data-ttu-id="991d0-169">Data Type</span><span class="sxs-lookup"><span data-stu-id="991d0-169">Data Type</span></span> | <span data-ttu-id="991d0-170">Required</span><span class="sxs-lookup"><span data-stu-id="991d0-170">Required</span></span> | <span data-ttu-id="991d0-171">Located In</span><span class="sxs-lookup"><span data-stu-id="991d0-171">Located In</span></span> | <span data-ttu-id="991d0-172">Default Value</span><span class="sxs-lookup"><span data-stu-id="991d0-172">Default Value</span></span> | <span data-ttu-id="991d0-173">Description</span><span class="sxs-lookup"><span data-stu-id="991d0-173">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="991d0-174">listId</span><span class="sxs-lookup"><span data-stu-id="991d0-174">listId</span></span> |<span data-ttu-id="991d0-175">string</span><span class="sxs-lookup"><span data-stu-id="991d0-175">string</span></span> |<span data-ttu-id="991d0-176">yes</span><span class="sxs-lookup"><span data-stu-id="991d0-176">yes</span></span> |<span data-ttu-id="991d0-177">path</span><span class="sxs-lookup"><span data-stu-id="991d0-177">path</span></span> |<span data-ttu-id="991d0-178">none</span><span class="sxs-lookup"><span data-stu-id="991d0-178">none</span></span> |<span data-ttu-id="991d0-179">Unique id of the recipient list</span><span class="sxs-lookup"><span data-stu-id="991d0-179">Unique id of the recipient list</span></span> |
| <span data-ttu-id="991d0-180">recipientId</span><span class="sxs-lookup"><span data-stu-id="991d0-180">recipientId</span></span> |<span data-ttu-id="991d0-181">string</span><span class="sxs-lookup"><span data-stu-id="991d0-181">string</span></span> |<span data-ttu-id="991d0-182">yes</span><span class="sxs-lookup"><span data-stu-id="991d0-182">yes</span></span> |<span data-ttu-id="991d0-183">path</span><span class="sxs-lookup"><span data-stu-id="991d0-183">path</span></span> |<span data-ttu-id="991d0-184">none</span><span class="sxs-lookup"><span data-stu-id="991d0-184">none</span></span> |<span data-ttu-id="991d0-185">Unique id of the recipient</span><span class="sxs-lookup"><span data-stu-id="991d0-185">Unique id of the recipient</span></span> |

#### <a name="response"></a><span data-ttu-id="991d0-186">Response</span><span class="sxs-lookup"><span data-stu-id="991d0-186">Response</span></span>
| <span data-ttu-id="991d0-187">Name</span><span class="sxs-lookup"><span data-stu-id="991d0-187">Name</span></span> | <span data-ttu-id="991d0-188">Description</span><span class="sxs-lookup"><span data-stu-id="991d0-188">Description</span></span> |
| --- | --- |
| <span data-ttu-id="991d0-189">200</span><span class="sxs-lookup"><span data-stu-id="991d0-189">200</span></span> |<span data-ttu-id="991d0-190">OK</span><span class="sxs-lookup"><span data-stu-id="991d0-190">OK</span></span> |
| <span data-ttu-id="991d0-191">400</span><span class="sxs-lookup"><span data-stu-id="991d0-191">400</span></span> |<span data-ttu-id="991d0-192">Bad Request</span><span class="sxs-lookup"><span data-stu-id="991d0-192">Bad Request</span></span> |
| <span data-ttu-id="991d0-193">401</span><span class="sxs-lookup"><span data-stu-id="991d0-193">401</span></span> |<span data-ttu-id="991d0-194">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="991d0-194">Unauthorized</span></span> |
| <span data-ttu-id="991d0-195">403</span><span class="sxs-lookup"><span data-stu-id="991d0-195">403</span></span> |<span data-ttu-id="991d0-196">Forbidden</span><span class="sxs-lookup"><span data-stu-id="991d0-196">Forbidden</span></span> |
| <span data-ttu-id="991d0-197">404</span><span class="sxs-lookup"><span data-stu-id="991d0-197">404</span></span> |<span data-ttu-id="991d0-198">Not Found</span><span class="sxs-lookup"><span data-stu-id="991d0-198">Not Found</span></span> |
| <span data-ttu-id="991d0-199">500</span><span class="sxs-lookup"><span data-stu-id="991d0-199">500</span></span> |<span data-ttu-id="991d0-200">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="991d0-200">Internal Server Error.</span></span> <span data-ttu-id="991d0-201">Unknown error occured</span><span class="sxs-lookup"><span data-stu-id="991d0-201">Unknown error occured</span></span> |
| <span data-ttu-id="991d0-202">default</span><span class="sxs-lookup"><span data-stu-id="991d0-202">default</span></span> |<span data-ttu-id="991d0-203">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="991d0-203">Operation Failed.</span></span> |

## <a name="object-definitions"></a><span data-ttu-id="991d0-204">Object definitions</span><span class="sxs-lookup"><span data-stu-id="991d0-204">Object definitions</span></span>
### <a name="emailrequest"></a><span data-ttu-id="991d0-205">EmailRequest</span><span class="sxs-lookup"><span data-stu-id="991d0-205">EmailRequest</span></span>
| <span data-ttu-id="991d0-206">Property Name</span><span class="sxs-lookup"><span data-stu-id="991d0-206">Property Name</span></span> | <span data-ttu-id="991d0-207">Data Type</span><span class="sxs-lookup"><span data-stu-id="991d0-207">Data Type</span></span> | <span data-ttu-id="991d0-208">Required</span><span class="sxs-lookup"><span data-stu-id="991d0-208">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="991d0-209">from</span><span class="sxs-lookup"><span data-stu-id="991d0-209">from</span></span> |<span data-ttu-id="991d0-210">string</span><span class="sxs-lookup"><span data-stu-id="991d0-210">string</span></span> |<span data-ttu-id="991d0-211">Yes</span><span class="sxs-lookup"><span data-stu-id="991d0-211">Yes</span></span> |
| <span data-ttu-id="991d0-212">fromname</span><span class="sxs-lookup"><span data-stu-id="991d0-212">fromname</span></span> |<span data-ttu-id="991d0-213">string</span><span class="sxs-lookup"><span data-stu-id="991d0-213">string</span></span> |<span data-ttu-id="991d0-214">No</span><span class="sxs-lookup"><span data-stu-id="991d0-214">No</span></span> |
| <span data-ttu-id="991d0-215">to</span><span class="sxs-lookup"><span data-stu-id="991d0-215">to</span></span> |<span data-ttu-id="991d0-216">string</span><span class="sxs-lookup"><span data-stu-id="991d0-216">string</span></span> |<span data-ttu-id="991d0-217">Yes</span><span class="sxs-lookup"><span data-stu-id="991d0-217">Yes</span></span> |
| <span data-ttu-id="991d0-218">toname</span><span class="sxs-lookup"><span data-stu-id="991d0-218">toname</span></span> |<span data-ttu-id="991d0-219">string</span><span class="sxs-lookup"><span data-stu-id="991d0-219">string</span></span> |<span data-ttu-id="991d0-220">No</span><span class="sxs-lookup"><span data-stu-id="991d0-220">No</span></span> |
| <span data-ttu-id="991d0-221">subject</span><span class="sxs-lookup"><span data-stu-id="991d0-221">subject</span></span> |<span data-ttu-id="991d0-222">string</span><span class="sxs-lookup"><span data-stu-id="991d0-222">string</span></span> |<span data-ttu-id="991d0-223">Yes</span><span class="sxs-lookup"><span data-stu-id="991d0-223">Yes</span></span> |
| <span data-ttu-id="991d0-224">body</span><span class="sxs-lookup"><span data-stu-id="991d0-224">body</span></span> |<span data-ttu-id="991d0-225">string</span><span class="sxs-lookup"><span data-stu-id="991d0-225">string</span></span> |<span data-ttu-id="991d0-226">Yes</span><span class="sxs-lookup"><span data-stu-id="991d0-226">Yes</span></span> |
| <span data-ttu-id="991d0-227">ishtml</span><span class="sxs-lookup"><span data-stu-id="991d0-227">ishtml</span></span> |<span data-ttu-id="991d0-228">boolean</span><span class="sxs-lookup"><span data-stu-id="991d0-228">boolean</span></span> |<span data-ttu-id="991d0-229">No</span><span class="sxs-lookup"><span data-stu-id="991d0-229">No</span></span> |
| <span data-ttu-id="991d0-230">cc</span><span class="sxs-lookup"><span data-stu-id="991d0-230">cc</span></span> |<span data-ttu-id="991d0-231">string</span><span class="sxs-lookup"><span data-stu-id="991d0-231">string</span></span> |<span data-ttu-id="991d0-232">No</span><span class="sxs-lookup"><span data-stu-id="991d0-232">No</span></span> |
| <span data-ttu-id="991d0-233">ccname</span><span class="sxs-lookup"><span data-stu-id="991d0-233">ccname</span></span> |<span data-ttu-id="991d0-234">string</span><span class="sxs-lookup"><span data-stu-id="991d0-234">string</span></span> |<span data-ttu-id="991d0-235">No</span><span class="sxs-lookup"><span data-stu-id="991d0-235">No</span></span> |
| <span data-ttu-id="991d0-236">bcc</span><span class="sxs-lookup"><span data-stu-id="991d0-236">bcc</span></span> |<span data-ttu-id="991d0-237">string</span><span class="sxs-lookup"><span data-stu-id="991d0-237">string</span></span> |<span data-ttu-id="991d0-238">No</span><span class="sxs-lookup"><span data-stu-id="991d0-238">No</span></span> |
| <span data-ttu-id="991d0-239">bccname</span><span class="sxs-lookup"><span data-stu-id="991d0-239">bccname</span></span> |<span data-ttu-id="991d0-240">string</span><span class="sxs-lookup"><span data-stu-id="991d0-240">string</span></span> |<span data-ttu-id="991d0-241">No</span><span class="sxs-lookup"><span data-stu-id="991d0-241">No</span></span> |
| <span data-ttu-id="991d0-242">replyto</span><span class="sxs-lookup"><span data-stu-id="991d0-242">replyto</span></span> |<span data-ttu-id="991d0-243">string</span><span class="sxs-lookup"><span data-stu-id="991d0-243">string</span></span> |<span data-ttu-id="991d0-244">No</span><span class="sxs-lookup"><span data-stu-id="991d0-244">No</span></span> |
| <span data-ttu-id="991d0-245">date</span><span class="sxs-lookup"><span data-stu-id="991d0-245">date</span></span> |<span data-ttu-id="991d0-246">string</span><span class="sxs-lookup"><span data-stu-id="991d0-246">string</span></span> |<span data-ttu-id="991d0-247">No</span><span class="sxs-lookup"><span data-stu-id="991d0-247">No</span></span> |
| <span data-ttu-id="991d0-248">headers</span><span class="sxs-lookup"><span data-stu-id="991d0-248">headers</span></span> |<span data-ttu-id="991d0-249">string</span><span class="sxs-lookup"><span data-stu-id="991d0-249">string</span></span> |<span data-ttu-id="991d0-250">No</span><span class="sxs-lookup"><span data-stu-id="991d0-250">No</span></span> |
| <span data-ttu-id="991d0-251">files</span><span class="sxs-lookup"><span data-stu-id="991d0-251">files</span></span> |<span data-ttu-id="991d0-252">array</span><span class="sxs-lookup"><span data-stu-id="991d0-252">array</span></span> |<span data-ttu-id="991d0-253">No</span><span class="sxs-lookup"><span data-stu-id="991d0-253">No</span></span> |
| <span data-ttu-id="991d0-254">filenames</span><span class="sxs-lookup"><span data-stu-id="991d0-254">filenames</span></span> |<span data-ttu-id="991d0-255">array</span><span class="sxs-lookup"><span data-stu-id="991d0-255">array</span></span> |<span data-ttu-id="991d0-256">No</span><span class="sxs-lookup"><span data-stu-id="991d0-256">No</span></span> |

### <a name="emailresponse"></a><span data-ttu-id="991d0-257">EmailResponse</span><span class="sxs-lookup"><span data-stu-id="991d0-257">EmailResponse</span></span>
| <span data-ttu-id="991d0-258">Property Name</span><span class="sxs-lookup"><span data-stu-id="991d0-258">Property Name</span></span> | <span data-ttu-id="991d0-259">Data Type</span><span class="sxs-lookup"><span data-stu-id="991d0-259">Data Type</span></span> | <span data-ttu-id="991d0-260">Required</span><span class="sxs-lookup"><span data-stu-id="991d0-260">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="991d0-261">message</span><span class="sxs-lookup"><span data-stu-id="991d0-261">message</span></span> |<span data-ttu-id="991d0-262">string</span><span class="sxs-lookup"><span data-stu-id="991d0-262">string</span></span> |<span data-ttu-id="991d0-263">No</span><span class="sxs-lookup"><span data-stu-id="991d0-263">No</span></span> |

### <a name="recipientlists"></a><span data-ttu-id="991d0-264">RecipientLists</span><span class="sxs-lookup"><span data-stu-id="991d0-264">RecipientLists</span></span>
| <span data-ttu-id="991d0-265">Property Name</span><span class="sxs-lookup"><span data-stu-id="991d0-265">Property Name</span></span> | <span data-ttu-id="991d0-266">Data Type</span><span class="sxs-lookup"><span data-stu-id="991d0-266">Data Type</span></span> | <span data-ttu-id="991d0-267">Required</span><span class="sxs-lookup"><span data-stu-id="991d0-267">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="991d0-268">lists</span><span class="sxs-lookup"><span data-stu-id="991d0-268">lists</span></span> |<span data-ttu-id="991d0-269">array</span><span class="sxs-lookup"><span data-stu-id="991d0-269">array</span></span> |<span data-ttu-id="991d0-270">No</span><span class="sxs-lookup"><span data-stu-id="991d0-270">No</span></span> |

### <a name="recipientlist"></a><span data-ttu-id="991d0-271">RecipientList</span><span class="sxs-lookup"><span data-stu-id="991d0-271">RecipientList</span></span>
| <span data-ttu-id="991d0-272">Property Name</span><span class="sxs-lookup"><span data-stu-id="991d0-272">Property Name</span></span> | <span data-ttu-id="991d0-273">Data Type</span><span class="sxs-lookup"><span data-stu-id="991d0-273">Data Type</span></span> | <span data-ttu-id="991d0-274">Required</span><span class="sxs-lookup"><span data-stu-id="991d0-274">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="991d0-275">id</span><span class="sxs-lookup"><span data-stu-id="991d0-275">id</span></span> |<span data-ttu-id="991d0-276">integer</span><span class="sxs-lookup"><span data-stu-id="991d0-276">integer</span></span> |<span data-ttu-id="991d0-277">No</span><span class="sxs-lookup"><span data-stu-id="991d0-277">No</span></span> |
| <span data-ttu-id="991d0-278">name</span><span class="sxs-lookup"><span data-stu-id="991d0-278">name</span></span> |<span data-ttu-id="991d0-279">string</span><span class="sxs-lookup"><span data-stu-id="991d0-279">string</span></span> |<span data-ttu-id="991d0-280">No</span><span class="sxs-lookup"><span data-stu-id="991d0-280">No</span></span> |
| <span data-ttu-id="991d0-281">recipient_count</span><span class="sxs-lookup"><span data-stu-id="991d0-281">recipient_count</span></span> |<span data-ttu-id="991d0-282">integer</span><span class="sxs-lookup"><span data-stu-id="991d0-282">integer</span></span> |<span data-ttu-id="991d0-283">No</span><span class="sxs-lookup"><span data-stu-id="991d0-283">No</span></span> |

### <a name="recipients"></a><span data-ttu-id="991d0-284">Recipients</span><span class="sxs-lookup"><span data-stu-id="991d0-284">Recipients</span></span>
| <span data-ttu-id="991d0-285">Property Name</span><span class="sxs-lookup"><span data-stu-id="991d0-285">Property Name</span></span> | <span data-ttu-id="991d0-286">Data Type</span><span class="sxs-lookup"><span data-stu-id="991d0-286">Data Type</span></span> | <span data-ttu-id="991d0-287">Required</span><span class="sxs-lookup"><span data-stu-id="991d0-287">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="991d0-288">recipients</span><span class="sxs-lookup"><span data-stu-id="991d0-288">recipients</span></span> |<span data-ttu-id="991d0-289">array</span><span class="sxs-lookup"><span data-stu-id="991d0-289">array</span></span> |<span data-ttu-id="991d0-290">No</span><span class="sxs-lookup"><span data-stu-id="991d0-290">No</span></span> |

### <a name="recipient"></a><span data-ttu-id="991d0-291">Recipient</span><span class="sxs-lookup"><span data-stu-id="991d0-291">Recipient</span></span>
| <span data-ttu-id="991d0-292">Property Name</span><span class="sxs-lookup"><span data-stu-id="991d0-292">Property Name</span></span> | <span data-ttu-id="991d0-293">Data Type</span><span class="sxs-lookup"><span data-stu-id="991d0-293">Data Type</span></span> | <span data-ttu-id="991d0-294">Required</span><span class="sxs-lookup"><span data-stu-id="991d0-294">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="991d0-295">email</span><span class="sxs-lookup"><span data-stu-id="991d0-295">email</span></span> |<span data-ttu-id="991d0-296">string</span><span class="sxs-lookup"><span data-stu-id="991d0-296">string</span></span> |<span data-ttu-id="991d0-297">No</span><span class="sxs-lookup"><span data-stu-id="991d0-297">No</span></span> |
| <span data-ttu-id="991d0-298">last_name</span><span class="sxs-lookup"><span data-stu-id="991d0-298">last_name</span></span> |<span data-ttu-id="991d0-299">string</span><span class="sxs-lookup"><span data-stu-id="991d0-299">string</span></span> |<span data-ttu-id="991d0-300">No</span><span class="sxs-lookup"><span data-stu-id="991d0-300">No</span></span> |
| <span data-ttu-id="991d0-301">first_name</span><span class="sxs-lookup"><span data-stu-id="991d0-301">first_name</span></span> |<span data-ttu-id="991d0-302">string</span><span class="sxs-lookup"><span data-stu-id="991d0-302">string</span></span> |<span data-ttu-id="991d0-303">No</span><span class="sxs-lookup"><span data-stu-id="991d0-303">No</span></span> |
| <span data-ttu-id="991d0-304">id</span><span class="sxs-lookup"><span data-stu-id="991d0-304">id</span></span> |<span data-ttu-id="991d0-305">string</span><span class="sxs-lookup"><span data-stu-id="991d0-305">string</span></span> |<span data-ttu-id="991d0-306">No</span><span class="sxs-lookup"><span data-stu-id="991d0-306">No</span></span> |

## <a name="next-steps"></a><span data-ttu-id="991d0-307">Next Steps</span><span class="sxs-lookup"><span data-stu-id="991d0-307">Next Steps</span></span>
[<span data-ttu-id="991d0-308">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="991d0-308">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

