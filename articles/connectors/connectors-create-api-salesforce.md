---
title: Learn to use the Salesforce Connector in your logic apps| Microsoft Docs
description: Create logic apps with Azure App service. The Salesforce Connector provides an API to work with Salesforce objects.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: 54fe5af8-7d2a-4da8-94e7-15d029e029bf
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/05/2016
ms.author: deonhe
ms.openlocfilehash: b6758aa36120c9c187e91ee5d9e7ceb5041eae6a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556359"
---
# <a name="get-started-with-the-salesforce-connector"></a><span data-ttu-id="67b66-104">Get started with the Salesforce connector</span><span class="sxs-lookup"><span data-stu-id="67b66-104">Get started with the Salesforce connector</span></span>
<span data-ttu-id="67b66-105">The Salesforce Connector provides an API to work with Salesforce objects.</span><span class="sxs-lookup"><span data-stu-id="67b66-105">The Salesforce Connector provides an API to work with Salesforce objects.</span></span>

<span data-ttu-id="67b66-106">To use [any connector](apis-list.md), you first need to create a logic app.</span><span class="sxs-lookup"><span data-stu-id="67b66-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="67b66-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="67b66-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-salesforce-connector"></a><span data-ttu-id="67b66-108">Connect to Salesforce connector</span><span class="sxs-lookup"><span data-stu-id="67b66-108">Connect to Salesforce connector</span></span>
<span data-ttu-id="67b66-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span><span class="sxs-lookup"><span data-stu-id="67b66-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="67b66-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span><span class="sxs-lookup"><span data-stu-id="67b66-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-salesforce-connector"></a><span data-ttu-id="67b66-111">Create a connection to Salesforce connector</span><span class="sxs-lookup"><span data-stu-id="67b66-111">Create a connection to Salesforce connector</span></span>
> [!INCLUDE [Steps to create a connection to Salesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="67b66-112">Use a Salesforce connector trigger</span><span class="sxs-lookup"><span data-stu-id="67b66-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="67b66-113">A trigger is an event that can be used to start the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="67b66-113">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="67b66-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="67b66-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="67b66-115">Add a condition</span><span class="sxs-lookup"><span data-stu-id="67b66-115">Add a condition</span></span>
> [!INCLUDE [Steps to create a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="67b66-116">Use a Salesforce connector action</span><span class="sxs-lookup"><span data-stu-id="67b66-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="67b66-117">An action is an operation carried out by the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="67b66-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="67b66-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="67b66-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="technical-details"></a><span data-ttu-id="67b66-119">Technical details</span><span class="sxs-lookup"><span data-stu-id="67b66-119">Technical details</span></span>
<span data-ttu-id="67b66-120">Here are the details about the triggers, actions and responses that this connection supports:</span><span class="sxs-lookup"><span data-stu-id="67b66-120">Here are the details about the triggers, actions and responses that this connection supports:</span></span>

## <a name="salesforce-connector-triggers"></a><span data-ttu-id="67b66-121">Salesforce connector triggers</span><span class="sxs-lookup"><span data-stu-id="67b66-121">Salesforce connector triggers</span></span>
<span data-ttu-id="67b66-122">Salesforce Connector has the following trigger(s):</span><span class="sxs-lookup"><span data-stu-id="67b66-122">Salesforce Connector has the following trigger(s):</span></span>  

| <span data-ttu-id="67b66-123">Trigger</span><span class="sxs-lookup"><span data-stu-id="67b66-123">Trigger</span></span> | <span data-ttu-id="67b66-124">Description</span><span class="sxs-lookup"><span data-stu-id="67b66-124">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="67b66-125">When an object is created</span><span class="sxs-lookup"><span data-stu-id="67b66-125">When an object is created</span></span>](connectors-create-api-salesforce.md#when-an-object-is-created) |<span data-ttu-id="67b66-126">This operation triggers a flow when an object is created.</span><span class="sxs-lookup"><span data-stu-id="67b66-126">This operation triggers a flow when an object is created.</span></span> |
| [<span data-ttu-id="67b66-127">When an object is modified</span><span class="sxs-lookup"><span data-stu-id="67b66-127">When an object is modified</span></span>](connectors-create-api-salesforce.md#when-an-object-is-modified) |<span data-ttu-id="67b66-128">This operation triggers a flow when an object is modified.</span><span class="sxs-lookup"><span data-stu-id="67b66-128">This operation triggers a flow when an object is modified.</span></span> |

## <a name="salesforce-connector-actions"></a><span data-ttu-id="67b66-129">Salesforce connector actions</span><span class="sxs-lookup"><span data-stu-id="67b66-129">Salesforce connector actions</span></span>
<span data-ttu-id="67b66-130">Salesforce Connector has the following actions:</span><span class="sxs-lookup"><span data-stu-id="67b66-130">Salesforce Connector has the following actions:</span></span>

| <span data-ttu-id="67b66-131">Action</span><span class="sxs-lookup"><span data-stu-id="67b66-131">Action</span></span> | <span data-ttu-id="67b66-132">Description</span><span class="sxs-lookup"><span data-stu-id="67b66-132">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="67b66-133">Get objects</span><span class="sxs-lookup"><span data-stu-id="67b66-133">Get objects</span></span>](connectors-create-api-salesforce.md#get-objects) |<span data-ttu-id="67b66-134">Thie operation gets objects of a certain object type like 'Lead'.</span><span class="sxs-lookup"><span data-stu-id="67b66-134">Thie operation gets objects of a certain object type like 'Lead'.</span></span> |
| [<span data-ttu-id="67b66-135">Create object</span><span class="sxs-lookup"><span data-stu-id="67b66-135">Create object</span></span>](connectors-create-api-salesforce.md#create-object) |<span data-ttu-id="67b66-136">This operation creates an object.</span><span class="sxs-lookup"><span data-stu-id="67b66-136">This operation creates an object.</span></span> |
| [<span data-ttu-id="67b66-137">Get object</span><span class="sxs-lookup"><span data-stu-id="67b66-137">Get object</span></span>](connectors-create-api-salesforce.md#get-object) |<span data-ttu-id="67b66-138">This operation gets an object.</span><span class="sxs-lookup"><span data-stu-id="67b66-138">This operation gets an object.</span></span> |
| [<span data-ttu-id="67b66-139">Delete object</span><span class="sxs-lookup"><span data-stu-id="67b66-139">Delete object</span></span>](connectors-create-api-salesforce.md#delete-object) |<span data-ttu-id="67b66-140">This operation deletes an object.</span><span class="sxs-lookup"><span data-stu-id="67b66-140">This operation deletes an object.</span></span> |
| [<span data-ttu-id="67b66-141">Update object</span><span class="sxs-lookup"><span data-stu-id="67b66-141">Update object</span></span>](connectors-create-api-salesforce.md#update-object) |<span data-ttu-id="67b66-142">This operation updates an object.</span><span class="sxs-lookup"><span data-stu-id="67b66-142">This operation updates an object.</span></span> |
| [<span data-ttu-id="67b66-143">Get object types</span><span class="sxs-lookup"><span data-stu-id="67b66-143">Get object types</span></span>](connectors-create-api-salesforce.md#get-object-types) |<span data-ttu-id="67b66-144">This operation lists the available object types.</span><span class="sxs-lookup"><span data-stu-id="67b66-144">This operation lists the available object types.</span></span> |

### <a name="action-details"></a><span data-ttu-id="67b66-145">Action details</span><span class="sxs-lookup"><span data-stu-id="67b66-145">Action details</span></span>
<span data-ttu-id="67b66-146">Here are the details for the actions and triggers for this connector, along with their responses:</span><span class="sxs-lookup"><span data-stu-id="67b66-146">Here are the details for the actions and triggers for this connector, along with their responses:</span></span>

### <a name="get-objects"></a><span data-ttu-id="67b66-147">Get objects</span><span class="sxs-lookup"><span data-stu-id="67b66-147">Get objects</span></span>
<span data-ttu-id="67b66-148">Thie operation gets objects of a certain object type like 'Lead'.</span><span class="sxs-lookup"><span data-stu-id="67b66-148">Thie operation gets objects of a certain object type like 'Lead'.</span></span> 

| <span data-ttu-id="67b66-149">Property Name</span><span class="sxs-lookup"><span data-stu-id="67b66-149">Property Name</span></span> | <span data-ttu-id="67b66-150">Display Name</span><span class="sxs-lookup"><span data-stu-id="67b66-150">Display Name</span></span> | <span data-ttu-id="67b66-151">Description</span><span class="sxs-lookup"><span data-stu-id="67b66-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67b66-152">table\*</span><span class="sxs-lookup"><span data-stu-id="67b66-152">table\*</span></span> |<span data-ttu-id="67b66-153">Object type</span><span class="sxs-lookup"><span data-stu-id="67b66-153">Object type</span></span> |<span data-ttu-id="67b66-154">Salesforce object type like 'Lead'</span><span class="sxs-lookup"><span data-stu-id="67b66-154">Salesforce object type like 'Lead'</span></span> |
| <span data-ttu-id="67b66-155">$filter</span><span class="sxs-lookup"><span data-stu-id="67b66-155">$filter</span></span> |<span data-ttu-id="67b66-156">Filter Query</span><span class="sxs-lookup"><span data-stu-id="67b66-156">Filter Query</span></span> |<span data-ttu-id="67b66-157">An ODATA filter query to restrict the number of entries</span><span class="sxs-lookup"><span data-stu-id="67b66-157">An ODATA filter query to restrict the number of entries</span></span> |
| <span data-ttu-id="67b66-158">$orderby</span><span class="sxs-lookup"><span data-stu-id="67b66-158">$orderby</span></span> |<span data-ttu-id="67b66-159">Order By</span><span class="sxs-lookup"><span data-stu-id="67b66-159">Order By</span></span> |<span data-ttu-id="67b66-160">An ODATA orderBy query for specifying the order of entries</span><span class="sxs-lookup"><span data-stu-id="67b66-160">An ODATA orderBy query for specifying the order of entries</span></span> |
| <span data-ttu-id="67b66-161">$skip</span><span class="sxs-lookup"><span data-stu-id="67b66-161">$skip</span></span> |<span data-ttu-id="67b66-162">Skip Count</span><span class="sxs-lookup"><span data-stu-id="67b66-162">Skip Count</span></span> |<span data-ttu-id="67b66-163">Number of entries to skip (default = 0)</span><span class="sxs-lookup"><span data-stu-id="67b66-163">Number of entries to skip (default = 0)</span></span> |
| <span data-ttu-id="67b66-164">$top</span><span class="sxs-lookup"><span data-stu-id="67b66-164">$top</span></span> |<span data-ttu-id="67b66-165">Maximum Get Count</span><span class="sxs-lookup"><span data-stu-id="67b66-165">Maximum Get Count</span></span> |<span data-ttu-id="67b66-166">Maximum number of entries to retrieve (default = 256)</span><span class="sxs-lookup"><span data-stu-id="67b66-166">Maximum number of entries to retrieve (default = 256)</span></span> |

<span data-ttu-id="67b66-167">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="67b66-167">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="67b66-168">Output details</span><span class="sxs-lookup"><span data-stu-id="67b66-168">Output details</span></span>
<span data-ttu-id="67b66-169">ItemsList</span><span class="sxs-lookup"><span data-stu-id="67b66-169">ItemsList</span></span>

| <span data-ttu-id="67b66-170">Property Name</span><span class="sxs-lookup"><span data-stu-id="67b66-170">Property Name</span></span> | <span data-ttu-id="67b66-171">Data Type</span><span class="sxs-lookup"><span data-stu-id="67b66-171">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="67b66-172">value</span><span class="sxs-lookup"><span data-stu-id="67b66-172">value</span></span> |<span data-ttu-id="67b66-173">array</span><span class="sxs-lookup"><span data-stu-id="67b66-173">array</span></span> |

### <a name="create-object"></a><span data-ttu-id="67b66-174">Create object</span><span class="sxs-lookup"><span data-stu-id="67b66-174">Create object</span></span>
<span data-ttu-id="67b66-175">This operation creates an object.</span><span class="sxs-lookup"><span data-stu-id="67b66-175">This operation creates an object.</span></span> 

| <span data-ttu-id="67b66-176">Property Name</span><span class="sxs-lookup"><span data-stu-id="67b66-176">Property Name</span></span> | <span data-ttu-id="67b66-177">Display Name</span><span class="sxs-lookup"><span data-stu-id="67b66-177">Display Name</span></span> | <span data-ttu-id="67b66-178">Description</span><span class="sxs-lookup"><span data-stu-id="67b66-178">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67b66-179">table\*</span><span class="sxs-lookup"><span data-stu-id="67b66-179">table\*</span></span> |<span data-ttu-id="67b66-180">Object type</span><span class="sxs-lookup"><span data-stu-id="67b66-180">Object type</span></span> |<span data-ttu-id="67b66-181">Object type like 'Lead'</span><span class="sxs-lookup"><span data-stu-id="67b66-181">Object type like 'Lead'</span></span> |
| <span data-ttu-id="67b66-182">item\*</span><span class="sxs-lookup"><span data-stu-id="67b66-182">item\*</span></span> |<span data-ttu-id="67b66-183">Object</span><span class="sxs-lookup"><span data-stu-id="67b66-183">Object</span></span> |<span data-ttu-id="67b66-184">Object to create</span><span class="sxs-lookup"><span data-stu-id="67b66-184">Object to create</span></span> |

<span data-ttu-id="67b66-185">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="67b66-185">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="67b66-186">Output details</span><span class="sxs-lookup"><span data-stu-id="67b66-186">Output details</span></span>
<span data-ttu-id="67b66-187">Item</span><span class="sxs-lookup"><span data-stu-id="67b66-187">Item</span></span>

| <span data-ttu-id="67b66-188">Property Name</span><span class="sxs-lookup"><span data-stu-id="67b66-188">Property Name</span></span> | <span data-ttu-id="67b66-189">Data Type</span><span class="sxs-lookup"><span data-stu-id="67b66-189">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="67b66-190">ItemInternalId</span><span class="sxs-lookup"><span data-stu-id="67b66-190">ItemInternalId</span></span> |<span data-ttu-id="67b66-191">string</span><span class="sxs-lookup"><span data-stu-id="67b66-191">string</span></span> |

### <a name="get-object"></a><span data-ttu-id="67b66-192">Get object</span><span class="sxs-lookup"><span data-stu-id="67b66-192">Get object</span></span>
<span data-ttu-id="67b66-193">This operation gets an object.</span><span class="sxs-lookup"><span data-stu-id="67b66-193">This operation gets an object.</span></span> 

| <span data-ttu-id="67b66-194">Property Name</span><span class="sxs-lookup"><span data-stu-id="67b66-194">Property Name</span></span> | <span data-ttu-id="67b66-195">Display Name</span><span class="sxs-lookup"><span data-stu-id="67b66-195">Display Name</span></span> | <span data-ttu-id="67b66-196">Description</span><span class="sxs-lookup"><span data-stu-id="67b66-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67b66-197">table\*</span><span class="sxs-lookup"><span data-stu-id="67b66-197">table\*</span></span> |<span data-ttu-id="67b66-198">Object type</span><span class="sxs-lookup"><span data-stu-id="67b66-198">Object type</span></span> |<span data-ttu-id="67b66-199">Salesforce object type like 'Lead'</span><span class="sxs-lookup"><span data-stu-id="67b66-199">Salesforce object type like 'Lead'</span></span> |
| <span data-ttu-id="67b66-200">id\*</span><span class="sxs-lookup"><span data-stu-id="67b66-200">id\*</span></span> |<span data-ttu-id="67b66-201">Object id</span><span class="sxs-lookup"><span data-stu-id="67b66-201">Object id</span></span> |<span data-ttu-id="67b66-202">Identifier of object to get</span><span class="sxs-lookup"><span data-stu-id="67b66-202">Identifier of object to get</span></span> |

<span data-ttu-id="67b66-203">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="67b66-203">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="67b66-204">Output details</span><span class="sxs-lookup"><span data-stu-id="67b66-204">Output details</span></span>
<span data-ttu-id="67b66-205">Item</span><span class="sxs-lookup"><span data-stu-id="67b66-205">Item</span></span>

| <span data-ttu-id="67b66-206">Property Name</span><span class="sxs-lookup"><span data-stu-id="67b66-206">Property Name</span></span> | <span data-ttu-id="67b66-207">Data Type</span><span class="sxs-lookup"><span data-stu-id="67b66-207">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="67b66-208">ItemInternalId</span><span class="sxs-lookup"><span data-stu-id="67b66-208">ItemInternalId</span></span> |<span data-ttu-id="67b66-209">string</span><span class="sxs-lookup"><span data-stu-id="67b66-209">string</span></span> |

### <a name="delete-object"></a><span data-ttu-id="67b66-210">Delete object</span><span class="sxs-lookup"><span data-stu-id="67b66-210">Delete object</span></span>
<span data-ttu-id="67b66-211">This operation deletes an object.</span><span class="sxs-lookup"><span data-stu-id="67b66-211">This operation deletes an object.</span></span> 

| <span data-ttu-id="67b66-212">Property Name</span><span class="sxs-lookup"><span data-stu-id="67b66-212">Property Name</span></span> | <span data-ttu-id="67b66-213">Display Name</span><span class="sxs-lookup"><span data-stu-id="67b66-213">Display Name</span></span> | <span data-ttu-id="67b66-214">Description</span><span class="sxs-lookup"><span data-stu-id="67b66-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67b66-215">table\*</span><span class="sxs-lookup"><span data-stu-id="67b66-215">table\*</span></span> |<span data-ttu-id="67b66-216">Object type</span><span class="sxs-lookup"><span data-stu-id="67b66-216">Object type</span></span> |<span data-ttu-id="67b66-217">Object type like 'Lead'</span><span class="sxs-lookup"><span data-stu-id="67b66-217">Object type like 'Lead'</span></span> |
| <span data-ttu-id="67b66-218">id\*</span><span class="sxs-lookup"><span data-stu-id="67b66-218">id\*</span></span> |<span data-ttu-id="67b66-219">Object id</span><span class="sxs-lookup"><span data-stu-id="67b66-219">Object id</span></span> |<span data-ttu-id="67b66-220">Identifier of object to delete</span><span class="sxs-lookup"><span data-stu-id="67b66-220">Identifier of object to delete</span></span> |

<span data-ttu-id="67b66-221">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="67b66-221">An \* indicates that a property is required</span></span>

### <a name="update-object"></a><span data-ttu-id="67b66-222">Update object</span><span class="sxs-lookup"><span data-stu-id="67b66-222">Update object</span></span>
<span data-ttu-id="67b66-223">This operation updates an object.</span><span class="sxs-lookup"><span data-stu-id="67b66-223">This operation updates an object.</span></span> 

| <span data-ttu-id="67b66-224">Property Name</span><span class="sxs-lookup"><span data-stu-id="67b66-224">Property Name</span></span> | <span data-ttu-id="67b66-225">Display Name</span><span class="sxs-lookup"><span data-stu-id="67b66-225">Display Name</span></span> | <span data-ttu-id="67b66-226">Description</span><span class="sxs-lookup"><span data-stu-id="67b66-226">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67b66-227">table\*</span><span class="sxs-lookup"><span data-stu-id="67b66-227">table\*</span></span> |<span data-ttu-id="67b66-228">Object type</span><span class="sxs-lookup"><span data-stu-id="67b66-228">Object type</span></span> |<span data-ttu-id="67b66-229">Object type like 'Lead'</span><span class="sxs-lookup"><span data-stu-id="67b66-229">Object type like 'Lead'</span></span> |
| <span data-ttu-id="67b66-230">id\*</span><span class="sxs-lookup"><span data-stu-id="67b66-230">id\*</span></span> |<span data-ttu-id="67b66-231">Object id</span><span class="sxs-lookup"><span data-stu-id="67b66-231">Object id</span></span> |<span data-ttu-id="67b66-232">Identifier of object to update</span><span class="sxs-lookup"><span data-stu-id="67b66-232">Identifier of object to update</span></span> |
| <span data-ttu-id="67b66-233">item\*</span><span class="sxs-lookup"><span data-stu-id="67b66-233">item\*</span></span> |<span data-ttu-id="67b66-234">Object</span><span class="sxs-lookup"><span data-stu-id="67b66-234">Object</span></span> |<span data-ttu-id="67b66-235">Object with changed properties</span><span class="sxs-lookup"><span data-stu-id="67b66-235">Object with changed properties</span></span> |

<span data-ttu-id="67b66-236">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="67b66-236">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="67b66-237">Output details</span><span class="sxs-lookup"><span data-stu-id="67b66-237">Output details</span></span>
<span data-ttu-id="67b66-238">Item</span><span class="sxs-lookup"><span data-stu-id="67b66-238">Item</span></span>

| <span data-ttu-id="67b66-239">Property Name</span><span class="sxs-lookup"><span data-stu-id="67b66-239">Property Name</span></span> | <span data-ttu-id="67b66-240">Data Type</span><span class="sxs-lookup"><span data-stu-id="67b66-240">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="67b66-241">ItemInternalId</span><span class="sxs-lookup"><span data-stu-id="67b66-241">ItemInternalId</span></span> |<span data-ttu-id="67b66-242">string</span><span class="sxs-lookup"><span data-stu-id="67b66-242">string</span></span> |

### <a name="when-an-object-is-created"></a><span data-ttu-id="67b66-243">When an object is created</span><span class="sxs-lookup"><span data-stu-id="67b66-243">When an object is created</span></span>
<span data-ttu-id="67b66-244">This operation triggers a flow when an object is created.</span><span class="sxs-lookup"><span data-stu-id="67b66-244">This operation triggers a flow when an object is created.</span></span> 

| <span data-ttu-id="67b66-245">Property Name</span><span class="sxs-lookup"><span data-stu-id="67b66-245">Property Name</span></span> | <span data-ttu-id="67b66-246">Display Name</span><span class="sxs-lookup"><span data-stu-id="67b66-246">Display Name</span></span> | <span data-ttu-id="67b66-247">Description</span><span class="sxs-lookup"><span data-stu-id="67b66-247">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67b66-248">table\*</span><span class="sxs-lookup"><span data-stu-id="67b66-248">table\*</span></span> |<span data-ttu-id="67b66-249">Object type</span><span class="sxs-lookup"><span data-stu-id="67b66-249">Object type</span></span> |<span data-ttu-id="67b66-250">Object type like 'Lead'</span><span class="sxs-lookup"><span data-stu-id="67b66-250">Object type like 'Lead'</span></span> |
| <span data-ttu-id="67b66-251">$filter</span><span class="sxs-lookup"><span data-stu-id="67b66-251">$filter</span></span> |<span data-ttu-id="67b66-252">Filter Query</span><span class="sxs-lookup"><span data-stu-id="67b66-252">Filter Query</span></span> |<span data-ttu-id="67b66-253">An ODATA filter query to restrict the number of entries</span><span class="sxs-lookup"><span data-stu-id="67b66-253">An ODATA filter query to restrict the number of entries</span></span> |
| <span data-ttu-id="67b66-254">$orderby</span><span class="sxs-lookup"><span data-stu-id="67b66-254">$orderby</span></span> |<span data-ttu-id="67b66-255">Order By</span><span class="sxs-lookup"><span data-stu-id="67b66-255">Order By</span></span> |<span data-ttu-id="67b66-256">An ODATA orderBy query for specifying the order of entries</span><span class="sxs-lookup"><span data-stu-id="67b66-256">An ODATA orderBy query for specifying the order of entries</span></span> |
| <span data-ttu-id="67b66-257">$skip</span><span class="sxs-lookup"><span data-stu-id="67b66-257">$skip</span></span> |<span data-ttu-id="67b66-258">Skip Count</span><span class="sxs-lookup"><span data-stu-id="67b66-258">Skip Count</span></span> |<span data-ttu-id="67b66-259">Number of entries to skip (default = 0)</span><span class="sxs-lookup"><span data-stu-id="67b66-259">Number of entries to skip (default = 0)</span></span> |
| <span data-ttu-id="67b66-260">$top</span><span class="sxs-lookup"><span data-stu-id="67b66-260">$top</span></span> |<span data-ttu-id="67b66-261">Maximum Get Count</span><span class="sxs-lookup"><span data-stu-id="67b66-261">Maximum Get Count</span></span> |<span data-ttu-id="67b66-262">Maximum number of entries to retrieve (default = 256)</span><span class="sxs-lookup"><span data-stu-id="67b66-262">Maximum number of entries to retrieve (default = 256)</span></span> |

<span data-ttu-id="67b66-263">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="67b66-263">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="67b66-264">Output details</span><span class="sxs-lookup"><span data-stu-id="67b66-264">Output details</span></span>
<span data-ttu-id="67b66-265">ItemsList</span><span class="sxs-lookup"><span data-stu-id="67b66-265">ItemsList</span></span>

| <span data-ttu-id="67b66-266">Property Name</span><span class="sxs-lookup"><span data-stu-id="67b66-266">Property Name</span></span> | <span data-ttu-id="67b66-267">Data Type</span><span class="sxs-lookup"><span data-stu-id="67b66-267">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="67b66-268">value</span><span class="sxs-lookup"><span data-stu-id="67b66-268">value</span></span> |<span data-ttu-id="67b66-269">array</span><span class="sxs-lookup"><span data-stu-id="67b66-269">array</span></span> |

### <a name="when-an-object-is-modified"></a><span data-ttu-id="67b66-270">When an object is modified</span><span class="sxs-lookup"><span data-stu-id="67b66-270">When an object is modified</span></span>
<span data-ttu-id="67b66-271">This operation triggers a flow when an object is modified.</span><span class="sxs-lookup"><span data-stu-id="67b66-271">This operation triggers a flow when an object is modified.</span></span> 

| <span data-ttu-id="67b66-272">Property Name</span><span class="sxs-lookup"><span data-stu-id="67b66-272">Property Name</span></span> | <span data-ttu-id="67b66-273">Display Name</span><span class="sxs-lookup"><span data-stu-id="67b66-273">Display Name</span></span> | <span data-ttu-id="67b66-274">Description</span><span class="sxs-lookup"><span data-stu-id="67b66-274">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67b66-275">table\*</span><span class="sxs-lookup"><span data-stu-id="67b66-275">table\*</span></span> |<span data-ttu-id="67b66-276">Object type</span><span class="sxs-lookup"><span data-stu-id="67b66-276">Object type</span></span> |<span data-ttu-id="67b66-277">Object type like 'Lead'</span><span class="sxs-lookup"><span data-stu-id="67b66-277">Object type like 'Lead'</span></span> |
| <span data-ttu-id="67b66-278">$filter</span><span class="sxs-lookup"><span data-stu-id="67b66-278">$filter</span></span> |<span data-ttu-id="67b66-279">Filter Query</span><span class="sxs-lookup"><span data-stu-id="67b66-279">Filter Query</span></span> |<span data-ttu-id="67b66-280">An ODATA filter query to restrict the number of entries</span><span class="sxs-lookup"><span data-stu-id="67b66-280">An ODATA filter query to restrict the number of entries</span></span> |
| <span data-ttu-id="67b66-281">$orderby</span><span class="sxs-lookup"><span data-stu-id="67b66-281">$orderby</span></span> |<span data-ttu-id="67b66-282">Order By</span><span class="sxs-lookup"><span data-stu-id="67b66-282">Order By</span></span> |<span data-ttu-id="67b66-283">An ODATA orderBy query for specifying the order of entries</span><span class="sxs-lookup"><span data-stu-id="67b66-283">An ODATA orderBy query for specifying the order of entries</span></span> |
| <span data-ttu-id="67b66-284">$skip</span><span class="sxs-lookup"><span data-stu-id="67b66-284">$skip</span></span> |<span data-ttu-id="67b66-285">Skip Count</span><span class="sxs-lookup"><span data-stu-id="67b66-285">Skip Count</span></span> |<span data-ttu-id="67b66-286">Number of entries to skip (default = 0)</span><span class="sxs-lookup"><span data-stu-id="67b66-286">Number of entries to skip (default = 0)</span></span> |
| <span data-ttu-id="67b66-287">$top</span><span class="sxs-lookup"><span data-stu-id="67b66-287">$top</span></span> |<span data-ttu-id="67b66-288">Maximum Get Count</span><span class="sxs-lookup"><span data-stu-id="67b66-288">Maximum Get Count</span></span> |<span data-ttu-id="67b66-289">Maximum number of entries to retrieve (default = 256)</span><span class="sxs-lookup"><span data-stu-id="67b66-289">Maximum number of entries to retrieve (default = 256)</span></span> |

<span data-ttu-id="67b66-290">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="67b66-290">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="67b66-291">Output details</span><span class="sxs-lookup"><span data-stu-id="67b66-291">Output details</span></span>
<span data-ttu-id="67b66-292">ItemsList</span><span class="sxs-lookup"><span data-stu-id="67b66-292">ItemsList</span></span>

| <span data-ttu-id="67b66-293">Property Name</span><span class="sxs-lookup"><span data-stu-id="67b66-293">Property Name</span></span> | <span data-ttu-id="67b66-294">Data Type</span><span class="sxs-lookup"><span data-stu-id="67b66-294">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="67b66-295">value</span><span class="sxs-lookup"><span data-stu-id="67b66-295">value</span></span> |<span data-ttu-id="67b66-296">array</span><span class="sxs-lookup"><span data-stu-id="67b66-296">array</span></span> |

### <a name="get-object-types"></a><span data-ttu-id="67b66-297">Get object types</span><span class="sxs-lookup"><span data-stu-id="67b66-297">Get object types</span></span>
<span data-ttu-id="67b66-298">This operation lists the available object types.</span><span class="sxs-lookup"><span data-stu-id="67b66-298">This operation lists the available object types.</span></span> 

<span data-ttu-id="67b66-299">There are no parameters for this call</span><span class="sxs-lookup"><span data-stu-id="67b66-299">There are no parameters for this call</span></span>

#### <a name="output-details"></a><span data-ttu-id="67b66-300">Output details</span><span class="sxs-lookup"><span data-stu-id="67b66-300">Output details</span></span>
<span data-ttu-id="67b66-301">TablesList</span><span class="sxs-lookup"><span data-stu-id="67b66-301">TablesList</span></span>

| <span data-ttu-id="67b66-302">Property Name</span><span class="sxs-lookup"><span data-stu-id="67b66-302">Property Name</span></span> | <span data-ttu-id="67b66-303">Data Type</span><span class="sxs-lookup"><span data-stu-id="67b66-303">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="67b66-304">value</span><span class="sxs-lookup"><span data-stu-id="67b66-304">value</span></span> |<span data-ttu-id="67b66-305">array</span><span class="sxs-lookup"><span data-stu-id="67b66-305">array</span></span> |

## <a name="http-responses"></a><span data-ttu-id="67b66-306">HTTP responses</span><span class="sxs-lookup"><span data-stu-id="67b66-306">HTTP responses</span></span>
<span data-ttu-id="67b66-307">The actions and triggers above can return one or more of the following HTTP status codes:</span><span class="sxs-lookup"><span data-stu-id="67b66-307">The actions and triggers above can return one or more of the following HTTP status codes:</span></span> 

| <span data-ttu-id="67b66-308">Name</span><span class="sxs-lookup"><span data-stu-id="67b66-308">Name</span></span> | <span data-ttu-id="67b66-309">Description</span><span class="sxs-lookup"><span data-stu-id="67b66-309">Description</span></span> |
| --- | --- |
| <span data-ttu-id="67b66-310">200</span><span class="sxs-lookup"><span data-stu-id="67b66-310">200</span></span> |<span data-ttu-id="67b66-311">OK</span><span class="sxs-lookup"><span data-stu-id="67b66-311">OK</span></span> |
| <span data-ttu-id="67b66-312">202</span><span class="sxs-lookup"><span data-stu-id="67b66-312">202</span></span> |<span data-ttu-id="67b66-313">Accepted</span><span class="sxs-lookup"><span data-stu-id="67b66-313">Accepted</span></span> |
| <span data-ttu-id="67b66-314">400</span><span class="sxs-lookup"><span data-stu-id="67b66-314">400</span></span> |<span data-ttu-id="67b66-315">Bad Request</span><span class="sxs-lookup"><span data-stu-id="67b66-315">Bad Request</span></span> |
| <span data-ttu-id="67b66-316">401</span><span class="sxs-lookup"><span data-stu-id="67b66-316">401</span></span> |<span data-ttu-id="67b66-317">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="67b66-317">Unauthorized</span></span> |
| <span data-ttu-id="67b66-318">403</span><span class="sxs-lookup"><span data-stu-id="67b66-318">403</span></span> |<span data-ttu-id="67b66-319">Forbidden</span><span class="sxs-lookup"><span data-stu-id="67b66-319">Forbidden</span></span> |
| <span data-ttu-id="67b66-320">404</span><span class="sxs-lookup"><span data-stu-id="67b66-320">404</span></span> |<span data-ttu-id="67b66-321">Not Found</span><span class="sxs-lookup"><span data-stu-id="67b66-321">Not Found</span></span> |
| <span data-ttu-id="67b66-322">500</span><span class="sxs-lookup"><span data-stu-id="67b66-322">500</span></span> |<span data-ttu-id="67b66-323">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="67b66-323">Internal Server Error.</span></span> <span data-ttu-id="67b66-324">Unknown error occurred.</span><span class="sxs-lookup"><span data-stu-id="67b66-324">Unknown error occurred.</span></span> |
| <span data-ttu-id="67b66-325">default</span><span class="sxs-lookup"><span data-stu-id="67b66-325">default</span></span> |<span data-ttu-id="67b66-326">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="67b66-326">Operation Failed.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="67b66-327">Next steps</span><span class="sxs-lookup"><span data-stu-id="67b66-327">Next steps</span></span>
[<span data-ttu-id="67b66-328">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="67b66-328">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

