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
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a>Create an index for documents in multiple languages in Azure Search
> [!div class="op_single_selector"]
>
> * [Portal](search-language-support.md)
> * [REST](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

Unleashing the power of language analyzers is as easy as setting one property on a searchable field in the index definition. Now you can do this step in the portal.

Below are screenshots of the Azure Portal blades for Azure Search that allow users to define an index schema. From this blade, users can create all of the fields and set the analyzer property for each of them.

> [!IMPORTANT]
> You can only set a language analyzer during field definition, as in when creating a new index from the ground up, or when adding a new field to an existing index. Make sure you fully specify all attributes, including the analyzer, while creating the field. You won't be able to edit the attributes or change the analyzer type once you save your changes.
>
>

## <a name="define-a-new-field-definition"></a>Define a new field definition
1. Sign in to the [Azure portal](https://portal.azure.com) and open the service blade of your search service.
2. Click **Add index** in the command bar at the top of the service dashboard to start a new index, or open an existing index to set an analyzer on new fields you're adding to an existing index.
3. The Fields blade appears, giving you options for defining the schema of the index, including the Analyzer tab used for choosing a language analyzer.
4. In Fields, start a field definition by providing a name, choosing the data type, and setting attributes to mark the field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.
5. Before moving on to the next field, open the **Analyzer** tab.

![][1]
*To select an analyzer, click the Analyzer tab on the Fields blade*

## <a name="choose-an-analyzer"></a>Choose an analyzer
1. Scroll to find the field you are defining.
2. If you haven't marked the field as searchable, click the checkbox now to mark it as **Searchable**.
3. Click the Analyzer area to display the list of available analyzers.
4. Choose the analyzer you want to use.

![][2]
*Select one of the supported analyzers for each field*

By default, all searchable fields use the [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic. To view the full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).

Once the language analyzer is selected for a field, it will be used with each indexing and search request for that field. When a query is issued against multiple fields using different analyzers, the query will be processed independently by the right analyzers for each field.

Many web and mobile applications serve users around the globe using different languages. It’s possible to define an index for a scenario like this by creating a field for each language supported.

![][3]
*Index definition with a description field for each language supported*

If the language of the agent issuing a query is known, a search request can be scoped to a specific field using the **searchFields** query parameter. The following query will be issued only against the description in Polish:

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

You can query your index from the portal, using **Search explorer** to paste in a query similar to the one shown above. Search explorer is available from the command bar in the service blade. See [Query your Azure Search index in the portal](search-explorer.md) for details.

Sometimes the language of the agent issuing a query is not known, in which case the query can be issued against all fields simultaneously. If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx). In the example below, matches found in the description in English will be scored higher relative to matches in Polish and French:

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

If you're a .NET developer, note that you can configure language analyzers using the [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search). The latest release includes support for the Microsoft language analyzers as well.

<!-- Image References -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-language-support/AnalyzerTab.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-language-support/SelectAnalyzer.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-language-support/IndexDefinition.png



