---
title: Create an Azure Search index using the Azure Portal | Microsoft Docs
description: Create an index using the Azure Portal.
services: search
manager: jhubbard
author: ashmaka
documentationcenter: ''
ms.assetid: c54d8787-6dae-4943-85ed-c8928d2a5caf
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: ashmaka
ms.openlocfilehash: a0d5d507fc54b996db050a8772bbd5dd455395bb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554597"
---
# <a name="create-an-azure-search-index-using-the-azure-portal"></a><span data-ttu-id="7ccce-103">Create an Azure Search index using the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7ccce-103">Create an Azure Search index using the Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [Overview](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

<span data-ttu-id="7ccce-108">This article will walk you through the process of creating an Azure Search [index](search-what-is-an-index.md) using the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7ccce-108">This article will walk you through the process of creating an Azure Search [index](search-what-is-an-index.md) using the Azure Portal.</span></span>

<span data-ttu-id="7ccce-109">Before following this guide and creating an index, you should have already [created an Azure Search service](search-create-service-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7ccce-109">Before following this guide and creating an index, you should have already [created an Azure Search service](search-create-service-portal.md).</span></span>

## <a name="go-to-your-azure-search-blade"></a><span data-ttu-id="7ccce-110">Go to your Azure Search blade</span><span class="sxs-lookup"><span data-stu-id="7ccce-110">Go to your Azure Search blade</span></span>
1. <span data-ttu-id="7ccce-111">Click "All resources" in the menu on the left side of the [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)</span><span class="sxs-lookup"><span data-stu-id="7ccce-111">Click "All resources" in the menu on the left side of the [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)</span></span>
2. <span data-ttu-id="7ccce-112">Select your Azure Search service</span><span class="sxs-lookup"><span data-stu-id="7ccce-112">Select your Azure Search service</span></span>

## <a name="add-and-name-your-index"></a><span data-ttu-id="7ccce-113">Add and name your index</span><span class="sxs-lookup"><span data-stu-id="7ccce-113">Add and name your index</span></span>
1. <span data-ttu-id="7ccce-114">Click the "Add index" button</span><span class="sxs-lookup"><span data-stu-id="7ccce-114">Click the "Add index" button</span></span>
2. <span data-ttu-id="7ccce-115">Name your Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="7ccce-115">Name your Azure Search index.</span></span> <span data-ttu-id="7ccce-116">Since we are creating an index to search for hotels in this guide, we have named our index "hotels".</span><span class="sxs-lookup"><span data-stu-id="7ccce-116">Since we are creating an index to search for hotels in this guide, we have named our index "hotels".</span></span>
   * <span data-ttu-id="7ccce-117">The index name must start with a letter and contain only lowercase letters, digits, or dashes ("-").</span><span class="sxs-lookup"><span data-stu-id="7ccce-117">The index name must start with a letter and contain only lowercase letters, digits, or dashes ("-").</span></span>
   * <span data-ttu-id="7ccce-118">Similar to your service name, the index name you pick will also be part of the endpoint URL where you will send your HTTP requests for the Azure Search API</span><span class="sxs-lookup"><span data-stu-id="7ccce-118">Similar to your service name, the index name you pick will also be part of the endpoint URL where you will send your HTTP requests for the Azure Search API</span></span>
3. <span data-ttu-id="7ccce-119">Click on the "Fields" entry to open a new blade</span><span class="sxs-lookup"><span data-stu-id="7ccce-119">Click on the "Fields" entry to open a new blade</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-create-index-portal/add-index.png)

