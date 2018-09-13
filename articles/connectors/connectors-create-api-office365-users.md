---
title: Add the Office 365 Users connector in Logic Apps | Microsoft Docs
description: Overview of Office 365 Users connector with REST API parameters
services: ''
documentationcenter: ''
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: b2146481-9105-4f56-b4c2-7ae340cb922f
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: deonhe
ms.openlocfilehash: 407aaf57cf7e174e1561a3c383e08ab25df78428
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552104"
---
# <a name="get-started-with-the-office-365-users-connector"></a><span data-ttu-id="21ea6-103">Get started with the Office 365 Users connector</span><span class="sxs-lookup"><span data-stu-id="21ea6-103">Get started with the Office 365 Users connector</span></span>
<span data-ttu-id="21ea6-104">Connect to Office 365 Users to get profiles, search users, and more.</span><span class="sxs-lookup"><span data-stu-id="21ea6-104">Connect to Office 365 Users to get profiles, search users, and more.</span></span> 

> [!NOTE]
> <span data-ttu-id="21ea6-105">This version of the article applies to logic apps 2015-08-01-preview schema version.</span><span class="sxs-lookup"><span data-stu-id="21ea6-105">This version of the article applies to logic apps 2015-08-01-preview schema version.</span></span>
> 
> 

<span data-ttu-id="21ea6-106">With Office 365 Users, you can:</span><span class="sxs-lookup"><span data-stu-id="21ea6-106">With Office 365 Users, you can:</span></span>

* <span data-ttu-id="21ea6-107">Build your business flow based on the data you get from Office 365 Users.</span><span class="sxs-lookup"><span data-stu-id="21ea6-107">Build your business flow based on the data you get from Office 365 Users.</span></span> 
* <span data-ttu-id="21ea6-108">Use actions that get direct reports, get a manager's user profile, and more.</span><span class="sxs-lookup"><span data-stu-id="21ea6-108">Use actions that get direct reports, get a manager's user profile, and more.</span></span> <span data-ttu-id="21ea6-109">These actions get a response, and then make the output available for other actions.</span><span class="sxs-lookup"><span data-stu-id="21ea6-109">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="21ea6-110">For example, get a person's direct reports, and then take this information and update a SQL Azure database.</span><span class="sxs-lookup"><span data-stu-id="21ea6-110">For example, get a person's direct reports, and then take this information and update a SQL Azure database.</span></span> 

<span data-ttu-id="21ea6-111">To add an operation in logic apps, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="21ea6-111">To add an operation in logic apps, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="triggers-and-actions"></a><span data-ttu-id="21ea6-112">Triggers and actions</span><span class="sxs-lookup"><span data-stu-id="21ea6-112">Triggers and actions</span></span>
<span data-ttu-id="21ea6-113">The Office 365 Users connector has the following actions available.</span><span class="sxs-lookup"><span data-stu-id="21ea6-113">The Office 365 Users connector has the following actions available.</span></span> <span data-ttu-id="21ea6-114">There are no triggers.</span><span class="sxs-lookup"><span data-stu-id="21ea6-114">There are no triggers.</span></span>

| <span data-ttu-id="21ea6-115">Triggers</span><span class="sxs-lookup"><span data-stu-id="21ea6-115">Triggers</span></span> | <span data-ttu-id="21ea6-116">Actions</span><span class="sxs-lookup"><span data-stu-id="21ea6-116">Actions</span></span> |
| --- | --- |
| <span data-ttu-id="21ea6-117">None</span><span class="sxs-lookup"><span data-stu-id="21ea6-117">None</span></span> |<ul><li><span data-ttu-id="21ea6-118">Get manager</span><span class="sxs-lookup"><span data-stu-id="21ea6-118">Get manager</span></span></li><li><span data-ttu-id="21ea6-119">Get my profile</span><span class="sxs-lookup"><span data-stu-id="21ea6-119">Get my profile</span></span></li><li><span data-ttu-id="21ea6-120">Get direct reports</span><span class="sxs-lookup"><span data-stu-id="21ea6-120">Get direct reports</span></span></li><li><span data-ttu-id="21ea6-121">Get user profile</span><span class="sxs-lookup"><span data-stu-id="21ea6-121">Get user profile</span></span></li><li><span data-ttu-id="21ea6-122">Search for users</span><span class="sxs-lookup"><span data-stu-id="21ea6-122">Search for users</span></span></li></ul> |

