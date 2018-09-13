---
title: How to discover data sources | Microsoft Docs
description: How-to article highlighting how to discover registered data assets with Azure Data Catalog, including searching and filtering and using the hit highlighting capabilities of the Azure Data Catalog portal.
services: data-catalog
documentationcenter: ''
author: steelanddata
manager: NA
editor: ''
tags: ''
ms.assetid: f72ae3a3-6573-4710-89a7-f13555e1968c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 01/23/2017
ms.author: maroche
ms.openlocfilehash: a99f6590dca368e6fdf584c22b3d7b7f491528bb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550759"
---
# <a name="how-to-discover-data-sources"></a><span data-ttu-id="190e8-103">How to discover data sources</span><span class="sxs-lookup"><span data-stu-id="190e8-103">How to discover data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="190e8-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="190e8-104">Introduction</span></span>
<span data-ttu-id="190e8-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span><span class="sxs-lookup"><span data-stu-id="190e8-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="190e8-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data.</span><span class="sxs-lookup"><span data-stu-id="190e8-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data.</span></span> <span data-ttu-id="190e8-107">Once a data source has been registered with **Azure Data Catalog**, its metadata is indexed by the service, so that users can easily search to discover the data they need.</span><span class="sxs-lookup"><span data-stu-id="190e8-107">Once a data source has been registered with **Azure Data Catalog**, its metadata is indexed by the service, so that users can easily search to discover the data they need.</span></span>

## <a name="searching-and-filtering"></a><span data-ttu-id="190e8-108">Searching and filtering</span><span class="sxs-lookup"><span data-stu-id="190e8-108">Searching and filtering</span></span>
<span data-ttu-id="190e8-109">Discovery in **Azure Data Catalog** uses two primary mechanisms: searching and filtering.</span><span class="sxs-lookup"><span data-stu-id="190e8-109">Discovery in **Azure Data Catalog** uses two primary mechanisms: searching and filtering.</span></span>

<span data-ttu-id="190e8-110">Searching is designed to be both intuitive and powerful – by default, search terms are matched against any property in the catalog, including user-provided annotations.</span><span class="sxs-lookup"><span data-stu-id="190e8-110">Searching is designed to be both intuitive and powerful – by default, search terms are matched against any property in the catalog, including user-provided annotations.</span></span>

<span data-ttu-id="190e8-111">Filtering is designed to complement searching.</span><span class="sxs-lookup"><span data-stu-id="190e8-111">Filtering is designed to complement searching.</span></span> <span data-ttu-id="190e8-112">Users can select specific characteristics such as experts, data source type, object type, and tags, to view only matching data assets, and to constrain search results to matching assets as well.</span><span class="sxs-lookup"><span data-stu-id="190e8-112">Users can select specific characteristics such as experts, data source type, object type, and tags, to view only matching data assets, and to constrain search results to matching assets as well.</span></span>

<span data-ttu-id="190e8-113">By using a combination of searching and filtering, users can quickly navigate the data sources that have been registered with **Azure Data Catalog** to discover the data sources they need.</span><span class="sxs-lookup"><span data-stu-id="190e8-113">By using a combination of searching and filtering, users can quickly navigate the data sources that have been registered with **Azure Data Catalog** to discover the data sources they need.</span></span>

## <a name="search-syntax"></a><span data-ttu-id="190e8-114">Search syntax</span><span class="sxs-lookup"><span data-stu-id="190e8-114">Search syntax</span></span>
<span data-ttu-id="190e8-115">Although the default free text search is simple and intuitive, users can also use **Azure Data Catalog**’s search syntax to have greater control over the search results.</span><span class="sxs-lookup"><span data-stu-id="190e8-115">Although the default free text search is simple and intuitive, users can also use **Azure Data Catalog**’s search syntax to have greater control over the search results.</span></span> <span data-ttu-id="190e8-116">**Azure Data Catalog** search supports the following techniques:</span><span class="sxs-lookup"><span data-stu-id="190e8-116">**Azure Data Catalog** search supports the following techniques:</span></span>

