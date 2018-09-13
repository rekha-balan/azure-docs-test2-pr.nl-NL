---
title: " Use the Slack Connector in your Logic apps| Microsoft Docs"
description: Get started using the Slack Connector in your logic apps
services: ''
documentationcenter: ''
author: msftman
manager: anneta
editor: ''
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: deonhe
ms.openlocfilehash: 9ed8810af33b9fdbd0c56c41781011a6471e7e48
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550430"
---
# <a name="get-started-with-the-slack-connector"></a><span data-ttu-id="62053-103">Get started with the Slack connector</span><span class="sxs-lookup"><span data-stu-id="62053-103">Get started with the Slack connector</span></span>
<span data-ttu-id="62053-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span><span class="sxs-lookup"><span data-stu-id="62053-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span>

> [!NOTE]
> <span data-ttu-id="62053-105">This version of the article applies to logic apps 2015-08-01-preview schema version.</span><span class="sxs-lookup"><span data-stu-id="62053-105">This version of the article applies to logic apps 2015-08-01-preview schema version.</span></span>
> 
> 

<span data-ttu-id="62053-106">With the Slack connector, you can:</span><span class="sxs-lookup"><span data-stu-id="62053-106">With the Slack connector, you can:</span></span>

* <span data-ttu-id="62053-107">Use it to build logic apps</span><span class="sxs-lookup"><span data-stu-id="62053-107">Use it to build logic apps</span></span>

<span data-ttu-id="62053-108">To add an operation in logic apps, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="62053-108">To add an operation in logic apps, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="lets-talk-about-triggers-and-actions"></a><span data-ttu-id="62053-109">Let's talk about triggers and actions</span><span class="sxs-lookup"><span data-stu-id="62053-109">Let's talk about triggers and actions</span></span>
<span data-ttu-id="62053-110">The Slack connector can be used as an action; there are no triggers.</span><span class="sxs-lookup"><span data-stu-id="62053-110">The Slack connector can be used as an action; there are no triggers.</span></span> <span data-ttu-id="62053-111">All connectors support data in JSON and XML formats.</span><span class="sxs-lookup"><span data-stu-id="62053-111">All connectors support data in JSON and XML formats.</span></span> 

 <span data-ttu-id="62053-112">The Slack connector has the following action(s) and/or trigger(s) available:</span><span class="sxs-lookup"><span data-stu-id="62053-112">The Slack connector has the following action(s) and/or trigger(s) available:</span></span>

### <a name="slack-actions"></a><span data-ttu-id="62053-113">Slack actions</span><span class="sxs-lookup"><span data-stu-id="62053-113">Slack actions</span></span>
<span data-ttu-id="62053-114">You can take these action(s):</span><span class="sxs-lookup"><span data-stu-id="62053-114">You can take these action(s):</span></span>

| <span data-ttu-id="62053-115">Action</span><span class="sxs-lookup"><span data-stu-id="62053-115">Action</span></span> | <span data-ttu-id="62053-116">Description</span><span class="sxs-lookup"><span data-stu-id="62053-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="62053-117">PostMessage</span><span class="sxs-lookup"><span data-stu-id="62053-117">PostMessage</span></span> |<span data-ttu-id="62053-118">Post a Message to a specified channel.</span><span class="sxs-lookup"><span data-stu-id="62053-118">Post a Message to a specified channel.</span></span> |

## <a name="create-a-connection-to-slack"></a><span data-ttu-id="62053-119">Create a connection to Slack</span><span class="sxs-lookup"><span data-stu-id="62053-119">Create a connection to Slack</span></span>
<span data-ttu-id="62053-120">To use the Slack connector, you first create a **connection** then provide the details for these properties:</span><span class="sxs-lookup"><span data-stu-id="62053-120">To use the Slack connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="62053-121">Property</span><span class="sxs-lookup"><span data-stu-id="62053-121">Property</span></span> | <span data-ttu-id="62053-122">Required</span><span class="sxs-lookup"><span data-stu-id="62053-122">Required</span></span> | <span data-ttu-id="62053-123">Description</span><span class="sxs-lookup"><span data-stu-id="62053-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62053-124">Token</span><span class="sxs-lookup"><span data-stu-id="62053-124">Token</span></span> |<span data-ttu-id="62053-125">Yes</span><span class="sxs-lookup"><span data-stu-id="62053-125">Yes</span></span> |<span data-ttu-id="62053-126">Provide Slack Credentials</span><span class="sxs-lookup"><span data-stu-id="62053-126">Provide Slack Credentials</span></span> |

<span data-ttu-id="62053-127">Follow these steps to sign into Slack and complete the configuration of the Slack **connection** in your logic app:</span><span class="sxs-lookup"><span data-stu-id="62053-127">Follow these steps to sign into Slack and complete the configuration of the Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="62053-128">Select **Recurrence**</span><span class="sxs-lookup"><span data-stu-id="62053-128">Select **Recurrence**</span></span>
2. <span data-ttu-id="62053-129">Select a **Frequency** and enter an **Interval**</span><span class="sxs-lookup"><span data-stu-id="62053-129">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="62053-130">Select **Add an action**</span><span class="sxs-lookup"><span data-stu-id="62053-130">Select **Add an action**</span></span>  
   <span data-ttu-id="62053-131">![Configure Slack][1]</span><span class="sxs-lookup"><span data-stu-id="62053-131">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="62053-132">Enter Slack in the search box and wait for the search to return all entries with Slack in the name</span><span class="sxs-lookup"><span data-stu-id="62053-132">Enter Slack in the search box and wait for the search to return all entries with Slack in the name</span></span>
5. <span data-ttu-id="62053-133">Select **Slack - Post message**</span><span class="sxs-lookup"><span data-stu-id="62053-133">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="62053-134">Select **Sign in to Slack**:</span><span class="sxs-lookup"><span data-stu-id="62053-134">Select **Sign in to Slack**:</span></span>  
   <span data-ttu-id="62053-135">![Configure Slack][2]</span><span class="sxs-lookup"><span data-stu-id="62053-135">![Configure Slack][2]</span></span>
7. <span data-ttu-id="62053-136">Provide your Slack credentials to sign in to authorize the  application</span><span class="sxs-lookup"><span data-stu-id="62053-136">Provide your Slack credentials to sign in to authorize the  application</span></span>    
   ![Configure Slack][3]  
8. <span data-ttu-id="62053-138">You'll be redirected to your organization's Log in page.</span><span class="sxs-lookup"><span data-stu-id="62053-138">You'll be redirected to your organization's Log in page.</span></span> <span data-ttu-id="62053-139">**Authorize** Slack to interact with your logic app:</span><span class="sxs-lookup"><span data-stu-id="62053-139">**Authorize** Slack to interact with your logic app:</span></span>      
   <span data-ttu-id="62053-140">![Configure Slack][5]</span><span class="sxs-lookup"><span data-stu-id="62053-140">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="62053-141">After the authorization completes you'll be redirected to your logic app to complete it by configuring the **Slack - Get all messages** section.</span><span class="sxs-lookup"><span data-stu-id="62053-141">After the authorization completes you'll be redirected to your logic app to complete it by configuring the **Slack - Get all messages** section.</span></span> <span data-ttu-id="62053-142">Add other triggers and actions that you need.</span><span class="sxs-lookup"><span data-stu-id="62053-142">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="62053-143">![Configure Slack][6]</span><span class="sxs-lookup"><span data-stu-id="62053-143">![Configure Slack][6]</span></span>
10. <span data-ttu-id="62053-144">Save your work by selecting **Save** on the menu bar above.</span><span class="sxs-lookup"><span data-stu-id="62053-144">Save your work by selecting **Save** on the menu bar above.</span></span>

> [!TIP]
> <span data-ttu-id="62053-145">You can use this connection in other logic apps.</span><span class="sxs-lookup"><span data-stu-id="62053-145">You can use this connection in other logic apps.</span></span>
> 
> 

