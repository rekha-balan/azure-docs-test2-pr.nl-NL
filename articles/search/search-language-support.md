---
title: Azure Search multi language | Microsoft Docs
description: Azure Search supports 56 languages, leveraging language analyzers from Lucene and Natural Language Processing technology from Microsoft.
services: search
documentationcenter: ''
author: yahnoosh
manager: pablocas
editor: ''
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: a9318a976dc32989c9e9002270dcc6468586ee65
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556252"
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="3b234-103">Create an index for documents in multiple languages in Azure Search</span><span class="sxs-lookup"><span data-stu-id="3b234-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [Portal](search-language-support.md)
> * [REST](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="3b234-107">Unleashing the power of language analyzers is as easy as setting one property on a searchable field in the index definition.</span><span class="sxs-lookup"><span data-stu-id="3b234-107">Unleashing the power of language analyzers is as easy as setting one property on a searchable field in the index definition.</span></span> <span data-ttu-id="3b234-108">Now you can do this step in the portal.</span><span class="sxs-lookup"><span data-stu-id="3b234-108">Now you can do this step in the portal.</span></span>

<span data-ttu-id="3b234-109">Below are screenshots of the Azure Portal blades for Azure Search that allow users to define an index schema.</span><span class="sxs-lookup"><span data-stu-id="3b234-109">Below are screenshots of the Azure Portal blades for Azure Search that allow users to define an index schema.</span></span> <span data-ttu-id="3b234-110">From this blade, users can create all of the fields and set the analyzer property for each of them.</span><span class="sxs-lookup"><span data-stu-id="3b234-110">From this blade, users can create all of the fields and set the analyzer property for each of them.</span></span>

> [!IMPORTANT]
> You can only set a language analyzer during field definition, as in when creating a new index from the ground up, or when adding a new field to an existing index. Make sure you fully specify all attributes, including the analyzer, while creating the field. You won't be able to edit the attributes or change the analyzer type once you save your changes.
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="3b234-114">Define a new field definition</span><span class="sxs-lookup"><span data-stu-id="3b234-114">Define a new field definition</span></span>
1. <span data-ttu-id="3b234-115">Sign in to the [Azure portal](https://portal.azure.com) and open the service blade of your search service.</span><span class="sxs-lookup"><span data-stu-id="3b234-115">Sign in to the [Azure portal](https://portal.azure.com) and open the service blade of your search service.</span></span>
2. <span data-ttu-id="3b234-116">Click **Add index** in the command bar at the top of the service dashboard to start a new index, or open an existing index to set an analyzer on new fields you're adding to an existing index.</span><span class="sxs-lookup"><span data-stu-id="3b234-116">Click **Add index** in the command bar at the top of the service dashboard to start a new index, or open an existing index to set an analyzer on new fields you're adding to an existing index.</span></span>
3. <span data-ttu-id="3b234-117">The Fields blade appears, giving you options for defining the schema of the index, including the Analyzer tab used for choosing a language analyzer.</span><span class="sxs-lookup"><span data-stu-id="3b234-117">The Fields blade appears, giving you options for defining the schema of the index, including the Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="3b234-118">In Fields, start a field definition by providing a name, choosing the data type, and setting attributes to mark the field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span><span class="sxs-lookup"><span data-stu-id="3b234-118">In Fields, start a field definition by providing a name, choosing the data type, and setting attributes to mark the field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="3b234-119">Before moving on to the next field, open the **Analyzer** tab.</span><span class="sxs-lookup"><span data-stu-id="3b234-119">Before moving on to the next field, open the **Analyzer** tab.</span></span>

<span data-ttu-id="3b234-120">![][1]
*To select an analyzer, click the Analyzer tab on the Fields blade*</span><span class="sxs-lookup"><span data-stu-id="3b234-120">![][1]
*To select an analyzer, click the Analyzer tab on the Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="3b234-121">Choose an analyzer</span><span class="sxs-lookup"><span data-stu-id="3b234-121">Choose an analyzer</span></span>
1. <span data-ttu-id="3b234-122">Scroll to find the field you are defining.</span><span class="sxs-lookup"><span data-stu-id="3b234-122">Scroll to find the field you are defining.</span></span>
2. <span data-ttu-id="3b234-123">If you haven't marked the field as searchable, click the checkbox now to mark it as **Searchable**.</span><span class="sxs-lookup"><span data-stu-id="3b234-123">If you haven't marked the field as searchable, click the checkbox now to mark it as **Searchable**.</span></span>
3. <span data-ttu-id="3b234-124">Click the Analyzer area to display the list of available analyzers.</span><span class="sxs-lookup"><span data-stu-id="3b234-124">Click the Analyzer area to display the list of available analyzers.</span></span>
4. <span data-ttu-id="3b234-125">Choose the analyzer you want to use.</span><span class="sxs-lookup"><span data-stu-id="3b234-125">Choose the analyzer you want to use.</span></span>

<span data-ttu-id="3b234-126">![][2]
*Select one of the supported analyzers for each field*</span><span class="sxs-lookup"><span data-stu-id="3b234-126">![][2]
*Select one of the supported analyzers for each field*</span></span>

<span data-ttu-id="3b234-127">By default, all searchable fields use the [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span><span class="sxs-lookup"><span data-stu-id="3b234-127">By default, all searchable fields use the [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="3b234-128">To view the full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b234-128">To view the full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="3b234-129">Once the language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span><span class="sxs-lookup"><span data-stu-id="3b234-129">Once the language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="3b234-130">When a query is issued against multiple fields using different analyzers, the query will be processed independently by the right analyzers for each field.</span><span class="sxs-lookup"><span data-stu-id="3b234-130">When a query is issued against multiple fields using different analyzers, the query will be processed independently by the right analyzers for each field.</span></span>

<span data-ttu-id="3b234-131">Many web and mobile applications serve users around the globe using different languages.</span><span class="sxs-lookup"><span data-stu-id="3b234-131">Many web and mobile applications serve users around the globe using different languages.</span></span> <span data-ttu-id="3b234-132">It’s possible to define an index for a scenario like this by creating a field for each language supported.</span><span class="sxs-lookup"><span data-stu-id="3b234-132">It’s possible to define an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="3b234-133">![][3]
*Index definition with a description field for each language supported*</span><span class="sxs-lookup"><span data-stu-id="3b234-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="3b234-134">If the language of the agent issuing a query is known, a search request can be scoped to a specific field using the **searchFields** query parameter.</span><span class="sxs-lookup"><span data-stu-id="3b234-134">If the language of the agent issuing a query is known, a search request can be scoped to a specific field using the **searchFields** query parameter.</span></span> <span data-ttu-id="3b234-135">The following query will be issued only against the description in Polish:</span><span class="sxs-lookup"><span data-stu-id="3b234-135">The following query will be issued only against the description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="3b234-136">You can query your index from the portal, using **Search explorer** to paste in a query similar to the one shown above.</span><span class="sxs-lookup"><span data-stu-id="3b234-136">You can query your index from the portal, using **Search explorer** to paste in a query similar to the one shown above.</span></span> <span data-ttu-id="3b234-137">Search explorer is available from the command bar in the service blade.</span><span class="sxs-lookup"><span data-stu-id="3b234-137">Search explorer is available from the command bar in the service blade.</span></span> <span data-ttu-id="3b234-138">See [Query your Azure Search index in the portal](search-explorer.md) for details.</span><span class="sxs-lookup"><span data-stu-id="3b234-138">See [Query your Azure Search index in the portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="3b234-139">Sometimes the language of the agent issuing a query is not known, in which case the query can be issued against all fields simultaneously.</span><span class="sxs-lookup"><span data-stu-id="3b234-139">Sometimes the language of the agent issuing a query is not known, in which case the query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="3b234-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b234-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="3b234-141">In the example below, matches found in the description in English will be scored higher relative to matches in Polish and French:</span><span class="sxs-lookup"><span data-stu-id="3b234-141">In the example below, matches found in the description in English will be scored higher relative to matches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="3b234-142">If you're a .NET developer, note that you can configure language analyzers using the [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span><span class="sxs-lookup"><span data-stu-id="3b234-142">If you're a .NET developer, note that you can configure language analyzers using the [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="3b234-143">The latest release includes support for the Microsoft language analyzers as well.</span><span class="sxs-lookup"><span data-stu-id="3b234-143">The latest release includes support for the Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-language-support/AnalyzerTab.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-language-support/SelectAnalyzer.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-language-support/IndexDefinition.png