| <span data-ttu-id="190e8-117">Technique</span><span class="sxs-lookup"><span data-stu-id="190e8-117">Technique</span></span> | <span data-ttu-id="190e8-118">Use</span><span class="sxs-lookup"><span data-stu-id="190e8-118">Use</span></span> | <span data-ttu-id="190e8-119">Example</span><span class="sxs-lookup"><span data-stu-id="190e8-119">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="190e8-120">Basic Search</span><span class="sxs-lookup"><span data-stu-id="190e8-120">Basic Search</span></span> |<span data-ttu-id="190e8-121">Basic search using one or more search terms.</span><span class="sxs-lookup"><span data-stu-id="190e8-121">Basic search using one or more search terms.</span></span> <span data-ttu-id="190e8-122">Results are any assets that match on any property with one or more of the terms specified.</span><span class="sxs-lookup"><span data-stu-id="190e8-122">Results are any assets that match on any property with one or more of the terms specified.</span></span> |<span data-ttu-id="190e8-123">sales data</span><span class="sxs-lookup"><span data-stu-id="190e8-123">sales data</span></span> |
| <span data-ttu-id="190e8-124">Property Scoping</span><span class="sxs-lookup"><span data-stu-id="190e8-124">Property Scoping</span></span> |<span data-ttu-id="190e8-125">Only return data sources where the search term is matched with the specified property</span><span class="sxs-lookup"><span data-stu-id="190e8-125">Only return data sources where the search term is matched with the specified property</span></span> |<span data-ttu-id="190e8-126">name:finance</span><span class="sxs-lookup"><span data-stu-id="190e8-126">name:finance</span></span> |
| <span data-ttu-id="190e8-127">Boolean Operators</span><span class="sxs-lookup"><span data-stu-id="190e8-127">Boolean Operators</span></span> |<span data-ttu-id="190e8-128">Broaden or narrow a search using Boolean operations</span><span class="sxs-lookup"><span data-stu-id="190e8-128">Broaden or narrow a search using Boolean operations</span></span> |<span data-ttu-id="190e8-129">finance NOT corporate</span><span class="sxs-lookup"><span data-stu-id="190e8-129">finance NOT corporate</span></span> |
| <span data-ttu-id="190e8-130">Grouping with Parenthesis</span><span class="sxs-lookup"><span data-stu-id="190e8-130">Grouping with Parenthesis</span></span> |<span data-ttu-id="190e8-131">Use parentheses to group parts of the query to achieve logical isolation, especially in conjunction with Boolean operators</span><span class="sxs-lookup"><span data-stu-id="190e8-131">Use parentheses to group parts of the query to achieve logical isolation, especially in conjunction with Boolean operators</span></span> |<span data-ttu-id="190e8-132">name:finance AND (tags:Q1 OR tags:Q2)</span><span class="sxs-lookup"><span data-stu-id="190e8-132">name:finance AND (tags:Q1 OR tags:Q2)</span></span> |
| <span data-ttu-id="190e8-133">Comparison Operators</span><span class="sxs-lookup"><span data-stu-id="190e8-133">Comparison Operators</span></span> |<span data-ttu-id="190e8-134">Use comparisons other than equality for properties that have numeric and date data types</span><span class="sxs-lookup"><span data-stu-id="190e8-134">Use comparisons other than equality for properties that have numeric and date data types</span></span> |<span data-ttu-id="190e8-135">modifiedTime > "11/05/2014"</span><span class="sxs-lookup"><span data-stu-id="190e8-135">modifiedTime > "11/05/2014"</span></span> |

