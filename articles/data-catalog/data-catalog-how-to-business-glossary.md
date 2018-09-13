---
title: How to set up the Business Glossary for governed tagging | Microsoft Docs
description: How-to article highlighting the business glossary in Azure Data Catalog for defining and using a common business vocabulary to tag registered data assets.
services: data-catalog
documentationcenter: ''
author: steelanddata
manager: NA
editor: ''
tags: ''
ms.assetid: b3d63dbe-1ae7-499f-bc46-42124e950cd6
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 01/23/2017
ms.author: maroche
ms.openlocfilehash: 3add863998c4b37c9e76b8e35ba864aa3fef85f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564623"
---
# <a name="how-to-set-up-the-business-glossary-for-governed-tagging"></a><span data-ttu-id="c780b-103">How to set up the Business Glossary for Governed Tagging</span><span class="sxs-lookup"><span data-stu-id="c780b-103">How to set up the Business Glossary for Governed Tagging</span></span>
## <a name="introduction"></a><span data-ttu-id="c780b-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="c780b-104">Introduction</span></span>
<span data-ttu-id="c780b-105">Azure Data Catalog provides capabilities for data source discovery, enabling users to easily discover and understand the data sources they need to perform analysis and make decisions.</span><span class="sxs-lookup"><span data-stu-id="c780b-105">Azure Data Catalog provides capabilities for data source discovery, enabling users to easily discover and understand the data sources they need to perform analysis and make decisions.</span></span> <span data-ttu-id="c780b-106">These discovery capabilities make the biggest impact when users can find and understand the broadest range of available data sources.</span><span class="sxs-lookup"><span data-stu-id="c780b-106">These discovery capabilities make the biggest impact when users can find and understand the broadest range of available data sources.</span></span>

<span data-ttu-id="c780b-107">One Data Catalog feature that promotes greater understanding of assets data is tagging.</span><span class="sxs-lookup"><span data-stu-id="c780b-107">One Data Catalog feature that promotes greater understanding of assets data is tagging.</span></span> <span data-ttu-id="c780b-108">Tagging allows users to associate keywords with an asset or a column, which in turn makes it easier to discover the asset via searching or browsing, and allows users to more easily understand the context and intent of the asset.</span><span class="sxs-lookup"><span data-stu-id="c780b-108">Tagging allows users to associate keywords with an asset or a column, which in turn makes it easier to discover the asset via searching or browsing, and allows users to more easily understand the context and intent of the asset.</span></span>

<span data-ttu-id="c780b-109">However, tagging can sometimes cause problems of its own.</span><span class="sxs-lookup"><span data-stu-id="c780b-109">However, tagging can sometimes cause problems of its own.</span></span> <span data-ttu-id="c780b-110">Some examples of problems that can be introduced by tagging are:</span><span class="sxs-lookup"><span data-stu-id="c780b-110">Some examples of problems that can be introduced by tagging are:</span></span>

1. <span data-ttu-id="c780b-111">Users using abbreviations on some assets and expanded text on others while tagging.</span><span class="sxs-lookup"><span data-stu-id="c780b-111">Users using abbreviations on some assets and expanded text on others while tagging.</span></span> <span data-ttu-id="c780b-112">This inconsistency hinders the discovery of assets even though the intent was to tag the assets with the same tag.</span><span class="sxs-lookup"><span data-stu-id="c780b-112">This inconsistency hinders the discovery of assets even though the intent was to tag the assets with the same tag.</span></span>
2. <span data-ttu-id="c780b-113">Tags which mean different things in different contexts.</span><span class="sxs-lookup"><span data-stu-id="c780b-113">Tags which mean different things in different contexts.</span></span> <span data-ttu-id="c780b-114">For example, a tag called "Revenue" on a customer data set might mean revenue by customer, but the same tag on a quarterly sales dataset could mean quarterly revenue for the company.</span><span class="sxs-lookup"><span data-stu-id="c780b-114">For example, a tag called "Revenue" on a customer data set might mean revenue by customer, but the same tag on a quarterly sales dataset could mean quarterly revenue for the company.</span></span>  