## <a name="slack-rest-api-reference"></a><span data-ttu-id="62053-146">Slack REST API reference</span><span class="sxs-lookup"><span data-stu-id="62053-146">Slack REST API reference</span></span>
#### <a name="this-documentation-is-for-version-10"></a><span data-ttu-id="62053-147">This documentation is for version: 1.0</span><span class="sxs-lookup"><span data-stu-id="62053-147">This documentation is for version: 1.0</span></span>
### <a name="post-a-message-to-a-specified-channel"></a><span data-ttu-id="62053-148">Post a Message to a specified channel.</span><span class="sxs-lookup"><span data-stu-id="62053-148">Post a Message to a specified channel.</span></span>
**```POST: /chat.postMessage```** 

| <span data-ttu-id="62053-149">Name</span><span class="sxs-lookup"><span data-stu-id="62053-149">Name</span></span> | <span data-ttu-id="62053-150">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-150">Data Type</span></span> | <span data-ttu-id="62053-151">Required</span><span class="sxs-lookup"><span data-stu-id="62053-151">Required</span></span> | <span data-ttu-id="62053-152">Located In</span><span class="sxs-lookup"><span data-stu-id="62053-152">Located In</span></span> | <span data-ttu-id="62053-153">Default Value</span><span class="sxs-lookup"><span data-stu-id="62053-153">Default Value</span></span> | <span data-ttu-id="62053-154">Description</span><span class="sxs-lookup"><span data-stu-id="62053-154">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="62053-155">channel</span><span class="sxs-lookup"><span data-stu-id="62053-155">channel</span></span> |<span data-ttu-id="62053-156">string</span><span class="sxs-lookup"><span data-stu-id="62053-156">string</span></span> |<span data-ttu-id="62053-157">yes</span><span class="sxs-lookup"><span data-stu-id="62053-157">yes</span></span> |<span data-ttu-id="62053-158">query</span><span class="sxs-lookup"><span data-stu-id="62053-158">query</span></span> |<span data-ttu-id="62053-159">none</span><span class="sxs-lookup"><span data-stu-id="62053-159">none</span></span> |<span data-ttu-id="62053-160">Channel, private group, or IM channel to send message to.</span><span class="sxs-lookup"><span data-stu-id="62053-160">Channel, private group, or IM channel to send message to.</span></span> <span data-ttu-id="62053-161">Can be a name(ex: #general) or an encoded ID.</span><span class="sxs-lookup"><span data-stu-id="62053-161">Can be a name(ex: #general) or an encoded ID.</span></span> |
| <span data-ttu-id="62053-162">text</span><span class="sxs-lookup"><span data-stu-id="62053-162">text</span></span> |<span data-ttu-id="62053-163">string</span><span class="sxs-lookup"><span data-stu-id="62053-163">string</span></span> |<span data-ttu-id="62053-164">yes</span><span class="sxs-lookup"><span data-stu-id="62053-164">yes</span></span> |<span data-ttu-id="62053-165">query</span><span class="sxs-lookup"><span data-stu-id="62053-165">query</span></span> |<span data-ttu-id="62053-166">none</span><span class="sxs-lookup"><span data-stu-id="62053-166">none</span></span> |<span data-ttu-id="62053-167">Text of the message to send.</span><span class="sxs-lookup"><span data-stu-id="62053-167">Text of the message to send.</span></span> <span data-ttu-id="62053-168">For formatting options, see https://api.slack.com/docs/formatting.</span><span class="sxs-lookup"><span data-stu-id="62053-168">For formatting options, see https://api.slack.com/docs/formatting.</span></span> |
| <span data-ttu-id="62053-169">username</span><span class="sxs-lookup"><span data-stu-id="62053-169">username</span></span> |<span data-ttu-id="62053-170">string</span><span class="sxs-lookup"><span data-stu-id="62053-170">string</span></span> |<span data-ttu-id="62053-171">no</span><span class="sxs-lookup"><span data-stu-id="62053-171">no</span></span> |<span data-ttu-id="62053-172">query</span><span class="sxs-lookup"><span data-stu-id="62053-172">query</span></span> |<span data-ttu-id="62053-173">none</span><span class="sxs-lookup"><span data-stu-id="62053-173">none</span></span> |<span data-ttu-id="62053-174">Name of the bot</span><span class="sxs-lookup"><span data-stu-id="62053-174">Name of the bot</span></span> |
| <span data-ttu-id="62053-175">as_user</span><span class="sxs-lookup"><span data-stu-id="62053-175">as_user</span></span> |<span data-ttu-id="62053-176">boolean</span><span class="sxs-lookup"><span data-stu-id="62053-176">boolean</span></span> |<span data-ttu-id="62053-177">no</span><span class="sxs-lookup"><span data-stu-id="62053-177">no</span></span> |<span data-ttu-id="62053-178">query</span><span class="sxs-lookup"><span data-stu-id="62053-178">query</span></span> |<span data-ttu-id="62053-179">none</span><span class="sxs-lookup"><span data-stu-id="62053-179">none</span></span> |<span data-ttu-id="62053-180">Pass true to post the message as the authenticated user, instead of as a bot</span><span class="sxs-lookup"><span data-stu-id="62053-180">Pass true to post the message as the authenticated user, instead of as a bot</span></span> |
| <span data-ttu-id="62053-181">parse</span><span class="sxs-lookup"><span data-stu-id="62053-181">parse</span></span> |<span data-ttu-id="62053-182">string</span><span class="sxs-lookup"><span data-stu-id="62053-182">string</span></span> |<span data-ttu-id="62053-183">no</span><span class="sxs-lookup"><span data-stu-id="62053-183">no</span></span> |<span data-ttu-id="62053-184">query</span><span class="sxs-lookup"><span data-stu-id="62053-184">query</span></span> |<span data-ttu-id="62053-185">none</span><span class="sxs-lookup"><span data-stu-id="62053-185">none</span></span> |<span data-ttu-id="62053-186">Change how messages are treated.</span><span class="sxs-lookup"><span data-stu-id="62053-186">Change how messages are treated.</span></span> <span data-ttu-id="62053-187">For details, see https://api.slack.com/docs/formatting.</span><span class="sxs-lookup"><span data-stu-id="62053-187">For details, see https://api.slack.com/docs/formatting.</span></span> |
| <span data-ttu-id="62053-188">link_names</span><span class="sxs-lookup"><span data-stu-id="62053-188">link_names</span></span> |<span data-ttu-id="62053-189">integer</span><span class="sxs-lookup"><span data-stu-id="62053-189">integer</span></span> |<span data-ttu-id="62053-190">no</span><span class="sxs-lookup"><span data-stu-id="62053-190">no</span></span> |<span data-ttu-id="62053-191">query</span><span class="sxs-lookup"><span data-stu-id="62053-191">query</span></span> |<span data-ttu-id="62053-192">none</span><span class="sxs-lookup"><span data-stu-id="62053-192">none</span></span> |<span data-ttu-id="62053-193">Find and link channel names and usernames.</span><span class="sxs-lookup"><span data-stu-id="62053-193">Find and link channel names and usernames.</span></span> |
| <span data-ttu-id="62053-194">unfurl_links</span><span class="sxs-lookup"><span data-stu-id="62053-194">unfurl_links</span></span> |<span data-ttu-id="62053-195">boolean</span><span class="sxs-lookup"><span data-stu-id="62053-195">boolean</span></span> |<span data-ttu-id="62053-196">no</span><span class="sxs-lookup"><span data-stu-id="62053-196">no</span></span> |<span data-ttu-id="62053-197">query</span><span class="sxs-lookup"><span data-stu-id="62053-197">query</span></span> |<span data-ttu-id="62053-198">none</span><span class="sxs-lookup"><span data-stu-id="62053-198">none</span></span> |<span data-ttu-id="62053-199">Pass true to enable unfurling of primarily text-based content.</span><span class="sxs-lookup"><span data-stu-id="62053-199">Pass true to enable unfurling of primarily text-based content.</span></span> |
| <span data-ttu-id="62053-200">unfurl_media</span><span class="sxs-lookup"><span data-stu-id="62053-200">unfurl_media</span></span> |<span data-ttu-id="62053-201">boolean</span><span class="sxs-lookup"><span data-stu-id="62053-201">boolean</span></span> |<span data-ttu-id="62053-202">no</span><span class="sxs-lookup"><span data-stu-id="62053-202">no</span></span> |<span data-ttu-id="62053-203">query</span><span class="sxs-lookup"><span data-stu-id="62053-203">query</span></span> |<span data-ttu-id="62053-204">none</span><span class="sxs-lookup"><span data-stu-id="62053-204">none</span></span> |<span data-ttu-id="62053-205">Pass false to disable unfurling of media content.</span><span class="sxs-lookup"><span data-stu-id="62053-205">Pass false to disable unfurling of media content.</span></span> |
| <span data-ttu-id="62053-206">icon_url</span><span class="sxs-lookup"><span data-stu-id="62053-206">icon_url</span></span> |<span data-ttu-id="62053-207">string</span><span class="sxs-lookup"><span data-stu-id="62053-207">string</span></span> |<span data-ttu-id="62053-208">no</span><span class="sxs-lookup"><span data-stu-id="62053-208">no</span></span> |<span data-ttu-id="62053-209">query</span><span class="sxs-lookup"><span data-stu-id="62053-209">query</span></span> |<span data-ttu-id="62053-210">none</span><span class="sxs-lookup"><span data-stu-id="62053-210">none</span></span> |<span data-ttu-id="62053-211">URL to an image to use as an icon for this message</span><span class="sxs-lookup"><span data-stu-id="62053-211">URL to an image to use as an icon for this message</span></span> |
| <span data-ttu-id="62053-212">icon_emoji</span><span class="sxs-lookup"><span data-stu-id="62053-212">icon_emoji</span></span> |<span data-ttu-id="62053-213">string</span><span class="sxs-lookup"><span data-stu-id="62053-213">string</span></span> |<span data-ttu-id="62053-214">no</span><span class="sxs-lookup"><span data-stu-id="62053-214">no</span></span> |<span data-ttu-id="62053-215">query</span><span class="sxs-lookup"><span data-stu-id="62053-215">query</span></span> |<span data-ttu-id="62053-216">none</span><span class="sxs-lookup"><span data-stu-id="62053-216">none</span></span> |<span data-ttu-id="62053-217">Emoji to use as an icon for this message</span><span class="sxs-lookup"><span data-stu-id="62053-217">Emoji to use as an icon for this message</span></span> |

