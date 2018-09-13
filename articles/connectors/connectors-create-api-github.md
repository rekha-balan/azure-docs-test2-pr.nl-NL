---
title: GitHub | Microsoft Docs
description: Create Logic apps with Azure App service. GitHub is a web-based Git repository hosting service. It offers all of the distributed revision control and source code management (SCM) functionality of Git as well as adding its own features.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: 8f873e6c-f4c0-4c2e-a5bd-2e953efe5e2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: deonhe
ms.openlocfilehash: 6f336db8c8719b99420b353dca82e36a0d837769
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549217"
---
# <a name="get-started-with-the-github-connector"></a><span data-ttu-id="5c072-105">Get started with the GitHub connector</span><span class="sxs-lookup"><span data-stu-id="5c072-105">Get started with the GitHub connector</span></span>
<span data-ttu-id="5c072-106">GitHub is a web-based Git repository hosting service.</span><span class="sxs-lookup"><span data-stu-id="5c072-106">GitHub is a web-based Git repository hosting service.</span></span> <span data-ttu-id="5c072-107">It offers all of the distributed revision control and source code management (SCM) functionality of Git as well as adding its own features.</span><span class="sxs-lookup"><span data-stu-id="5c072-107">It offers all of the distributed revision control and source code management (SCM) functionality of Git as well as adding its own features.</span></span>

> [!NOTE]
> <span data-ttu-id="5c072-108">This version of the article applies to logic apps 2015-08-01-preview schema version.</span><span class="sxs-lookup"><span data-stu-id="5c072-108">This version of the article applies to logic apps 2015-08-01-preview schema version.</span></span> 
> 
> 

<span data-ttu-id="5c072-109">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5c072-109">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="triggers-and-actions"></a><span data-ttu-id="5c072-110">Triggers and actions</span><span class="sxs-lookup"><span data-stu-id="5c072-110">Triggers and actions</span></span>
<span data-ttu-id="5c072-111">The GitHub connector can be used as an action; it has trigger(s).</span><span class="sxs-lookup"><span data-stu-id="5c072-111">The GitHub connector can be used as an action; it has trigger(s).</span></span> <span data-ttu-id="5c072-112">All connectors support data in JSON and XML formats.</span><span class="sxs-lookup"><span data-stu-id="5c072-112">All connectors support data in JSON and XML formats.</span></span> 

 <span data-ttu-id="5c072-113">The GitHub connector has the following action(s) and/or trigger(s) available:</span><span class="sxs-lookup"><span data-stu-id="5c072-113">The GitHub connector has the following action(s) and/or trigger(s) available:</span></span>

### <a name="github-actions"></a><span data-ttu-id="5c072-114">GitHub actions</span><span class="sxs-lookup"><span data-stu-id="5c072-114">GitHub actions</span></span>
<span data-ttu-id="5c072-115">You can take these action(s):</span><span class="sxs-lookup"><span data-stu-id="5c072-115">You can take these action(s):</span></span>

