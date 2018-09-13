---
title: RSS | Microsoft Docs
description: Create Logic apps with Azure App service. RSS connector allows the users to publish and retrieve feed items. It also allows the users to trigger operations when a new item is published to the feed.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: a10a6277-ed29-4e68-a881-ccdad6fd0ad8
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: deonhe
ms.openlocfilehash: 5e13e126fecda66a453b4ced619016121af98b2c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552022"
---
# <a name="get-started-with-the-rss-connector"></a><span data-ttu-id="3e404-105">Get started with the RSS connector</span><span class="sxs-lookup"><span data-stu-id="3e404-105">Get started with the RSS connector</span></span>
<span data-ttu-id="3e404-106">RSS is a popular web syndication format used to publish frequently updated content – like blog entries and news headlines.</span><span class="sxs-lookup"><span data-stu-id="3e404-106">RSS is a popular web syndication format used to publish frequently updated content – like blog entries and news headlines.</span></span>  <span data-ttu-id="3e404-107">Many content publishers provide an RSS feed to allow users to subscribe to it.</span><span class="sxs-lookup"><span data-stu-id="3e404-107">Many content publishers provide an RSS feed to allow users to subscribe to it.</span></span>  <span data-ttu-id="3e404-108">Use the RSS connector to retrieve feed information and trigger flows when new items are published in an RSS feed.</span><span class="sxs-lookup"><span data-stu-id="3e404-108">Use the RSS connector to retrieve feed information and trigger flows when new items are published in an RSS feed.</span></span>

> [!NOTE]
> <span data-ttu-id="3e404-109">This version of the article applies to logic apps 2015-08-01-preview schema version.</span><span class="sxs-lookup"><span data-stu-id="3e404-109">This version of the article applies to logic apps 2015-08-01-preview schema version.</span></span> 
> 
> 

<span data-ttu-id="3e404-110">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3e404-110">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="triggers-and-actions"></a><span data-ttu-id="3e404-111">Triggers and actions</span><span class="sxs-lookup"><span data-stu-id="3e404-111">Triggers and actions</span></span>
<span data-ttu-id="3e404-112">The RSS connector can be used as an action; it has trigger(s).</span><span class="sxs-lookup"><span data-stu-id="3e404-112">The RSS connector can be used as an action; it has trigger(s).</span></span> <span data-ttu-id="3e404-113">All connectors support data in JSON and XML formats.</span><span class="sxs-lookup"><span data-stu-id="3e404-113">All connectors support data in JSON and XML formats.</span></span> 

 <span data-ttu-id="3e404-114">The RSS connector has the following action(s) and/or trigger(s) available:</span><span class="sxs-lookup"><span data-stu-id="3e404-114">The RSS connector has the following action(s) and/or trigger(s) available:</span></span>

### <a name="rss-actions"></a><span data-ttu-id="3e404-115">RSS actions</span><span class="sxs-lookup"><span data-stu-id="3e404-115">RSS actions</span></span>
<span data-ttu-id="3e404-116">You can take these action(s):</span><span class="sxs-lookup"><span data-stu-id="3e404-116">You can take these action(s):</span></span>

