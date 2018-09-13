---
title: How to save searches and pin data assets | Microsoft Docs
description: How-to article highlighting capabilities in Azure Data Catalog for saving data sources and data assets for later reuse.
services: data-catalog
documentationcenter: ''
author: steelanddata
manager: NA
editor: ''
tags: ''
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 01/23/2017
ms.author: maroche
ms.openlocfilehash: be22fa576d4896239a6fed803f9b5d3fd023efc9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564472"
---
# <a name="how-to-save-searches-and-pin-data-assets"></a><span data-ttu-id="ad2b0-103">How to save searches and pin data assets</span><span class="sxs-lookup"><span data-stu-id="ad2b0-103">How to save searches and pin data assets</span></span>
## <a name="introduction"></a><span data-ttu-id="ad2b0-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="ad2b0-104">Introduction</span></span>
<span data-ttu-id="ad2b0-105">Microsoft Azure Data Catalog provides capabilities for data source discovery.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-105">Microsoft Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="ad2b0-106">Users can quickly search and filter the catalog to locate data sources and understand their intended purpose, making it easier to find the right data for the job at hand.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-106">Users can quickly search and filter the catalog to locate data sources and understand their intended purpose, making it easier to find the right data for the job at hand.</span></span>

<span data-ttu-id="ad2b0-107">But what about when users need to regularly work with the same data?</span><span class="sxs-lookup"><span data-stu-id="ad2b0-107">But what about when users need to regularly work with the same data?</span></span> <span data-ttu-id="ad2b0-108">What about when users regularly contribute their knowledge to the same data sources in the catalog?</span><span class="sxs-lookup"><span data-stu-id="ad2b0-108">What about when users regularly contribute their knowledge to the same data sources in the catalog?</span></span> <span data-ttu-id="ad2b0-109">In these situations, having to repeatedly issue the same searches can be inefficient – this is where saved search and pinned data assets can help.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-109">In these situations, having to repeatedly issue the same searches can be inefficient – this is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="ad2b0-110">Saved searches</span><span class="sxs-lookup"><span data-stu-id="ad2b0-110">Saved searches</span></span>
<span data-ttu-id="ad2b0-111">A saved search in Azure Data Catalog is a reusable, per-user search definition.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-111">A saved search in Azure Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="ad2b0-112">Once a user has defined a search – including search terms, tags, and other filters – he can save it for later use.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-112">Once a user has defined a search – including search terms, tags, and other filters – he can save it for later use.</span></span> <span data-ttu-id="ad2b0-113">The saved search definition can then be re-run at a later date, to return any data assets that match its search criteria.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-113">The saved search definition can then be re-run at a later date, to return any data assets that match its search criteria.</span></span>

### <a name="creating-a-saved-search"></a><span data-ttu-id="ad2b0-114">Creating a saved search</span><span class="sxs-lookup"><span data-stu-id="ad2b0-114">Creating a saved search</span></span>
<span data-ttu-id="ad2b0-115">To create a saved search, first enter the search criteria to be reused.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-115">To create a saved search, first enter the search criteria to be reused.</span></span> <span data-ttu-id="ad2b0-116">Then click the “Save” link in the “Current Search” box in the Azure Data Catalog portal.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-116">Then click the “Save” link in the “Current Search” box in the Azure Data Catalog portal.</span></span>

 ![Select 'Save' to save the current search settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/01-save-option.png)

<span data-ttu-id="ad2b0-118">When prompted, enter a name for the saved search.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-118">When prompted, enter a name for the saved search.</span></span> <span data-ttu-id="ad2b0-119">Pick a name that is meaningful and descriptive of the data assets that will be returned by the search.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-119">Pick a name that is meaningful and descriptive of the data assets that will be returned by the search.</span></span>

 ![Provide a name for the saved search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/02-name.png)