### <a name="here-are-the-possible-responses"></a><span data-ttu-id="62053-218">Here are the possible responses:</span><span class="sxs-lookup"><span data-stu-id="62053-218">Here are the possible responses:</span></span>
| <span data-ttu-id="62053-219">Name</span><span class="sxs-lookup"><span data-stu-id="62053-219">Name</span></span> | <span data-ttu-id="62053-220">Description</span><span class="sxs-lookup"><span data-stu-id="62053-220">Description</span></span> |
| --- | --- |
| <span data-ttu-id="62053-221">200</span><span class="sxs-lookup"><span data-stu-id="62053-221">200</span></span> |<span data-ttu-id="62053-222">OK</span><span class="sxs-lookup"><span data-stu-id="62053-222">OK</span></span> |
| <span data-ttu-id="62053-223">400</span><span class="sxs-lookup"><span data-stu-id="62053-223">400</span></span> |<span data-ttu-id="62053-224">Bad Request</span><span class="sxs-lookup"><span data-stu-id="62053-224">Bad Request</span></span> |
| <span data-ttu-id="62053-225">408</span><span class="sxs-lookup"><span data-stu-id="62053-225">408</span></span> |<span data-ttu-id="62053-226">Request Timeout</span><span class="sxs-lookup"><span data-stu-id="62053-226">Request Timeout</span></span> |
| <span data-ttu-id="62053-227">429</span><span class="sxs-lookup"><span data-stu-id="62053-227">429</span></span> |<span data-ttu-id="62053-228">Too Many Requests</span><span class="sxs-lookup"><span data-stu-id="62053-228">Too Many Requests</span></span> |
| <span data-ttu-id="62053-229">500</span><span class="sxs-lookup"><span data-stu-id="62053-229">500</span></span> |<span data-ttu-id="62053-230">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="62053-230">Internal Server Error.</span></span> <span data-ttu-id="62053-231">Unknown error occured</span><span class="sxs-lookup"><span data-stu-id="62053-231">Unknown error occured</span></span> |
| <span data-ttu-id="62053-232">503</span><span class="sxs-lookup"><span data-stu-id="62053-232">503</span></span> |<span data-ttu-id="62053-233">Slack Service Unavailable</span><span class="sxs-lookup"><span data-stu-id="62053-233">Slack Service Unavailable</span></span> |
| <span data-ttu-id="62053-234">504</span><span class="sxs-lookup"><span data-stu-id="62053-234">504</span></span> |<span data-ttu-id="62053-235">Gateway Timeout</span><span class="sxs-lookup"><span data-stu-id="62053-235">Gateway Timeout</span></span> |
| <span data-ttu-id="62053-236">default</span><span class="sxs-lookup"><span data-stu-id="62053-236">default</span></span> |<span data-ttu-id="62053-237">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="62053-237">Operation Failed.</span></span> |

- - -
## <a name="object-definitions"></a><span data-ttu-id="62053-238">Object definition(s):</span><span class="sxs-lookup"><span data-stu-id="62053-238">Object definition(s):</span></span>
 <span data-ttu-id="62053-239">**Message**:Slack Message</span><span class="sxs-lookup"><span data-stu-id="62053-239">**Message**:Slack Message</span></span>

<span data-ttu-id="62053-240">Required properties for Message:</span><span class="sxs-lookup"><span data-stu-id="62053-240">Required properties for Message:</span></span>

<span data-ttu-id="62053-241">None of the properties are required.</span><span class="sxs-lookup"><span data-stu-id="62053-241">None of the properties are required.</span></span> 

<span data-ttu-id="62053-242">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-242">**All properties**:</span></span> 