<span data-ttu-id="21ea6-123">All connectors support data in JSON and XML formats.</span><span class="sxs-lookup"><span data-stu-id="21ea6-123">All connectors support data in JSON and XML formats.</span></span> 

## <a name="create-a-connection-to-office-365-users"></a><span data-ttu-id="21ea6-124">Create a connection to Office 365 Users</span><span class="sxs-lookup"><span data-stu-id="21ea6-124">Create a connection to Office 365 Users</span></span>
<span data-ttu-id="21ea6-125">When you add this connector to your logic apps, you must sign-in to your Office 365 Users account and allow logic apps to connect to your account.</span><span class="sxs-lookup"><span data-stu-id="21ea6-125">When you add this connector to your logic apps, you must sign-in to your Office 365 Users account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Users](../../includes/connectors-create-api-office365users.md)]
> 
> 

<span data-ttu-id="21ea6-126">After you create the connection, you enter the Office 365 Users properties, like the user ID.</span><span class="sxs-lookup"><span data-stu-id="21ea6-126">After you create the connection, you enter the Office 365 Users properties, like the user ID.</span></span> <span data-ttu-id="21ea6-127">The **REST API reference** in this topic describes these properties.</span><span class="sxs-lookup"><span data-stu-id="21ea6-127">The **REST API reference** in this topic describes these properties.</span></span>

> [!TIP]
> <span data-ttu-id="21ea6-128">You can use this same Office 365 Users connection in other logic apps.</span><span class="sxs-lookup"><span data-stu-id="21ea6-128">You can use this same Office 365 Users connection in other logic apps.</span></span>
> 
> 

## <a name="office-365-users-rest-api-reference"></a><span data-ttu-id="21ea6-129">Office 365 Users REST API reference</span><span class="sxs-lookup"><span data-stu-id="21ea6-129">Office 365 Users REST API reference</span></span>
<span data-ttu-id="21ea6-130">Applies to version: 1.0.</span><span class="sxs-lookup"><span data-stu-id="21ea6-130">Applies to version: 1.0.</span></span>

### <a name="get-my-profile"></a><span data-ttu-id="21ea6-131">Get my profile</span><span class="sxs-lookup"><span data-stu-id="21ea6-131">Get my profile</span></span>
<span data-ttu-id="21ea6-132">Retrieves the profile for the current user.</span><span class="sxs-lookup"><span data-stu-id="21ea6-132">Retrieves the profile for the current user.</span></span>  
```GET: /users/me``` 

<span data-ttu-id="21ea6-133">There are no parameters for this call.</span><span class="sxs-lookup"><span data-stu-id="21ea6-133">There are no parameters for this call.</span></span>

#### <a name="response"></a><span data-ttu-id="21ea6-134">Response</span><span class="sxs-lookup"><span data-stu-id="21ea6-134">Response</span></span>
| <span data-ttu-id="21ea6-135">Name</span><span class="sxs-lookup"><span data-stu-id="21ea6-135">Name</span></span> | <span data-ttu-id="21ea6-136">Description</span><span class="sxs-lookup"><span data-stu-id="21ea6-136">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21ea6-137">200</span><span class="sxs-lookup"><span data-stu-id="21ea6-137">200</span></span> |<span data-ttu-id="21ea6-138">Operation was successful</span><span class="sxs-lookup"><span data-stu-id="21ea6-138">Operation was successful</span></span> |
| <span data-ttu-id="21ea6-139">202</span><span class="sxs-lookup"><span data-stu-id="21ea6-139">202</span></span> |<span data-ttu-id="21ea6-140">Operation was successful</span><span class="sxs-lookup"><span data-stu-id="21ea6-140">Operation was successful</span></span> |
| <span data-ttu-id="21ea6-141">400</span><span class="sxs-lookup"><span data-stu-id="21ea6-141">400</span></span> |<span data-ttu-id="21ea6-142">BadRequest</span><span class="sxs-lookup"><span data-stu-id="21ea6-142">BadRequest</span></span> |
| <span data-ttu-id="21ea6-143">401</span><span class="sxs-lookup"><span data-stu-id="21ea6-143">401</span></span> |<span data-ttu-id="21ea6-144">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="21ea6-144">Unauthorized</span></span> |
| <span data-ttu-id="21ea6-145">403</span><span class="sxs-lookup"><span data-stu-id="21ea6-145">403</span></span> |<span data-ttu-id="21ea6-146">Forbidden</span><span class="sxs-lookup"><span data-stu-id="21ea6-146">Forbidden</span></span> |
| <span data-ttu-id="21ea6-147">500</span><span class="sxs-lookup"><span data-stu-id="21ea6-147">500</span></span> |<span data-ttu-id="21ea6-148">Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="21ea6-148">Internal Server Error</span></span> |
| <span data-ttu-id="21ea6-149">default</span><span class="sxs-lookup"><span data-stu-id="21ea6-149">default</span></span> |<span data-ttu-id="21ea6-150">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="21ea6-150">Operation Failed.</span></span> |