## <a name="create-and-define-the-fields-of-your-index"></a><span data-ttu-id="7ccce-120">Create and define the fields of your index</span><span class="sxs-lookup"><span data-stu-id="7ccce-120">Create and define the fields of your index</span></span>
1. <span data-ttu-id="7ccce-121">By selecting the "Fields" entry, a new blade will open with a form to enter your index definition.</span><span class="sxs-lookup"><span data-stu-id="7ccce-121">By selecting the "Fields" entry, a new blade will open with a form to enter your index definition.</span></span>
2. <span data-ttu-id="7ccce-122">Add fields to your index using the form.</span><span class="sxs-lookup"><span data-stu-id="7ccce-122">Add fields to your index using the form.</span></span>
   
   * <span data-ttu-id="7ccce-123">A *key* field of type Edm.String is mandatory for every Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="7ccce-123">A *key* field of type Edm.String is mandatory for every Azure Search index.</span></span> <span data-ttu-id="7ccce-124">This key field is created by default with the field name "id".</span><span class="sxs-lookup"><span data-stu-id="7ccce-124">This key field is created by default with the field name "id".</span></span> <span data-ttu-id="7ccce-125">We have changed it to "hotelId" in our index.</span><span class="sxs-lookup"><span data-stu-id="7ccce-125">We have changed it to "hotelId" in our index.</span></span>
   * <span data-ttu-id="7ccce-126">Certain properties of your index schema can only be set once and cannot be updated in the future.</span><span class="sxs-lookup"><span data-stu-id="7ccce-126">Certain properties of your index schema can only be set once and cannot be updated in the future.</span></span> <span data-ttu-id="7ccce-127">Because of this, any schema updates that would require re-indexing such as changing field types are not currently possible after the initial configuration.</span><span class="sxs-lookup"><span data-stu-id="7ccce-127">Because of this, any schema updates that would require re-indexing such as changing field types are not currently possible after the initial configuration.</span></span>
   * <span data-ttu-id="7ccce-128">We have carefully chosen the property values for each field based on how we think they will be used in an application.</span><span class="sxs-lookup"><span data-stu-id="7ccce-128">We have carefully chosen the property values for each field based on how we think they will be used in an application.</span></span> <span data-ttu-id="7ccce-129">Keep your search user experience and business needs in mind when designing your index as each field must be assigned the [appropriate properties](https://msdn.microsoft.com/library/azure/dn798941.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ccce-129">Keep your search user experience and business needs in mind when designing your index as each field must be assigned the [appropriate properties](https://msdn.microsoft.com/library/azure/dn798941.aspx).</span></span> <span data-ttu-id="7ccce-130">These properties control which search features (filtering, faceting, sorting, full-text search, etc.) apply to which fields.</span><span class="sxs-lookup"><span data-stu-id="7ccce-130">These properties control which search features (filtering, faceting, sorting, full-text search, etc.) apply to which fields.</span></span> <span data-ttu-id="7ccce-131">For example, it is likely that people searching for hotels will be interested in keyword matches on the "description" field, so we enable full-text search for that field by setting the "Searchable" property.</span><span class="sxs-lookup"><span data-stu-id="7ccce-131">For example, it is likely that people searching for hotels will be interested in keyword matches on the "description" field, so we enable full-text search for that field by setting the "Searchable" property.</span></span>
     * <span data-ttu-id="7ccce-132">You can also set the [language analyzer](https://msdn.microsoft.com/en-us/library/azure/dn879793.aspx) for each field by clicking on the "Analyzer" tab at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="7ccce-132">You can also set the [language analyzer](https://msdn.microsoft.com/en-us/library/azure/dn879793.aspx) for each field by clicking on the "Analyzer" tab at the top of the blade.</span></span> <span data-ttu-id="7ccce-133">You can see below that we have selected a French analyzer for a field in our index intended for French text.</span><span class="sxs-lookup"><span data-stu-id="7ccce-133">You can see below that we have selected a French analyzer for a field in our index intended for French text.</span></span>
3. <span data-ttu-id="7ccce-134">Click **OK** on the "Fields" blade to confirm your field definitions</span><span class="sxs-lookup"><span data-stu-id="7ccce-134">Click **OK** on the "Fields" blade to confirm your field definitions</span></span>
4. <span data-ttu-id="7ccce-135">Click **OK** on the "Add index" blade to save and create the index you just defined.</span><span class="sxs-lookup"><span data-stu-id="7ccce-135">Click **OK** on the "Add index" blade to save and create the index you just defined.</span></span>

<span data-ttu-id="7ccce-136">In the screenshots below, you can see how we have named and defined the fields for our "hotels" index.</span><span class="sxs-lookup"><span data-stu-id="7ccce-136">In the screenshots below, you can see how we have named and defined the fields for our "hotels" index.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-create-index-portal/field-definitions.png)

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-create-index-portal/set-analyzer.png)

## <a name="next-steps"></a><span data-ttu-id="7ccce-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ccce-137">Next steps</span></span>
<span data-ttu-id="7ccce-138">After creating an Azure Search index, you will be ready to [upload your content into the index](search-what-is-data-import.md) so you can start searching your data.</span><span class="sxs-lookup"><span data-stu-id="7ccce-138">After creating an Azure Search index, you will be ready to [upload your content into the index](search-what-is-data-import.md) so you can start searching your data.</span></span>




