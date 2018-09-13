---
title: Manage data assets in Azure Data Catalog
description: The article highlights how to control visibility and ownership of data assets registered in Azure Data Catalog.
services: data-catalog
author: steelanddata
ms.author: maroche
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.topic: conceptual
ms.date: 01/18/2018
ms.openlocfilehash: e102b1f436b4f6d39f57445b02638ffd11f27786
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44811303"
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="bfea4-103">Manage data assets in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="bfea4-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="bfea4-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="bfea4-104">Introduction</span></span>
<span data-ttu-id="bfea4-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand the data sources you need to perform analysis and make decisions.</span><span class="sxs-lookup"><span data-stu-id="bfea4-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand the data sources you need to perform analysis and make decisions.</span></span> <span data-ttu-id="bfea4-106">These discovery capabilities make the biggest impact when you and other users can find and understand the broadest range of available data sources.</span><span class="sxs-lookup"><span data-stu-id="bfea4-106">These discovery capabilities make the biggest impact when you and other users can find and understand the broadest range of available data sources.</span></span> <span data-ttu-id="bfea4-107">With these elements in mind, the default behavior of Data Catalog is for all registered data sources to be visible to and discoverable by all catalog users.</span><span class="sxs-lookup"><span data-stu-id="bfea4-107">With these elements in mind, the default behavior of Data Catalog is for all registered data sources to be visible to and discoverable by all catalog users.</span></span>

<span data-ttu-id="bfea4-108">Data Catalog does not give you access to the data itself.</span><span class="sxs-lookup"><span data-stu-id="bfea4-108">Data Catalog does not give you access to the data itself.</span></span> <span data-ttu-id="bfea4-109">Data access is controlled by the owner of the data source.</span><span class="sxs-lookup"><span data-stu-id="bfea4-109">Data access is controlled by the owner of the data source.</span></span> <span data-ttu-id="bfea4-110">With Data Catalog, you can discover data sources and view the metadata that's related to the sources that are registered in the catalog.</span><span class="sxs-lookup"><span data-stu-id="bfea4-110">With Data Catalog, you can discover data sources and view the metadata that's related to the sources that are registered in the catalog.</span></span>

<span data-ttu-id="bfea4-111">There might be situations, however, where data sources should only be visible to specific users, or to members of specific groups.</span><span class="sxs-lookup"><span data-stu-id="bfea4-111">There might be situations, however, where data sources should only be visible to specific users, or to members of specific groups.</span></span> <span data-ttu-id="bfea4-112">In such scenarios, users can take ownership of registered data assets within the catalog and then control the visibility of the assets they own.</span><span class="sxs-lookup"><span data-stu-id="bfea4-112">In such scenarios, users can take ownership of registered data assets within the catalog and then control the visibility of the assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="bfea4-113">The functionality described in this article is available only in the Standard Edition of Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="bfea4-113">The functionality described in this article is available only in the Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="bfea4-114">The Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span><span class="sxs-lookup"><span data-stu-id="bfea4-114">The Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="bfea4-115">Manage ownership of data assets</span><span class="sxs-lookup"><span data-stu-id="bfea4-115">Manage ownership of data assets</span></span>
<span data-ttu-id="bfea4-116">By default, data assets that are registered in Data Catalog are unowned.</span><span class="sxs-lookup"><span data-stu-id="bfea4-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="bfea4-117">Any user with permission to access the catalog can discover and annotate these assets.</span><span class="sxs-lookup"><span data-stu-id="bfea4-117">Any user with permission to access the catalog can discover and annotate these assets.</span></span> <span data-ttu-id="bfea4-118">Users can take ownership of unowned data assets and then limit the visibility of the assets they own.</span><span class="sxs-lookup"><span data-stu-id="bfea4-118">Users can take ownership of unowned data assets and then limit the visibility of the assets they own.</span></span>