### <a name="get-user-profile"></a><span data-ttu-id="21ea6-151">Get user profile</span><span class="sxs-lookup"><span data-stu-id="21ea6-151">Get user profile</span></span>
<span data-ttu-id="21ea6-152">Retrieves a specific user profile.</span><span class="sxs-lookup"><span data-stu-id="21ea6-152">Retrieves a specific user profile.</span></span>  
```GET: /users/{userId}``` 

| <span data-ttu-id="21ea6-153">Name</span><span class="sxs-lookup"><span data-stu-id="21ea6-153">Name</span></span> | <span data-ttu-id="21ea6-154">Data Type</span><span class="sxs-lookup"><span data-stu-id="21ea6-154">Data Type</span></span> | <span data-ttu-id="21ea6-155">Required</span><span class="sxs-lookup"><span data-stu-id="21ea6-155">Required</span></span> | <span data-ttu-id="21ea6-156">Located In</span><span class="sxs-lookup"><span data-stu-id="21ea6-156">Located In</span></span> | <span data-ttu-id="21ea6-157">Default Value</span><span class="sxs-lookup"><span data-stu-id="21ea6-157">Default Value</span></span> | <span data-ttu-id="21ea6-158">Description</span><span class="sxs-lookup"><span data-stu-id="21ea6-158">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="21ea6-159">userId</span><span class="sxs-lookup"><span data-stu-id="21ea6-159">userId</span></span> |<span data-ttu-id="21ea6-160">string</span><span class="sxs-lookup"><span data-stu-id="21ea6-160">string</span></span> |<span data-ttu-id="21ea6-161">yes</span><span class="sxs-lookup"><span data-stu-id="21ea6-161">yes</span></span> |<span data-ttu-id="21ea6-162">path</span><span class="sxs-lookup"><span data-stu-id="21ea6-162">path</span></span> |<span data-ttu-id="21ea6-163">none</span><span class="sxs-lookup"><span data-stu-id="21ea6-163">none</span></span> |<span data-ttu-id="21ea6-164">User principal name or email id</span><span class="sxs-lookup"><span data-stu-id="21ea6-164">User principal name or email id</span></span> |

#### <a name="response"></a><span data-ttu-id="21ea6-165">Response</span><span class="sxs-lookup"><span data-stu-id="21ea6-165">Response</span></span>
| <span data-ttu-id="21ea6-166">Name</span><span class="sxs-lookup"><span data-stu-id="21ea6-166">Name</span></span> | <span data-ttu-id="21ea6-167">Description</span><span class="sxs-lookup"><span data-stu-id="21ea6-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21ea6-168">200</span><span class="sxs-lookup"><span data-stu-id="21ea6-168">200</span></span> |<span data-ttu-id="21ea6-169">Operation was successful</span><span class="sxs-lookup"><span data-stu-id="21ea6-169">Operation was successful</span></span> |
| <span data-ttu-id="21ea6-170">202</span><span class="sxs-lookup"><span data-stu-id="21ea6-170">202</span></span> |<span data-ttu-id="21ea6-171">Operation was successful</span><span class="sxs-lookup"><span data-stu-id="21ea6-171">Operation was successful</span></span> |
| <span data-ttu-id="21ea6-172">400</span><span class="sxs-lookup"><span data-stu-id="21ea6-172">400</span></span> |<span data-ttu-id="21ea6-173">BadRequest</span><span class="sxs-lookup"><span data-stu-id="21ea6-173">BadRequest</span></span> |
| <span data-ttu-id="21ea6-174">401</span><span class="sxs-lookup"><span data-stu-id="21ea6-174">401</span></span> |<span data-ttu-id="21ea6-175">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="21ea6-175">Unauthorized</span></span> |
| <span data-ttu-id="21ea6-176">403</span><span class="sxs-lookup"><span data-stu-id="21ea6-176">403</span></span> |<span data-ttu-id="21ea6-177">Forbidden</span><span class="sxs-lookup"><span data-stu-id="21ea6-177">Forbidden</span></span> |
| <span data-ttu-id="21ea6-178">500</span><span class="sxs-lookup"><span data-stu-id="21ea6-178">500</span></span> |<span data-ttu-id="21ea6-179">Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="21ea6-179">Internal Server Error</span></span> |
| <span data-ttu-id="21ea6-180">default</span><span class="sxs-lookup"><span data-stu-id="21ea6-180">default</span></span> |<span data-ttu-id="21ea6-181">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="21ea6-181">Operation Failed.</span></span> |

