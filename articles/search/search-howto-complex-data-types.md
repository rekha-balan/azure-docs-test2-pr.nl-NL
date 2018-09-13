---
title: How to model complex data types in Azure Search | Microsoft Docs
description: Nested or hierarchical data structures can be modeled in an Azure Search index using flattened rowset and Collections data type.
author: brjohnstmsft
manager: jlembicz
ms.author: brjohnst
tags: complex data types; compound data types; aggregate data types
services: search
ms.service: search
ms.topic: conceptual
ms.date: 05/01/2017
ms.openlocfilehash: 81298bedd43a89ea948753dffc5f80248f5429ca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803795"
---
# <a name="how-to-model-complex-data-types-in-azure-search"></a><span data-ttu-id="9f4a0-103">How to model complex data types in Azure Search</span><span class="sxs-lookup"><span data-stu-id="9f4a0-103">How to model complex data types in Azure Search</span></span>
<span data-ttu-id="9f4a0-104">External datasets used to populate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-104">External datasets used to populate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="9f4a0-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="9f4a0-106">In modeling terms, you might see these structures referred to as *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, to name a few.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-106">In modeling terms, you might see these structures referred to as *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, to name a few.</span></span>

<span data-ttu-id="9f4a0-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening the structure and then using a **Collection** data type to reconstitute the interior structure.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening the structure and then using a **Collection** data type to reconstitute the interior structure.</span></span> <span data-ttu-id="9f4a0-108">Following the technique described in this article allows the content to be searched, faceted, filtered, and sorted.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-108">Following the technique described in this article allows the content to be searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="9f4a0-109">Example of a complex data structure</span><span class="sxs-lookup"><span data-stu-id="9f4a0-109">Example of a complex data structure</span></span>
<span data-ttu-id="9f4a0-110">Typically, the data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-110">Typically, the data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="9f4a0-111">Structurally, the challenge stems from having multiple child items that need to be searched and filtered.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-111">Structurally, the challenge stems from having multiple child items that need to be searched and filtered.</span></span>  <span data-ttu-id="9f4a0-112">As a starting point for illustrating the workaround, take the following JSON document that lists a set of contacts as an example:</span><span class="sxs-lookup"><span data-stu-id="9f4a0-112">As a starting point for illustrating the workaround, take the following JSON document that lists a set of contacts as an example:</span></span>

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