| <span data-ttu-id="62053-243">Name</span><span class="sxs-lookup"><span data-stu-id="62053-243">Name</span></span> | <span data-ttu-id="62053-244">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-244">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-245">id</span><span class="sxs-lookup"><span data-stu-id="62053-245">id</span></span> |<span data-ttu-id="62053-246">integer</span><span class="sxs-lookup"><span data-stu-id="62053-246">integer</span></span> |
| <span data-ttu-id="62053-247">content_excerpt</span><span class="sxs-lookup"><span data-stu-id="62053-247">content_excerpt</span></span> |<span data-ttu-id="62053-248">string</span><span class="sxs-lookup"><span data-stu-id="62053-248">string</span></span> |
| <span data-ttu-id="62053-249">sender_id</span><span class="sxs-lookup"><span data-stu-id="62053-249">sender_id</span></span> |<span data-ttu-id="62053-250">integer</span><span class="sxs-lookup"><span data-stu-id="62053-250">integer</span></span> |
| <span data-ttu-id="62053-251">replied_to_id</span><span class="sxs-lookup"><span data-stu-id="62053-251">replied_to_id</span></span> |<span data-ttu-id="62053-252">integer</span><span class="sxs-lookup"><span data-stu-id="62053-252">integer</span></span> |
| <span data-ttu-id="62053-253">created_at</span><span class="sxs-lookup"><span data-stu-id="62053-253">created_at</span></span> |<span data-ttu-id="62053-254">string</span><span class="sxs-lookup"><span data-stu-id="62053-254">string</span></span> |
| <span data-ttu-id="62053-255">network_id</span><span class="sxs-lookup"><span data-stu-id="62053-255">network_id</span></span> |<span data-ttu-id="62053-256">integer</span><span class="sxs-lookup"><span data-stu-id="62053-256">integer</span></span> |
| <span data-ttu-id="62053-257">message_type</span><span class="sxs-lookup"><span data-stu-id="62053-257">message_type</span></span> |<span data-ttu-id="62053-258">string</span><span class="sxs-lookup"><span data-stu-id="62053-258">string</span></span> |
| <span data-ttu-id="62053-259">sender_type</span><span class="sxs-lookup"><span data-stu-id="62053-259">sender_type</span></span> |<span data-ttu-id="62053-260">string</span><span class="sxs-lookup"><span data-stu-id="62053-260">string</span></span> |
| <span data-ttu-id="62053-261">url</span><span class="sxs-lookup"><span data-stu-id="62053-261">url</span></span> |<span data-ttu-id="62053-262">string</span><span class="sxs-lookup"><span data-stu-id="62053-262">string</span></span> |
| <span data-ttu-id="62053-263">web_url</span><span class="sxs-lookup"><span data-stu-id="62053-263">web_url</span></span> |<span data-ttu-id="62053-264">string</span><span class="sxs-lookup"><span data-stu-id="62053-264">string</span></span> |
| <span data-ttu-id="62053-265">group_id</span><span class="sxs-lookup"><span data-stu-id="62053-265">group_id</span></span> |<span data-ttu-id="62053-266">integer</span><span class="sxs-lookup"><span data-stu-id="62053-266">integer</span></span> |
| <span data-ttu-id="62053-267">body</span><span class="sxs-lookup"><span data-stu-id="62053-267">body</span></span> |<span data-ttu-id="62053-268">not defined</span><span class="sxs-lookup"><span data-stu-id="62053-268">not defined</span></span> |
| <span data-ttu-id="62053-269">thread_id</span><span class="sxs-lookup"><span data-stu-id="62053-269">thread_id</span></span> |<span data-ttu-id="62053-270">integer</span><span class="sxs-lookup"><span data-stu-id="62053-270">integer</span></span> |
| <span data-ttu-id="62053-271">direct_message</span><span class="sxs-lookup"><span data-stu-id="62053-271">direct_message</span></span> |<span data-ttu-id="62053-272">boolean</span><span class="sxs-lookup"><span data-stu-id="62053-272">boolean</span></span> |
| <span data-ttu-id="62053-273">client_type</span><span class="sxs-lookup"><span data-stu-id="62053-273">client_type</span></span> |<span data-ttu-id="62053-274">string</span><span class="sxs-lookup"><span data-stu-id="62053-274">string</span></span> |
| <span data-ttu-id="62053-275">client_url</span><span class="sxs-lookup"><span data-stu-id="62053-275">client_url</span></span> |<span data-ttu-id="62053-276">string</span><span class="sxs-lookup"><span data-stu-id="62053-276">string</span></span> |
| <span data-ttu-id="62053-277">language</span><span class="sxs-lookup"><span data-stu-id="62053-277">language</span></span> |<span data-ttu-id="62053-278">string</span><span class="sxs-lookup"><span data-stu-id="62053-278">string</span></span> |
| <span data-ttu-id="62053-279">notified_user_ids</span><span class="sxs-lookup"><span data-stu-id="62053-279">notified_user_ids</span></span> |<span data-ttu-id="62053-280">array</span><span class="sxs-lookup"><span data-stu-id="62053-280">array</span></span> |
| <span data-ttu-id="62053-281">privacy</span><span class="sxs-lookup"><span data-stu-id="62053-281">privacy</span></span> |<span data-ttu-id="62053-282">string</span><span class="sxs-lookup"><span data-stu-id="62053-282">string</span></span> |
| <span data-ttu-id="62053-283">liked_by</span><span class="sxs-lookup"><span data-stu-id="62053-283">liked_by</span></span> |<span data-ttu-id="62053-284">not defined</span><span class="sxs-lookup"><span data-stu-id="62053-284">not defined</span></span> |
| <span data-ttu-id="62053-285">system_message</span><span class="sxs-lookup"><span data-stu-id="62053-285">system_message</span></span> |<span data-ttu-id="62053-286">boolean</span><span class="sxs-lookup"><span data-stu-id="62053-286">boolean</span></span> |

 <span data-ttu-id="62053-287">**PostOperationRequest**:Represents a post request for Slack Connector to post to Slack</span><span class="sxs-lookup"><span data-stu-id="62053-287">**PostOperationRequest**:Represents a post request for Slack Connector to post to Slack</span></span>

<span data-ttu-id="62053-288">Required properties for PostOperationRequest:</span><span class="sxs-lookup"><span data-stu-id="62053-288">Required properties for PostOperationRequest:</span></span>

<span data-ttu-id="62053-289">body</span><span class="sxs-lookup"><span data-stu-id="62053-289">body</span></span>

<span data-ttu-id="62053-290">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-290">**All properties**:</span></span> 

| <span data-ttu-id="62053-291">Name</span><span class="sxs-lookup"><span data-stu-id="62053-291">Name</span></span> | <span data-ttu-id="62053-292">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-292">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-293">body</span><span class="sxs-lookup"><span data-stu-id="62053-293">body</span></span> |<span data-ttu-id="62053-294">string</span><span class="sxs-lookup"><span data-stu-id="62053-294">string</span></span> |
| <span data-ttu-id="62053-295">group_id</span><span class="sxs-lookup"><span data-stu-id="62053-295">group_id</span></span> |<span data-ttu-id="62053-296">integer</span><span class="sxs-lookup"><span data-stu-id="62053-296">integer</span></span> |
| <span data-ttu-id="62053-297">replied_to_id</span><span class="sxs-lookup"><span data-stu-id="62053-297">replied_to_id</span></span> |<span data-ttu-id="62053-298">integer</span><span class="sxs-lookup"><span data-stu-id="62053-298">integer</span></span> |
| <span data-ttu-id="62053-299">direct_to_id</span><span class="sxs-lookup"><span data-stu-id="62053-299">direct_to_id</span></span> |<span data-ttu-id="62053-300">integer</span><span class="sxs-lookup"><span data-stu-id="62053-300">integer</span></span> |
| <span data-ttu-id="62053-301">broadcast</span><span class="sxs-lookup"><span data-stu-id="62053-301">broadcast</span></span> |<span data-ttu-id="62053-302">boolean</span><span class="sxs-lookup"><span data-stu-id="62053-302">boolean</span></span> |
| <span data-ttu-id="62053-303">topic1</span><span class="sxs-lookup"><span data-stu-id="62053-303">topic1</span></span> |<span data-ttu-id="62053-304">string</span><span class="sxs-lookup"><span data-stu-id="62053-304">string</span></span> |
| <span data-ttu-id="62053-305">topic2</span><span class="sxs-lookup"><span data-stu-id="62053-305">topic2</span></span> |<span data-ttu-id="62053-306">string</span><span class="sxs-lookup"><span data-stu-id="62053-306">string</span></span> |
| <span data-ttu-id="62053-307">topic3</span><span class="sxs-lookup"><span data-stu-id="62053-307">topic3</span></span> |<span data-ttu-id="62053-308">string</span><span class="sxs-lookup"><span data-stu-id="62053-308">string</span></span> |
| <span data-ttu-id="62053-309">topic4</span><span class="sxs-lookup"><span data-stu-id="62053-309">topic4</span></span> |<span data-ttu-id="62053-310">string</span><span class="sxs-lookup"><span data-stu-id="62053-310">string</span></span> |
| <span data-ttu-id="62053-311">topic5</span><span class="sxs-lookup"><span data-stu-id="62053-311">topic5</span></span> |<span data-ttu-id="62053-312">string</span><span class="sxs-lookup"><span data-stu-id="62053-312">string</span></span> |
| <span data-ttu-id="62053-313">topic6</span><span class="sxs-lookup"><span data-stu-id="62053-313">topic6</span></span> |<span data-ttu-id="62053-314">string</span><span class="sxs-lookup"><span data-stu-id="62053-314">string</span></span> |
| <span data-ttu-id="62053-315">topic7</span><span class="sxs-lookup"><span data-stu-id="62053-315">topic7</span></span> |<span data-ttu-id="62053-316">string</span><span class="sxs-lookup"><span data-stu-id="62053-316">string</span></span> |
| <span data-ttu-id="62053-317">topic8</span><span class="sxs-lookup"><span data-stu-id="62053-317">topic8</span></span> |<span data-ttu-id="62053-318">string</span><span class="sxs-lookup"><span data-stu-id="62053-318">string</span></span> |
| <span data-ttu-id="62053-319">topic9</span><span class="sxs-lookup"><span data-stu-id="62053-319">topic9</span></span> |<span data-ttu-id="62053-320">string</span><span class="sxs-lookup"><span data-stu-id="62053-320">string</span></span> |
| <span data-ttu-id="62053-321">topic10</span><span class="sxs-lookup"><span data-stu-id="62053-321">topic10</span></span> |<span data-ttu-id="62053-322">string</span><span class="sxs-lookup"><span data-stu-id="62053-322">string</span></span> |
| <span data-ttu-id="62053-323">topic11</span><span class="sxs-lookup"><span data-stu-id="62053-323">topic11</span></span> |<span data-ttu-id="62053-324">string</span><span class="sxs-lookup"><span data-stu-id="62053-324">string</span></span> |
| <span data-ttu-id="62053-325">topic12</span><span class="sxs-lookup"><span data-stu-id="62053-325">topic12</span></span> |<span data-ttu-id="62053-326">string</span><span class="sxs-lookup"><span data-stu-id="62053-326">string</span></span> |
| <span data-ttu-id="62053-327">topic13</span><span class="sxs-lookup"><span data-stu-id="62053-327">topic13</span></span> |<span data-ttu-id="62053-328">string</span><span class="sxs-lookup"><span data-stu-id="62053-328">string</span></span> |
| <span data-ttu-id="62053-329">topic14</span><span class="sxs-lookup"><span data-stu-id="62053-329">topic14</span></span> |<span data-ttu-id="62053-330">string</span><span class="sxs-lookup"><span data-stu-id="62053-330">string</span></span> |
| <span data-ttu-id="62053-331">topic15</span><span class="sxs-lookup"><span data-stu-id="62053-331">topic15</span></span> |<span data-ttu-id="62053-332">string</span><span class="sxs-lookup"><span data-stu-id="62053-332">string</span></span> |
| <span data-ttu-id="62053-333">topic16</span><span class="sxs-lookup"><span data-stu-id="62053-333">topic16</span></span> |<span data-ttu-id="62053-334">string</span><span class="sxs-lookup"><span data-stu-id="62053-334">string</span></span> |
| <span data-ttu-id="62053-335">topic17</span><span class="sxs-lookup"><span data-stu-id="62053-335">topic17</span></span> |<span data-ttu-id="62053-336">string</span><span class="sxs-lookup"><span data-stu-id="62053-336">string</span></span> |
| <span data-ttu-id="62053-337">topic18</span><span class="sxs-lookup"><span data-stu-id="62053-337">topic18</span></span> |<span data-ttu-id="62053-338">string</span><span class="sxs-lookup"><span data-stu-id="62053-338">string</span></span> |
| <span data-ttu-id="62053-339">topic19</span><span class="sxs-lookup"><span data-stu-id="62053-339">topic19</span></span> |<span data-ttu-id="62053-340">string</span><span class="sxs-lookup"><span data-stu-id="62053-340">string</span></span> |
| <span data-ttu-id="62053-341">topic20</span><span class="sxs-lookup"><span data-stu-id="62053-341">topic20</span></span> |<span data-ttu-id="62053-342">string</span><span class="sxs-lookup"><span data-stu-id="62053-342">string</span></span> |

 <span data-ttu-id="62053-343">**MessageList**:List of messages</span><span class="sxs-lookup"><span data-stu-id="62053-343">**MessageList**:List of messages</span></span>