### <a name="get-manager"></a><span data-ttu-id="21ea6-182">Get manager</span><span class="sxs-lookup"><span data-stu-id="21ea6-182">Get manager</span></span>
<span data-ttu-id="21ea6-183">Retrieves user profile for the manager of the specified user.</span><span class="sxs-lookup"><span data-stu-id="21ea6-183">Retrieves user profile for the manager of the specified user.</span></span>  
```GET: /users/{userId}/manager``` 

| <span data-ttu-id="21ea6-184">Name</span><span class="sxs-lookup"><span data-stu-id="21ea6-184">Name</span></span> | <span data-ttu-id="21ea6-185">Data Type</span><span class="sxs-lookup"><span data-stu-id="21ea6-185">Data Type</span></span> | <span data-ttu-id="21ea6-186">Required</span><span class="sxs-lookup"><span data-stu-id="21ea6-186">Required</span></span> | <span data-ttu-id="21ea6-187">Located In</span><span class="sxs-lookup"><span data-stu-id="21ea6-187">Located In</span></span> | <span data-ttu-id="21ea6-188">Default Value</span><span class="sxs-lookup"><span data-stu-id="21ea6-188">Default Value</span></span> | <span data-ttu-id="21ea6-189">Description</span><span class="sxs-lookup"><span data-stu-id="21ea6-189">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="21ea6-190">userId</span><span class="sxs-lookup"><span data-stu-id="21ea6-190">userId</span></span> |<span data-ttu-id="21ea6-191">string</span><span class="sxs-lookup"><span data-stu-id="21ea6-191">string</span></span> |<span data-ttu-id="21ea6-192">yes</span><span class="sxs-lookup"><span data-stu-id="21ea6-192">yes</span></span> |<span data-ttu-id="21ea6-193">path</span><span class="sxs-lookup"><span data-stu-id="21ea6-193">path</span></span> |<span data-ttu-id="21ea6-194">none</span><span class="sxs-lookup"><span data-stu-id="21ea6-194">none</span></span> |<span data-ttu-id="21ea6-195">User principal name or email id</span><span class="sxs-lookup"><span data-stu-id="21ea6-195">User principal name or email id</span></span> |