<span data-ttu-id="9f4a0-113">While the fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, the ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-113">While the fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, the ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="9f4a0-114">Given that Azure Search does not have a data type that supports this, we need a different way to model this in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-114">Given that Azure Search does not have a data type that supports this, we need a different way to model this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="9f4a0-115">This technique is also described by Kirk Evans in a blog post [Indexing Azure Cosmos DB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening the data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span><span class="sxs-lookup"><span data-stu-id="9f4a0-115">This technique is also described by Kirk Evans in a blog post [Indexing Azure Cosmos DB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening the data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-the-array-into-individual-fields"></a><span data-ttu-id="9f4a0-116">Part 1: Flatten the array into individual fields</span><span class="sxs-lookup"><span data-stu-id="9f4a0-116">Part 1: Flatten the array into individual fields</span></span>
<span data-ttu-id="9f4a0-117">To create an Azure Search index that accommodates this dataset, create individual fields for the nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span><span class="sxs-lookup"><span data-stu-id="9f4a0-117">To create an Azure Search index that accommodates this dataset, create individual fields for the nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="9f4a0-118">In these fields you would index the values ‘1’ and ‘2’ into the `locationsID` field for John Smith and the values ‘3’ & ‘4’ into the `locationsID` field for Jen Campbell.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-118">In these fields you would index the values ‘1’ and ‘2’ into the `locationsID` field for John Smith and the values ‘3’ & ‘4’ into the `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="9f4a0-119">Your data within Azure Search would look like this:</span><span class="sxs-lookup"><span data-stu-id="9f4a0-119">Your data within Azure Search would look like this:</span></span> 

![sample data, 2 rows](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-the-index-definition"></a><span data-ttu-id="9f4a0-121">Part 2: Add a collection field in the index definition</span><span class="sxs-lookup"><span data-stu-id="9f4a0-121">Part 2: Add a collection field in the index definition</span></span>
<span data-ttu-id="9f4a0-122">In the index schema, the field definitions might look similar to this example.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-122">In the index schema, the field definitions might look similar to this example.</span></span>

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-the-index"></a><span data-ttu-id="9f4a0-123">Validate search behaviors and optionally extend the index</span><span class="sxs-lookup"><span data-stu-id="9f4a0-123">Validate search behaviors and optionally extend the index</span></span>
<span data-ttu-id="9f4a0-124">Assuming you created the index and loaded the data, you can now test the solution to verify search query execution against the dataset.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-124">Assuming you created the index and loaded the data, you can now test the solution to verify search query execution against the dataset.</span></span> <span data-ttu-id="9f4a0-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="9f4a0-126">You should be able to run queries like:</span><span class="sxs-lookup"><span data-stu-id="9f4a0-126">You should be able to run queries like:</span></span>

* <span data-ttu-id="9f4a0-127">Find all people who work at the ‘Adventureworks Headquarters’.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-127">Find all people who work at the ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="9f4a0-128">Get a count of the number of people who work in a ‘Home Office’.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-128">Get a count of the number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="9f4a0-129">Of the people who work at a ‘Home Office’, show what other offices they work along with a count of the people in each location.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-129">Of the people who work at a ‘Home Office’, show what other offices they work along with a count of the people in each location.</span></span>  

<span data-ttu-id="9f4a0-130">Where this technique falls apart is when you need to do a search that combines both the location id as well as the location description.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-130">Where this technique falls apart is when you need to do a search that combines both the location id as well as the location description.</span></span> <span data-ttu-id="9f4a0-131">For example:</span><span class="sxs-lookup"><span data-stu-id="9f4a0-131">For example:</span></span>

* <span data-ttu-id="9f4a0-132">Find all people where they have a Home Office AND has a location ID of 4.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="9f4a0-133">If you recall the original content looked like this:</span><span class="sxs-lookup"><span data-stu-id="9f4a0-133">If you recall the original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="9f4a0-134">However, now that we have separated the data into separate fields, we have no way of knowing if the Home Office for Jen Campbell relates to `locationsID 3` or `locationsID 4`.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-134">However, now that we have separated the data into separate fields, we have no way of knowing if the Home Office for Jen Campbell relates to `locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="9f4a0-135">To handle this case, define another field in the index that combines all of the data into a single collection.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-135">To handle this case, define another field in the index that combines all of the data into a single collection.</span></span>  <span data-ttu-id="9f4a0-136">For our example, we will call this field `locationsCombined` and we will separate the content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-136">For our example, we will call this field `locationsCombined` and we will separate the content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="9f4a0-137">For example:</span><span class="sxs-lookup"><span data-stu-id="9f4a0-137">For example:</span></span> 

![sample data, 2 rows with separator](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="9f4a0-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span><span class="sxs-lookup"><span data-stu-id="9f4a0-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="9f4a0-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="9f4a0-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="9f4a0-142">Limitations</span><span class="sxs-lookup"><span data-stu-id="9f4a0-142">Limitations</span></span>
<span data-ttu-id="9f4a0-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="9f4a0-144">For example:</span><span class="sxs-lookup"><span data-stu-id="9f4a0-144">For example:</span></span>

1. <span data-ttu-id="9f4a0-145">If you do not have a static set of fields in your complex data type and there was no way to map all the possible types to a single field.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-145">If you do not have a static set of fields in your complex data type and there was no way to map all the possible types to a single field.</span></span> 
2. <span data-ttu-id="9f4a0-146">Updating the nested objects requires some extra work to determine exactly what needs to be updated in the Azure Search index</span><span class="sxs-lookup"><span data-stu-id="9f4a0-146">Updating the nested objects requires some extra work to determine exactly what needs to be updated in the Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="9f4a0-147">Sample code</span><span class="sxs-lookup"><span data-stu-id="9f4a0-147">Sample code</span></span>
<span data-ttu-id="9f4a0-148">You can see an example on how to index a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span><span class="sxs-lookup"><span data-stu-id="9f4a0-148">You can see an example on how to index a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="9f4a0-149">Next step</span><span class="sxs-lookup"><span data-stu-id="9f4a0-149">Next step</span></span>
<span data-ttu-id="9f4a0-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on the Azure Search UserVoice page and provide any additional input that you’d like us to consider regarding feature implementation.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on the Azure Search UserVoice page and provide any additional input that you’d like us to consider regarding feature implementation.</span></span> <span data-ttu-id="9f4a0-151">You can also reach out to me directly on Twitter at @liamca.</span><span class="sxs-lookup"><span data-stu-id="9f4a0-151">You can also reach out to me directly on Twitter at @liamca.</span></span>

