---
title: Field mappings in Azure Search indexers
description: Configure Azure Search indexer field mappings to account for differences in field names and data representations
author: chaosrealm
manager: jlembicz
services: search
ms.service: search
ms.devlang: rest-api
ms.topic: conceptual
ms.date: 08/30/2017
ms.author: eugenesh
ms.openlocfilehash: 51fa689030c4a8ce4e900ecd600cdd0524aa13d9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828568"
---
# <a name="field-mappings-in-azure-search-indexers"></a><span data-ttu-id="b50d3-103">Field mappings in Azure Search indexers</span><span class="sxs-lookup"><span data-stu-id="b50d3-103">Field mappings in Azure Search indexers</span></span>
<span data-ttu-id="b50d3-104">When using Azure Search indexers, you can occasionally find yourself in situations where your input data doesn't quite match the schema of your target index.</span><span class="sxs-lookup"><span data-stu-id="b50d3-104">When using Azure Search indexers, you can occasionally find yourself in situations where your input data doesn't quite match the schema of your target index.</span></span> <span data-ttu-id="b50d3-105">In those cases, you can use **field mappings** to transform your data into the desired shape.</span><span class="sxs-lookup"><span data-stu-id="b50d3-105">In those cases, you can use **field mappings** to transform your data into the desired shape.</span></span>

<span data-ttu-id="b50d3-106">Some situations where field mappings are useful:</span><span class="sxs-lookup"><span data-stu-id="b50d3-106">Some situations where field mappings are useful:</span></span>

* <span data-ttu-id="b50d3-107">Your data source has a field `_id`, but Azure Search doesn't allow field names starting with an underscore.</span><span class="sxs-lookup"><span data-stu-id="b50d3-107">Your data source has a field `_id`, but Azure Search doesn't allow field names starting with an underscore.</span></span> <span data-ttu-id="b50d3-108">A field mapping allows you to "rename" a field.</span><span class="sxs-lookup"><span data-stu-id="b50d3-108">A field mapping allows you to "rename" a field.</span></span>
* <span data-ttu-id="b50d3-109">You want to populate several fields in the index with the same data source data, for example because you want to apply different analyzers to those fields.</span><span class="sxs-lookup"><span data-stu-id="b50d3-109">You want to populate several fields in the index with the same data source data, for example because you want to apply different analyzers to those fields.</span></span> <span data-ttu-id="b50d3-110">Field mappings let you "fork" a data source field.</span><span class="sxs-lookup"><span data-stu-id="b50d3-110">Field mappings let you "fork" a data source field.</span></span>
* <span data-ttu-id="b50d3-111">You need to Base64 encode or decode your data.</span><span class="sxs-lookup"><span data-stu-id="b50d3-111">You need to Base64 encode or decode your data.</span></span> <span data-ttu-id="b50d3-112">Field mappings support several **mapping functions**, including functions for Base64 encoding and decoding.</span><span class="sxs-lookup"><span data-stu-id="b50d3-112">Field mappings support several **mapping functions**, including functions for Base64 encoding and decoding.</span></span>   