<span data-ttu-id="bfea4-119">When a data asset in Data Catalog is owned, only users who are authorized by the owners can discover the asset and view its metadata, and only the owners can delete the asset from the catalog.</span><span class="sxs-lookup"><span data-stu-id="bfea4-119">When a data asset in Data Catalog is owned, only users who are authorized by the owners can discover the asset and view its metadata, and only the owners can delete the asset from the catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="bfea4-120">Ownership in Data Catalog affects only the metadata that's stored in the catalog.</span><span class="sxs-lookup"><span data-stu-id="bfea4-120">Ownership in Data Catalog affects only the metadata that's stored in the catalog.</span></span> <span data-ttu-id="bfea4-121">Ownership does not confer any permissions on the underlying data source.</span><span class="sxs-lookup"><span data-stu-id="bfea4-121">Ownership does not confer any permissions on the underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="bfea4-122">Take ownership</span><span class="sxs-lookup"><span data-stu-id="bfea4-122">Take ownership</span></span>
<span data-ttu-id="bfea4-123">Users can take ownership of data assets by selecting the **Take Ownership** option in the Data Catalog portal.</span><span class="sxs-lookup"><span data-stu-id="bfea4-123">Users can take ownership of data assets by selecting the **Take Ownership** option in the Data Catalog portal.</span></span> <span data-ttu-id="bfea4-124">No special permissions are required to take ownership of an unowned data asset.</span><span class="sxs-lookup"><span data-stu-id="bfea4-124">No special permissions are required to take ownership of an unowned data asset.</span></span> <span data-ttu-id="bfea4-125">Any user can take ownership of an unowned data asset.</span><span class="sxs-lookup"><span data-stu-id="bfea4-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="bfea4-126">Add owners and co-owners</span><span class="sxs-lookup"><span data-stu-id="bfea4-126">Add owners and co-owners</span></span>
<span data-ttu-id="bfea4-127">If a data asset is already owned, other users cannot simply take ownership.</span><span class="sxs-lookup"><span data-stu-id="bfea4-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="bfea4-128">They must be added as co-owners by an existing owner.</span><span class="sxs-lookup"><span data-stu-id="bfea4-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="bfea4-129">Any owner can add additional users or security groups as co-owners.</span><span class="sxs-lookup"><span data-stu-id="bfea4-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="bfea4-130">It is a best practice to have at least two individuals as owners for any owned data asset.</span><span class="sxs-lookup"><span data-stu-id="bfea4-130">It is a best practice to have at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="bfea4-131">Remove owners</span><span class="sxs-lookup"><span data-stu-id="bfea4-131">Remove owners</span></span>
<span data-ttu-id="bfea4-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span><span class="sxs-lookup"><span data-stu-id="bfea4-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="bfea4-133">An asset owner who removes him or herself as an owner can no longer manage the asset.</span><span class="sxs-lookup"><span data-stu-id="bfea4-133">An asset owner who removes him or herself as an owner can no longer manage the asset.</span></span> <span data-ttu-id="bfea4-134">If the asset owner removes him or herself as an owner and there are no other co-owners, the asset reverts to an unowned state.</span><span class="sxs-lookup"><span data-stu-id="bfea4-134">If the asset owner removes him or herself as an owner and there are no other co-owners, the asset reverts to an unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="bfea4-135">Control visibility</span><span class="sxs-lookup"><span data-stu-id="bfea4-135">Control visibility</span></span>
<span data-ttu-id="bfea4-136">Data-asset owners can control the visibility of the data assets they own.</span><span class="sxs-lookup"><span data-stu-id="bfea4-136">Data-asset owners can control the visibility of the data assets they own.</span></span> <span data-ttu-id="bfea4-137">To restrict visibility as the default, where all Data Catalog users can discover and view the data asset, the asset owner can toggle the visibility setting from **Everyone** to **Owners & These Users** in the properties for the asset.</span><span class="sxs-lookup"><span data-stu-id="bfea4-137">To restrict visibility as the default, where all Data Catalog users can discover and view the data asset, the asset owner can toggle the visibility setting from **Everyone** to **Owners & These Users** in the properties for the asset.</span></span> <span data-ttu-id="bfea4-138">Owners can then add specific users and security groups.</span><span class="sxs-lookup"><span data-stu-id="bfea4-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="bfea4-139">Whenever possible, asset ownership and visibility permissions should be assigned to security groups and not to individual users.</span><span class="sxs-lookup"><span data-stu-id="bfea4-139">Whenever possible, asset ownership and visibility permissions should be assigned to security groups and not to individual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="bfea4-140">Catalog administrators</span><span class="sxs-lookup"><span data-stu-id="bfea4-140">Catalog administrators</span></span>
<span data-ttu-id="bfea4-141">Data Catalog administrators are implicitly co-owners of all assets in the catalog.</span><span class="sxs-lookup"><span data-stu-id="bfea4-141">Data Catalog administrators are implicitly co-owners of all assets in the catalog.</span></span> <span data-ttu-id="bfea4-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in the catalog.</span><span class="sxs-lookup"><span data-stu-id="bfea4-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in the catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="bfea4-143">Summary</span><span class="sxs-lookup"><span data-stu-id="bfea4-143">Summary</span></span>
<span data-ttu-id="bfea4-144">The Data Catalog crowdsourcing model to metadata and data asset discovery allows all catalog users to contribute and discover.</span><span class="sxs-lookup"><span data-stu-id="bfea4-144">The Data Catalog crowdsourcing model to metadata and data asset discovery allows all catalog users to contribute and discover.</span></span> <span data-ttu-id="bfea4-145">The Standard Edition of Data Catalog is designed for ownership and management to limit the visibility and use of specific data assets.</span><span class="sxs-lookup"><span data-stu-id="bfea4-145">The Standard Edition of Data Catalog is designed for ownership and management to limit the visibility and use of specific data assets.</span></span>
