---
title: Field mappings in Azure Search indexers
description: Configure Azure Search indexer field mappings to account for differences in field names and data representations
services: search
documentationcenter: ''
author: chaosrealm
manager: pablocas
editor: ''
ms.assetid: 0325a4de-0190-4dd5-a64d-4e56601d973b
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: eugenesh
ms.openlocfilehash: 57e91f070d9a42882a56e708f12b1ce238ed9191
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661319"
---
# <a name="field-mappings-in-azure-search-indexers"></a><span data-ttu-id="22599-103">Field mappings in Azure Search indexers</span><span class="sxs-lookup"><span data-stu-id="22599-103">Field mappings in Azure Search indexers</span></span>
<span data-ttu-id="22599-104">When using Azure Search indexers, you can occasionally find yourself in situations where your input data doesn't quite match the schema of your target index.</span><span class="sxs-lookup"><span data-stu-id="22599-104">When using Azure Search indexers, you can occasionally find yourself in situations where your input data doesn't quite match the schema of your target index.</span></span> <span data-ttu-id="22599-105">In those cases, you can use **field mappings** to transform your data into the desired shape.</span><span class="sxs-lookup"><span data-stu-id="22599-105">In those cases, you can use **field mappings** to transform your data into the desired shape.</span></span>

<span data-ttu-id="22599-106">Some situations where field mappings are useful:</span><span class="sxs-lookup"><span data-stu-id="22599-106">Some situations where field mappings are useful:</span></span>

* <span data-ttu-id="22599-107">Your data source has a field `_id`, but Azure Search doesn't allow field names starting with an underscore.</span><span class="sxs-lookup"><span data-stu-id="22599-107">Your data source has a field `_id`, but Azure Search doesn't allow field names starting with an underscore.</span></span> <span data-ttu-id="22599-108">A field mapping allows you to "rename" a field.</span><span class="sxs-lookup"><span data-stu-id="22599-108">A field mapping allows you to "rename" a field.</span></span>
* <span data-ttu-id="22599-109">You want to populate several fields in the index with the same data source data, for example because you want to apply different analyzers to those fields.</span><span class="sxs-lookup"><span data-stu-id="22599-109">You want to populate several fields in the index with the same data source data, for example because you want to apply different analyzers to those fields.</span></span> <span data-ttu-id="22599-110">Field mappings let you "fork" a data source field.</span><span class="sxs-lookup"><span data-stu-id="22599-110">Field mappings let you "fork" a data source field.</span></span>
* <span data-ttu-id="22599-111">You need to Base64 encode or decode your data.</span><span class="sxs-lookup"><span data-stu-id="22599-111">You need to Base64 encode or decode your data.</span></span> <span data-ttu-id="22599-112">Field mappings support several **mapping functions**, including functions for Base64 encoding and decoding.</span><span class="sxs-lookup"><span data-stu-id="22599-112">Field mappings support several **mapping functions**, including functions for Base64 encoding and decoding.</span></span>   

