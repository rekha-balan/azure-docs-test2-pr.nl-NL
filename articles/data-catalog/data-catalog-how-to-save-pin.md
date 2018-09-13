---
title: Save searches and pin data assets in Azure Data Catalog
description: How-to article highlighting capabilities in Azure Data Catalog for saving data sources and data assets for later use.
services: data-catalog
author: steelanddata
ms.author: maroche
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.topic: conceptual
ms.date: 01/18/2018
ms.openlocfilehash: 786d65eaf667ae8ae9dc2c91d3113f5057a98a27
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44814098"
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="bd7e6-103">Save searches and pin data assets in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="bd7e6-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="bd7e6-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="bd7e6-104">Introduction</span></span>
<span data-ttu-id="bd7e6-105">Azure Data Catalog provides capabilities for data source discovery.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="bd7e6-106">You can quickly search and filter the catalog to locate data sources and understand their intended purpose, making it easier to find the right data for the job at hand.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-106">You can quickly search and filter the catalog to locate data sources and understand their intended purpose, making it easier to find the right data for the job at hand.</span></span>

<span data-ttu-id="bd7e6-107">But what if you need to regularly work with the same data?</span><span class="sxs-lookup"><span data-stu-id="bd7e6-107">But what if you need to regularly work with the same data?</span></span> <span data-ttu-id="bd7e6-108">And what if you and other users regularly contribute your knowledge to the same data sources in the catalog?</span><span class="sxs-lookup"><span data-stu-id="bd7e6-108">And what if you and other users regularly contribute your knowledge to the same data sources in the catalog?</span></span> <span data-ttu-id="bd7e6-109">In these situations, having to repeatedly issue the same searches can be inefficient.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-109">In these situations, having to repeatedly issue the same searches can be inefficient.</span></span> <span data-ttu-id="bd7e6-110">This is where saved search and pinned data assets can help.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="bd7e6-111">Saved searches</span><span class="sxs-lookup"><span data-stu-id="bd7e6-111">Saved searches</span></span>
<span data-ttu-id="bd7e6-112">A saved search in Data Catalog is a reusable, per-user search definition.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="bd7e6-113">You can define a search, including search terms, tags, and other filters, and then save it.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="bd7e6-114">You can re-run the saved search definition later to return any data assets that match its search criteria.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-114">You can re-run the saved search definition later to return any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="bd7e6-115">Create a saved search</span><span class="sxs-lookup"><span data-stu-id="bd7e6-115">Create a saved search</span></span>
<span data-ttu-id="bd7e6-116">To create a saved search, do the following:</span><span class="sxs-lookup"><span data-stu-id="bd7e6-116">To create a saved search, do the following:</span></span>
1. <span data-ttu-id="bd7e6-117">In the Azure Data Catalog portal, in the **Current Search** window, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-117">In the Azure Data Catalog portal, in the **Current Search** window, click **Save**.</span></span> 

    ![Current Search settings Save link](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="bd7e6-119">Enter the search criteria that you want to reuse, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-119">Enter the search criteria that you want to reuse, and then click **Save**.</span></span>

    ![Current Search settings saved search name](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="bd7e6-121">When you are prompted, enter a name for the saved search.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-121">When you are prompted, enter a name for the saved search.</span></span> <span data-ttu-id="bd7e6-122">Pick a name that is meaningful and that describes the data assets that will be returned by the search.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-122">Pick a name that is meaningful and that describes the data assets that will be returned by the search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="bd7e6-123">Manage saved searches</span><span class="sxs-lookup"><span data-stu-id="bd7e6-123">Manage saved searches</span></span>
<span data-ttu-id="bd7e6-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath the **Current Search** box.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath the **Current Search** box.</span></span> <span data-ttu-id="bd7e6-125">When the list is expanded, all saved searches are displayed.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-125">When the list is expanded, all saved searches are displayed.</span></span>

 ![List of saved searches](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="bd7e6-127">Do any of the following:</span><span class="sxs-lookup"><span data-stu-id="bd7e6-127">Do any of the following:</span></span>

* <span data-ttu-id="bd7e6-128">To execute a search, select a saved search in the list.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-128">To execute a search, select a saved search in the list.</span></span>

* <span data-ttu-id="bd7e6-129">To view a list of management options for a saved search, click the down arrow next to the search name.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-129">To view a list of management options for a saved search, click the down arrow next to the search name.</span></span>

    ![Options for managing saved searches](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="bd7e6-131">To enter a new name for the saved search, select **Rename**.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-131">To enter a new name for the saved search, select **Rename**.</span></span> <span data-ttu-id="bd7e6-132">The search definition is not changed.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-132">The search definition is not changed.</span></span>

* <span data-ttu-id="bd7e6-133">To remove the saved search from your list, select **Delete**, and then confirm the deletion.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-133">To remove the saved search from your list, select **Delete**, and then confirm the deletion.</span></span>

* <span data-ttu-id="bd7e6-134">To mark the saved search as your default search, select **Save As Default**.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-134">To mark the saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="bd7e6-135">If you perform an “empty” search from the Azure Data Catalog home page, your default search is executed.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-135">If you perform an “empty” search from the Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="bd7e6-136">In addition, the search that's marked as the default search is displayed at the top of the **Saved Searches** list.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-136">In addition, the search that's marked as the default search is displayed at the top of the **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="bd7e6-137">Organizational saved searches</span><span class="sxs-lookup"><span data-stu-id="bd7e6-137">Organizational saved searches</span></span>
<span data-ttu-id="bd7e6-138">All user in your organization can save searches for their own use.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="bd7e6-139">Data Catalog administrators can also save searches for all users within the organization.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-139">Data Catalog administrators can also save searches for all users within the organization.</span></span> <span data-ttu-id="bd7e6-140">When administrators save a search, they're presented with a **Share within the company** option.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-140">When administrators save a search, they're presented with a **Share within the company** option.</span></span> <span data-ttu-id="bd7e6-141">Selecting this option shares the saved search for all users in the organization.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-141">Selecting this option shares the saved search for all users in the organization.</span></span>

 ![Organizational saved searches](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="bd7e6-143">Pinned data assets</span><span class="sxs-lookup"><span data-stu-id="bd7e6-143">Pinned data assets</span></span>
<span data-ttu-id="bd7e6-144">With saved searches, you can save and reuse search definitions.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="bd7e6-145">The data assets that are returned by the searches might change over time as the contents of the catalog change.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-145">The data assets that are returned by the searches might change over time as the contents of the catalog change.</span></span> <span data-ttu-id="bd7e6-146">When you pin data assets, you can explicitly identify specific data assets to make them easier to access without needing to use a search.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-146">When you pin data assets, you can explicitly identify specific data assets to make them easier to access without needing to use a search.</span></span>

<span data-ttu-id="bd7e6-147">Pinning a data asset is straightforward.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="bd7e6-148">To add the data asset to your pinned list, you simply click the **pin** icon.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-148">To add the data asset to your pinned list, you simply click the **pin** icon.</span></span> <span data-ttu-id="bd7e6-149">The icon is displayed in the corner of the asset tile in the tile view, and in the left-most column in the list view in the Azure Data Catalog portal.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-149">The icon is displayed in the corner of the asset tile in the tile view, and in the left-most column in the list view in the Azure Data Catalog portal.</span></span>

![The data-asset pin icon](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="bd7e6-151">Unpinning a data asset is equally straightforward.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="bd7e6-152">Simply click the **unpin** icon to toggle the setting for the selected asset.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-152">Simply click the **unpin** icon to toggle the setting for the selected asset.</span></span>

![The data-asset unpin icon](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="the-my-assets-section"></a><span data-ttu-id="bd7e6-154">The My Assets section</span><span class="sxs-lookup"><span data-stu-id="bd7e6-154">The My Assets section</span></span>
<span data-ttu-id="bd7e6-155">The Data Catalog portal home page includes a **My Assets** section that displays assets of interest to the current user.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-155">The Data Catalog portal home page includes a **My Assets** section that displays assets of interest to the current user.</span></span> <span data-ttu-id="bd7e6-156">This section includes both pinned assets and saved searches.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-156">This section includes both pinned assets and saved searches.</span></span>

![The My Assets section on the home page](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="bd7e6-158">Summary</span><span class="sxs-lookup"><span data-stu-id="bd7e6-158">Summary</span></span>
<span data-ttu-id="bd7e6-159">Azure Data Catalog provides capabilities that make it easier to discover the data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-159">Azure Data Catalog provides capabilities that make it easier to discover the data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="bd7e6-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span><span class="sxs-lookup"><span data-stu-id="bd7e6-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