### <a name="managing-saved-searches"></a><span data-ttu-id="ad2b0-121">Managing saved searches</span><span class="sxs-lookup"><span data-stu-id="ad2b0-121">Managing saved searches</span></span>
<span data-ttu-id="ad2b0-122">Once a user has saved one or more searches, a “Saved Searches” option will appear in the Azure Data Catalog portal under the “Current Search” box.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-122">Once a user has saved one or more searches, a “Saved Searches” option will appear in the Azure Data Catalog portal under the “Current Search” box.</span></span> <span data-ttu-id="ad2b0-123">When expanded, the complete list of saves searches will be displayed.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-123">When expanded, the complete list of saves searches will be displayed.</span></span>

 ![List of saved searches](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="ad2b0-125">Selecting a saved search from the list will cause the search to be executed.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-125">Selecting a saved search from the list will cause the search to be executed.</span></span>

<span data-ttu-id="ad2b0-126">Selecting the drop-down menu will provide a set of management options:</span><span class="sxs-lookup"><span data-stu-id="ad2b0-126">Selecting the drop-down menu will provide a set of management options:</span></span>

 ![Options for managing saved searches](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/04-managing.png)

<span data-ttu-id="ad2b0-128">Selecting “Rename” will prompt the user to enter a new name for the saved search.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-128">Selecting “Rename” will prompt the user to enter a new name for the saved search.</span></span> <span data-ttu-id="ad2b0-129">The search definition will not be changed.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-129">The search definition will not be changed.</span></span>

<span data-ttu-id="ad2b0-130">Selecting “Delete” will prompt the user for confirmation, and will then remove the saved search from the user’s list.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-130">Selecting “Delete” will prompt the user for confirmation, and will then remove the saved search from the user’s list.</span></span>

<span data-ttu-id="ad2b0-131">Selecting “Save as Default” will mark the chosen saved search as the default search for the user.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-131">Selecting “Save as Default” will mark the chosen saved search as the default search for the user.</span></span> <span data-ttu-id="ad2b0-132">If the user performs an “empty” search from the Azure Data Catalog home page, the user’s default search will be executed.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-132">If the user performs an “empty” search from the Azure Data Catalog home page, the user’s default search will be executed.</span></span> <span data-ttu-id="ad2b0-133">In addition, the search marked as default will appear at the top of the saved search list.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-133">In addition, the search marked as default will appear at the top of the saved search list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="ad2b0-134">Organizational saved searches</span><span class="sxs-lookup"><span data-stu-id="ad2b0-134">Organizational saved searches</span></span>
<span data-ttu-id="ad2b0-135">Every user can save searches for their own use.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-135">Every user can save searches for their own use.</span></span> <span data-ttu-id="ad2b0-136">Data Catalog administrators can also save searches for all users within the organization.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-136">Data Catalog administrators can also save searches for all users within the organization.</span></span> <span data-ttu-id="ad2b0-137">When saving a search, administrators are presented with an option to share the saved search within the company.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-137">When saving a search, administrators are presented with an option to share the saved search within the company.</span></span> <span data-ttu-id="ad2b0-138">If this option is selected, the saved search will be included in the list of available searches for all users.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-138">If this option is selected, the saved search will be included in the list of available searches for all users.</span></span>

 ![Organizational saved searches](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="ad2b0-140">Pinned data assets</span><span class="sxs-lookup"><span data-stu-id="ad2b0-140">Pinned data assets</span></span>
<span data-ttu-id="ad2b0-141">Saved searches allow users to save and reuse search definitions; the data assets returned by the searches may change over time as the contents of the catalog change.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-141">Saved searches allow users to save and reuse search definitions; the data assets returned by the searches may change over time as the contents of the catalog change.</span></span> <span data-ttu-id="ad2b0-142">Pinning data assets allows users to explicitly identify specific data assets to make them easier to access without needing to use a search.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-142">Pinning data assets allows users to explicitly identify specific data assets to make them easier to access without needing to use a search.</span></span>

<span data-ttu-id="ad2b0-143">Pinning a data asset is straightforward – users can simply click the “pin” icon for the data asset to add it to their pinned list.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-143">Pinning a data asset is straightforward – users can simply click the “pin” icon for the data asset to add it to their pinned list.</span></span> <span data-ttu-id="ad2b0-144">This icon appears in the corner of the asset tile in the tile view, and in the left-most column in the list view in the Azure Data Catalog portal.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-144">This icon appears in the corner of the asset tile in the tile view, and in the left-most column in the list view in the Azure Data Catalog portal.</span></span>

![Pinning a data asset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="ad2b0-146">Unpinning an asset is equally straightforward – users simply click the “pin” icon again to toggle the setting for the selected asset.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-146">Unpinning an asset is equally straightforward – users simply click the “pin” icon again to toggle the setting for the selected asset.</span></span>

![Unpinning a data asset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="my-assets"></a><span data-ttu-id="ad2b0-148">“My Assets”</span><span class="sxs-lookup"><span data-stu-id="ad2b0-148">“My Assets”</span></span>
<span data-ttu-id="ad2b0-149">The Azure Data Catalog portal home page includes a “My Assets” section that displays assets of interest to the current user.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-149">The Azure Data Catalog portal home page includes a “My Assets” section that displays assets of interest to the current user.</span></span> <span data-ttu-id="ad2b0-150">This section includes both pinned assets and saved searches.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-150">This section includes both pinned assets and saved searches.</span></span>

!['My Assets' on the home page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="ad2b0-152">Summary</span><span class="sxs-lookup"><span data-stu-id="ad2b0-152">Summary</span></span>
<span data-ttu-id="ad2b0-153">Azure Data Catalog provides capabilities that make it easier for users to discover the data sources they need, so they can spend less time looking for data and more time working with it.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-153">Azure Data Catalog provides capabilities that make it easier for users to discover the data sources they need, so they can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="ad2b0-154">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources with which they will work repeatedly.</span><span class="sxs-lookup"><span data-stu-id="ad2b0-154">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources with which they will work repeatedly.</span></span>








