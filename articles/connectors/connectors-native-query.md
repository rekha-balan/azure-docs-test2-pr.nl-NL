---
title: Add the query action in logic apps | Microsoft Docs
description: Overview of the query action for performing actions like filter array.
services: ''
documentationcenter: ''
author: jeffhollan
manager: erikre
editor: ''
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 05dd4ae3c4ee439d66401a3f5595f9104051f8ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44790951"
---
# <a name="get-started-with-the-query-action"></a><span data-ttu-id="44aee-103">Get started with the query action</span><span class="sxs-lookup"><span data-stu-id="44aee-103">Get started with the query action</span></span>
<span data-ttu-id="44aee-104">By using the query action, you can work with batches and arrays to accomplish workflows to:</span><span class="sxs-lookup"><span data-stu-id="44aee-104">By using the query action, you can work with batches and arrays to accomplish workflows to:</span></span>

* <span data-ttu-id="44aee-105">Create a task for all high-priority records from a database.</span><span class="sxs-lookup"><span data-stu-id="44aee-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="44aee-106">Save all PDF attachments for emails into an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="44aee-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="44aee-107">To get started using the query action in a logic app, see [Create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="44aee-107">To get started using the query action in a logic app, see [Create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>

## <a name="use-the-query-action"></a><span data-ttu-id="44aee-108">Use the query action</span><span class="sxs-lookup"><span data-stu-id="44aee-108">Use the query action</span></span>
<span data-ttu-id="44aee-109">An action is an operation that is carried out by the workflow that is defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="44aee-109">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="44aee-110">[Learn more about actions](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="44aee-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="44aee-111">The query action currently has one operation, called the filter array, that is exposed in the designer.</span><span class="sxs-lookup"><span data-stu-id="44aee-111">The query action currently has one operation, called the filter array, that is exposed in the designer.</span></span> <span data-ttu-id="44aee-112">This allows you to query an array and return a set of filtered results.</span><span class="sxs-lookup"><span data-stu-id="44aee-112">This allows you to query an array and return a set of filtered results.</span></span>

<span data-ttu-id="44aee-113">Here's how you can add it in a logic app:</span><span class="sxs-lookup"><span data-stu-id="44aee-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="44aee-114">Select the **New Step** button.</span><span class="sxs-lookup"><span data-stu-id="44aee-114">Select the **New Step** button.</span></span>
2. <span data-ttu-id="44aee-115">Choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="44aee-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="44aee-116">In the action search box, type **filter** to list the **Filter array** action.</span><span class="sxs-lookup"><span data-stu-id="44aee-116">In the action search box, type **filter** to list the **Filter array** action.</span></span>
   
    ![Select the query action](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="44aee-118">Select an array to filter.</span><span class="sxs-lookup"><span data-stu-id="44aee-118">Select an array to filter.</span></span> <span data-ttu-id="44aee-119">(The following screenshot shows the array of results from a Twitter search.)</span><span class="sxs-lookup"><span data-stu-id="44aee-119">(The following screenshot shows the array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="44aee-120">Create a condition to evaluate on each item.</span><span class="sxs-lookup"><span data-stu-id="44aee-120">Create a condition to evaluate on each item.</span></span> <span data-ttu-id="44aee-121">(The following screenshot filters tweets from users who have more than 100 followers.)</span><span class="sxs-lookup"><span data-stu-id="44aee-121">(The following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![Complete the query action](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="44aee-123">The action will output a new array that contains only results that met the filter requirements.</span><span class="sxs-lookup"><span data-stu-id="44aee-123">The action will output a new array that contains only results that met the filter requirements.</span></span>
6. <span data-ttu-id="44aee-124">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span><span class="sxs-lookup"><span data-stu-id="44aee-124">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

<span data-ttu-id="44aee-125">\* If you're calling an HTTP endpoint, and receiving a JSON response, use the _Parse JSON_ action to parse the JSON response.</span><span class="sxs-lookup"><span data-stu-id="44aee-125">\* If you're calling an HTTP endpoint, and receiving a JSON response, use the _Parse JSON_ action to parse the JSON response.</span></span> <span data-ttu-id="44aee-126">Without taking this step, _Filter Array_ will see only Body and not understand the structure of the JSON payload.</span><span class="sxs-lookup"><span data-stu-id="44aee-126">Without taking this step, _Filter Array_ will see only Body and not understand the structure of the JSON payload.</span></span>

## <a name="query-action"></a><span data-ttu-id="44aee-127">Query action</span><span class="sxs-lookup"><span data-stu-id="44aee-127">Query action</span></span>
<span data-ttu-id="44aee-128">Here are the details for the action that this connector supports.</span><span class="sxs-lookup"><span data-stu-id="44aee-128">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="44aee-129">The connector has one possible action.</span><span class="sxs-lookup"><span data-stu-id="44aee-129">The connector has one possible action.</span></span>

| <span data-ttu-id="44aee-130">Action</span><span class="sxs-lookup"><span data-stu-id="44aee-130">Action</span></span> | <span data-ttu-id="44aee-131">Description</span><span class="sxs-lookup"><span data-stu-id="44aee-131">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44aee-132">Filter array</span><span class="sxs-lookup"><span data-stu-id="44aee-132">Filter array</span></span> |<span data-ttu-id="44aee-133">Evaluates a condition for each item in an array and returns the results</span><span class="sxs-lookup"><span data-stu-id="44aee-133">Evaluates a condition for each item in an array and returns the results</span></span> |

## <a name="action-details"></a><span data-ttu-id="44aee-134">Action details</span><span class="sxs-lookup"><span data-stu-id="44aee-134">Action details</span></span>
<span data-ttu-id="44aee-135">The query action comes with one possible action.</span><span class="sxs-lookup"><span data-stu-id="44aee-135">The query action comes with one possible action.</span></span> <span data-ttu-id="44aee-136">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span><span class="sxs-lookup"><span data-stu-id="44aee-136">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="44aee-137">Filter array</span><span class="sxs-lookup"><span data-stu-id="44aee-137">Filter array</span></span>
<span data-ttu-id="44aee-138">The following are input fields for the action, which makes an HTTP outbound request.</span><span class="sxs-lookup"><span data-stu-id="44aee-138">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="44aee-139">A \* means that it is a required field.</span><span class="sxs-lookup"><span data-stu-id="44aee-139">A \* means that it is a required field.</span></span>

| <span data-ttu-id="44aee-140">Display name</span><span class="sxs-lookup"><span data-stu-id="44aee-140">Display name</span></span> | <span data-ttu-id="44aee-141">Property name</span><span class="sxs-lookup"><span data-stu-id="44aee-141">Property name</span></span> | <span data-ttu-id="44aee-142">Description</span><span class="sxs-lookup"><span data-stu-id="44aee-142">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44aee-143">From\*</span><span class="sxs-lookup"><span data-stu-id="44aee-143">From\*</span></span> |<span data-ttu-id="44aee-144">from</span><span class="sxs-lookup"><span data-stu-id="44aee-144">from</span></span> |<span data-ttu-id="44aee-145">The array to filter</span><span class="sxs-lookup"><span data-stu-id="44aee-145">The array to filter</span></span> |
| <span data-ttu-id="44aee-146">Condition\*</span><span class="sxs-lookup"><span data-stu-id="44aee-146">Condition\*</span></span> |<span data-ttu-id="44aee-147">where</span><span class="sxs-lookup"><span data-stu-id="44aee-147">where</span></span> |<span data-ttu-id="44aee-148">The condition to evaluate for each item</span><span class="sxs-lookup"><span data-stu-id="44aee-148">The condition to evaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="44aee-149">Output details</span><span class="sxs-lookup"><span data-stu-id="44aee-149">Output details</span></span>
<span data-ttu-id="44aee-150">The following are output details for the HTTP response.</span><span class="sxs-lookup"><span data-stu-id="44aee-150">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="44aee-151">Property name</span><span class="sxs-lookup"><span data-stu-id="44aee-151">Property name</span></span> | <span data-ttu-id="44aee-152">Data type</span><span class="sxs-lookup"><span data-stu-id="44aee-152">Data type</span></span> | <span data-ttu-id="44aee-153">Description</span><span class="sxs-lookup"><span data-stu-id="44aee-153">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44aee-154">Filtered array</span><span class="sxs-lookup"><span data-stu-id="44aee-154">Filtered array</span></span> |<span data-ttu-id="44aee-155">array</span><span class="sxs-lookup"><span data-stu-id="44aee-155">array</span></span> |<span data-ttu-id="44aee-156">An array that contains an object for each filtered result</span><span class="sxs-lookup"><span data-stu-id="44aee-156">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="44aee-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="44aee-157">Next steps</span></span>
<span data-ttu-id="44aee-158">Now, try out the platform and [create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="44aee-158">Now, try out the platform and [create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span> <span data-ttu-id="44aee-159">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="44aee-159">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