#### <a name="response"></a><span data-ttu-id="21ea6-196">Response</span><span class="sxs-lookup"><span data-stu-id="21ea6-196">Response</span></span>
| <span data-ttu-id="21ea6-197">Name</span><span class="sxs-lookup"><span data-stu-id="21ea6-197">Name</span></span> | <span data-ttu-id="21ea6-198">Description</span><span class="sxs-lookup"><span data-stu-id="21ea6-198">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21ea6-199">200</span><span class="sxs-lookup"><span data-stu-id="21ea6-199">200</span></span> |<span data-ttu-id="21ea6-200">Operation was successful</span><span class="sxs-lookup"><span data-stu-id="21ea6-200">Operation was successful</span></span> |
| <span data-ttu-id="21ea6-201">202</span><span class="sxs-lookup"><span data-stu-id="21ea6-201">202</span></span> |<span data-ttu-id="21ea6-202">Operation was successful</span><span class="sxs-lookup"><span data-stu-id="21ea6-202">Operation was successful</span></span> |
| <span data-ttu-id="21ea6-203">400</span><span class="sxs-lookup"><span data-stu-id="21ea6-203">400</span></span> |<span data-ttu-id="21ea6-204">BadRequest</span><span class="sxs-lookup"><span data-stu-id="21ea6-204">BadRequest</span></span> |
| <span data-ttu-id="21ea6-205">401</span><span class="sxs-lookup"><span data-stu-id="21ea6-205">401</span></span> |<span data-ttu-id="21ea6-206">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="21ea6-206">Unauthorized</span></span> |
| <span data-ttu-id="21ea6-207">403</span><span class="sxs-lookup"><span data-stu-id="21ea6-207">403</span></span> |<span data-ttu-id="21ea6-208">Forbidden</span><span class="sxs-lookup"><span data-stu-id="21ea6-208">Forbidden</span></span> |
| <span data-ttu-id="21ea6-209">500</span><span class="sxs-lookup"><span data-stu-id="21ea6-209">500</span></span> |<span data-ttu-id="21ea6-210">Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="21ea6-210">Internal Server Error</span></span> |
| <span data-ttu-id="21ea6-211">default</span><span class="sxs-lookup"><span data-stu-id="21ea6-211">default</span></span> |<span data-ttu-id="21ea6-212">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="21ea6-212">Operation Failed.</span></span> |

### <a name="get-direct-reports"></a><span data-ttu-id="21ea6-213">Get direct reports</span><span class="sxs-lookup"><span data-stu-id="21ea6-213">Get direct reports</span></span>
<span data-ttu-id="21ea6-214">Get direct reports.</span><span class="sxs-lookup"><span data-stu-id="21ea6-214">Get direct reports.</span></span>  
```GET: /users/{userId}/directReports``` 

| <span data-ttu-id="21ea6-215">Name</span><span class="sxs-lookup"><span data-stu-id="21ea6-215">Name</span></span> | <span data-ttu-id="21ea6-216">Data Type</span><span class="sxs-lookup"><span data-stu-id="21ea6-216">Data Type</span></span> | <span data-ttu-id="21ea6-217">Required</span><span class="sxs-lookup"><span data-stu-id="21ea6-217">Required</span></span> | <span data-ttu-id="21ea6-218">Located In</span><span class="sxs-lookup"><span data-stu-id="21ea6-218">Located In</span></span> | <span data-ttu-id="21ea6-219">Default Value</span><span class="sxs-lookup"><span data-stu-id="21ea6-219">Default Value</span></span> | <span data-ttu-id="21ea6-220">Description</span><span class="sxs-lookup"><span data-stu-id="21ea6-220">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="21ea6-221">userId</span><span class="sxs-lookup"><span data-stu-id="21ea6-221">userId</span></span> |<span data-ttu-id="21ea6-222">string</span><span class="sxs-lookup"><span data-stu-id="21ea6-222">string</span></span> |<span data-ttu-id="21ea6-223">yes</span><span class="sxs-lookup"><span data-stu-id="21ea6-223">yes</span></span> |<span data-ttu-id="21ea6-224">path</span><span class="sxs-lookup"><span data-stu-id="21ea6-224">path</span></span> |<span data-ttu-id="21ea6-225">none</span><span class="sxs-lookup"><span data-stu-id="21ea6-225">none</span></span> |<span data-ttu-id="21ea6-226">User principal name or email id</span><span class="sxs-lookup"><span data-stu-id="21ea6-226">User principal name or email id</span></span> |