<span data-ttu-id="c780b-115">To help address these and other similar challenges, Data Catalog includes a Business Glossary.</span><span class="sxs-lookup"><span data-stu-id="c780b-115">To help address these and other similar challenges, Data Catalog includes a Business Glossary.</span></span>

<span data-ttu-id="c780b-116">The Data Catalog Business Glossary allows organizations to document key business terms and their definitions to create a common business vocabulary.</span><span class="sxs-lookup"><span data-stu-id="c780b-116">The Data Catalog Business Glossary allows organizations to document key business terms and their definitions to create a common business vocabulary.</span></span> <span data-ttu-id="c780b-117">This governance enables consistency in data usage across the organization.</span><span class="sxs-lookup"><span data-stu-id="c780b-117">This governance enables consistency in data usage across the organization.</span></span> <span data-ttu-id="c780b-118">Once terms are defined in the business glossary, they can be assigned to data assets in the catalog, using the same approach as tagging, thereby enabling *governed tagging*.</span><span class="sxs-lookup"><span data-stu-id="c780b-118">Once terms are defined in the business glossary, they can be assigned to data assets in the catalog, using the same approach as tagging, thereby enabling *governed tagging*.</span></span>

> [!NOTE]
> <span data-ttu-id="c780b-119">The functionality described in this article are available only in the Standard Edition of Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="c780b-119">The functionality described in this article are available only in the Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="c780b-120">The Free Edition does not provide capabilities for governed tagging or a business glossary.</span><span class="sxs-lookup"><span data-stu-id="c780b-120">The Free Edition does not provide capabilities for governed tagging or a business glossary.</span></span>
>
>

## <a name="glossary-availability-and-privileges"></a><span data-ttu-id="c780b-121">Glossary availability and privileges</span><span class="sxs-lookup"><span data-stu-id="c780b-121">Glossary availability and privileges</span></span>
<span data-ttu-id="c780b-122">*The business glossary is available in the Standard Edition of Azure Data Catalog. The Free Edition of Data Catalog does not include a glossary.*</span><span class="sxs-lookup"><span data-stu-id="c780b-122">*The business glossary is available in the Standard Edition of Azure Data Catalog. The Free Edition of Data Catalog does not include a glossary.*</span></span>

<span data-ttu-id="c780b-123">The business glossary can be accessed via the "Glossary" option in the Data Catalog portal's navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c780b-123">The business glossary can be accessed via the "Glossary" option in the Data Catalog portal's navigation menu.</span></span>  

![Accessing the business glossary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-business-glossary/01-portal-menu.png)

<span data-ttu-id="c780b-125">Data Catalog administrators and members of the Glossary Administrators role can create, edit and delete glossary terms in the business glossary.</span><span class="sxs-lookup"><span data-stu-id="c780b-125">Data Catalog administrators and members of the Glossary Administrators role can create, edit and delete glossary terms in the business glossary.</span></span> <span data-ttu-id="c780b-126">All Data Catalog users can view the term definitions, and can tag assets with glossary terms.</span><span class="sxs-lookup"><span data-stu-id="c780b-126">All Data Catalog users can view the term definitions, and can tag assets with glossary terms.</span></span>

![Adding a new glossary term](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-business-glossary/02-new-term.png)

## <a name="creating-glossary-terms"></a><span data-ttu-id="c780b-128">Creating glossary terms</span><span class="sxs-lookup"><span data-stu-id="c780b-128">Creating glossary terms</span></span>
<span data-ttu-id="c780b-129">Data Catalog administrators and Glossary administrators can create new glossary terms by clicking on the New Term’ button to create glossary terms with the following fields:</span><span class="sxs-lookup"><span data-stu-id="c780b-129">Data Catalog administrators and Glossary administrators can create new glossary terms by clicking on the New Term’ button to create glossary terms with the following fields:</span></span>