<span data-ttu-id="62053-344">Required properties for MessageList:</span><span class="sxs-lookup"><span data-stu-id="62053-344">Required properties for MessageList:</span></span>

<span data-ttu-id="62053-345">None of the properties are required.</span><span class="sxs-lookup"><span data-stu-id="62053-345">None of the properties are required.</span></span> 

<span data-ttu-id="62053-346">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-346">**All properties**:</span></span> 

| <span data-ttu-id="62053-347">Name</span><span class="sxs-lookup"><span data-stu-id="62053-347">Name</span></span> | <span data-ttu-id="62053-348">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-348">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-349">messages</span><span class="sxs-lookup"><span data-stu-id="62053-349">messages</span></span> |<span data-ttu-id="62053-350">array</span><span class="sxs-lookup"><span data-stu-id="62053-350">array</span></span> |

 <span data-ttu-id="62053-351">**MessageBody**:Message Body</span><span class="sxs-lookup"><span data-stu-id="62053-351">**MessageBody**:Message Body</span></span>

<span data-ttu-id="62053-352">Required properties for MessageBody:</span><span class="sxs-lookup"><span data-stu-id="62053-352">Required properties for MessageBody:</span></span>

<span data-ttu-id="62053-353">None of the properties are required.</span><span class="sxs-lookup"><span data-stu-id="62053-353">None of the properties are required.</span></span> 

<span data-ttu-id="62053-354">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-354">**All properties**:</span></span> 

| <span data-ttu-id="62053-355">Name</span><span class="sxs-lookup"><span data-stu-id="62053-355">Name</span></span> | <span data-ttu-id="62053-356">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-356">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-357">parsed</span><span class="sxs-lookup"><span data-stu-id="62053-357">parsed</span></span> |<span data-ttu-id="62053-358">string</span><span class="sxs-lookup"><span data-stu-id="62053-358">string</span></span> |
| <span data-ttu-id="62053-359">plain</span><span class="sxs-lookup"><span data-stu-id="62053-359">plain</span></span> |<span data-ttu-id="62053-360">string</span><span class="sxs-lookup"><span data-stu-id="62053-360">string</span></span> |
| <span data-ttu-id="62053-361">rich</span><span class="sxs-lookup"><span data-stu-id="62053-361">rich</span></span> |<span data-ttu-id="62053-362">string</span><span class="sxs-lookup"><span data-stu-id="62053-362">string</span></span> |

 <span data-ttu-id="62053-363">**LikedBy**:Liked By</span><span class="sxs-lookup"><span data-stu-id="62053-363">**LikedBy**:Liked By</span></span>

<span data-ttu-id="62053-364">Required properties for LikedBy:</span><span class="sxs-lookup"><span data-stu-id="62053-364">Required properties for LikedBy:</span></span>

<span data-ttu-id="62053-365">None of the properties are required.</span><span class="sxs-lookup"><span data-stu-id="62053-365">None of the properties are required.</span></span> 

<span data-ttu-id="62053-366">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-366">**All properties**:</span></span> 

| <span data-ttu-id="62053-367">Name</span><span class="sxs-lookup"><span data-stu-id="62053-367">Name</span></span> | <span data-ttu-id="62053-368">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-368">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-369">count</span><span class="sxs-lookup"><span data-stu-id="62053-369">count</span></span> |<span data-ttu-id="62053-370">integer</span><span class="sxs-lookup"><span data-stu-id="62053-370">integer</span></span> |
| <span data-ttu-id="62053-371">names</span><span class="sxs-lookup"><span data-stu-id="62053-371">names</span></span> |<span data-ttu-id="62053-372">array</span><span class="sxs-lookup"><span data-stu-id="62053-372">array</span></span> |

 <span data-ttu-id="62053-373">**YammmerEntity**:Liked By</span><span class="sxs-lookup"><span data-stu-id="62053-373">**YammmerEntity**:Liked By</span></span>

<span data-ttu-id="62053-374">Required properties for YammmerEntity:</span><span class="sxs-lookup"><span data-stu-id="62053-374">Required properties for YammmerEntity:</span></span>

<span data-ttu-id="62053-375">None of the properties are required.</span><span class="sxs-lookup"><span data-stu-id="62053-375">None of the properties are required.</span></span> 

<span data-ttu-id="62053-376">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-376">**All properties**:</span></span> 

| <span data-ttu-id="62053-377">Name</span><span class="sxs-lookup"><span data-stu-id="62053-377">Name</span></span> | <span data-ttu-id="62053-378">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-378">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-379">type</span><span class="sxs-lookup"><span data-stu-id="62053-379">type</span></span> |<span data-ttu-id="62053-380">string</span><span class="sxs-lookup"><span data-stu-id="62053-380">string</span></span> |
| <span data-ttu-id="62053-381">id</span><span class="sxs-lookup"><span data-stu-id="62053-381">id</span></span> |<span data-ttu-id="62053-382">integer</span><span class="sxs-lookup"><span data-stu-id="62053-382">integer</span></span> |
| <span data-ttu-id="62053-383">full_name</span><span class="sxs-lookup"><span data-stu-id="62053-383">full_name</span></span> |<span data-ttu-id="62053-384">string</span><span class="sxs-lookup"><span data-stu-id="62053-384">string</span></span> |