#### <a name="response"></a><span data-ttu-id="21ea6-227">Response</span><span class="sxs-lookup"><span data-stu-id="21ea6-227">Response</span></span>
| <span data-ttu-id="21ea6-228">Name</span><span class="sxs-lookup"><span data-stu-id="21ea6-228">Name</span></span> | <span data-ttu-id="21ea6-229">Description</span><span class="sxs-lookup"><span data-stu-id="21ea6-229">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21ea6-230">200</span><span class="sxs-lookup"><span data-stu-id="21ea6-230">200</span></span> |<span data-ttu-id="21ea6-231">Operation was successful</span><span class="sxs-lookup"><span data-stu-id="21ea6-231">Operation was successful</span></span> |
| <span data-ttu-id="21ea6-232">202</span><span class="sxs-lookup"><span data-stu-id="21ea6-232">202</span></span> |<span data-ttu-id="21ea6-233">Operation was successful</span><span class="sxs-lookup"><span data-stu-id="21ea6-233">Operation was successful</span></span> |
| <span data-ttu-id="21ea6-234">400</span><span class="sxs-lookup"><span data-stu-id="21ea6-234">400</span></span> |<span data-ttu-id="21ea6-235">BadRequest</span><span class="sxs-lookup"><span data-stu-id="21ea6-235">BadRequest</span></span> |
| <span data-ttu-id="21ea6-236">401</span><span class="sxs-lookup"><span data-stu-id="21ea6-236">401</span></span> |<span data-ttu-id="21ea6-237">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="21ea6-237">Unauthorized</span></span> |
| <span data-ttu-id="21ea6-238">403</span><span class="sxs-lookup"><span data-stu-id="21ea6-238">403</span></span> |<span data-ttu-id="21ea6-239">Forbidden</span><span class="sxs-lookup"><span data-stu-id="21ea6-239">Forbidden</span></span> |
| <span data-ttu-id="21ea6-240">500</span><span class="sxs-lookup"><span data-stu-id="21ea6-240">500</span></span> |<span data-ttu-id="21ea6-241">Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="21ea6-241">Internal Server Error</span></span> |
| <span data-ttu-id="21ea6-242">default</span><span class="sxs-lookup"><span data-stu-id="21ea6-242">default</span></span> |<span data-ttu-id="21ea6-243">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="21ea6-243">Operation Failed.</span></span> |

### <a name="search-for-users"></a><span data-ttu-id="21ea6-244">Search for users</span><span class="sxs-lookup"><span data-stu-id="21ea6-244">Search for users</span></span>
<span data-ttu-id="21ea6-245">Retrieves search results of user profiles.</span><span class="sxs-lookup"><span data-stu-id="21ea6-245">Retrieves search results of user profiles.</span></span>  
```GET: /users``` 

| <span data-ttu-id="21ea6-246">Name</span><span class="sxs-lookup"><span data-stu-id="21ea6-246">Name</span></span> | <span data-ttu-id="21ea6-247">Data Type</span><span class="sxs-lookup"><span data-stu-id="21ea6-247">Data Type</span></span> | <span data-ttu-id="21ea6-248">Required</span><span class="sxs-lookup"><span data-stu-id="21ea6-248">Required</span></span> | <span data-ttu-id="21ea6-249">Located In</span><span class="sxs-lookup"><span data-stu-id="21ea6-249">Located In</span></span> | <span data-ttu-id="21ea6-250">Default Value</span><span class="sxs-lookup"><span data-stu-id="21ea6-250">Default Value</span></span> | <span data-ttu-id="21ea6-251">Description</span><span class="sxs-lookup"><span data-stu-id="21ea6-251">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="21ea6-252">searchTerm</span><span class="sxs-lookup"><span data-stu-id="21ea6-252">searchTerm</span></span> |<span data-ttu-id="21ea6-253">string</span><span class="sxs-lookup"><span data-stu-id="21ea6-253">string</span></span> |<span data-ttu-id="21ea6-254">no</span><span class="sxs-lookup"><span data-stu-id="21ea6-254">no</span></span> |<span data-ttu-id="21ea6-255">query</span><span class="sxs-lookup"><span data-stu-id="21ea6-255">query</span></span> |<span data-ttu-id="21ea6-256">none</span><span class="sxs-lookup"><span data-stu-id="21ea6-256">none</span></span> |<span data-ttu-id="21ea6-257">Search string (applies to: display name, given name, surname, mail, mail nickname and user principal name)</span><span class="sxs-lookup"><span data-stu-id="21ea6-257">Search string (applies to: display name, given name, surname, mail, mail nickname and user principal name)</span></span> |