* <span data-ttu-id="c780b-130">A business definition for the term</span><span class="sxs-lookup"><span data-stu-id="c780b-130">A business definition for the term</span></span>
* <span data-ttu-id="c780b-131">A description which captures the intended use or business rules for the asset/column</span><span class="sxs-lookup"><span data-stu-id="c780b-131">A description which captures the intended use or business rules for the asset/column</span></span>
* <span data-ttu-id="c780b-132">A list of stakeholders who know the most about the term</span><span class="sxs-lookup"><span data-stu-id="c780b-132">A list of stakeholders who know the most about the term</span></span>
* <span data-ttu-id="c780b-133">The parent term, which defines the hierarchy in which the term is organized</span><span class="sxs-lookup"><span data-stu-id="c780b-133">The parent term, which defines the hierarchy in which the term is organized</span></span>

## <a name="glossary-term-hierarchies"></a><span data-ttu-id="c780b-134">Glossary term hierarchies</span><span class="sxs-lookup"><span data-stu-id="c780b-134">Glossary term hierarchies</span></span>
<span data-ttu-id="c780b-135">The Data Catalog business glossary provides the ability to describe your business vocabulary as a hierarchy of terms.</span><span class="sxs-lookup"><span data-stu-id="c780b-135">The Data Catalog business glossary provides the ability to describe your business vocabulary as a hierarchy of terms.</span></span> <span data-ttu-id="c780b-136">This allows organizations to create a classification of terms which better represents their business taxonomy.</span><span class="sxs-lookup"><span data-stu-id="c780b-136">This allows organizations to create a classification of terms which better represents their business taxonomy.</span></span>

<span data-ttu-id="c780b-137">The name of a term must be unique at a given level of hierarchy - duplicate names are not allowed.</span><span class="sxs-lookup"><span data-stu-id="c780b-137">The name of a term must be unique at a given level of hierarchy - duplicate names are not allowed.</span></span> <span data-ttu-id="c780b-138">There is no limit to the number of levels in a hierarchy, but a hierarchy is often more easily understood when there are three levels or fewer.</span><span class="sxs-lookup"><span data-stu-id="c780b-138">There is no limit to the number of levels in a hierarchy, but a hierarchy is often more easily understood when there are three levels or fewer.</span></span>

<span data-ttu-id="c780b-139">The use of hierarchies in the business glossary is optional.</span><span class="sxs-lookup"><span data-stu-id="c780b-139">The use of hierarchies in the business glossary is optional.</span></span> <span data-ttu-id="c780b-140">Leaving the parent term field blank for glossary terms will create a flat (non-hierarchical) list of terms in the glossary.</span><span class="sxs-lookup"><span data-stu-id="c780b-140">Leaving the parent term field blank for glossary terms will create a flat (non-hierarchical) list of terms in the glossary.</span></span>  

## <a name="tagging-assets-with-glossary-terms"></a><span data-ttu-id="c780b-141">Tagging assets with glossary terms</span><span class="sxs-lookup"><span data-stu-id="c780b-141">Tagging assets with glossary terms</span></span>
<span data-ttu-id="c780b-142">Once glossary terms have been defined within the catalog, the experience of tagging assets is optimized to search the glossary as the user types their tag.</span><span class="sxs-lookup"><span data-stu-id="c780b-142">Once glossary terms have been defined within the catalog, the experience of tagging assets is optimized to search the glossary as the user types their tag.</span></span> <span data-ttu-id="c780b-143">The Data Catalog portal displays a list of matching glossary terms for the user to choose from.</span><span class="sxs-lookup"><span data-stu-id="c780b-143">The Data Catalog portal displays a list of matching glossary terms for the user to choose from.</span></span> <span data-ttu-id="c780b-144">If the user selects a glossary term from the list it is added to the asset as a tag (a.k.a.</span><span class="sxs-lookup"><span data-stu-id="c780b-144">If the user selects a glossary term from the list it is added to the asset as a tag (a.k.a.</span></span> <span data-ttu-id="c780b-145">glossary tag).</span><span class="sxs-lookup"><span data-stu-id="c780b-145">glossary tag).</span></span> <span data-ttu-id="c780b-146">The user can also choose to create a new tag by typing a term which is not in the glossary (a.k.a.</span><span class="sxs-lookup"><span data-stu-id="c780b-146">The user can also choose to create a new tag by typing a term which is not in the glossary (a.k.a.</span></span> <span data-ttu-id="c780b-147">user tag).</span><span class="sxs-lookup"><span data-stu-id="c780b-147">user tag).</span></span>

