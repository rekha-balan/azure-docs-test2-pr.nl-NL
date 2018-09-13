---
title: How to manage data assets in Azure Data Catalog | Microsoft Docs
description: How-to article highlighting how to control visibility and ownership of data assets registered in Azure Data Catalog.
services: data-catalog
documentationcenter: ''
author: steelanddata
manager: NA
editor: ''
tags: ''
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 01/23/2017
ms.author: maroche
ms.openlocfilehash: 45a7b2df88a2edf2bccdfc9d2aaea932f2096f24
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562824"
---
# <a name="how-to-manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="abefd-103">How to manage data assets in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="abefd-103">How to manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="abefd-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="abefd-104">Introduction</span></span>
<span data-ttu-id="abefd-105">**Azure Data Catalog** provides capabilities for data source discovery, enabling users to easily discover and understand the data sources they need to perform analysis and make decisions.</span><span class="sxs-lookup"><span data-stu-id="abefd-105">**Azure Data Catalog** provides capabilities for data source discovery, enabling users to easily discover and understand the data sources they need to perform analysis and make decisions.</span></span> <span data-ttu-id="abefd-106">These discovery capabilities make the biggest impact when all users can find and understand the broadest range of available data sources.</span><span class="sxs-lookup"><span data-stu-id="abefd-106">These discovery capabilities make the biggest impact when all users can find and understand the broadest range of available data sources.</span></span> <span data-ttu-id="abefd-107">With this in mind, the default behavior of Data Catalog is for all registered data sources to be visible to – and discoverable by – all catalog users.</span><span class="sxs-lookup"><span data-stu-id="abefd-107">With this in mind, the default behavior of Data Catalog is for all registered data sources to be visible to – and discoverable by – all catalog users.</span></span>

<span data-ttu-id="abefd-108">Data Catalog does not give users access to the data itself.</span><span class="sxs-lookup"><span data-stu-id="abefd-108">Data Catalog does not give users access to the data itself.</span></span> <span data-ttu-id="abefd-109">Data access is controlled by the owner of the data source.</span><span class="sxs-lookup"><span data-stu-id="abefd-109">Data access is controlled by the owner of the data source.</span></span> <span data-ttu-id="abefd-110">Data Catalog allows users to discover data sources and to view the metadata related to the sources registered in the catalog.</span><span class="sxs-lookup"><span data-stu-id="abefd-110">Data Catalog allows users to discover data sources and to view the metadata related to the sources registered in the catalog.</span></span>

<span data-ttu-id="abefd-111">There may be situations, however, where data sources should only be visible to specific users, or to members of specific groups.</span><span class="sxs-lookup"><span data-stu-id="abefd-111">There may be situations, however, where data sources should only be visible to specific users, or to members of specific groups.</span></span> <span data-ttu-id="abefd-112">For these scenarios, Data Catalog allows users to take ownership of registered data assets within the catalog, and to then control the visibility of the assets they own.</span><span class="sxs-lookup"><span data-stu-id="abefd-112">For these scenarios, Data Catalog allows users to take ownership of registered data assets within the catalog, and to then control the visibility of the assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="abefd-113">The functionality described in this article are available only in the Standard Edition of Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="abefd-113">The functionality described in this article are available only in the Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="abefd-114">The Free Edition does not provide capabilities for ownership and restricting data asset visibility.</span><span class="sxs-lookup"><span data-stu-id="abefd-114">The Free Edition does not provide capabilities for ownership and restricting data asset visibility.</span></span>
>
>

## <a name="managing-ownership-of-data-assets"></a><span data-ttu-id="abefd-115">Managing ownership of data assets</span><span class="sxs-lookup"><span data-stu-id="abefd-115">Managing ownership of data assets</span></span>
<span data-ttu-id="abefd-116">By default, data assets registered in Data Catalog are unowned; any user with permission to access the catalog can discover and annotate these assets.</span><span class="sxs-lookup"><span data-stu-id="abefd-116">By default, data assets registered in Data Catalog are unowned; any user with permission to access the catalog can discover and annotate these assets.</span></span> <span data-ttu-id="abefd-117">Users can take ownership of unowned data assets, and can then limit the visibility of the assets they own.</span><span class="sxs-lookup"><span data-stu-id="abefd-117">Users can take ownership of unowned data assets, and can then limit the visibility of the assets they own.</span></span>

<span data-ttu-id="abefd-118">When a data asset in Data Catalog is owned, only users authorized by the owners can discover the asset and view its metadata, and only the owners can delete the asset from the Catalog.</span><span class="sxs-lookup"><span data-stu-id="abefd-118">When a data asset in Data Catalog is owned, only users authorized by the owners can discover the asset and view its metadata, and only the owners can delete the asset from the Catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="abefd-119">Ownership in Data Catalog only affects the metadata stored in the Catalog.</span><span class="sxs-lookup"><span data-stu-id="abefd-119">Ownership in Data Catalog only affects the metadata stored in the Catalog.</span></span> <span data-ttu-id="abefd-120">It does not confer any permissions on the underlying data source.</span><span class="sxs-lookup"><span data-stu-id="abefd-120">It does not confer any permissions on the underlying data source.</span></span>
>
>

