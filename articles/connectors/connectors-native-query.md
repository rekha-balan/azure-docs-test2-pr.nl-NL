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
ms.openlocfilehash: 207971c29112c1cb4c7c1074a9f35f9baf0d4bc7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554925"
---
# <a name="get-started-with-the-query-action"></a><span data-ttu-id="5e0b0-103">Get started with the query action</span><span class="sxs-lookup"><span data-stu-id="5e0b0-103">Get started with the query action</span></span>
<span data-ttu-id="5e0b0-104">By using the query action, you can work with batches and arrays to accomplish workflows to:</span><span class="sxs-lookup"><span data-stu-id="5e0b0-104">By using the query action, you can work with batches and arrays to accomplish workflows to:</span></span>

* <span data-ttu-id="5e0b0-105">Create a task for all high-priority records from a database.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="5e0b0-106">Save all PDF attachments for emails into an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="5e0b0-107">To get started using the query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5e0b0-107">To get started using the query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-query-action"></a><span data-ttu-id="5e0b0-108">Use the query action</span><span class="sxs-lookup"><span data-stu-id="5e0b0-108">Use the query action</span></span>
<span data-ttu-id="5e0b0-109">An action is an operation that is carried out by the workflow that is defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-109">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="5e0b0-110">[Learn more about actions](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e0b0-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="5e0b0-111">The query action currently has one operation, called the filter array, that is exposed in the designer.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-111">The query action currently has one operation, called the filter array, that is exposed in the designer.</span></span> <span data-ttu-id="5e0b0-112">This allows you to query an array and return a set of filtered results.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-112">This allows you to query an array and return a set of filtered results.</span></span>

<span data-ttu-id="5e0b0-113">Here's how you can add it in a logic app:</span><span class="sxs-lookup"><span data-stu-id="5e0b0-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="5e0b0-114">Select the **New Step** button.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-114">Select the **New Step** button.</span></span>
2. <span data-ttu-id="5e0b0-115">Choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="5e0b0-116">In the action search box, type **filter** to list the **Filter array** action.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-116">In the action search box, type **filter** to list the **Filter array** action.</span></span>
   
    ![Select the query action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="5e0b0-118">Select an array to filter.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-118">Select an array to filter.</span></span> <span data-ttu-id="5e0b0-119">(The following screenshot shows the array of results from a Twitter search.)</span><span class="sxs-lookup"><span data-stu-id="5e0b0-119">(The following screenshot shows the array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="5e0b0-120">Create a condition to evaluate on each item.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-120">Create a condition to evaluate on each item.</span></span> <span data-ttu-id="5e0b0-121">(The following screenshot filters tweets from users who have more than 100 followers.)</span><span class="sxs-lookup"><span data-stu-id="5e0b0-121">(The following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![Complete the query action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="5e0b0-123">The action will output a new array that contains only results that met the filter requirements.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-123">The action will output a new array that contains only results that met the filter requirements.</span></span>
6. <span data-ttu-id="5e0b0-124">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span><span class="sxs-lookup"><span data-stu-id="5e0b0-124">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="5e0b0-125">Query action</span><span class="sxs-lookup"><span data-stu-id="5e0b0-125">Query action</span></span>
<span data-ttu-id="5e0b0-126">Here are the details for the action that this connector supports.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-126">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="5e0b0-127">The connector has one possible action.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-127">The connector has one possible action.</span></span>

| <span data-ttu-id="5e0b0-128">Action</span><span class="sxs-lookup"><span data-stu-id="5e0b0-128">Action</span></span> | <span data-ttu-id="5e0b0-129">Description</span><span class="sxs-lookup"><span data-stu-id="5e0b0-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5e0b0-130">Filter array</span><span class="sxs-lookup"><span data-stu-id="5e0b0-130">Filter array</span></span> |<span data-ttu-id="5e0b0-131">Evaluates a condition for each item in an array and returns the results</span><span class="sxs-lookup"><span data-stu-id="5e0b0-131">Evaluates a condition for each item in an array and returns the results</span></span> |

## <a name="action-details"></a><span data-ttu-id="5e0b0-132">Action details</span><span class="sxs-lookup"><span data-stu-id="5e0b0-132">Action details</span></span>
<span data-ttu-id="5e0b0-133">The query action comes with one possible action.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-133">The query action comes with one possible action.</span></span> <span data-ttu-id="5e0b0-134">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-134">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="5e0b0-135">Filter array</span><span class="sxs-lookup"><span data-stu-id="5e0b0-135">Filter array</span></span>
<span data-ttu-id="5e0b0-136">The following are input fields for the action, which makes an HTTP outbound request.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-136">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="5e0b0-137">A \* means that it is a required field.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-137">A \* means that it is a required field.</span></span>

| <span data-ttu-id="5e0b0-138">Display name</span><span class="sxs-lookup"><span data-stu-id="5e0b0-138">Display name</span></span> | <span data-ttu-id="5e0b0-139">Property name</span><span class="sxs-lookup"><span data-stu-id="5e0b0-139">Property name</span></span> | <span data-ttu-id="5e0b0-140">Description</span><span class="sxs-lookup"><span data-stu-id="5e0b0-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5e0b0-141">From\*</span><span class="sxs-lookup"><span data-stu-id="5e0b0-141">From\*</span></span> |<span data-ttu-id="5e0b0-142">from</span><span class="sxs-lookup"><span data-stu-id="5e0b0-142">from</span></span> |<span data-ttu-id="5e0b0-143">The array to filter</span><span class="sxs-lookup"><span data-stu-id="5e0b0-143">The array to filter</span></span> |
| <span data-ttu-id="5e0b0-144">Condition\*</span><span class="sxs-lookup"><span data-stu-id="5e0b0-144">Condition\*</span></span> |<span data-ttu-id="5e0b0-145">where</span><span class="sxs-lookup"><span data-stu-id="5e0b0-145">where</span></span> |<span data-ttu-id="5e0b0-146">The condition to evaluate for each item</span><span class="sxs-lookup"><span data-stu-id="5e0b0-146">The condition to evaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="5e0b0-147">Output details</span><span class="sxs-lookup"><span data-stu-id="5e0b0-147">Output details</span></span>
<span data-ttu-id="5e0b0-148">The following are output details for the HTTP response.</span><span class="sxs-lookup"><span data-stu-id="5e0b0-148">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="5e0b0-149">Property name</span><span class="sxs-lookup"><span data-stu-id="5e0b0-149">Property name</span></span> | <span data-ttu-id="5e0b0-150">Data type</span><span class="sxs-lookup"><span data-stu-id="5e0b0-150">Data type</span></span> | <span data-ttu-id="5e0b0-151">Description</span><span class="sxs-lookup"><span data-stu-id="5e0b0-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5e0b0-152">Filtered array</span><span class="sxs-lookup"><span data-stu-id="5e0b0-152">Filtered array</span></span> |<span data-ttu-id="5e0b0-153">array</span><span class="sxs-lookup"><span data-stu-id="5e0b0-153">array</span></span> |<span data-ttu-id="5e0b0-154">An array that contains an object for each filtered result</span><span class="sxs-lookup"><span data-stu-id="5e0b0-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5e0b0-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e0b0-155">Next steps</span></span>
<span data-ttu-id="5e0b0-156">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5e0b0-156">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="5e0b0-157">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="5e0b0-157">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>