#### <a name="response"></a><span data-ttu-id="21ea6-258">Response</span><span class="sxs-lookup"><span data-stu-id="21ea6-258">Response</span></span>
| <span data-ttu-id="21ea6-259">Name</span><span class="sxs-lookup"><span data-stu-id="21ea6-259">Name</span></span> | <span data-ttu-id="21ea6-260">Description</span><span class="sxs-lookup"><span data-stu-id="21ea6-260">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21ea6-261">200</span><span class="sxs-lookup"><span data-stu-id="21ea6-261">200</span></span> |<span data-ttu-id="21ea6-262">Operation was successful</span><span class="sxs-lookup"><span data-stu-id="21ea6-262">Operation was successful</span></span> |
| <span data-ttu-id="21ea6-263">202</span><span class="sxs-lookup"><span data-stu-id="21ea6-263">202</span></span> |<span data-ttu-id="21ea6-264">Operation was successful</span><span class="sxs-lookup"><span data-stu-id="21ea6-264">Operation was successful</span></span> |
| <span data-ttu-id="21ea6-265">400</span><span class="sxs-lookup"><span data-stu-id="21ea6-265">400</span></span> |<span data-ttu-id="21ea6-266">BadRequest</span><span class="sxs-lookup"><span data-stu-id="21ea6-266">BadRequest</span></span> |
| <span data-ttu-id="21ea6-267">401</span><span class="sxs-lookup"><span data-stu-id="21ea6-267">401</span></span> |<span data-ttu-id="21ea6-268">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="21ea6-268">Unauthorized</span></span> |
| <span data-ttu-id="21ea6-269">403</span><span class="sxs-lookup"><span data-stu-id="21ea6-269">403</span></span> |<span data-ttu-id="21ea6-270">Forbidden</span><span class="sxs-lookup"><span data-stu-id="21ea6-270">Forbidden</span></span> |
| <span data-ttu-id="21ea6-271">500</span><span class="sxs-lookup"><span data-stu-id="21ea6-271">500</span></span> |<span data-ttu-id="21ea6-272">Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="21ea6-272">Internal Server Error</span></span> |
| <span data-ttu-id="21ea6-273">default</span><span class="sxs-lookup"><span data-stu-id="21ea6-273">default</span></span> |<span data-ttu-id="21ea6-274">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="21ea6-274">Operation Failed.</span></span> |