<span data-ttu-id="190e8-136">For more information on **Azure Data Catalog** search, see [https://msdn.microsoft.com/library/azure/mt267594.aspx](https://msdn.microsoft.com/library/azure/mt267594.aspx).</span><span class="sxs-lookup"><span data-stu-id="190e8-136">For more information on **Azure Data Catalog** search, see [https://msdn.microsoft.com/library/azure/mt267594.aspx](https://msdn.microsoft.com/library/azure/mt267594.aspx).</span></span>

## <a name="hit-highlighting"></a><span data-ttu-id="190e8-137">Hit highlighting</span><span class="sxs-lookup"><span data-stu-id="190e8-137">Hit highlighting</span></span>
<span data-ttu-id="190e8-138">When viewing search results, any displayed properties that match the specified search terms – such as the data asset name, description, and tags – will be highlighted to make it easier to identify why a given data asset was returned by a given search.</span><span class="sxs-lookup"><span data-stu-id="190e8-138">When viewing search results, any displayed properties that match the specified search terms – such as the data asset name, description, and tags – will be highlighted to make it easier to identify why a given data asset was returned by a given search.</span></span>

> [!NOTE]
> <span data-ttu-id="190e8-139">Users can turn hit highlighting off if desired, using the “Highlight” switch in the **Azure Data Catalog** portal.</span><span class="sxs-lookup"><span data-stu-id="190e8-139">Users can turn hit highlighting off if desired, using the “Highlight” switch in the **Azure Data Catalog** portal.</span></span>
>
>

<span data-ttu-id="190e8-140">When viewing search results, it may not always be obvious why a data asset is included, even with hit highlighting enabled.</span><span class="sxs-lookup"><span data-stu-id="190e8-140">When viewing search results, it may not always be obvious why a data asset is included, even with hit highlighting enabled.</span></span> <span data-ttu-id="190e8-141">Because all properties are searched by default, a data asset may be returned due to a match on a column-level property.</span><span class="sxs-lookup"><span data-stu-id="190e8-141">Because all properties are searched by default, a data asset may be returned due to a match on a column-level property.</span></span> <span data-ttu-id="190e8-142">And because multiple users can annotate registered data assets with their own tags and descriptions, not all metadata may be displayed in the list of search results.</span><span class="sxs-lookup"><span data-stu-id="190e8-142">And because multiple users can annotate registered data assets with their own tags and descriptions, not all metadata may be displayed in the list of search results.</span></span>

<span data-ttu-id="190e8-143">In the default tile view, each tile displayed in the search results will include a “View search term matches” icon, which allows the user to quickly view the number of matches and their location, and to jump to them if desired.</span><span class="sxs-lookup"><span data-stu-id="190e8-143">In the default tile view, each tile displayed in the search results will include a “View search term matches” icon, which allows the user to quickly view the number of matches and their location, and to jump to them if desired.</span></span>

 ![Hit highlighting and search matches in the Azure Data Catalog portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-discover/search-matches.png)

## <a name="summary"></a><span data-ttu-id="190e8-145">Summary</span><span class="sxs-lookup"><span data-stu-id="190e8-145">Summary</span></span>
<span data-ttu-id="190e8-146">Registering a data source with **Azure Data Catalog** makes that data source easier to discover and understand, by copying structural and descriptive metadata from the data source into the Catalog service.</span><span class="sxs-lookup"><span data-stu-id="190e8-146">Registering a data source with **Azure Data Catalog** makes that data source easier to discover and understand, by copying structural and descriptive metadata from the data source into the Catalog service.</span></span> <span data-ttu-id="190e8-147">Once a data source has been registered, users can discover it using filtering and search from within the **Azure Data Catalog** portal.</span><span class="sxs-lookup"><span data-stu-id="190e8-147">Once a data source has been registered, users can discover it using filtering and search from within the **Azure Data Catalog** portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="190e8-148">See also</span><span class="sxs-lookup"><span data-stu-id="190e8-148">See also</span></span>
* <span data-ttu-id="190e8-149">[Get Started with Azure Data Catalog](data-catalog-get-started.md) tutorial for step-by-step details about how to discover data sources.</span><span class="sxs-lookup"><span data-stu-id="190e8-149">[Get Started with Azure Data Catalog](data-catalog-get-started.md) tutorial for step-by-step details about how to discover data sources.</span></span>