| <span data-ttu-id="5c072-116">Action</span><span class="sxs-lookup"><span data-stu-id="5c072-116">Action</span></span> | <span data-ttu-id="5c072-117">Description</span><span class="sxs-lookup"><span data-stu-id="5c072-117">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="5c072-118">CreateIssue</span><span class="sxs-lookup"><span data-stu-id="5c072-118">CreateIssue</span></span>](connectors-create-api-github.md#createissue) |<span data-ttu-id="5c072-119">Creates an issue</span><span class="sxs-lookup"><span data-stu-id="5c072-119">Creates an issue</span></span> |

### <a name="github-triggers"></a><span data-ttu-id="5c072-120">GitHub triggers</span><span class="sxs-lookup"><span data-stu-id="5c072-120">GitHub triggers</span></span>
<span data-ttu-id="5c072-121">You can listen for these event(s):</span><span class="sxs-lookup"><span data-stu-id="5c072-121">You can listen for these event(s):</span></span>

| <span data-ttu-id="5c072-122">Trigger</span><span class="sxs-lookup"><span data-stu-id="5c072-122">Trigger</span></span> | <span data-ttu-id="5c072-123">Description</span><span class="sxs-lookup"><span data-stu-id="5c072-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5c072-124">When an issue is opened</span><span class="sxs-lookup"><span data-stu-id="5c072-124">When an issue is opened</span></span> |<span data-ttu-id="5c072-125">An issue is opened</span><span class="sxs-lookup"><span data-stu-id="5c072-125">An issue is opened</span></span> |
| <span data-ttu-id="5c072-126">When an issue is closed</span><span class="sxs-lookup"><span data-stu-id="5c072-126">When an issue is closed</span></span> |<span data-ttu-id="5c072-127">An issue is closed</span><span class="sxs-lookup"><span data-stu-id="5c072-127">An issue is closed</span></span> |
| <span data-ttu-id="5c072-128">When an issue is assigned</span><span class="sxs-lookup"><span data-stu-id="5c072-128">When an issue is assigned</span></span> |<span data-ttu-id="5c072-129">An issue is assigned</span><span class="sxs-lookup"><span data-stu-id="5c072-129">An issue is assigned</span></span> |

## <a name="create-a-connection-to-github"></a><span data-ttu-id="5c072-130">Create a connection to GitHub</span><span class="sxs-lookup"><span data-stu-id="5c072-130">Create a connection to GitHub</span></span>
<span data-ttu-id="5c072-131">To create Logic apps with GitHub, you must first create a **connection** then provide the details for the following properties:</span><span class="sxs-lookup"><span data-stu-id="5c072-131">To create Logic apps with GitHub, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="5c072-132">Property</span><span class="sxs-lookup"><span data-stu-id="5c072-132">Property</span></span> | <span data-ttu-id="5c072-133">Required</span><span class="sxs-lookup"><span data-stu-id="5c072-133">Required</span></span> | <span data-ttu-id="5c072-134">Description</span><span class="sxs-lookup"><span data-stu-id="5c072-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5c072-135">Token</span><span class="sxs-lookup"><span data-stu-id="5c072-135">Token</span></span> |<span data-ttu-id="5c072-136">Yes</span><span class="sxs-lookup"><span data-stu-id="5c072-136">Yes</span></span> |<span data-ttu-id="5c072-137">Provide GitHub Credentials</span><span class="sxs-lookup"><span data-stu-id="5c072-137">Provide GitHub Credentials</span></span> |

<span data-ttu-id="5c072-138">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span><span class="sxs-lookup"><span data-stu-id="5c072-138">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span> 

> [!INCLUDE [Steps to create a connection to GitHub](../../includes/connectors-create-api-github.md)]
> 
> [!TIP]
> <span data-ttu-id="5c072-139">You can use this connection in other logic apps.</span><span class="sxs-lookup"><span data-stu-id="5c072-139">You can use this connection in other logic apps.</span></span>
> 
> 

## <a name="reference-for-github"></a><span data-ttu-id="5c072-140">Reference for GitHub</span><span class="sxs-lookup"><span data-stu-id="5c072-140">Reference for GitHub</span></span>
<span data-ttu-id="5c072-141">Applies to version: 1.0</span><span class="sxs-lookup"><span data-stu-id="5c072-141">Applies to version: 1.0</span></span>

## <a name="createissue"></a><span data-ttu-id="5c072-142">CreateIssue</span><span class="sxs-lookup"><span data-stu-id="5c072-142">CreateIssue</span></span>
<span data-ttu-id="5c072-143">Create an issue: Creates an issue</span><span class="sxs-lookup"><span data-stu-id="5c072-143">Create an issue: Creates an issue</span></span> 

```POST: /repos/{repositoryOwner}/{repositoryName}/issues``` 

| <span data-ttu-id="5c072-144">Name</span><span class="sxs-lookup"><span data-stu-id="5c072-144">Name</span></span> | <span data-ttu-id="5c072-145">Data Type</span><span class="sxs-lookup"><span data-stu-id="5c072-145">Data Type</span></span> | <span data-ttu-id="5c072-146">Required</span><span class="sxs-lookup"><span data-stu-id="5c072-146">Required</span></span> | <span data-ttu-id="5c072-147">Located In</span><span class="sxs-lookup"><span data-stu-id="5c072-147">Located In</span></span> | <span data-ttu-id="5c072-148">Default Value</span><span class="sxs-lookup"><span data-stu-id="5c072-148">Default Value</span></span> | <span data-ttu-id="5c072-149">Description</span><span class="sxs-lookup"><span data-stu-id="5c072-149">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="5c072-150">repositoryOwner</span><span class="sxs-lookup"><span data-stu-id="5c072-150">repositoryOwner</span></span> |<span data-ttu-id="5c072-151">string</span><span class="sxs-lookup"><span data-stu-id="5c072-151">string</span></span> |<span data-ttu-id="5c072-152">yes</span><span class="sxs-lookup"><span data-stu-id="5c072-152">yes</span></span> |<span data-ttu-id="5c072-153">path</span><span class="sxs-lookup"><span data-stu-id="5c072-153">path</span></span> |<span data-ttu-id="5c072-154">none</span><span class="sxs-lookup"><span data-stu-id="5c072-154">none</span></span> |<span data-ttu-id="5c072-155">Repository owner</span><span class="sxs-lookup"><span data-stu-id="5c072-155">Repository owner</span></span> |
| <span data-ttu-id="5c072-156">repositoryName</span><span class="sxs-lookup"><span data-stu-id="5c072-156">repositoryName</span></span> |<span data-ttu-id="5c072-157">string</span><span class="sxs-lookup"><span data-stu-id="5c072-157">string</span></span> |<span data-ttu-id="5c072-158">yes</span><span class="sxs-lookup"><span data-stu-id="5c072-158">yes</span></span> |<span data-ttu-id="5c072-159">path</span><span class="sxs-lookup"><span data-stu-id="5c072-159">path</span></span> |<span data-ttu-id="5c072-160">none</span><span class="sxs-lookup"><span data-stu-id="5c072-160">none</span></span> |<span data-ttu-id="5c072-161">Repository name</span><span class="sxs-lookup"><span data-stu-id="5c072-161">Repository name</span></span> |
| <span data-ttu-id="5c072-162">issueBasicDetails</span><span class="sxs-lookup"><span data-stu-id="5c072-162">issueBasicDetails</span></span> | |<span data-ttu-id="5c072-163">yes</span><span class="sxs-lookup"><span data-stu-id="5c072-163">yes</span></span> |<span data-ttu-id="5c072-164">body</span><span class="sxs-lookup"><span data-stu-id="5c072-164">body</span></span> |<span data-ttu-id="5c072-165">none</span><span class="sxs-lookup"><span data-stu-id="5c072-165">none</span></span> |<span data-ttu-id="5c072-166">Issue details</span><span class="sxs-lookup"><span data-stu-id="5c072-166">Issue details</span></span> |

#### <a name="response"></a><span data-ttu-id="5c072-167">Response</span><span class="sxs-lookup"><span data-stu-id="5c072-167">Response</span></span>
| <span data-ttu-id="5c072-168">Name</span><span class="sxs-lookup"><span data-stu-id="5c072-168">Name</span></span> | <span data-ttu-id="5c072-169">Description</span><span class="sxs-lookup"><span data-stu-id="5c072-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5c072-170">200</span><span class="sxs-lookup"><span data-stu-id="5c072-170">200</span></span> |<span data-ttu-id="5c072-171">OK</span><span class="sxs-lookup"><span data-stu-id="5c072-171">OK</span></span> |
| <span data-ttu-id="5c072-172">400</span><span class="sxs-lookup"><span data-stu-id="5c072-172">400</span></span> |<span data-ttu-id="5c072-173">Bad Request</span><span class="sxs-lookup"><span data-stu-id="5c072-173">Bad Request</span></span> |
| <span data-ttu-id="5c072-174">401</span><span class="sxs-lookup"><span data-stu-id="5c072-174">401</span></span> |<span data-ttu-id="5c072-175">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="5c072-175">Unauthorized</span></span> |
| <span data-ttu-id="5c072-176">403</span><span class="sxs-lookup"><span data-stu-id="5c072-176">403</span></span> |<span data-ttu-id="5c072-177">Forbidden</span><span class="sxs-lookup"><span data-stu-id="5c072-177">Forbidden</span></span> |
| <span data-ttu-id="5c072-178">404</span><span class="sxs-lookup"><span data-stu-id="5c072-178">404</span></span> |<span data-ttu-id="5c072-179">Not Found</span><span class="sxs-lookup"><span data-stu-id="5c072-179">Not Found</span></span> |
| <span data-ttu-id="5c072-180">500</span><span class="sxs-lookup"><span data-stu-id="5c072-180">500</span></span> |<span data-ttu-id="5c072-181">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="5c072-181">Internal Server Error.</span></span> <span data-ttu-id="5c072-182">Unknown error occured</span><span class="sxs-lookup"><span data-stu-id="5c072-182">Unknown error occured</span></span> |
| <span data-ttu-id="5c072-183">default</span><span class="sxs-lookup"><span data-stu-id="5c072-183">default</span></span> |<span data-ttu-id="5c072-184">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="5c072-184">Operation Failed.</span></span> |

## <a name="issueopened"></a><span data-ttu-id="5c072-185">IssueOpened</span><span class="sxs-lookup"><span data-stu-id="5c072-185">IssueOpened</span></span>
<span data-ttu-id="5c072-186">When an issue is opened: An issue is opened</span><span class="sxs-lookup"><span data-stu-id="5c072-186">When an issue is opened: An issue is opened</span></span> 

```GET: /trigger/issueOpened``` 

<span data-ttu-id="5c072-187">There are no parameters for this call</span><span class="sxs-lookup"><span data-stu-id="5c072-187">There are no parameters for this call</span></span>

#### <a name="response"></a><span data-ttu-id="5c072-188">Response</span><span class="sxs-lookup"><span data-stu-id="5c072-188">Response</span></span>
| <span data-ttu-id="5c072-189">Name</span><span class="sxs-lookup"><span data-stu-id="5c072-189">Name</span></span> | <span data-ttu-id="5c072-190">Description</span><span class="sxs-lookup"><span data-stu-id="5c072-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5c072-191">200</span><span class="sxs-lookup"><span data-stu-id="5c072-191">200</span></span> |<span data-ttu-id="5c072-192">OK</span><span class="sxs-lookup"><span data-stu-id="5c072-192">OK</span></span> |
| <span data-ttu-id="5c072-193">400</span><span class="sxs-lookup"><span data-stu-id="5c072-193">400</span></span> |<span data-ttu-id="5c072-194">Bad Request</span><span class="sxs-lookup"><span data-stu-id="5c072-194">Bad Request</span></span> |
| <span data-ttu-id="5c072-195">401</span><span class="sxs-lookup"><span data-stu-id="5c072-195">401</span></span> |<span data-ttu-id="5c072-196">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="5c072-196">Unauthorized</span></span> |
| <span data-ttu-id="5c072-197">403</span><span class="sxs-lookup"><span data-stu-id="5c072-197">403</span></span> |<span data-ttu-id="5c072-198">Forbidden</span><span class="sxs-lookup"><span data-stu-id="5c072-198">Forbidden</span></span> |
| <span data-ttu-id="5c072-199">404</span><span class="sxs-lookup"><span data-stu-id="5c072-199">404</span></span> |<span data-ttu-id="5c072-200">Not Found</span><span class="sxs-lookup"><span data-stu-id="5c072-200">Not Found</span></span> |
| <span data-ttu-id="5c072-201">500</span><span class="sxs-lookup"><span data-stu-id="5c072-201">500</span></span> |<span data-ttu-id="5c072-202">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="5c072-202">Internal Server Error.</span></span> <span data-ttu-id="5c072-203">Unknown error occured</span><span class="sxs-lookup"><span data-stu-id="5c072-203">Unknown error occured</span></span> |
| <span data-ttu-id="5c072-204">default</span><span class="sxs-lookup"><span data-stu-id="5c072-204">default</span></span> |<span data-ttu-id="5c072-205">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="5c072-205">Operation Failed.</span></span> |

## <a name="issueclosed"></a><span data-ttu-id="5c072-206">IssueClosed</span><span class="sxs-lookup"><span data-stu-id="5c072-206">IssueClosed</span></span>
<span data-ttu-id="5c072-207">When an issue is closed: An issue is closed</span><span class="sxs-lookup"><span data-stu-id="5c072-207">When an issue is closed: An issue is closed</span></span> 

```GET: /trigger/issueClosed``` 

<span data-ttu-id="5c072-208">There are no parameters for this call</span><span class="sxs-lookup"><span data-stu-id="5c072-208">There are no parameters for this call</span></span>

#### <a name="response"></a><span data-ttu-id="5c072-209">Response</span><span class="sxs-lookup"><span data-stu-id="5c072-209">Response</span></span>
| <span data-ttu-id="5c072-210">Name</span><span class="sxs-lookup"><span data-stu-id="5c072-210">Name</span></span> | <span data-ttu-id="5c072-211">Description</span><span class="sxs-lookup"><span data-stu-id="5c072-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5c072-212">200</span><span class="sxs-lookup"><span data-stu-id="5c072-212">200</span></span> |<span data-ttu-id="5c072-213">OK</span><span class="sxs-lookup"><span data-stu-id="5c072-213">OK</span></span> |
| <span data-ttu-id="5c072-214">400</span><span class="sxs-lookup"><span data-stu-id="5c072-214">400</span></span> |<span data-ttu-id="5c072-215">Bad Request</span><span class="sxs-lookup"><span data-stu-id="5c072-215">Bad Request</span></span> |
| <span data-ttu-id="5c072-216">401</span><span class="sxs-lookup"><span data-stu-id="5c072-216">401</span></span> |<span data-ttu-id="5c072-217">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="5c072-217">Unauthorized</span></span> |
| <span data-ttu-id="5c072-218">403</span><span class="sxs-lookup"><span data-stu-id="5c072-218">403</span></span> |<span data-ttu-id="5c072-219">Forbidden</span><span class="sxs-lookup"><span data-stu-id="5c072-219">Forbidden</span></span> |
| <span data-ttu-id="5c072-220">404</span><span class="sxs-lookup"><span data-stu-id="5c072-220">404</span></span> |<span data-ttu-id="5c072-221">Not Found</span><span class="sxs-lookup"><span data-stu-id="5c072-221">Not Found</span></span> |
| <span data-ttu-id="5c072-222">500</span><span class="sxs-lookup"><span data-stu-id="5c072-222">500</span></span> |<span data-ttu-id="5c072-223">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="5c072-223">Internal Server Error.</span></span> <span data-ttu-id="5c072-224">Unknown error occured</span><span class="sxs-lookup"><span data-stu-id="5c072-224">Unknown error occured</span></span> |
| <span data-ttu-id="5c072-225">default</span><span class="sxs-lookup"><span data-stu-id="5c072-225">default</span></span> |<span data-ttu-id="5c072-226">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="5c072-226">Operation Failed.</span></span> |

## <a name="issueassigned"></a><span data-ttu-id="5c072-227">IssueAssigned</span><span class="sxs-lookup"><span data-stu-id="5c072-227">IssueAssigned</span></span>
<span data-ttu-id="5c072-228">When an issue is assigned: An issue is assigned</span><span class="sxs-lookup"><span data-stu-id="5c072-228">When an issue is assigned: An issue is assigned</span></span> 

```GET: /trigger/issueAssigned``` 

<span data-ttu-id="5c072-229">There are no parameters for this call</span><span class="sxs-lookup"><span data-stu-id="5c072-229">There are no parameters for this call</span></span>

#### <a name="response"></a><span data-ttu-id="5c072-230">Response</span><span class="sxs-lookup"><span data-stu-id="5c072-230">Response</span></span>
| <span data-ttu-id="5c072-231">Name</span><span class="sxs-lookup"><span data-stu-id="5c072-231">Name</span></span> | <span data-ttu-id="5c072-232">Description</span><span class="sxs-lookup"><span data-stu-id="5c072-232">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5c072-233">200</span><span class="sxs-lookup"><span data-stu-id="5c072-233">200</span></span> |<span data-ttu-id="5c072-234">OK</span><span class="sxs-lookup"><span data-stu-id="5c072-234">OK</span></span> |
| <span data-ttu-id="5c072-235">400</span><span class="sxs-lookup"><span data-stu-id="5c072-235">400</span></span> |<span data-ttu-id="5c072-236">Bad Request</span><span class="sxs-lookup"><span data-stu-id="5c072-236">Bad Request</span></span> |
| <span data-ttu-id="5c072-237">401</span><span class="sxs-lookup"><span data-stu-id="5c072-237">401</span></span> |<span data-ttu-id="5c072-238">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="5c072-238">Unauthorized</span></span> |
| <span data-ttu-id="5c072-239">403</span><span class="sxs-lookup"><span data-stu-id="5c072-239">403</span></span> |<span data-ttu-id="5c072-240">Forbidden</span><span class="sxs-lookup"><span data-stu-id="5c072-240">Forbidden</span></span> |
| <span data-ttu-id="5c072-241">404</span><span class="sxs-lookup"><span data-stu-id="5c072-241">404</span></span> |<span data-ttu-id="5c072-242">Not Found</span><span class="sxs-lookup"><span data-stu-id="5c072-242">Not Found</span></span> |
| <span data-ttu-id="5c072-243">500</span><span class="sxs-lookup"><span data-stu-id="5c072-243">500</span></span> |<span data-ttu-id="5c072-244">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="5c072-244">Internal Server Error.</span></span> <span data-ttu-id="5c072-245">Unknown error occured</span><span class="sxs-lookup"><span data-stu-id="5c072-245">Unknown error occured</span></span> |
| <span data-ttu-id="5c072-246">default</span><span class="sxs-lookup"><span data-stu-id="5c072-246">default</span></span> |<span data-ttu-id="5c072-247">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="5c072-247">Operation Failed.</span></span> |

## <a name="object-definitions"></a><span data-ttu-id="5c072-248">Object definitions</span><span class="sxs-lookup"><span data-stu-id="5c072-248">Object definitions</span></span>
### <a name="issuebasicdetailsmodel"></a><span data-ttu-id="5c072-249">IssueBasicDetailsModel</span><span class="sxs-lookup"><span data-stu-id="5c072-249">IssueBasicDetailsModel</span></span>
| <span data-ttu-id="5c072-250">Property Name</span><span class="sxs-lookup"><span data-stu-id="5c072-250">Property Name</span></span> | <span data-ttu-id="5c072-251">Data Type</span><span class="sxs-lookup"><span data-stu-id="5c072-251">Data Type</span></span> | <span data-ttu-id="5c072-252">Required</span><span class="sxs-lookup"><span data-stu-id="5c072-252">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5c072-253">title</span><span class="sxs-lookup"><span data-stu-id="5c072-253">title</span></span> |<span data-ttu-id="5c072-254">string</span><span class="sxs-lookup"><span data-stu-id="5c072-254">string</span></span> |<span data-ttu-id="5c072-255">Yes</span><span class="sxs-lookup"><span data-stu-id="5c072-255">Yes</span></span> |
| <span data-ttu-id="5c072-256">body</span><span class="sxs-lookup"><span data-stu-id="5c072-256">body</span></span> |<span data-ttu-id="5c072-257">string</span><span class="sxs-lookup"><span data-stu-id="5c072-257">string</span></span> |<span data-ttu-id="5c072-258">Yes</span><span class="sxs-lookup"><span data-stu-id="5c072-258">Yes</span></span> |
| <span data-ttu-id="5c072-259">assignee</span><span class="sxs-lookup"><span data-stu-id="5c072-259">assignee</span></span> |<span data-ttu-id="5c072-260">string</span><span class="sxs-lookup"><span data-stu-id="5c072-260">string</span></span> |<span data-ttu-id="5c072-261">Yes</span><span class="sxs-lookup"><span data-stu-id="5c072-261">Yes</span></span> |

### <a name="issuedetailsmodel"></a><span data-ttu-id="5c072-262">IssueDetailsModel</span><span class="sxs-lookup"><span data-stu-id="5c072-262">IssueDetailsModel</span></span>
| <span data-ttu-id="5c072-263">Property Name</span><span class="sxs-lookup"><span data-stu-id="5c072-263">Property Name</span></span> | <span data-ttu-id="5c072-264">Data Type</span><span class="sxs-lookup"><span data-stu-id="5c072-264">Data Type</span></span> | <span data-ttu-id="5c072-265">Required</span><span class="sxs-lookup"><span data-stu-id="5c072-265">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5c072-266">title</span><span class="sxs-lookup"><span data-stu-id="5c072-266">title</span></span> |<span data-ttu-id="5c072-267">string</span><span class="sxs-lookup"><span data-stu-id="5c072-267">string</span></span> |<span data-ttu-id="5c072-268">Yes</span><span class="sxs-lookup"><span data-stu-id="5c072-268">Yes</span></span> |
| <span data-ttu-id="5c072-269">body</span><span class="sxs-lookup"><span data-stu-id="5c072-269">body</span></span> |<span data-ttu-id="5c072-270">string</span><span class="sxs-lookup"><span data-stu-id="5c072-270">string</span></span> |<span data-ttu-id="5c072-271">Yes</span><span class="sxs-lookup"><span data-stu-id="5c072-271">Yes</span></span> |
| <span data-ttu-id="5c072-272">assignee</span><span class="sxs-lookup"><span data-stu-id="5c072-272">assignee</span></span> |<span data-ttu-id="5c072-273">string</span><span class="sxs-lookup"><span data-stu-id="5c072-273">string</span></span> |<span data-ttu-id="5c072-274">Yes</span><span class="sxs-lookup"><span data-stu-id="5c072-274">Yes</span></span> |
| <span data-ttu-id="5c072-275">number</span><span class="sxs-lookup"><span data-stu-id="5c072-275">number</span></span> |<span data-ttu-id="5c072-276">string</span><span class="sxs-lookup"><span data-stu-id="5c072-276">string</span></span> |<span data-ttu-id="5c072-277">No</span><span class="sxs-lookup"><span data-stu-id="5c072-277">No</span></span> |
| <span data-ttu-id="5c072-278">state</span><span class="sxs-lookup"><span data-stu-id="5c072-278">state</span></span> |<span data-ttu-id="5c072-279">string</span><span class="sxs-lookup"><span data-stu-id="5c072-279">string</span></span> |<span data-ttu-id="5c072-280">No</span><span class="sxs-lookup"><span data-stu-id="5c072-280">No</span></span> |
| <span data-ttu-id="5c072-281">created_at</span><span class="sxs-lookup"><span data-stu-id="5c072-281">created_at</span></span> |<span data-ttu-id="5c072-282">string</span><span class="sxs-lookup"><span data-stu-id="5c072-282">string</span></span> |<span data-ttu-id="5c072-283">No</span><span class="sxs-lookup"><span data-stu-id="5c072-283">No</span></span> |
| <span data-ttu-id="5c072-284">repository_url</span><span class="sxs-lookup"><span data-stu-id="5c072-284">repository_url</span></span> |<span data-ttu-id="5c072-285">string</span><span class="sxs-lookup"><span data-stu-id="5c072-285">string</span></span> |<span data-ttu-id="5c072-286">No</span><span class="sxs-lookup"><span data-stu-id="5c072-286">No</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5c072-287">Next Steps</span><span class="sxs-lookup"><span data-stu-id="5c072-287">Next Steps</span></span>
[<span data-ttu-id="5c072-288">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="5c072-288">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