## <a name="setting-up-field-mappings"></a><span data-ttu-id="b50d3-113">Setting up field mappings</span><span class="sxs-lookup"><span data-stu-id="b50d3-113">Setting up field mappings</span></span>
<span data-ttu-id="b50d3-114">You can add field mappings when creating a new indexer using the [Create Indexer](https://msdn.microsoft.com/library/azure/dn946899.aspx) API.</span><span class="sxs-lookup"><span data-stu-id="b50d3-114">You can add field mappings when creating a new indexer using the [Create Indexer](https://msdn.microsoft.com/library/azure/dn946899.aspx) API.</span></span> <span data-ttu-id="b50d3-115">You can manage field mappings on an indexing indexer using the [Update Indexer](https://msdn.microsoft.com/library/azure/dn946892.aspx) API.</span><span class="sxs-lookup"><span data-stu-id="b50d3-115">You can manage field mappings on an indexing indexer using the [Update Indexer](https://msdn.microsoft.com/library/azure/dn946892.aspx) API.</span></span>

<span data-ttu-id="b50d3-116">A field mapping consists of three parts:</span><span class="sxs-lookup"><span data-stu-id="b50d3-116">A field mapping consists of three parts:</span></span>

1. <span data-ttu-id="b50d3-117">A `sourceFieldName`, which represents a field in your data source.</span><span class="sxs-lookup"><span data-stu-id="b50d3-117">A `sourceFieldName`, which represents a field in your data source.</span></span> <span data-ttu-id="b50d3-118">This property is required.</span><span class="sxs-lookup"><span data-stu-id="b50d3-118">This property is required.</span></span>
2. <span data-ttu-id="b50d3-119">An optional `targetFieldName`, which represents a field in your search index.</span><span class="sxs-lookup"><span data-stu-id="b50d3-119">An optional `targetFieldName`, which represents a field in your search index.</span></span> <span data-ttu-id="b50d3-120">If omitted, the same name as in the data source is used.</span><span class="sxs-lookup"><span data-stu-id="b50d3-120">If omitted, the same name as in the data source is used.</span></span>
3. <span data-ttu-id="b50d3-121">An optional `mappingFunction`, which can transform your data using one of several predefined functions.</span><span class="sxs-lookup"><span data-stu-id="b50d3-121">An optional `mappingFunction`, which can transform your data using one of several predefined functions.</span></span> <span data-ttu-id="b50d3-122">The full list of functions is [below](#mappingFunctions).</span><span class="sxs-lookup"><span data-stu-id="b50d3-122">The full list of functions is [below](#mappingFunctions).</span></span>

<span data-ttu-id="b50d3-123">Fields mappings are added to the `fieldMappings` array on the indexer definition.</span><span class="sxs-lookup"><span data-stu-id="b50d3-123">Fields mappings are added to the `fieldMappings` array on the indexer definition.</span></span>

<span data-ttu-id="b50d3-124">For example, here's how you can accommodate differences in field names:</span><span class="sxs-lookup"><span data-stu-id="b50d3-124">For example, here's how you can accommodate differences in field names:</span></span>

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

<span data-ttu-id="b50d3-125">An indexer can have multiple field mappings.</span><span class="sxs-lookup"><span data-stu-id="b50d3-125">An indexer can have multiple field mappings.</span></span> <span data-ttu-id="b50d3-126">For example, here's how you can "fork" a field:</span><span class="sxs-lookup"><span data-stu-id="b50d3-126">For example, here's how you can "fork" a field:</span></span>

```JSON

"fieldMappings" : [
    { "sourceFieldName" : "text", "targetFieldName" : "textStandardEnglishAnalyzer" },
    { "sourceFieldName" : "text", "targetFieldName" : "textSoundexAnalyzer" }
]
```

> [!NOTE]
> <span data-ttu-id="b50d3-127">Azure Search uses case-insensitive comparison to resolve the field and function names in field mappings.</span><span class="sxs-lookup"><span data-stu-id="b50d3-127">Azure Search uses case-insensitive comparison to resolve the field and function names in field mappings.</span></span> <span data-ttu-id="b50d3-128">This is convenient (you don't have to get all the casing right), but it means that your data source or index cannot have fields that differ only by case.</span><span class="sxs-lookup"><span data-stu-id="b50d3-128">This is convenient (you don't have to get all the casing right), but it means that your data source or index cannot have fields that differ only by case.</span></span>  
>
>

<a name="mappingFunctions"></a>

## <a name="field-mapping-functions"></a><span data-ttu-id="b50d3-129">Field mapping functions</span><span class="sxs-lookup"><span data-stu-id="b50d3-129">Field mapping functions</span></span>
<span data-ttu-id="b50d3-130">These functions are currently supported:</span><span class="sxs-lookup"><span data-stu-id="b50d3-130">These functions are currently supported:</span></span>

* [<span data-ttu-id="b50d3-131">base64Encode</span><span class="sxs-lookup"><span data-stu-id="b50d3-131">base64Encode</span></span>](#base64EncodeFunction)
* [<span data-ttu-id="b50d3-132">base64Decode</span><span class="sxs-lookup"><span data-stu-id="b50d3-132">base64Decode</span></span>](#base64DecodeFunction)
* [<span data-ttu-id="b50d3-133">extractTokenAtPosition</span><span class="sxs-lookup"><span data-stu-id="b50d3-133">extractTokenAtPosition</span></span>](#extractTokenAtPositionFunction)
* [<span data-ttu-id="b50d3-134">jsonArrayToStringCollection</span><span class="sxs-lookup"><span data-stu-id="b50d3-134">jsonArrayToStringCollection</span></span>](#jsonArrayToStringCollectionFunction)

<a name="base64EncodeFunction"></a>

## <a name="base64encode"></a><span data-ttu-id="b50d3-135">base64Encode</span><span class="sxs-lookup"><span data-stu-id="b50d3-135">base64Encode</span></span>
<span data-ttu-id="b50d3-136">Performs *URL-safe* Base64 encoding of the input string.</span><span class="sxs-lookup"><span data-stu-id="b50d3-136">Performs *URL-safe* Base64 encoding of the input string.</span></span> <span data-ttu-id="b50d3-137">Assumes that the input is UTF-8 encoded.</span><span class="sxs-lookup"><span data-stu-id="b50d3-137">Assumes that the input is UTF-8 encoded.</span></span>

### <a name="sample-use-case---document-key-lookup"></a><span data-ttu-id="b50d3-138">Sample use case - document key lookup</span><span class="sxs-lookup"><span data-stu-id="b50d3-138">Sample use case - document key lookup</span></span>
<span data-ttu-id="b50d3-139">Only URL-safe characters can appear in an Azure Search document key (because customers must be able to address the document using the [Lookup API](https://docs.microsoft.com/rest/api/searchservice/lookup-document), for example).</span><span class="sxs-lookup"><span data-stu-id="b50d3-139">Only URL-safe characters can appear in an Azure Search document key (because customers must be able to address the document using the [Lookup API](https://docs.microsoft.com/rest/api/searchservice/lookup-document), for example).</span></span> <span data-ttu-id="b50d3-140">If your data contains URL-unsafe characters and you want to use it to populate a key field in your search index, use this function.</span><span class="sxs-lookup"><span data-stu-id="b50d3-140">If your data contains URL-unsafe characters and you want to use it to populate a key field in your search index, use this function.</span></span> <span data-ttu-id="b50d3-141">Once the key is encoded, you can use base64 decode to retrieve the original value.</span><span class="sxs-lookup"><span data-stu-id="b50d3-141">Once the key is encoded, you can use base64 decode to retrieve the original value.</span></span> <span data-ttu-id="b50d3-142">For details, see the [base64 encoding and decoding](#base64details) section.</span><span class="sxs-lookup"><span data-stu-id="b50d3-142">For details, see the [base64 encoding and decoding](#base64details) section.</span></span>

#### <a name="example"></a><span data-ttu-id="b50d3-143">Example</span><span class="sxs-lookup"><span data-stu-id="b50d3-143">Example</span></span>
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "SourceKey",
    "targetFieldName" : "IndexKey",
    "mappingFunction" : { "name" : "base64Encode" }
  }]
```

### <a name="sample-use-case---retrieve-original-key"></a><span data-ttu-id="b50d3-144">Sample use case - retrieve original key</span><span class="sxs-lookup"><span data-stu-id="b50d3-144">Sample use case - retrieve original key</span></span>
<span data-ttu-id="b50d3-145">You have a blob indexer that indexes blobs with the blob path metadata as the document key.</span><span class="sxs-lookup"><span data-stu-id="b50d3-145">You have a blob indexer that indexes blobs with the blob path metadata as the document key.</span></span> <span data-ttu-id="b50d3-146">After retrieving the encoded document key, you want to decode the path and download the blob.</span><span class="sxs-lookup"><span data-stu-id="b50d3-146">After retrieving the encoded document key, you want to decode the path and download the blob.</span></span>

#### <a name="example"></a><span data-ttu-id="b50d3-147">Example</span><span class="sxs-lookup"><span data-stu-id="b50d3-147">Example</span></span>
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "SourceKey",
    "targetFieldName" : "IndexKey",
    "mappingFunction" : { "name" : "base64Encode", "parameters" : { "useHttpServerUtilityUrlTokenEncode" : false } }
  }]
 ```

<span data-ttu-id="b50d3-148">If you don't need to look up documents by keys and also don't need to decode the encoded content, you can just leave out `parameters` for the mapping function, which defaults `useHttpServerUtilityUrlTokenEncode` to `true`.</span><span class="sxs-lookup"><span data-stu-id="b50d3-148">If you don't need to look up documents by keys and also don't need to decode the encoded content, you can just leave out `parameters` for the mapping function, which defaults `useHttpServerUtilityUrlTokenEncode` to `true`.</span></span> <span data-ttu-id="b50d3-149">Otherwise, see [base64 details](#base64details) section to decide which settings to use.</span><span class="sxs-lookup"><span data-stu-id="b50d3-149">Otherwise, see [base64 details](#base64details) section to decide which settings to use.</span></span>

<a name="base64DecodeFunction"></a>

## <a name="base64decode"></a><span data-ttu-id="b50d3-150">base64Decode</span><span class="sxs-lookup"><span data-stu-id="b50d3-150">base64Decode</span></span>
<span data-ttu-id="b50d3-151">Performs Base64 decoding of the input string.</span><span class="sxs-lookup"><span data-stu-id="b50d3-151">Performs Base64 decoding of the input string.</span></span> <span data-ttu-id="b50d3-152">The input is assumed to a *URL-safe* Base64-encoded string.</span><span class="sxs-lookup"><span data-stu-id="b50d3-152">The input is assumed to a *URL-safe* Base64-encoded string.</span></span>

### <a name="sample-use-case"></a><span data-ttu-id="b50d3-153">Sample use case</span><span class="sxs-lookup"><span data-stu-id="b50d3-153">Sample use case</span></span>
<span data-ttu-id="b50d3-154">Blob custom metadata values must be ASCII-encoded.</span><span class="sxs-lookup"><span data-stu-id="b50d3-154">Blob custom metadata values must be ASCII-encoded.</span></span> <span data-ttu-id="b50d3-155">You can use Base64 encoding to represent arbitrary UTF-8 strings in blob custom metadata.</span><span class="sxs-lookup"><span data-stu-id="b50d3-155">You can use Base64 encoding to represent arbitrary UTF-8 strings in blob custom metadata.</span></span> <span data-ttu-id="b50d3-156">However, to make search meaningful, you can use this function to turn the encoded data back into "regular" strings when populating your search index.</span><span class="sxs-lookup"><span data-stu-id="b50d3-156">However, to make search meaningful, you can use this function to turn the encoded data back into "regular" strings when populating your search index.</span></span>

#### <a name="example"></a><span data-ttu-id="b50d3-157">Example</span><span class="sxs-lookup"><span data-stu-id="b50d3-157">Example</span></span>
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Base64EncodedMetadata",
    "targetFieldName" : "SearchableMetadata",
    "mappingFunction" : { "name" : "base64Decode", "parameters" : { "useHttpServerUtilityUrlTokenDecode" : false } }
  }]
```

<span data-ttu-id="b50d3-158">If you don't specify any `parameters`, then the default value of `useHttpServerUtilityUrlTokenDecode` is `true`.</span><span class="sxs-lookup"><span data-stu-id="b50d3-158">If you don't specify any `parameters`, then the default value of `useHttpServerUtilityUrlTokenDecode` is `true`.</span></span> <span data-ttu-id="b50d3-159">See [base64 details](#base64details) section to decide which settings to use.</span><span class="sxs-lookup"><span data-stu-id="b50d3-159">See [base64 details](#base64details) section to decide which settings to use.</span></span>

<a name="base64details"></a>

### <a name="details-of-base64-encoding-and-decoding"></a><span data-ttu-id="b50d3-160">Details of base64 encoding and decoding</span><span class="sxs-lookup"><span data-stu-id="b50d3-160">Details of base64 encoding and decoding</span></span>
<span data-ttu-id="b50d3-161">Azure Search supports two base64 encodings: HttpServerUtility URL token and URL-safe base64 encoding without padding.</span><span class="sxs-lookup"><span data-stu-id="b50d3-161">Azure Search supports two base64 encodings: HttpServerUtility URL token and URL-safe base64 encoding without padding.</span></span> <span data-ttu-id="b50d3-162">You need to use the same encoding as the mapping functions if you want to encode a document key for look up, encode a value to be decoded by the indexer, or decode a field encoded by the indexer.</span><span class="sxs-lookup"><span data-stu-id="b50d3-162">You need to use the same encoding as the mapping functions if you want to encode a document key for look up, encode a value to be decoded by the indexer, or decode a field encoded by the indexer.</span></span>

<span data-ttu-id="b50d3-163">If `useHttpServerUtilityUrlTokenEncode` or `useHttpServerUtilityUrlTokenDecode` parameters for encoding and decoding respectively are set to `true`, then `base64Encode` behaves like [HttpServerUtility.UrlTokenEncode](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx) and `base64Decode` behaves like [HttpServerUtility.UrlTokenDecode](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokendecode.aspx).</span><span class="sxs-lookup"><span data-stu-id="b50d3-163">If `useHttpServerUtilityUrlTokenEncode` or `useHttpServerUtilityUrlTokenDecode` parameters for encoding and decoding respectively are set to `true`, then `base64Encode` behaves like [HttpServerUtility.UrlTokenEncode](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx) and `base64Decode` behaves like [HttpServerUtility.UrlTokenDecode](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokendecode.aspx).</span></span>

<span data-ttu-id="b50d3-164">If you are not using the full .NET Framework (i.e., you are using .NET Core or other programming environment) to produce the key values to emulate Azure Search behavior, then you should set `useHttpServerUtilityUrlTokenEncode` and `useHttpServerUtilityUrlTokenDecode` to `false`.</span><span class="sxs-lookup"><span data-stu-id="b50d3-164">If you are not using the full .NET Framework (i.e., you are using .NET Core or other programming environment) to produce the key values to emulate Azure Search behavior, then you should set `useHttpServerUtilityUrlTokenEncode` and `useHttpServerUtilityUrlTokenDecode` to `false`.</span></span> <span data-ttu-id="b50d3-165">Depending on the library you use, the base64 encode and decode utility functions may be  different from Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b50d3-165">Depending on the library you use, the base64 encode and decode utility functions may be  different from Azure Search.</span></span>

<span data-ttu-id="b50d3-166">The following table compares different base64 encodings of the string `00>00?00`.</span><span class="sxs-lookup"><span data-stu-id="b50d3-166">The following table compares different base64 encodings of the string `00>00?00`.</span></span> <span data-ttu-id="b50d3-167">To determine the required additional processing (if any) for your base64 functions, apply your library encode function on the string `00>00?00` and compare the output with the expected output `MDA-MDA_MDA`.</span><span class="sxs-lookup"><span data-stu-id="b50d3-167">To determine the required additional processing (if any) for your base64 functions, apply your library encode function on the string `00>00?00` and compare the output with the expected output `MDA-MDA_MDA`.</span></span>

| <span data-ttu-id="b50d3-168">Encoding</span><span class="sxs-lookup"><span data-stu-id="b50d3-168">Encoding</span></span> | <span data-ttu-id="b50d3-169">Base64 encode output</span><span class="sxs-lookup"><span data-stu-id="b50d3-169">Base64 encode output</span></span> | <span data-ttu-id="b50d3-170">Additional processing after library encoding</span><span class="sxs-lookup"><span data-stu-id="b50d3-170">Additional processing after library encoding</span></span> | <span data-ttu-id="b50d3-171">Additional processing before library decoding</span><span class="sxs-lookup"><span data-stu-id="b50d3-171">Additional processing before library decoding</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b50d3-172">Base64 with padding</span><span class="sxs-lookup"><span data-stu-id="b50d3-172">Base64 with padding</span></span> | `MDA+MDA/MDA=` | <span data-ttu-id="b50d3-173">Use URL-safe characters and remove padding</span><span class="sxs-lookup"><span data-stu-id="b50d3-173">Use URL-safe characters and remove padding</span></span> | <span data-ttu-id="b50d3-174">Use standard base64 characters and add padding</span><span class="sxs-lookup"><span data-stu-id="b50d3-174">Use standard base64 characters and add padding</span></span> |
| <span data-ttu-id="b50d3-175">Base64 without padding</span><span class="sxs-lookup"><span data-stu-id="b50d3-175">Base64 without padding</span></span> | `MDA+MDA/MDA` | <span data-ttu-id="b50d3-176">Use URL-safe characters</span><span class="sxs-lookup"><span data-stu-id="b50d3-176">Use URL-safe characters</span></span> | <span data-ttu-id="b50d3-177">Use standard base64 characters</span><span class="sxs-lookup"><span data-stu-id="b50d3-177">Use standard base64 characters</span></span> |
| <span data-ttu-id="b50d3-178">URL-safe base64 with padding</span><span class="sxs-lookup"><span data-stu-id="b50d3-178">URL-safe base64 with padding</span></span> | `MDA-MDA_MDA=` | <span data-ttu-id="b50d3-179">Remove padding</span><span class="sxs-lookup"><span data-stu-id="b50d3-179">Remove padding</span></span> | <span data-ttu-id="b50d3-180">Add padding</span><span class="sxs-lookup"><span data-stu-id="b50d3-180">Add padding</span></span> |
| <span data-ttu-id="b50d3-181">URL-safe base64 without padding</span><span class="sxs-lookup"><span data-stu-id="b50d3-181">URL-safe base64 without padding</span></span> | `MDA-MDA_MDA` | <span data-ttu-id="b50d3-182">None</span><span class="sxs-lookup"><span data-stu-id="b50d3-182">None</span></span> | <span data-ttu-id="b50d3-183">None</span><span class="sxs-lookup"><span data-stu-id="b50d3-183">None</span></span> |

<a name="extractTokenAtPositionFunction"></a>

## <a name="extracttokenatposition"></a><span data-ttu-id="b50d3-184">extractTokenAtPosition</span><span class="sxs-lookup"><span data-stu-id="b50d3-184">extractTokenAtPosition</span></span>
<span data-ttu-id="b50d3-185">Splits a string field using the specified delimiter, and picks the token at the specified position in the resulting split.</span><span class="sxs-lookup"><span data-stu-id="b50d3-185">Splits a string field using the specified delimiter, and picks the token at the specified position in the resulting split.</span></span>

<span data-ttu-id="b50d3-186">For example, if the input is `Jane Doe`, the `delimiter` is `" "`(space) and the `position` is 0, the result is `Jane`; if the `position` is 1, the result is `Doe`.</span><span class="sxs-lookup"><span data-stu-id="b50d3-186">For example, if the input is `Jane Doe`, the `delimiter` is `" "`(space) and the `position` is 0, the result is `Jane`; if the `position` is 1, the result is `Doe`.</span></span> <span data-ttu-id="b50d3-187">If the position refers to a token that doesn't exist, an error is returned.</span><span class="sxs-lookup"><span data-stu-id="b50d3-187">If the position refers to a token that doesn't exist, an error is returned.</span></span>

### <a name="sample-use-case"></a><span data-ttu-id="b50d3-188">Sample use case</span><span class="sxs-lookup"><span data-stu-id="b50d3-188">Sample use case</span></span>
<span data-ttu-id="b50d3-189">Your data source contains a `PersonName` field, and you want to index it as two separate `FirstName` and `LastName` fields.</span><span class="sxs-lookup"><span data-stu-id="b50d3-189">Your data source contains a `PersonName` field, and you want to index it as two separate `FirstName` and `LastName` fields.</span></span> <span data-ttu-id="b50d3-190">You can use this function to split the input using the space character as the delimiter.</span><span class="sxs-lookup"><span data-stu-id="b50d3-190">You can use this function to split the input using the space character as the delimiter.</span></span>

### <a name="parameters"></a><span data-ttu-id="b50d3-191">Parameters</span><span class="sxs-lookup"><span data-stu-id="b50d3-191">Parameters</span></span>
* <span data-ttu-id="b50d3-192">`delimiter`: a string to use as the separator when splitting the input string.</span><span class="sxs-lookup"><span data-stu-id="b50d3-192">`delimiter`: a string to use as the separator when splitting the input string.</span></span>
* <span data-ttu-id="b50d3-193">`position`: an integer zero-based position of the token to pick after the input string is split.</span><span class="sxs-lookup"><span data-stu-id="b50d3-193">`position`: an integer zero-based position of the token to pick after the input string is split.</span></span>    

### <a name="example"></a><span data-ttu-id="b50d3-194">Example</span><span class="sxs-lookup"><span data-stu-id="b50d3-194">Example</span></span>
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

## <a name="jsonarraytostringcollection"></a><span data-ttu-id="b50d3-195">jsonArrayToStringCollection</span><span class="sxs-lookup"><span data-stu-id="b50d3-195">jsonArrayToStringCollection</span></span>
<span data-ttu-id="b50d3-196">Transforms a string formatted as a JSON array of strings into a string array that can be used to populate a `Collection(Edm.String)` field in the index.</span><span class="sxs-lookup"><span data-stu-id="b50d3-196">Transforms a string formatted as a JSON array of strings into a string array that can be used to populate a `Collection(Edm.String)` field in the index.</span></span>

<span data-ttu-id="b50d3-197">For example, if the input string is `["red", "white", "blue"]`, then the target field of type `Collection(Edm.String)` will be populated with the three values `red`, `white`, and `blue`.</span><span class="sxs-lookup"><span data-stu-id="b50d3-197">For example, if the input string is `["red", "white", "blue"]`, then the target field of type `Collection(Edm.String)` will be populated with the three values `red`, `white`, and `blue`.</span></span> <span data-ttu-id="b50d3-198">For input values that cannot be parsed as JSON string arrays, an error is returned.</span><span class="sxs-lookup"><span data-stu-id="b50d3-198">For input values that cannot be parsed as JSON string arrays, an error is returned.</span></span>

### <a name="sample-use-case"></a><span data-ttu-id="b50d3-199">Sample use case</span><span class="sxs-lookup"><span data-stu-id="b50d3-199">Sample use case</span></span>
<span data-ttu-id="b50d3-200">Azure SQL database doesn't have a built-in data type that naturally maps to `Collection(Edm.String)` fields in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b50d3-200">Azure SQL database doesn't have a built-in data type that naturally maps to `Collection(Edm.String)` fields in Azure Search.</span></span> <span data-ttu-id="b50d3-201">To populate string collection fields, format your source data as a JSON string array and use this function.</span><span class="sxs-lookup"><span data-stu-id="b50d3-201">To populate string collection fields, format your source data as a JSON string array and use this function.</span></span>

### <a name="example"></a><span data-ttu-id="b50d3-202">Example</span><span class="sxs-lookup"><span data-stu-id="b50d3-202">Example</span></span>
```JSON

"fieldMappings" : [
  { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } }
]
```


## <a name="help-us-make-azure-search-better"></a><span data-ttu-id="b50d3-203">Help us make Azure Search better</span><span class="sxs-lookup"><span data-stu-id="b50d3-203">Help us make Azure Search better</span></span>
<span data-ttu-id="b50d3-204">If you have feature requests or ideas for improvements, please reach out to us on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="b50d3-204">If you have feature requests or ideas for improvements, please reach out to us on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span></span>