### <a name="taking-ownership"></a><span data-ttu-id="abefd-121">Taking ownership</span><span class="sxs-lookup"><span data-stu-id="abefd-121">Taking ownership</span></span>
<span data-ttu-id="abefd-122">Users can take ownership of data assets by selecting the “Take Ownership” option in the Data Catalog portal.</span><span class="sxs-lookup"><span data-stu-id="abefd-122">Users can take ownership of data assets by selecting the “Take Ownership” option in the Data Catalog portal.</span></span> <span data-ttu-id="abefd-123">No special permissions are required to take ownership of an unowned data asset; any user can take ownership of an unowned data asset.</span><span class="sxs-lookup"><span data-stu-id="abefd-123">No special permissions are required to take ownership of an unowned data asset; any user can take ownership of an unowned data asset.</span></span>

### <a name="adding-owners-and-co-owners"></a><span data-ttu-id="abefd-124">Adding owners and co-owners</span><span class="sxs-lookup"><span data-stu-id="abefd-124">Adding owners and co-owners</span></span>
<span data-ttu-id="abefd-125">If a data asset is already owned, users cannot simply take ownership – they must be added as co-owners by an existing owner.</span><span class="sxs-lookup"><span data-stu-id="abefd-125">If a data asset is already owned, users cannot simply take ownership – they must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="abefd-126">Any owner can add additional users or security groups as co-owners.</span><span class="sxs-lookup"><span data-stu-id="abefd-126">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="abefd-127">It is a best practice to have at least two individuals as owners for any owned data asset.</span><span class="sxs-lookup"><span data-stu-id="abefd-127">It is a best practice to have at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="removing-owners"></a><span data-ttu-id="abefd-128">Removing owners</span><span class="sxs-lookup"><span data-stu-id="abefd-128">Removing owners</span></span>
<span data-ttu-id="abefd-129">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span><span class="sxs-lookup"><span data-stu-id="abefd-129">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="abefd-130">If an asset owner removes himself as an owner, he can no longer manage the asset.</span><span class="sxs-lookup"><span data-stu-id="abefd-130">If an asset owner removes himself as an owner, he can no longer manage the asset.</span></span> <span data-ttu-id="abefd-131">If an asset owner removes himself as an owner and there are no other co-owners, the asset will revert to an unowned state.</span><span class="sxs-lookup"><span data-stu-id="abefd-131">If an asset owner removes himself as an owner and there are no other co-owners, the asset will revert to an unowned state.</span></span>

## <a name="visibility"></a><span data-ttu-id="abefd-132">Visibility</span><span class="sxs-lookup"><span data-stu-id="abefd-132">Visibility</span></span>
<span data-ttu-id="abefd-133">Data asset owners can control the visibility of the data assets they own.</span><span class="sxs-lookup"><span data-stu-id="abefd-133">Data asset owners can control the visibility of the data assets they own.</span></span> <span data-ttu-id="abefd-134">To restrict visibility from the default – where all Data Catalog users can discover and view the data asset – the asset owner can toggle the visibility setting from “Everyone” to “Owners & These Users” in the properties for the asset.</span><span class="sxs-lookup"><span data-stu-id="abefd-134">To restrict visibility from the default – where all Data Catalog users can discover and view the data asset – the asset owner can toggle the visibility setting from “Everyone” to “Owners & These Users” in the properties for the asset.</span></span> <span data-ttu-id="abefd-135">Owners can then add specific users and security groups.</span><span class="sxs-lookup"><span data-stu-id="abefd-135">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="abefd-136">Whenever possible, asset ownership and visibility permissions should be assigned to security groups and not to individual users.</span><span class="sxs-lookup"><span data-stu-id="abefd-136">Whenever possible, asset ownership and visibility permissions should be assigned to security groups and not to individual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="abefd-137">Catalog administrators</span><span class="sxs-lookup"><span data-stu-id="abefd-137">Catalog administrators</span></span>
<span data-ttu-id="abefd-138">Data Catalog administrators are implicitly co-owners of all assets in the Catalog.</span><span class="sxs-lookup"><span data-stu-id="abefd-138">Data Catalog administrators are implicitly co-owners of all assets in the Catalog.</span></span> <span data-ttu-id="abefd-139">Asset owners cannot remove visibility from Catalog administrators, and administrators can manage ownership and visibility for all data assets in the Catalog.</span><span class="sxs-lookup"><span data-stu-id="abefd-139">Asset owners cannot remove visibility from Catalog administrators, and administrators can manage ownership and visibility for all data assets in the Catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="abefd-140">Summary</span><span class="sxs-lookup"><span data-stu-id="abefd-140">Summary</span></span>
<span data-ttu-id="abefd-141">Data Catalog’s crowdsourcing model to metadata and data asset discovery allows all Catalog users to contribute and discover.</span><span class="sxs-lookup"><span data-stu-id="abefd-141">Data Catalog’s crowdsourcing model to metadata and data asset discovery allows all Catalog users to contribute and discover.</span></span> <span data-ttu-id="abefd-142">The Standard Edition of Data Catalog provides capabilities for ownership and management to limit the visibility and use of specific data assets.</span><span class="sxs-lookup"><span data-stu-id="abefd-142">The Standard Edition of Data Catalog provides capabilities for ownership and management to limit the visibility and use of specific data assets.</span></span>