![Data asset tagged with one user tag and two glossary tags](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-business-glossary/03-tagged-asset.png)

> [!NOTE]
> <span data-ttu-id="c780b-149">User Tags are the only type of tag supported in the Free Edition of Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="c780b-149">User Tags are the only type of tag supported in the Free Edition of Data Catalog.</span></span>
>
>

### <a name="hover-behavior-on-tags"></a><span data-ttu-id="c780b-150">Hover behavior on tags</span><span class="sxs-lookup"><span data-stu-id="c780b-150">Hover behavior on tags</span></span>
<span data-ttu-id="c780b-151">In the Data Catalog portal the two types of tags are visually distinct, with different hover behaviors.</span><span class="sxs-lookup"><span data-stu-id="c780b-151">In the Data Catalog portal the two types of tags are visually distinct, with different hover behaviors.</span></span> <span data-ttu-id="c780b-152">When the user hovers over a user tag they can see the tag text and the user or users who have added the tag.</span><span class="sxs-lookup"><span data-stu-id="c780b-152">When the user hovers over a user tag they can see the tag text and the user or users who have added the tag.</span></span> <span data-ttu-id="c780b-153">When the user hovers over a glossary tag, they also see the definition of the glossary term and a link to open the business glossary to view the full definition of the term.</span><span class="sxs-lookup"><span data-stu-id="c780b-153">When the user hovers over a glossary tag, they also see the definition of the glossary term and a link to open the business glossary to view the full definition of the term.</span></span>

### <a name="search-filters-for-tags"></a><span data-ttu-id="c780b-154">Search filters for tags</span><span class="sxs-lookup"><span data-stu-id="c780b-154">Search filters for tags</span></span>
<span data-ttu-id="c780b-155">Both glossary tags and user tags are searchable, and can be applied as filters in a search.</span><span class="sxs-lookup"><span data-stu-id="c780b-155">Both glossary tags and user tags are searchable, and can be applied as filters in a search.</span></span>

## <a name="summary"></a><span data-ttu-id="c780b-156">Summary</span><span class="sxs-lookup"><span data-stu-id="c780b-156">Summary</span></span>
<span data-ttu-id="c780b-157">The business glossary in Azure Data Catalog, and the governed tagging it enables, allow data assets to be identified, managed, and discovered in a consistent manner.</span><span class="sxs-lookup"><span data-stu-id="c780b-157">The business glossary in Azure Data Catalog, and the governed tagging it enables, allow data assets to be identified, managed, and discovered in a consistent manner.</span></span> <span data-ttu-id="c780b-158">The business glossary can promote learning of the business vocabulary amongst users of an organization and supports meaningful meta-data to be captured, making asset discovery and understanding a breeze.</span><span class="sxs-lookup"><span data-stu-id="c780b-158">The business glossary can promote learning of the business vocabulary amongst users of an organization and supports meaningful meta-data to be captured, making asset discovery and understanding a breeze.</span></span>

## <a name="see-also"></a><span data-ttu-id="c780b-159">See Also</span><span class="sxs-lookup"><span data-stu-id="c780b-159">See Also</span></span>
* [<span data-ttu-id="c780b-160">REST API documentation for business glossary operations</span><span class="sxs-lookup"><span data-stu-id="c780b-160">REST API documentation for business glossary operations</span></span>](https://msdn.microsoft.com/library/mt708855.aspx)