## <a name="next-steps"></a><span data-ttu-id="62053-385">Next Steps</span><span class="sxs-lookup"><span data-stu-id="62053-385">Next Steps</span></span>
[<span data-ttu-id="62053-386">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="62053-386">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

## <a name="object-definitions"></a><span data-ttu-id="62053-387">Object definition(s):</span><span class="sxs-lookup"><span data-stu-id="62053-387">Object definition(s):</span></span>
 <span data-ttu-id="62053-388">**WebResultModel**:Bing web search results</span><span class="sxs-lookup"><span data-stu-id="62053-388">**WebResultModel**:Bing web search results</span></span>

<span data-ttu-id="62053-389">Required properties for WebResultModel:</span><span class="sxs-lookup"><span data-stu-id="62053-389">Required properties for WebResultModel:</span></span>

<span data-ttu-id="62053-390">None of the properties are required.</span><span class="sxs-lookup"><span data-stu-id="62053-390">None of the properties are required.</span></span> 

<span data-ttu-id="62053-391">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-391">**All properties**:</span></span> 

| <span data-ttu-id="62053-392">Name</span><span class="sxs-lookup"><span data-stu-id="62053-392">Name</span></span> | <span data-ttu-id="62053-393">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-393">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-394">Title</span><span class="sxs-lookup"><span data-stu-id="62053-394">Title</span></span> |<span data-ttu-id="62053-395">string</span><span class="sxs-lookup"><span data-stu-id="62053-395">string</span></span> |
| <span data-ttu-id="62053-396">Description</span><span class="sxs-lookup"><span data-stu-id="62053-396">Description</span></span> |<span data-ttu-id="62053-397">string</span><span class="sxs-lookup"><span data-stu-id="62053-397">string</span></span> |
| <span data-ttu-id="62053-398">DisplayUrl</span><span class="sxs-lookup"><span data-stu-id="62053-398">DisplayUrl</span></span> |<span data-ttu-id="62053-399">string</span><span class="sxs-lookup"><span data-stu-id="62053-399">string</span></span> |
| <span data-ttu-id="62053-400">Id</span><span class="sxs-lookup"><span data-stu-id="62053-400">Id</span></span> |<span data-ttu-id="62053-401">string</span><span class="sxs-lookup"><span data-stu-id="62053-401">string</span></span> |
| <span data-ttu-id="62053-402">FullUrl</span><span class="sxs-lookup"><span data-stu-id="62053-402">FullUrl</span></span> |<span data-ttu-id="62053-403">string</span><span class="sxs-lookup"><span data-stu-id="62053-403">string</span></span> |

 <span data-ttu-id="62053-404">**VideoResultModel**:Bing video search results</span><span class="sxs-lookup"><span data-stu-id="62053-404">**VideoResultModel**:Bing video search results</span></span>

<span data-ttu-id="62053-405">Required properties for VideoResultModel:</span><span class="sxs-lookup"><span data-stu-id="62053-405">Required properties for VideoResultModel:</span></span>

<span data-ttu-id="62053-406">None of the properties are required.</span><span class="sxs-lookup"><span data-stu-id="62053-406">None of the properties are required.</span></span> 

<span data-ttu-id="62053-407">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-407">**All properties**:</span></span> 

| <span data-ttu-id="62053-408">Name</span><span class="sxs-lookup"><span data-stu-id="62053-408">Name</span></span> | <span data-ttu-id="62053-409">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-409">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-410">Title</span><span class="sxs-lookup"><span data-stu-id="62053-410">Title</span></span> |<span data-ttu-id="62053-411">string</span><span class="sxs-lookup"><span data-stu-id="62053-411">string</span></span> |
| <span data-ttu-id="62053-412">DisplayUrl</span><span class="sxs-lookup"><span data-stu-id="62053-412">DisplayUrl</span></span> |<span data-ttu-id="62053-413">string</span><span class="sxs-lookup"><span data-stu-id="62053-413">string</span></span> |
| <span data-ttu-id="62053-414">Id</span><span class="sxs-lookup"><span data-stu-id="62053-414">Id</span></span> |<span data-ttu-id="62053-415">string</span><span class="sxs-lookup"><span data-stu-id="62053-415">string</span></span> |
| <span data-ttu-id="62053-416">MediaUrl</span><span class="sxs-lookup"><span data-stu-id="62053-416">MediaUrl</span></span> |<span data-ttu-id="62053-417">string</span><span class="sxs-lookup"><span data-stu-id="62053-417">string</span></span> |
| <span data-ttu-id="62053-418">Runtime</span><span class="sxs-lookup"><span data-stu-id="62053-418">Runtime</span></span> |<span data-ttu-id="62053-419">integer</span><span class="sxs-lookup"><span data-stu-id="62053-419">integer</span></span> |
| <span data-ttu-id="62053-420">Thumbnail</span><span class="sxs-lookup"><span data-stu-id="62053-420">Thumbnail</span></span> |<span data-ttu-id="62053-421">not defined</span><span class="sxs-lookup"><span data-stu-id="62053-421">not defined</span></span> |

 <span data-ttu-id="62053-422">**ThumbnailModel**:Thumbnail properties of the multimedia element</span><span class="sxs-lookup"><span data-stu-id="62053-422">**ThumbnailModel**:Thumbnail properties of the multimedia element</span></span>

<span data-ttu-id="62053-423">Required properties for ThumbnailModel:</span><span class="sxs-lookup"><span data-stu-id="62053-423">Required properties for ThumbnailModel:</span></span>

<span data-ttu-id="62053-424">None of the properties are required.</span><span class="sxs-lookup"><span data-stu-id="62053-424">None of the properties are required.</span></span> 

<span data-ttu-id="62053-425">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-425">**All properties**:</span></span> 

| <span data-ttu-id="62053-426">Name</span><span class="sxs-lookup"><span data-stu-id="62053-426">Name</span></span> | <span data-ttu-id="62053-427">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-427">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-428">MediaUrl</span><span class="sxs-lookup"><span data-stu-id="62053-428">MediaUrl</span></span> |<span data-ttu-id="62053-429">string</span><span class="sxs-lookup"><span data-stu-id="62053-429">string</span></span> |
| <span data-ttu-id="62053-430">ContentType</span><span class="sxs-lookup"><span data-stu-id="62053-430">ContentType</span></span> |<span data-ttu-id="62053-431">string</span><span class="sxs-lookup"><span data-stu-id="62053-431">string</span></span> |
| <span data-ttu-id="62053-432">Width</span><span class="sxs-lookup"><span data-stu-id="62053-432">Width</span></span> |<span data-ttu-id="62053-433">integer</span><span class="sxs-lookup"><span data-stu-id="62053-433">integer</span></span> |
| <span data-ttu-id="62053-434">Height</span><span class="sxs-lookup"><span data-stu-id="62053-434">Height</span></span> |<span data-ttu-id="62053-435">integer</span><span class="sxs-lookup"><span data-stu-id="62053-435">integer</span></span> |
| <span data-ttu-id="62053-436">FileSize</span><span class="sxs-lookup"><span data-stu-id="62053-436">FileSize</span></span> |<span data-ttu-id="62053-437">integer</span><span class="sxs-lookup"><span data-stu-id="62053-437">integer</span></span> |

 <span data-ttu-id="62053-438">**ImageResultModel**:Bing image search results</span><span class="sxs-lookup"><span data-stu-id="62053-438">**ImageResultModel**:Bing image search results</span></span>

<span data-ttu-id="62053-439">Required properties for ImageResultModel:</span><span class="sxs-lookup"><span data-stu-id="62053-439">Required properties for ImageResultModel:</span></span>

<span data-ttu-id="62053-440">None of the properties are required.</span><span class="sxs-lookup"><span data-stu-id="62053-440">None of the properties are required.</span></span> 

<span data-ttu-id="62053-441">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-441">**All properties**:</span></span> 

| <span data-ttu-id="62053-442">Name</span><span class="sxs-lookup"><span data-stu-id="62053-442">Name</span></span> | <span data-ttu-id="62053-443">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-443">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-444">Title</span><span class="sxs-lookup"><span data-stu-id="62053-444">Title</span></span> |<span data-ttu-id="62053-445">string</span><span class="sxs-lookup"><span data-stu-id="62053-445">string</span></span> |
| <span data-ttu-id="62053-446">DisplayUrl</span><span class="sxs-lookup"><span data-stu-id="62053-446">DisplayUrl</span></span> |<span data-ttu-id="62053-447">string</span><span class="sxs-lookup"><span data-stu-id="62053-447">string</span></span> |
| <span data-ttu-id="62053-448">Id</span><span class="sxs-lookup"><span data-stu-id="62053-448">Id</span></span> |<span data-ttu-id="62053-449">string</span><span class="sxs-lookup"><span data-stu-id="62053-449">string</span></span> |
| <span data-ttu-id="62053-450">MediaUrl</span><span class="sxs-lookup"><span data-stu-id="62053-450">MediaUrl</span></span> |<span data-ttu-id="62053-451">string</span><span class="sxs-lookup"><span data-stu-id="62053-451">string</span></span> |
| <span data-ttu-id="62053-452">SourceUrl</span><span class="sxs-lookup"><span data-stu-id="62053-452">SourceUrl</span></span> |<span data-ttu-id="62053-453">string</span><span class="sxs-lookup"><span data-stu-id="62053-453">string</span></span> |
| <span data-ttu-id="62053-454">Thumbnail</span><span class="sxs-lookup"><span data-stu-id="62053-454">Thumbnail</span></span> |<span data-ttu-id="62053-455">not defined</span><span class="sxs-lookup"><span data-stu-id="62053-455">not defined</span></span> |

 <span data-ttu-id="62053-456">**NewsResultModel**:Bing news search results</span><span class="sxs-lookup"><span data-stu-id="62053-456">**NewsResultModel**:Bing news search results</span></span>

<span data-ttu-id="62053-457">Required properties for NewsResultModel:</span><span class="sxs-lookup"><span data-stu-id="62053-457">Required properties for NewsResultModel:</span></span>

<span data-ttu-id="62053-458">None of the properties are required.</span><span class="sxs-lookup"><span data-stu-id="62053-458">None of the properties are required.</span></span> 

<span data-ttu-id="62053-459">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-459">**All properties**:</span></span> 

| <span data-ttu-id="62053-460">Name</span><span class="sxs-lookup"><span data-stu-id="62053-460">Name</span></span> | <span data-ttu-id="62053-461">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-461">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-462">Title</span><span class="sxs-lookup"><span data-stu-id="62053-462">Title</span></span> |<span data-ttu-id="62053-463">string</span><span class="sxs-lookup"><span data-stu-id="62053-463">string</span></span> |
| <span data-ttu-id="62053-464">Description</span><span class="sxs-lookup"><span data-stu-id="62053-464">Description</span></span> |<span data-ttu-id="62053-465">string</span><span class="sxs-lookup"><span data-stu-id="62053-465">string</span></span> |
| <span data-ttu-id="62053-466">DisplayUrl</span><span class="sxs-lookup"><span data-stu-id="62053-466">DisplayUrl</span></span> |<span data-ttu-id="62053-467">string</span><span class="sxs-lookup"><span data-stu-id="62053-467">string</span></span> |
| <span data-ttu-id="62053-468">Id</span><span class="sxs-lookup"><span data-stu-id="62053-468">Id</span></span> |<span data-ttu-id="62053-469">string</span><span class="sxs-lookup"><span data-stu-id="62053-469">string</span></span> |
| <span data-ttu-id="62053-470">Source</span><span class="sxs-lookup"><span data-stu-id="62053-470">Source</span></span> |<span data-ttu-id="62053-471">string</span><span class="sxs-lookup"><span data-stu-id="62053-471">string</span></span> |
| <span data-ttu-id="62053-472">Date</span><span class="sxs-lookup"><span data-stu-id="62053-472">Date</span></span> |<span data-ttu-id="62053-473">string</span><span class="sxs-lookup"><span data-stu-id="62053-473">string</span></span> |

 <span data-ttu-id="62053-474">**SpellResultModel**:Bing spelling suggestions results</span><span class="sxs-lookup"><span data-stu-id="62053-474">**SpellResultModel**:Bing spelling suggestions results</span></span>

<span data-ttu-id="62053-475">Required properties for SpellResultModel:</span><span class="sxs-lookup"><span data-stu-id="62053-475">Required properties for SpellResultModel:</span></span>

<span data-ttu-id="62053-476">None of the properties are required.</span><span class="sxs-lookup"><span data-stu-id="62053-476">None of the properties are required.</span></span> 

<span data-ttu-id="62053-477">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-477">**All properties**:</span></span> 

| <span data-ttu-id="62053-478">Name</span><span class="sxs-lookup"><span data-stu-id="62053-478">Name</span></span> | <span data-ttu-id="62053-479">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-479">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-480">Id</span><span class="sxs-lookup"><span data-stu-id="62053-480">Id</span></span> |<span data-ttu-id="62053-481">string</span><span class="sxs-lookup"><span data-stu-id="62053-481">string</span></span> |
| <span data-ttu-id="62053-482">Value</span><span class="sxs-lookup"><span data-stu-id="62053-482">Value</span></span> |<span data-ttu-id="62053-483">string</span><span class="sxs-lookup"><span data-stu-id="62053-483">string</span></span> |

 <span data-ttu-id="62053-484">**RelatedSearchResultModel**:Bing related search results</span><span class="sxs-lookup"><span data-stu-id="62053-484">**RelatedSearchResultModel**:Bing related search results</span></span>

<span data-ttu-id="62053-485">Required properties for RelatedSearchResultModel:</span><span class="sxs-lookup"><span data-stu-id="62053-485">Required properties for RelatedSearchResultModel:</span></span>

<span data-ttu-id="62053-486">None of the properties are required.</span><span class="sxs-lookup"><span data-stu-id="62053-486">None of the properties are required.</span></span> 

<span data-ttu-id="62053-487">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-487">**All properties**:</span></span> 

| <span data-ttu-id="62053-488">Name</span><span class="sxs-lookup"><span data-stu-id="62053-488">Name</span></span> | <span data-ttu-id="62053-489">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-489">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-490">Title</span><span class="sxs-lookup"><span data-stu-id="62053-490">Title</span></span> |<span data-ttu-id="62053-491">string</span><span class="sxs-lookup"><span data-stu-id="62053-491">string</span></span> |
| <span data-ttu-id="62053-492">Id</span><span class="sxs-lookup"><span data-stu-id="62053-492">Id</span></span> |<span data-ttu-id="62053-493">string</span><span class="sxs-lookup"><span data-stu-id="62053-493">string</span></span> |
| <span data-ttu-id="62053-494">BingUrl</span><span class="sxs-lookup"><span data-stu-id="62053-494">BingUrl</span></span> |<span data-ttu-id="62053-495">string</span><span class="sxs-lookup"><span data-stu-id="62053-495">string</span></span> |

 <span data-ttu-id="62053-496">**CompositeSearchResultModel**:Bing composite search results</span><span class="sxs-lookup"><span data-stu-id="62053-496">**CompositeSearchResultModel**:Bing composite search results</span></span>

<span data-ttu-id="62053-497">Required properties for CompositeSearchResultModel:</span><span class="sxs-lookup"><span data-stu-id="62053-497">Required properties for CompositeSearchResultModel:</span></span>

<span data-ttu-id="62053-498">None of the properties are required.</span><span class="sxs-lookup"><span data-stu-id="62053-498">None of the properties are required.</span></span> 

<span data-ttu-id="62053-499">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-499">**All properties**:</span></span> 

| <span data-ttu-id="62053-500">Name</span><span class="sxs-lookup"><span data-stu-id="62053-500">Name</span></span> | <span data-ttu-id="62053-501">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-501">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-502">WebResultsTotal</span><span class="sxs-lookup"><span data-stu-id="62053-502">WebResultsTotal</span></span> |<span data-ttu-id="62053-503">integer</span><span class="sxs-lookup"><span data-stu-id="62053-503">integer</span></span> |
| <span data-ttu-id="62053-504">ImageResultsTotal</span><span class="sxs-lookup"><span data-stu-id="62053-504">ImageResultsTotal</span></span> |<span data-ttu-id="62053-505">integer</span><span class="sxs-lookup"><span data-stu-id="62053-505">integer</span></span> |
| <span data-ttu-id="62053-506">VideoResultsTotal</span><span class="sxs-lookup"><span data-stu-id="62053-506">VideoResultsTotal</span></span> |<span data-ttu-id="62053-507">integer</span><span class="sxs-lookup"><span data-stu-id="62053-507">integer</span></span> |
| <span data-ttu-id="62053-508">NewsResultsTotal</span><span class="sxs-lookup"><span data-stu-id="62053-508">NewsResultsTotal</span></span> |<span data-ttu-id="62053-509">integer</span><span class="sxs-lookup"><span data-stu-id="62053-509">integer</span></span> |
| <span data-ttu-id="62053-510">SpellSuggestionsTotal</span><span class="sxs-lookup"><span data-stu-id="62053-510">SpellSuggestionsTotal</span></span> |<span data-ttu-id="62053-511">integer</span><span class="sxs-lookup"><span data-stu-id="62053-511">integer</span></span> |
| <span data-ttu-id="62053-512">WebResults</span><span class="sxs-lookup"><span data-stu-id="62053-512">WebResults</span></span> |<span data-ttu-id="62053-513">array</span><span class="sxs-lookup"><span data-stu-id="62053-513">array</span></span> |
| <span data-ttu-id="62053-514">ImageResults</span><span class="sxs-lookup"><span data-stu-id="62053-514">ImageResults</span></span> |<span data-ttu-id="62053-515">array</span><span class="sxs-lookup"><span data-stu-id="62053-515">array</span></span> |
| <span data-ttu-id="62053-516">VideoResults</span><span class="sxs-lookup"><span data-stu-id="62053-516">VideoResults</span></span> |<span data-ttu-id="62053-517">array</span><span class="sxs-lookup"><span data-stu-id="62053-517">array</span></span> |
| <span data-ttu-id="62053-518">NewsResults</span><span class="sxs-lookup"><span data-stu-id="62053-518">NewsResults</span></span> |<span data-ttu-id="62053-519">array</span><span class="sxs-lookup"><span data-stu-id="62053-519">array</span></span> |
| <span data-ttu-id="62053-520">SpellSuggestionResults</span><span class="sxs-lookup"><span data-stu-id="62053-520">SpellSuggestionResults</span></span> |<span data-ttu-id="62053-521">array</span><span class="sxs-lookup"><span data-stu-id="62053-521">array</span></span> |
| <span data-ttu-id="62053-522">RelatedSearchResults</span><span class="sxs-lookup"><span data-stu-id="62053-522">RelatedSearchResults</span></span> |<span data-ttu-id="62053-523">array</span><span class="sxs-lookup"><span data-stu-id="62053-523">array</span></span> |

## <a name="object-definitions"></a><span data-ttu-id="62053-524">Object definition(s):</span><span class="sxs-lookup"><span data-stu-id="62053-524">Object definition(s):</span></span>
 <span data-ttu-id="62053-525">**PostOperationResponse**:Represents response of post operation of Slack Connector for posting to Slack</span><span class="sxs-lookup"><span data-stu-id="62053-525">**PostOperationResponse**:Represents response of post operation of Slack Connector for posting to Slack</span></span>

<span data-ttu-id="62053-526">Required properties for PostOperationResponse:</span><span class="sxs-lookup"><span data-stu-id="62053-526">Required properties for PostOperationResponse:</span></span>

<span data-ttu-id="62053-527">None of the properties are required.</span><span class="sxs-lookup"><span data-stu-id="62053-527">None of the properties are required.</span></span> 

<span data-ttu-id="62053-528">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-528">**All properties**:</span></span> 

| <span data-ttu-id="62053-529">Name</span><span class="sxs-lookup"><span data-stu-id="62053-529">Name</span></span> | <span data-ttu-id="62053-530">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-530">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-531">ok</span><span class="sxs-lookup"><span data-stu-id="62053-531">ok</span></span> |<span data-ttu-id="62053-532">boolean</span><span class="sxs-lookup"><span data-stu-id="62053-532">boolean</span></span> |
| <span data-ttu-id="62053-533">channel</span><span class="sxs-lookup"><span data-stu-id="62053-533">channel</span></span> |<span data-ttu-id="62053-534">string</span><span class="sxs-lookup"><span data-stu-id="62053-534">string</span></span> |
| <span data-ttu-id="62053-535">ts</span><span class="sxs-lookup"><span data-stu-id="62053-535">ts</span></span> |<span data-ttu-id="62053-536">string</span><span class="sxs-lookup"><span data-stu-id="62053-536">string</span></span> |
| <span data-ttu-id="62053-537">message</span><span class="sxs-lookup"><span data-stu-id="62053-537">message</span></span> |<span data-ttu-id="62053-538">not defined</span><span class="sxs-lookup"><span data-stu-id="62053-538">not defined</span></span> |
| <span data-ttu-id="62053-539">error</span><span class="sxs-lookup"><span data-stu-id="62053-539">error</span></span> |<span data-ttu-id="62053-540">string</span><span class="sxs-lookup"><span data-stu-id="62053-540">string</span></span> |

 <span data-ttu-id="62053-541">**MessageItem**:A channel message.</span><span class="sxs-lookup"><span data-stu-id="62053-541">**MessageItem**:A channel message.</span></span>

<span data-ttu-id="62053-542">Required properties for MessageItem:</span><span class="sxs-lookup"><span data-stu-id="62053-542">Required properties for MessageItem:</span></span>

<span data-ttu-id="62053-543">None of the properties are required.</span><span class="sxs-lookup"><span data-stu-id="62053-543">None of the properties are required.</span></span> 

<span data-ttu-id="62053-544">**All properties**:</span><span class="sxs-lookup"><span data-stu-id="62053-544">**All properties**:</span></span> 

| <span data-ttu-id="62053-545">Name</span><span class="sxs-lookup"><span data-stu-id="62053-545">Name</span></span> | <span data-ttu-id="62053-546">Data Type</span><span class="sxs-lookup"><span data-stu-id="62053-546">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="62053-547">text</span><span class="sxs-lookup"><span data-stu-id="62053-547">text</span></span> |<span data-ttu-id="62053-548">string</span><span class="sxs-lookup"><span data-stu-id="62053-548">string</span></span> |
| <span data-ttu-id="62053-549">id</span><span class="sxs-lookup"><span data-stu-id="62053-549">id</span></span> |<span data-ttu-id="62053-550">string</span><span class="sxs-lookup"><span data-stu-id="62053-550">string</span></span> |
| <span data-ttu-id="62053-551">user</span><span class="sxs-lookup"><span data-stu-id="62053-551">user</span></span> |<span data-ttu-id="62053-552">string</span><span class="sxs-lookup"><span data-stu-id="62053-552">string</span></span> |
| <span data-ttu-id="62053-553">created</span><span class="sxs-lookup"><span data-stu-id="62053-553">created</span></span> |<span data-ttu-id="62053-554">integer</span><span class="sxs-lookup"><span data-stu-id="62053-554">integer</span></span> |
| <span data-ttu-id="62053-555">is_user-deleted</span><span class="sxs-lookup"><span data-stu-id="62053-555">is_user-deleted</span></span> |<span data-ttu-id="62053-556">boolean</span><span class="sxs-lookup"><span data-stu-id="62053-556">boolean</span></span> |

## <a name="next-steps"></a><span data-ttu-id="62053-557">Next Steps</span><span class="sxs-lookup"><span data-stu-id="62053-557">Next Steps</span></span>
[<span data-ttu-id="62053-558">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="62053-558">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-slack/connectionconfig1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-slack/connectionconfig2.png 
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-slack/connectionconfig3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-slack/connectionconfig4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-slack/connectionconfig5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-slack/connectionconfig6.png