| <span data-ttu-id="3e404-117">Action</span><span class="sxs-lookup"><span data-stu-id="3e404-117">Action</span></span> | <span data-ttu-id="3e404-118">Description</span><span class="sxs-lookup"><span data-stu-id="3e404-118">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="3e404-119">ListFeedItems</span><span class="sxs-lookup"><span data-stu-id="3e404-119">ListFeedItems</span></span>](connectors-create-api-rss.md#listfeeditems) |<span data-ttu-id="3e404-120">Get all RSS feed items.</span><span class="sxs-lookup"><span data-stu-id="3e404-120">Get all RSS feed items.</span></span> |

### <a name="rss-triggers"></a><span data-ttu-id="3e404-121">RSS triggers</span><span class="sxs-lookup"><span data-stu-id="3e404-121">RSS triggers</span></span>
<span data-ttu-id="3e404-122">You can listen for these event(s):</span><span class="sxs-lookup"><span data-stu-id="3e404-122">You can listen for these event(s):</span></span>

| <span data-ttu-id="3e404-123">Trigger</span><span class="sxs-lookup"><span data-stu-id="3e404-123">Trigger</span></span> | <span data-ttu-id="3e404-124">Description</span><span class="sxs-lookup"><span data-stu-id="3e404-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3e404-125">When a new feed item published</span><span class="sxs-lookup"><span data-stu-id="3e404-125">When a new feed item published</span></span> |<span data-ttu-id="3e404-126">Triggers a workflow when a new feed is published</span><span class="sxs-lookup"><span data-stu-id="3e404-126">Triggers a workflow when a new feed is published</span></span> |

## <a name="create-a-connection-to-rss"></a><span data-ttu-id="3e404-127">Create a connection to RSS</span><span class="sxs-lookup"><span data-stu-id="3e404-127">Create a connection to RSS</span></span>
> [!INCLUDE [Steps to create a connection to an RSS feed](../../includes/connectors-create-api-rss.md)]
> 
> [!TIP]
> <span data-ttu-id="3e404-128">You can use this connection in other logic apps.</span><span class="sxs-lookup"><span data-stu-id="3e404-128">You can use this connection in other logic apps.</span></span>
> 
> 

## <a name="reference-for-rss"></a><span data-ttu-id="3e404-129">Reference for RSS</span><span class="sxs-lookup"><span data-stu-id="3e404-129">Reference for RSS</span></span>
<span data-ttu-id="3e404-130">Applies to version: 1.0</span><span class="sxs-lookup"><span data-stu-id="3e404-130">Applies to version: 1.0</span></span>

## <a name="onnewfeed"></a><span data-ttu-id="3e404-131">OnNewFeed</span><span class="sxs-lookup"><span data-stu-id="3e404-131">OnNewFeed</span></span>
<span data-ttu-id="3e404-132">When a new feed item published: Triggers a workflow when a new feed is published</span><span class="sxs-lookup"><span data-stu-id="3e404-132">When a new feed item published: Triggers a workflow when a new feed is published</span></span> 

```GET: /OnNewFeed``` 

| <span data-ttu-id="3e404-133">Name</span><span class="sxs-lookup"><span data-stu-id="3e404-133">Name</span></span> | <span data-ttu-id="3e404-134">Data Type</span><span class="sxs-lookup"><span data-stu-id="3e404-134">Data Type</span></span> | <span data-ttu-id="3e404-135">Required</span><span class="sxs-lookup"><span data-stu-id="3e404-135">Required</span></span> | <span data-ttu-id="3e404-136">Located In</span><span class="sxs-lookup"><span data-stu-id="3e404-136">Located In</span></span> | <span data-ttu-id="3e404-137">Default Value</span><span class="sxs-lookup"><span data-stu-id="3e404-137">Default Value</span></span> | <span data-ttu-id="3e404-138">Description</span><span class="sxs-lookup"><span data-stu-id="3e404-138">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="3e404-139">feedUrl</span><span class="sxs-lookup"><span data-stu-id="3e404-139">feedUrl</span></span> |<span data-ttu-id="3e404-140">string</span><span class="sxs-lookup"><span data-stu-id="3e404-140">string</span></span> |<span data-ttu-id="3e404-141">yes</span><span class="sxs-lookup"><span data-stu-id="3e404-141">yes</span></span> |<span data-ttu-id="3e404-142">query</span><span class="sxs-lookup"><span data-stu-id="3e404-142">query</span></span> |<span data-ttu-id="3e404-143">none</span><span class="sxs-lookup"><span data-stu-id="3e404-143">none</span></span> |<span data-ttu-id="3e404-144">Feed url</span><span class="sxs-lookup"><span data-stu-id="3e404-144">Feed url</span></span> |

#### <a name="response"></a><span data-ttu-id="3e404-145">Response</span><span class="sxs-lookup"><span data-stu-id="3e404-145">Response</span></span>
| <span data-ttu-id="3e404-146">Name</span><span class="sxs-lookup"><span data-stu-id="3e404-146">Name</span></span> | <span data-ttu-id="3e404-147">Description</span><span class="sxs-lookup"><span data-stu-id="3e404-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3e404-148">200</span><span class="sxs-lookup"><span data-stu-id="3e404-148">200</span></span> |<span data-ttu-id="3e404-149">OK</span><span class="sxs-lookup"><span data-stu-id="3e404-149">OK</span></span> |
| <span data-ttu-id="3e404-150">202</span><span class="sxs-lookup"><span data-stu-id="3e404-150">202</span></span> |<span data-ttu-id="3e404-151">Accepted</span><span class="sxs-lookup"><span data-stu-id="3e404-151">Accepted</span></span> |
| <span data-ttu-id="3e404-152">400</span><span class="sxs-lookup"><span data-stu-id="3e404-152">400</span></span> |<span data-ttu-id="3e404-153">Bad Request</span><span class="sxs-lookup"><span data-stu-id="3e404-153">Bad Request</span></span> |
| <span data-ttu-id="3e404-154">401</span><span class="sxs-lookup"><span data-stu-id="3e404-154">401</span></span> |<span data-ttu-id="3e404-155">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="3e404-155">Unauthorized</span></span> |
| <span data-ttu-id="3e404-156">403</span><span class="sxs-lookup"><span data-stu-id="3e404-156">403</span></span> |<span data-ttu-id="3e404-157">Forbidden</span><span class="sxs-lookup"><span data-stu-id="3e404-157">Forbidden</span></span> |
| <span data-ttu-id="3e404-158">404</span><span class="sxs-lookup"><span data-stu-id="3e404-158">404</span></span> |<span data-ttu-id="3e404-159">Not Found</span><span class="sxs-lookup"><span data-stu-id="3e404-159">Not Found</span></span> |
| <span data-ttu-id="3e404-160">500</span><span class="sxs-lookup"><span data-stu-id="3e404-160">500</span></span> |<span data-ttu-id="3e404-161">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="3e404-161">Internal Server Error.</span></span> <span data-ttu-id="3e404-162">Unknown error occured</span><span class="sxs-lookup"><span data-stu-id="3e404-162">Unknown error occured</span></span> |
| <span data-ttu-id="3e404-163">default</span><span class="sxs-lookup"><span data-stu-id="3e404-163">default</span></span> |<span data-ttu-id="3e404-164">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="3e404-164">Operation Failed.</span></span> |

## <a name="listfeeditems"></a><span data-ttu-id="3e404-165">ListFeedItems</span><span class="sxs-lookup"><span data-stu-id="3e404-165">ListFeedItems</span></span>
<span data-ttu-id="3e404-166">List all RSS feed items.: Get all RSS feed items.</span><span class="sxs-lookup"><span data-stu-id="3e404-166">List all RSS feed items.: Get all RSS feed items.</span></span> 

```GET: /ListFeedItems``` 

| <span data-ttu-id="3e404-167">Name</span><span class="sxs-lookup"><span data-stu-id="3e404-167">Name</span></span> | <span data-ttu-id="3e404-168">Data Type</span><span class="sxs-lookup"><span data-stu-id="3e404-168">Data Type</span></span> | <span data-ttu-id="3e404-169">Required</span><span class="sxs-lookup"><span data-stu-id="3e404-169">Required</span></span> | <span data-ttu-id="3e404-170">Located In</span><span class="sxs-lookup"><span data-stu-id="3e404-170">Located In</span></span> | <span data-ttu-id="3e404-171">Default Value</span><span class="sxs-lookup"><span data-stu-id="3e404-171">Default Value</span></span> | <span data-ttu-id="3e404-172">Description</span><span class="sxs-lookup"><span data-stu-id="3e404-172">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="3e404-173">feedUrl</span><span class="sxs-lookup"><span data-stu-id="3e404-173">feedUrl</span></span> |<span data-ttu-id="3e404-174">string</span><span class="sxs-lookup"><span data-stu-id="3e404-174">string</span></span> |<span data-ttu-id="3e404-175">yes</span><span class="sxs-lookup"><span data-stu-id="3e404-175">yes</span></span> |<span data-ttu-id="3e404-176">query</span><span class="sxs-lookup"><span data-stu-id="3e404-176">query</span></span> |<span data-ttu-id="3e404-177">none</span><span class="sxs-lookup"><span data-stu-id="3e404-177">none</span></span> |<span data-ttu-id="3e404-178">Feed url</span><span class="sxs-lookup"><span data-stu-id="3e404-178">Feed url</span></span> |

#### <a name="response"></a><span data-ttu-id="3e404-179">Response</span><span class="sxs-lookup"><span data-stu-id="3e404-179">Response</span></span>
| <span data-ttu-id="3e404-180">Name</span><span class="sxs-lookup"><span data-stu-id="3e404-180">Name</span></span> | <span data-ttu-id="3e404-181">Description</span><span class="sxs-lookup"><span data-stu-id="3e404-181">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3e404-182">200</span><span class="sxs-lookup"><span data-stu-id="3e404-182">200</span></span> |<span data-ttu-id="3e404-183">OK</span><span class="sxs-lookup"><span data-stu-id="3e404-183">OK</span></span> |
| <span data-ttu-id="3e404-184">202</span><span class="sxs-lookup"><span data-stu-id="3e404-184">202</span></span> |<span data-ttu-id="3e404-185">Accepted</span><span class="sxs-lookup"><span data-stu-id="3e404-185">Accepted</span></span> |
| <span data-ttu-id="3e404-186">400</span><span class="sxs-lookup"><span data-stu-id="3e404-186">400</span></span> |<span data-ttu-id="3e404-187">Bad Request</span><span class="sxs-lookup"><span data-stu-id="3e404-187">Bad Request</span></span> |
| <span data-ttu-id="3e404-188">401</span><span class="sxs-lookup"><span data-stu-id="3e404-188">401</span></span> |<span data-ttu-id="3e404-189">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="3e404-189">Unauthorized</span></span> |
| <span data-ttu-id="3e404-190">403</span><span class="sxs-lookup"><span data-stu-id="3e404-190">403</span></span> |<span data-ttu-id="3e404-191">Forbidden</span><span class="sxs-lookup"><span data-stu-id="3e404-191">Forbidden</span></span> |
| <span data-ttu-id="3e404-192">404</span><span class="sxs-lookup"><span data-stu-id="3e404-192">404</span></span> |<span data-ttu-id="3e404-193">Not Found</span><span class="sxs-lookup"><span data-stu-id="3e404-193">Not Found</span></span> |
| <span data-ttu-id="3e404-194">500</span><span class="sxs-lookup"><span data-stu-id="3e404-194">500</span></span> |<span data-ttu-id="3e404-195">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="3e404-195">Internal Server Error.</span></span> <span data-ttu-id="3e404-196">Unknown error occured</span><span class="sxs-lookup"><span data-stu-id="3e404-196">Unknown error occured</span></span> |
| <span data-ttu-id="3e404-197">default</span><span class="sxs-lookup"><span data-stu-id="3e404-197">default</span></span> |<span data-ttu-id="3e404-198">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="3e404-198">Operation Failed.</span></span> |

## <a name="object-definitions"></a><span data-ttu-id="3e404-199">Object definitions</span><span class="sxs-lookup"><span data-stu-id="3e404-199">Object definitions</span></span>
### <a name="triggerbatchresponsefeeditem"></a><span data-ttu-id="3e404-200">TriggerBatchResponse[FeedItem]</span><span class="sxs-lookup"><span data-stu-id="3e404-200">TriggerBatchResponse[FeedItem]</span></span>
| <span data-ttu-id="3e404-201">Property Name</span><span class="sxs-lookup"><span data-stu-id="3e404-201">Property Name</span></span> | <span data-ttu-id="3e404-202">Data Type</span><span class="sxs-lookup"><span data-stu-id="3e404-202">Data Type</span></span> | <span data-ttu-id="3e404-203">Required</span><span class="sxs-lookup"><span data-stu-id="3e404-203">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e404-204">value</span><span class="sxs-lookup"><span data-stu-id="3e404-204">value</span></span> |<span data-ttu-id="3e404-205">array</span><span class="sxs-lookup"><span data-stu-id="3e404-205">array</span></span> |<span data-ttu-id="3e404-206">No</span><span class="sxs-lookup"><span data-stu-id="3e404-206">No</span></span> |

### <a name="feeditem"></a><span data-ttu-id="3e404-207">FeedItem</span><span class="sxs-lookup"><span data-stu-id="3e404-207">FeedItem</span></span>
| <span data-ttu-id="3e404-208">Property Name</span><span class="sxs-lookup"><span data-stu-id="3e404-208">Property Name</span></span> | <span data-ttu-id="3e404-209">Data Type</span><span class="sxs-lookup"><span data-stu-id="3e404-209">Data Type</span></span> | <span data-ttu-id="3e404-210">Required</span><span class="sxs-lookup"><span data-stu-id="3e404-210">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e404-211">id</span><span class="sxs-lookup"><span data-stu-id="3e404-211">id</span></span> |<span data-ttu-id="3e404-212">string</span><span class="sxs-lookup"><span data-stu-id="3e404-212">string</span></span> |<span data-ttu-id="3e404-213">Yes</span><span class="sxs-lookup"><span data-stu-id="3e404-213">Yes</span></span> |
| <span data-ttu-id="3e404-214">title</span><span class="sxs-lookup"><span data-stu-id="3e404-214">title</span></span> |<span data-ttu-id="3e404-215">string</span><span class="sxs-lookup"><span data-stu-id="3e404-215">string</span></span> |<span data-ttu-id="3e404-216">Yes</span><span class="sxs-lookup"><span data-stu-id="3e404-216">Yes</span></span> |
| <span data-ttu-id="3e404-217">content</span><span class="sxs-lookup"><span data-stu-id="3e404-217">content</span></span> |<span data-ttu-id="3e404-218">string</span><span class="sxs-lookup"><span data-stu-id="3e404-218">string</span></span> |<span data-ttu-id="3e404-219">Yes</span><span class="sxs-lookup"><span data-stu-id="3e404-219">Yes</span></span> |
| <span data-ttu-id="3e404-220">links</span><span class="sxs-lookup"><span data-stu-id="3e404-220">links</span></span> |<span data-ttu-id="3e404-221">array</span><span class="sxs-lookup"><span data-stu-id="3e404-221">array</span></span> |<span data-ttu-id="3e404-222">No</span><span class="sxs-lookup"><span data-stu-id="3e404-222">No</span></span> |
| <span data-ttu-id="3e404-223">updatedOn</span><span class="sxs-lookup"><span data-stu-id="3e404-223">updatedOn</span></span> |<span data-ttu-id="3e404-224">string</span><span class="sxs-lookup"><span data-stu-id="3e404-224">string</span></span> |<span data-ttu-id="3e404-225">No</span><span class="sxs-lookup"><span data-stu-id="3e404-225">No</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3e404-226">Next Steps</span><span class="sxs-lookup"><span data-stu-id="3e404-226">Next Steps</span></span>
[<span data-ttu-id="3e404-227">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="3e404-227">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