## <a name="setting-up-field-mappings"></a><span data-ttu-id="22599-113">Setting up field mappings</span><span class="sxs-lookup"><span data-stu-id="22599-113">Setting up field mappings</span></span>
<span data-ttu-id="22599-114">You can add field mappings when creating a new indexer using the [Create Indexer](https://msdn.microsoft.com/library/azure/dn946899.aspx) API.</span><span class="sxs-lookup"><span data-stu-id="22599-114">You can add field mappings when creating a new indexer using the [Create Indexer](https://msdn.microsoft.com/library/azure/dn946899.aspx) API.</span></span> <span data-ttu-id="22599-115">You can manage field mappings on an indexing indexer using the [Update Indexer](https://msdn.microsoft.com/library/azure/dn946892.aspx) API.</span><span class="sxs-lookup"><span data-stu-id="22599-115">You can manage field mappings on an indexing indexer using the [Update Indexer](https://msdn.microsoft.com/library/azure/dn946892.aspx) API.</span></span>

<span data-ttu-id="22599-116">A field mapping consists of 3 parts:</span><span class="sxs-lookup"><span data-stu-id="22599-116">A field mapping consists of 3 parts:</span></span>

1. <span data-ttu-id="22599-117">A `sourceFieldName`, which represents a field in your data source.</span><span class="sxs-lookup"><span data-stu-id="22599-117">A `sourceFieldName`, which represents a field in your data source.</span></span> <span data-ttu-id="22599-118">This property is required.</span><span class="sxs-lookup"><span data-stu-id="22599-118">This property is required.</span></span>
2. <span data-ttu-id="22599-119">An optional `targetFieldName`, which represents a field in your search index.</span><span class="sxs-lookup"><span data-stu-id="22599-119">An optional `targetFieldName`, which represents a field in your search index.</span></span> <span data-ttu-id="22599-120">If omitted, the same name as in the data source is used.</span><span class="sxs-lookup"><span data-stu-id="22599-120">If omitted, the same name as in the data source is used.</span></span>
3. <span data-ttu-id="22599-121">An optional `mappingFunction`, which can transform your data using one of several predefined functions.</span><span class="sxs-lookup"><span data-stu-id="22599-121">An optional `mappingFunction`, which can transform your data using one of several predefined functions.</span></span> <span data-ttu-id="22599-122">The full list of functions is [below](#mappingFunctions).</span><span class="sxs-lookup"><span data-stu-id="22599-122">The full list of functions is [below](#mappingFunctions).</span></span>

<span data-ttu-id="22599-123">Fields mappings are added to the `fieldMappings` array on the indexer definition.</span><span class="sxs-lookup"><span data-stu-id="22599-123">Fields mappings are added to the `fieldMappings` array on the indexer definition.</span></span>

<span data-ttu-id="22599-124">For example, here's how you can accommodate differences in field names:</span><span class="sxs-lookup"><span data-stu-id="22599-124">For example, here's how you can accommodate differences in field names:</span></span>

```JSON

PUT https://[service name].search.windows.net/indexers/myindexer?api-version=[api-version]
Content-Type: application/json
api-key: [admin key]
{
    "dataSourceName" : "mydatasource",
    "targetIndexName" : "myindex",
    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ]
}
```

<span data-ttu-id="22599-125">An indexer can have multiple field mappings.</span><span class="sxs-lookup"><span data-stu-id="22599-125">An indexer can have multiple field mappings.</span></span> <span data-ttu-id="22599-126">For example, here's how you can "fork" a field:</span><span class="sxs-lookup"><span data-stu-id="22599-126">For example, here's how you can "fork" a field:</span></span>

```JSON

"fieldMappings" : [
    { "sourceFieldName" : "text", "targetFieldName" : "textStandardEnglishAnalyzer" },
    { "sourceFieldName" : "text", "targetFieldName" : "textSoundexAnalyzer" },
]
```

> [!NOTE]
> <span data-ttu-id="22599-127">Azure Search uses case-insensitive comparison to resolve the field and function names in field mappings.</span><span class="sxs-lookup"><span data-stu-id="22599-127">Azure Search uses case-insensitive comparison to resolve the field and function names in field mappings.</span></span> <span data-ttu-id="22599-128">This is convenient (you don't have to get all the casing right), but it means that your data source or index cannot have fields that differ only by case.</span><span class="sxs-lookup"><span data-stu-id="22599-128">This is convenient (you don't have to get all the casing right), but it means that your data source or index cannot have fields that differ only by case.</span></span>  
>
>

<a name="mappingFunctions"></a>

## <a name="field-mapping-functions"></a><span data-ttu-id="22599-129">Field mapping functions</span><span class="sxs-lookup"><span data-stu-id="22599-129">Field mapping functions</span></span>
<span data-ttu-id="22599-130">These functions are currently supported:</span><span class="sxs-lookup"><span data-stu-id="22599-130">These functions are currently supported:</span></span>

* [<span data-ttu-id="22599-131">base64Encode</span><span class="sxs-lookup"><span data-stu-id="22599-131">base64Encode</span></span>](#base64EncodeFunction)
* [<span data-ttu-id="22599-132">base64Decode</span><span class="sxs-lookup"><span data-stu-id="22599-132">base64Decode</span></span>](#base64DecodeFunction)
* [<span data-ttu-id="22599-133">extractTokenAtPosition</span><span class="sxs-lookup"><span data-stu-id="22599-133">extractTokenAtPosition</span></span>](#extractTokenAtPositionFunction)
* [<span data-ttu-id="22599-134">jsonArrayToStringCollection</span><span class="sxs-lookup"><span data-stu-id="22599-134">jsonArrayToStringCollection</span></span>](#jsonArrayToStringCollectionFunction)

<a name="base64EncodeFunction"></a>

### <a name="base64encode"></a><span data-ttu-id="22599-135">base64Encode</span><span class="sxs-lookup"><span data-stu-id="22599-135">base64Encode</span></span>
<span data-ttu-id="22599-136">Performs *URL-safe* Base64 encoding of the input string.</span><span class="sxs-lookup"><span data-stu-id="22599-136">Performs *URL-safe* Base64 encoding of the input string.</span></span> <span data-ttu-id="22599-137">Assumes that the input is UTF-8 encoded.</span><span class="sxs-lookup"><span data-stu-id="22599-137">Assumes that the input is UTF-8 encoded.</span></span>

#### <a name="sample-use-case"></a><span data-ttu-id="22599-138">Sample use case</span><span class="sxs-lookup"><span data-stu-id="22599-138">Sample use case</span></span>
<span data-ttu-id="22599-139">Only URL-safe characters can appear in an Azure Search document key (because customers must be able to address the document using the Lookup API, for example).</span><span class="sxs-lookup"><span data-stu-id="22599-139">Only URL-safe characters can appear in an Azure Search document key (because customers must be able to address the document using the Lookup API, for example).</span></span> <span data-ttu-id="22599-140">If your data contains URL-unsafe characters and you want to use it to populate a key field in your search index, use this function.</span><span class="sxs-lookup"><span data-stu-id="22599-140">If your data contains URL-unsafe characters and you want to use it to populate a key field in your search index, use this function.</span></span>   

#### <a name="example"></a><span data-ttu-id="22599-141">Example</span><span class="sxs-lookup"><span data-stu-id="22599-141">Example</span></span>
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Path",
    "targetFieldName" : "UrlSafePath",
    "mappingFunction" : { "name" : "base64Encode" }
  }]
```

<a name="base64DecodeFunction"></a>

### <a name="base64decode"></a><span data-ttu-id="22599-142">base64Decode</span><span class="sxs-lookup"><span data-stu-id="22599-142">base64Decode</span></span>
<span data-ttu-id="22599-143">Performs Base64 decoding of the input string.</span><span class="sxs-lookup"><span data-stu-id="22599-143">Performs Base64 decoding of the input string.</span></span> <span data-ttu-id="22599-144">The input is assumed to a *URL-safe* Base64-encoded string.</span><span class="sxs-lookup"><span data-stu-id="22599-144">The input is assumed to a *URL-safe* Base64-encoded string.</span></span>

#### <a name="sample-use-case"></a><span data-ttu-id="22599-145">Sample use case</span><span class="sxs-lookup"><span data-stu-id="22599-145">Sample use case</span></span>
<span data-ttu-id="22599-146">Blob custom metadata values must be ASCII-encoded.</span><span class="sxs-lookup"><span data-stu-id="22599-146">Blob custom metadata values must be ASCII-encoded.</span></span> <span data-ttu-id="22599-147">You can use Base64 encoding to represent arbitrary Unicode strings in blob custom metadata.</span><span class="sxs-lookup"><span data-stu-id="22599-147">You can use Base64 encoding to represent arbitrary Unicode strings in blob custom metadata.</span></span> <span data-ttu-id="22599-148">However, to make search meaningful, you can use this function to turn the encoded data back into "regular" strings when populating your search index.</span><span class="sxs-lookup"><span data-stu-id="22599-148">However, to make search meaningful, you can use this function to turn the encoded data back into "regular" strings when populating your search index.</span></span>  

#### <a name="example"></a><span data-ttu-id="22599-149">Example</span><span class="sxs-lookup"><span data-stu-id="22599-149">Example</span></span>
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Base64EncodedMetadata",
    "targetFieldName" : "SearchableMetadata",
    "mappingFunction" : { "name" : "base64Decode" }
  }]
```

<a name="extractTokenAtPositionFunction"></a>

### <a name="extracttokenatposition"></a><span data-ttu-id="22599-150">extractTokenAtPosition</span><span class="sxs-lookup"><span data-stu-id="22599-150">extractTokenAtPosition</span></span>
<span data-ttu-id="22599-151">Splits a string field using the specified delimiter, and picks the token at the specified position in the resulting split.</span><span class="sxs-lookup"><span data-stu-id="22599-151">Splits a string field using the specified delimiter, and picks the token at the specified position in the resulting split.</span></span>

<span data-ttu-id="22599-152">For example, if the input is `Jane Doe`, the `delimiter` is `" "`(space) and the `position` is 0, the result is `Jane`; if the `position` is 1, the result is `Doe`.</span><span class="sxs-lookup"><span data-stu-id="22599-152">For example, if the input is `Jane Doe`, the `delimiter` is `" "`(space) and the `position` is 0, the result is `Jane`; if the `position` is 1, the result is `Doe`.</span></span> <span data-ttu-id="22599-153">If the position refers to a token that doesn't exist, an error will be returned.</span><span class="sxs-lookup"><span data-stu-id="22599-153">If the position refers to a token that doesn't exist, an error will be returned.</span></span>

#### <a name="sample-use-case"></a><span data-ttu-id="22599-154">Sample use case</span><span class="sxs-lookup"><span data-stu-id="22599-154">Sample use case</span></span>
<span data-ttu-id="22599-155">Your data source contains a `PersonName` field, and you want to index it as two separate `FirstName` and `LastName` fields.</span><span class="sxs-lookup"><span data-stu-id="22599-155">Your data source contains a `PersonName` field, and you want to index it as two separate `FirstName` and `LastName` fields.</span></span> <span data-ttu-id="22599-156">You can use this function to split the input using the space character as the delimiter.</span><span class="sxs-lookup"><span data-stu-id="22599-156">You can use this function to split the input using the space character as the delimiter.</span></span>

#### <a name="parameters"></a><span data-ttu-id="22599-157">Parameters</span><span class="sxs-lookup"><span data-stu-id="22599-157">Parameters</span></span>
* <span data-ttu-id="22599-158">`delimiter`: a string to use as the separator when splitting the input string.</span><span class="sxs-lookup"><span data-stu-id="22599-158">`delimiter`: a string to use as the separator when splitting the input string.</span></span>
* <span data-ttu-id="22599-159">`position`: an integer zero-based position of the token to pick after the input string is split.</span><span class="sxs-lookup"><span data-stu-id="22599-159">`position`: an integer zero-based position of the token to pick after the input string is split.</span></span>    

#### <a name="example"></a><span data-ttu-id="22599-160">Example</span><span class="sxs-lookup"><span data-stu-id="22599-160">Example</span></span>
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "FirstName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 0 } }
  },
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "LastName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 1 } }
  }]
```

<a name="jsonArrayToStringCollectionFunction"></a>

### <a name="jsonarraytostringcollection"></a><span data-ttu-id="22599-161">jsonArrayToStringCollection</span><span class="sxs-lookup"><span data-stu-id="22599-161">jsonArrayToStringCollection</span></span>
<span data-ttu-id="22599-162">Transforms a string formatted as a JSON array of strings into a string array that can be used to populate a `Collection(Edm.String)` field in the index.</span><span class="sxs-lookup"><span data-stu-id="22599-162">Transforms a string formatted as a JSON array of strings into a string array that can be used to populate a `Collection(Edm.String)` field in the index.</span></span>

<span data-ttu-id="22599-163">For example, if the input string is `["red", "white", "blue"]`, then the target field of type `Collection(Edm.String)` will be populated with the three values `red`, `white` and `blue`.</span><span class="sxs-lookup"><span data-stu-id="22599-163">For example, if the input string is `["red", "white", "blue"]`, then the target field of type `Collection(Edm.String)` will be populated with the three values `red`, `white` and `blue`.</span></span> <span data-ttu-id="22599-164">For input values that cannot be parsed as JSON string arrays, an error will be returned.</span><span class="sxs-lookup"><span data-stu-id="22599-164">For input values that cannot be parsed as JSON string arrays, an error will be returned.</span></span>

#### <a name="sample-use-case"></a><span data-ttu-id="22599-165">Sample use case</span><span class="sxs-lookup"><span data-stu-id="22599-165">Sample use case</span></span>
<span data-ttu-id="22599-166">Azure SQL database doesn't have a built-in data type that naturally maps to `Collection(Edm.String)` fields in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="22599-166">Azure SQL database doesn't have a built-in data type that naturally maps to `Collection(Edm.String)` fields in Azure Search.</span></span> <span data-ttu-id="22599-167">To populate string collection fields, format your source data as a JSON string array and use this function.</span><span class="sxs-lookup"><span data-stu-id="22599-167">To populate string collection fields, format your source data as a JSON string array and use this function.</span></span>

#### <a name="example"></a><span data-ttu-id="22599-168">Example</span><span class="sxs-lookup"><span data-stu-id="22599-168">Example</span></span>
```JSON

"fieldMappings" : [
  { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } }
]
```

## <a name="help-us-make-azure-search-better"></a><span data-ttu-id="22599-169">Help us make Azure Search better</span><span class="sxs-lookup"><span data-stu-id="22599-169">Help us make Azure Search better</span></span>
<span data-ttu-id="22599-170">If you have feature requests or ideas for improvements, please reach out to us on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="22599-170">If you have feature requests or ideas for improvements, please reach out to us on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span></span>