## <a name="object-definitions"></a><span data-ttu-id="21ea6-275">Object definitions</span><span class="sxs-lookup"><span data-stu-id="21ea6-275">Object definitions</span></span>
#### <a name="user-user-model-class"></a><span data-ttu-id="21ea6-276">User: User model class</span><span class="sxs-lookup"><span data-stu-id="21ea6-276">User: User model class</span></span>
| <span data-ttu-id="21ea6-277">Property Name</span><span class="sxs-lookup"><span data-stu-id="21ea6-277">Property Name</span></span> | <span data-ttu-id="21ea6-278">Data Type</span><span class="sxs-lookup"><span data-stu-id="21ea6-278">Data Type</span></span> | <span data-ttu-id="21ea6-279">Required</span><span class="sxs-lookup"><span data-stu-id="21ea6-279">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21ea6-280">DisplayName</span><span class="sxs-lookup"><span data-stu-id="21ea6-280">DisplayName</span></span> |<span data-ttu-id="21ea6-281">string</span><span class="sxs-lookup"><span data-stu-id="21ea6-281">string</span></span> |<span data-ttu-id="21ea6-282">no</span><span class="sxs-lookup"><span data-stu-id="21ea6-282">no</span></span> |
| <span data-ttu-id="21ea6-283">GivenName</span><span class="sxs-lookup"><span data-stu-id="21ea6-283">GivenName</span></span> |<span data-ttu-id="21ea6-284">string</span><span class="sxs-lookup"><span data-stu-id="21ea6-284">string</span></span> |<span data-ttu-id="21ea6-285">no</span><span class="sxs-lookup"><span data-stu-id="21ea6-285">no</span></span> |
| <span data-ttu-id="21ea6-286">Surname</span><span class="sxs-lookup"><span data-stu-id="21ea6-286">Surname</span></span> |<span data-ttu-id="21ea6-287">string</span><span class="sxs-lookup"><span data-stu-id="21ea6-287">string</span></span> |<span data-ttu-id="21ea6-288">no</span><span class="sxs-lookup"><span data-stu-id="21ea6-288">no</span></span> |
| <span data-ttu-id="21ea6-289">Mail</span><span class="sxs-lookup"><span data-stu-id="21ea6-289">Mail</span></span> |<span data-ttu-id="21ea6-290">string</span><span class="sxs-lookup"><span data-stu-id="21ea6-290">string</span></span> |<span data-ttu-id="21ea6-291">no</span><span class="sxs-lookup"><span data-stu-id="21ea6-291">no</span></span> |
| <span data-ttu-id="21ea6-292">MailNickname</span><span class="sxs-lookup"><span data-stu-id="21ea6-292">MailNickname</span></span> |<span data-ttu-id="21ea6-293">string</span><span class="sxs-lookup"><span data-stu-id="21ea6-293">string</span></span> |<span data-ttu-id="21ea6-294">no</span><span class="sxs-lookup"><span data-stu-id="21ea6-294">no</span></span> |
| <span data-ttu-id="21ea6-295">TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="21ea6-295">TelephoneNumber</span></span> |<span data-ttu-id="21ea6-296">string</span><span class="sxs-lookup"><span data-stu-id="21ea6-296">string</span></span> |<span data-ttu-id="21ea6-297">no</span><span class="sxs-lookup"><span data-stu-id="21ea6-297">no</span></span> |
| <span data-ttu-id="21ea6-298">AccountEnabled</span><span class="sxs-lookup"><span data-stu-id="21ea6-298">AccountEnabled</span></span> |<span data-ttu-id="21ea6-299">boolean</span><span class="sxs-lookup"><span data-stu-id="21ea6-299">boolean</span></span> |<span data-ttu-id="21ea6-300">no</span><span class="sxs-lookup"><span data-stu-id="21ea6-300">no</span></span> |
| <span data-ttu-id="21ea6-301">Id</span><span class="sxs-lookup"><span data-stu-id="21ea6-301">Id</span></span> |<span data-ttu-id="21ea6-302">string</span><span class="sxs-lookup"><span data-stu-id="21ea6-302">string</span></span> |<span data-ttu-id="21ea6-303">yes</span><span class="sxs-lookup"><span data-stu-id="21ea6-303">yes</span></span> |
| <span data-ttu-id="21ea6-304">UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="21ea6-304">UserPrincipalName</span></span> |<span data-ttu-id="21ea6-305">string</span><span class="sxs-lookup"><span data-stu-id="21ea6-305">string</span></span> |<span data-ttu-id="21ea6-306">no</span><span class="sxs-lookup"><span data-stu-id="21ea6-306">no</span></span> |
| <span data-ttu-id="21ea6-307">Department</span><span class="sxs-lookup"><span data-stu-id="21ea6-307">Department</span></span> |<span data-ttu-id="21ea6-308">string</span><span class="sxs-lookup"><span data-stu-id="21ea6-308">string</span></span> |<span data-ttu-id="21ea6-309">no</span><span class="sxs-lookup"><span data-stu-id="21ea6-309">no</span></span> |
| <span data-ttu-id="21ea6-310">JobTitle</span><span class="sxs-lookup"><span data-stu-id="21ea6-310">JobTitle</span></span> |<span data-ttu-id="21ea6-311">string</span><span class="sxs-lookup"><span data-stu-id="21ea6-311">string</span></span> |<span data-ttu-id="21ea6-312">no</span><span class="sxs-lookup"><span data-stu-id="21ea6-312">no</span></span> |
| <span data-ttu-id="21ea6-313">mobilePhone</span><span class="sxs-lookup"><span data-stu-id="21ea6-313">mobilePhone</span></span> |<span data-ttu-id="21ea6-314">string</span><span class="sxs-lookup"><span data-stu-id="21ea6-314">string</span></span> |<span data-ttu-id="21ea6-315">no</span><span class="sxs-lookup"><span data-stu-id="21ea6-315">no</span></span> |

## <a name="next-steps"></a><span data-ttu-id="21ea6-316">Next Steps</span><span class="sxs-lookup"><span data-stu-id="21ea6-316">Next Steps</span></span>
<span data-ttu-id="21ea6-317">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="21ea6-317">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="21ea6-318">Go back to the [APIs list](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="21ea6-318">Go back to the [APIs list](apis-list.md).</span></span>

<!--References-->
[5]: https://portal.azure.com
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-office365-users/aad-tenant-applications.PNG
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-office365-users/aad-tenant-applications-add-appinfo.PNG
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-office365-users/aad-tenant-applications-add-app-properties.PNG
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-office365-users/contoso-aad-app.PNG
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-office365-users/contoso-aad-app-configure.PNG





