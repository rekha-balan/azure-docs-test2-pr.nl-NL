---
title: Upgrading to the Azure Search .NET SDK version 1.1 | Microsoft Docs
description: Upgrading to the Azure Search .NET SDK version 1.1
services: search
documentationcenter: ''
author: brjohnstmsft
manager: pablocas
editor: ''
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 9782454e3bfc697b63cde8aa28a14be0c393c36b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564091"
---
# <a name="upgrading-to-the-azure-search-net-sdk-version-3"></a><span data-ttu-id="7c69d-103">Upgrading to the Azure Search .NET SDK version 3</span><span class="sxs-lookup"><span data-stu-id="7c69d-103">Upgrading to the Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="7c69d-104">If you're using version 2.0-preview or older of the [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application to use version 3.</span><span class="sxs-lookup"><span data-stu-id="7c69d-104">If you're using version 2.0-preview or older of the [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application to use version 3.</span></span>

<span data-ttu-id="7c69d-105">For a more general walkthrough of the SDK including examples, see [How to use Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7c69d-105">For a more general walkthrough of the SDK including examples, see [How to use Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="7c69d-106">Version 3 of the Azure Search .NET SDK contains some changes from earlier versions.</span><span class="sxs-lookup"><span data-stu-id="7c69d-106">Version 3 of the Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="7c69d-107">These are mostly minor, so changing your code should require only minimal effort.</span><span class="sxs-lookup"><span data-stu-id="7c69d-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="7c69d-108">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new SDK version.</span><span class="sxs-lookup"><span data-stu-id="7c69d-108">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="7c69d-109">If you're using version 1.0.2-preview or older, you should upgrade to version 1.1 first, and then upgrade to version 3.</span><span class="sxs-lookup"><span data-stu-id="7c69d-109">If you're using version 1.0.2-preview or older, you should upgrade to version 1.1 first, and then upgrade to version 3.</span></span> <span data-ttu-id="7c69d-110">See [Appendix: Steps to upgrade to version 1.1](#UpgradeStepsV1) for instructions.</span><span class="sxs-lookup"><span data-stu-id="7c69d-110">See [Appendix: Steps to upgrade to version 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="7c69d-111">Your Azure Search service instance supports several REST API versions, including the latest one.</span><span class="sxs-lookup"><span data-stu-id="7c69d-111">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="7c69d-112">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span><span class="sxs-lookup"><span data-stu-id="7c69d-112">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span> <span data-ttu-id="7c69d-113">When using the REST API, you must specify the API version in every request via the api-version parameter.</span><span class="sxs-lookup"><span data-stu-id="7c69d-113">When using the REST API, you must specify the API version in every request via the api-version parameter.</span></span> <span data-ttu-id="7c69d-114">When using the .NET SDK, the version of the SDK you’re using determines the corresponding version of the REST API.</span><span class="sxs-lookup"><span data-stu-id="7c69d-114">When using the .NET SDK, the version of the SDK you’re using determines the corresponding version of the REST API.</span></span> <span data-ttu-id="7c69d-115">If you are using an older SDK, you can continue to run that code with no changes even if the service is upgraded to support a newer API version.</span><span class="sxs-lookup"><span data-stu-id="7c69d-115">If you are using an older SDK, you can continue to run that code with no changes even if the service is upgraded to support a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="7c69d-116">What's new in version 3</span><span class="sxs-lookup"><span data-stu-id="7c69d-116">What's new in version 3</span></span>
<span data-ttu-id="7c69d-117">Version 3 of the Azure Search .NET SDK targets the latest generally available version of the Azure Search REST API, specifically 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="7c69d-117">Version 3 of the Azure Search .NET SDK targets the latest generally available version of the Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="7c69d-118">This makes it possible to use many new features of Azure Search from a .NET application, including the following:</span><span class="sxs-lookup"><span data-stu-id="7c69d-118">This makes it possible to use many new features of Azure Search from a .NET application, including the following:</span></span>

* [<span data-ttu-id="7c69d-119">Custom analyzers</span><span class="sxs-lookup"><span data-stu-id="7c69d-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="7c69d-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span><span class="sxs-lookup"><span data-stu-id="7c69d-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="7c69d-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="7c69d-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="7c69d-122">ETags support to enable safe concurrent updating of index definitions, indexers, and data sources</span><span class="sxs-lookup"><span data-stu-id="7c69d-122">ETags support to enable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="7c69d-123">Support for building index field definitions declaratively by decorating your model class and using the new `FieldBuilder` class.</span><span class="sxs-lookup"><span data-stu-id="7c69d-123">Support for building index field definitions declaratively by decorating your model class and using the new `FieldBuilder` class.</span></span>
* <span data-ttu-id="7c69d-124">Support for .NET Core and .NET Portable Profile 111</span><span class="sxs-lookup"><span data-stu-id="7c69d-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="7c69d-125">Steps to upgrade</span><span class="sxs-lookup"><span data-stu-id="7c69d-125">Steps to upgrade</span></span>
<span data-ttu-id="7c69d-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c69d-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="7c69d-127">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span><span class="sxs-lookup"><span data-stu-id="7c69d-127">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="7c69d-128">Depending on how your code is structured, it may rebuild successfully.</span><span class="sxs-lookup"><span data-stu-id="7c69d-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="7c69d-129">If so, you're ready to go!</span><span class="sxs-lookup"><span data-stu-id="7c69d-129">If so, you're ready to go!</span></span>

<span data-ttu-id="7c69d-130">If your build fails, you should see a build error like the following:</span><span class="sxs-lookup"><span data-stu-id="7c69d-130">If your build fails, you should see a build error like the following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' to 'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="7c69d-131">The next step is to fix this build error.</span><span class="sxs-lookup"><span data-stu-id="7c69d-131">The next step is to fix this build error.</span></span> <span data-ttu-id="7c69d-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes the error and how to fix it.</span><span class="sxs-lookup"><span data-stu-id="7c69d-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes the error and how to fix it.</span></span>

<span data-ttu-id="7c69d-133">You may see additional build warnings related to obsolete methods or properties.</span><span class="sxs-lookup"><span data-stu-id="7c69d-133">You may see additional build warnings related to obsolete methods or properties.</span></span> <span data-ttu-id="7c69d-134">The warnings will include instructions on what to use instead of the deprecated feature.</span><span class="sxs-lookup"><span data-stu-id="7c69d-134">The warnings will include instructions on what to use instead of the deprecated feature.</span></span> <span data-ttu-id="7c69d-135">For example, if your application uses the `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="7c69d-135">For example, if your application uses the `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="7c69d-136">Once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span><span class="sxs-lookup"><span data-stu-id="7c69d-136">Once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span> <span data-ttu-id="7c69d-137">New features in the SDK are detailed in [What's new in version 3](#WhatsNew).</span><span class="sxs-lookup"><span data-stu-id="7c69d-137">New features in the SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="7c69d-138">Breaking changes in version 3</span><span class="sxs-lookup"><span data-stu-id="7c69d-138">Breaking changes in version 3</span></span>
<span data-ttu-id="7c69d-139">There a small number of breaking changes in version 3 that may require code changes in addition to rebuilding your application.</span><span class="sxs-lookup"><span data-stu-id="7c69d-139">There a small number of breaking changes in version 3 that may require code changes in addition to rebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="7c69d-140">Indexes.GetClient return type</span><span class="sxs-lookup"><span data-stu-id="7c69d-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="7c69d-141">The `Indexes.GetClient` method has a new return type.</span><span class="sxs-lookup"><span data-stu-id="7c69d-141">The `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="7c69d-142">Previously, it returned `SearchIndexClient`, but this was changed to `ISearchIndexClient` in version 2.0-preview, and that change carries over to version 3.</span><span class="sxs-lookup"><span data-stu-id="7c69d-142">Previously, it returned `SearchIndexClient`, but this was changed to `ISearchIndexClient` in version 2.0-preview, and that change carries over to version 3.</span></span> <span data-ttu-id="7c69d-143">This is to support customers that wish to mock the `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-143">This is to support customers that wish to mock the `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="7c69d-144">Example</span><span class="sxs-lookup"><span data-stu-id="7c69d-144">Example</span></span>
<span data-ttu-id="7c69d-145">If your code looks like this:</span><span class="sxs-lookup"><span data-stu-id="7c69d-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="7c69d-146">You can change it to this to fix any build errors:</span><span class="sxs-lookup"><span data-stu-id="7c69d-146">You can change it to this to fix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-to-strings"></a><span data-ttu-id="7c69d-147">AnalyzerName, DataType, and others are no longer implicitly convertible to strings</span><span class="sxs-lookup"><span data-stu-id="7c69d-147">AnalyzerName, DataType, and others are no longer implicitly convertible to strings</span></span>
<span data-ttu-id="7c69d-148">There are many types in the Azure Search .NET SDK that derive from `ExtensibleEnum`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-148">There are many types in the Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="7c69d-149">Previously these types were all implicitly convertible to type `string`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-149">Previously these types were all implicitly convertible to type `string`.</span></span> <span data-ttu-id="7c69d-150">However, a bug was discovered in the `Object.Equals` implementation for these classes, and fixing the bug required disabling this implicit conversion.</span><span class="sxs-lookup"><span data-stu-id="7c69d-150">However, a bug was discovered in the `Object.Equals` implementation for these classes, and fixing the bug required disabling this implicit conversion.</span></span> <span data-ttu-id="7c69d-151">Explicit conversion to `string` is still allowed.</span><span class="sxs-lookup"><span data-stu-id="7c69d-151">Explicit conversion to `string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="7c69d-152">Example</span><span class="sxs-lookup"><span data-stu-id="7c69d-152">Example</span></span>
<span data-ttu-id="7c69d-153">If your code looks like this:</span><span class="sxs-lookup"><span data-stu-id="7c69d-153">If your code looks like this:</span></span>

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

<span data-ttu-id="7c69d-154">You can change it to this to fix any build errors:</span><span class="sxs-lookup"><span data-stu-id="7c69d-154">You can change it to this to fix any build errors:</span></span>

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a><span data-ttu-id="7c69d-155">Removed obsolete members</span><span class="sxs-lookup"><span data-stu-id="7c69d-155">Removed obsolete members</span></span>

<span data-ttu-id="7c69d-156">You may see build errors related to methods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span><span class="sxs-lookup"><span data-stu-id="7c69d-156">You may see build errors related to methods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="7c69d-157">If you encounter such errors, here is how to resolve them:</span><span class="sxs-lookup"><span data-stu-id="7c69d-157">If you encounter such errors, here is how to resolve them:</span></span>

- <span data-ttu-id="7c69d-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span><span class="sxs-lookup"><span data-stu-id="7c69d-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="7c69d-159">If you were using the `ScoringParameter.Value` property, use the `ScoringParameter.Values` property or the `ToString` method instead.</span><span class="sxs-lookup"><span data-stu-id="7c69d-159">If you were using the `ScoringParameter.Value` property, use the `ScoringParameter.Values` property or the `ToString` method instead.</span></span>
- <span data-ttu-id="7c69d-160">If you were using the `SearchRequestOptions.RequestId` property, use the `ClientRequestId` property instead.</span><span class="sxs-lookup"><span data-stu-id="7c69d-160">If you were using the `SearchRequestOptions.RequestId` property, use the `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="7c69d-161">Removed preview features</span><span class="sxs-lookup"><span data-stu-id="7c69d-161">Removed preview features</span></span>

<span data-ttu-id="7c69d-162">If you are upgrading from version 2.0-preview to version 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span><span class="sxs-lookup"><span data-stu-id="7c69d-162">If you are upgrading from version 2.0-preview to version 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="7c69d-163">Specifically, the following methods of the `IndexingParametersExtensions` class have been removed:</span><span class="sxs-lookup"><span data-stu-id="7c69d-163">Specifically, the following methods of the `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="7c69d-164">If your application has a hard dependency on these features, you will not be able to upgrade to version 3 of the Azure Search .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="7c69d-164">If your application has a hard dependency on these features, you will not be able to upgrade to version 3 of the Azure Search .NET SDK.</span></span> <span data-ttu-id="7c69d-165">You can continue to use version 2.0-preview.</span><span class="sxs-lookup"><span data-stu-id="7c69d-165">You can continue to use version 2.0-preview.</span></span> <span data-ttu-id="7c69d-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span><span class="sxs-lookup"><span data-stu-id="7c69d-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="7c69d-167">Preview features are for evaluation only and may change.</span><span class="sxs-lookup"><span data-stu-id="7c69d-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="7c69d-168">Conclusion</span><span class="sxs-lookup"><span data-stu-id="7c69d-168">Conclusion</span></span>
<span data-ttu-id="7c69d-169">If you need more details on using the Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7c69d-169">If you need more details on using the Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="7c69d-170">We welcome your feedback on the SDK.</span><span class="sxs-lookup"><span data-stu-id="7c69d-170">We welcome your feedback on the SDK.</span></span> <span data-ttu-id="7c69d-171">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span><span class="sxs-lookup"><span data-stu-id="7c69d-171">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="7c69d-172">If you find a bug, you can file an issue in the [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span><span class="sxs-lookup"><span data-stu-id="7c69d-172">If you find a bug, you can file an issue in the [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="7c69d-173">Make sure to prefix your issue title with "Search SDK: ".</span><span class="sxs-lookup"><span data-stu-id="7c69d-173">Make sure to prefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="7c69d-174">Thank you for using Azure Search!</span><span class="sxs-lookup"><span data-stu-id="7c69d-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-to-upgrade-to-version-11"></a><span data-ttu-id="7c69d-175">Appendix: Steps to upgrade to version 1.1</span><span class="sxs-lookup"><span data-stu-id="7c69d-175">Appendix: Steps to upgrade to version 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="7c69d-176">This section applies only to users of the Azure Search .NET SDK version 1.0.2-preview and older.</span><span class="sxs-lookup"><span data-stu-id="7c69d-176">This section applies only to users of the Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="7c69d-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c69d-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="7c69d-178">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span><span class="sxs-lookup"><span data-stu-id="7c69d-178">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="7c69d-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, the build should succeed and you're ready to go!</span><span class="sxs-lookup"><span data-stu-id="7c69d-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, the build should succeed and you're ready to go!</span></span>

<span data-ttu-id="7c69d-180">If you were previously using version 0.13.0-preview or older, you should see build errors like the following:</span><span class="sxs-lookup"><span data-stu-id="7c69d-180">If you were previously using version 0.13.0-preview or older, you should see build errors like the following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: The type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="7c69d-181">The next step is to fix the build errors one by one.</span><span class="sxs-lookup"><span data-stu-id="7c69d-181">The next step is to fix the build errors one by one.</span></span> <span data-ttu-id="7c69d-182">Most will require changing some class and method names that have been renamed in the SDK.</span><span class="sxs-lookup"><span data-stu-id="7c69d-182">Most will require changing some class and method names that have been renamed in the SDK.</span></span> <span data-ttu-id="7c69d-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span><span class="sxs-lookup"><span data-stu-id="7c69d-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="7c69d-184">If you're using custom classes to model your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in the 1.1 version of the SDK of which you should be aware.</span><span class="sxs-lookup"><span data-stu-id="7c69d-184">If you're using custom classes to model your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in the 1.1 version of the SDK of which you should be aware.</span></span> <span data-ttu-id="7c69d-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span><span class="sxs-lookup"><span data-stu-id="7c69d-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="7c69d-186">Finally, once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span><span class="sxs-lookup"><span data-stu-id="7c69d-186">Finally, once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="7c69d-187">List of breaking changes in version 1.1</span><span class="sxs-lookup"><span data-stu-id="7c69d-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="7c69d-188">The following list is ordered by the likelihood that the change will affect your application code.</span><span class="sxs-lookup"><span data-stu-id="7c69d-188">The following list is ordered by the likelihood that the change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="7c69d-189">IndexBatch and IndexAction changes</span><span class="sxs-lookup"><span data-stu-id="7c69d-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="7c69d-190">`IndexBatch.Create` has been renamed to `IndexBatch.New` and no longer has a `params` argument.</span><span class="sxs-lookup"><span data-stu-id="7c69d-190">`IndexBatch.Create` has been renamed to `IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="7c69d-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span><span class="sxs-lookup"><span data-stu-id="7c69d-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="7c69d-192">In addition, there are new static methods for creating batches where all the actions are the same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-192">In addition, there are new static methods for creating batches where all the actions are the same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="7c69d-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span><span class="sxs-lookup"><span data-stu-id="7c69d-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="7c69d-194">You should use the new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-194">You should use the new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="7c69d-195">`IndexAction.Create` has been removed.</span><span class="sxs-lookup"><span data-stu-id="7c69d-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="7c69d-196">If you used the overload that takes only a document, make sure to use `Upload` instead.</span><span class="sxs-lookup"><span data-stu-id="7c69d-196">If you used the overload that takes only a document, make sure to use `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="7c69d-197">Example</span><span class="sxs-lookup"><span data-stu-id="7c69d-197">Example</span></span>
<span data-ttu-id="7c69d-198">If your code looks like this:</span><span class="sxs-lookup"><span data-stu-id="7c69d-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="7c69d-199">You can change it to this to fix any build errors:</span><span class="sxs-lookup"><span data-stu-id="7c69d-199">You can change it to this to fix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="7c69d-200">If you want, you can further simplify it to this:</span><span class="sxs-lookup"><span data-stu-id="7c69d-200">If you want, you can further simplify it to this:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="7c69d-201">IndexBatchException changes</span><span class="sxs-lookup"><span data-stu-id="7c69d-201">IndexBatchException changes</span></span>
<span data-ttu-id="7c69d-202">The `IndexBatchException.IndexResponse` property has been renamed to `IndexingResults`, and its type is now `IList<IndexingResult>`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-202">The `IndexBatchException.IndexResponse` property has been renamed to `IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="7c69d-203">Example</span><span class="sxs-lookup"><span data-stu-id="7c69d-203">Example</span></span>
<span data-ttu-id="7c69d-204">If your code looks like this:</span><span class="sxs-lookup"><span data-stu-id="7c69d-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="7c69d-205">You can change it to this to fix any build errors:</span><span class="sxs-lookup"><span data-stu-id="7c69d-205">You can change it to this to fix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="7c69d-206">Operation method changes</span><span class="sxs-lookup"><span data-stu-id="7c69d-206">Operation method changes</span></span>
<span data-ttu-id="7c69d-207">Each operation in the Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span><span class="sxs-lookup"><span data-stu-id="7c69d-207">Each operation in the Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="7c69d-208">The signatures and factoring of these method overloads has changed in version 1.1.</span><span class="sxs-lookup"><span data-stu-id="7c69d-208">The signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="7c69d-209">For example, the "Get Index Statistics" operation in older versions of the SDK exposed these signatures:</span><span class="sxs-lookup"><span data-stu-id="7c69d-209">For example, the "Get Index Statistics" operation in older versions of the SDK exposed these signatures:</span></span>

<span data-ttu-id="7c69d-210">In `IIndexOperations`:</span><span class="sxs-lookup"><span data-stu-id="7c69d-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="7c69d-211">In `IndexOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="7c69d-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="7c69d-212">The method signatures for the same operation in version 1.1 look like this:</span><span class="sxs-lookup"><span data-stu-id="7c69d-212">The method signatures for the same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="7c69d-213">In `IIndexesOperations`:</span><span class="sxs-lookup"><span data-stu-id="7c69d-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="7c69d-214">In `IndexesOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="7c69d-214">In `IndexesOperationsExtensions`:</span></span>

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

<span data-ttu-id="7c69d-215">Starting with version 1.1, the Azure Search .NET SDK organizes operation methods differently:</span><span class="sxs-lookup"><span data-stu-id="7c69d-215">Starting with version 1.1, the Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="7c69d-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span><span class="sxs-lookup"><span data-stu-id="7c69d-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="7c69d-217">This reduces the number of method overloads, sometimes dramatically.</span><span class="sxs-lookup"><span data-stu-id="7c69d-217">This reduces the number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="7c69d-218">The extension methods now hide a lot of the extraneous details of HTTP from the caller.</span><span class="sxs-lookup"><span data-stu-id="7c69d-218">The extension methods now hide a lot of the extraneous details of HTTP from the caller.</span></span> <span data-ttu-id="7c69d-219">For example, older versions of the SDK returned a response object with an HTTP status code, which you often didn't need to check because operation methods throw `CloudException` for any status code that indicates an error.</span><span class="sxs-lookup"><span data-stu-id="7c69d-219">For example, older versions of the SDK returned a response object with an HTTP status code, which you often didn't need to check because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="7c69d-220">The new extension methods just return model objects, saving you the trouble of having to unwrap them in your code.</span><span class="sxs-lookup"><span data-stu-id="7c69d-220">The new extension methods just return model objects, saving you the trouble of having to unwrap them in your code.</span></span>
* <span data-ttu-id="7c69d-221">Conversely, the core interfaces now expose methods that give you more control at the HTTP level if you need it.</span><span class="sxs-lookup"><span data-stu-id="7c69d-221">Conversely, the core interfaces now expose methods that give you more control at the HTTP level if you need it.</span></span> <span data-ttu-id="7c69d-222">You can now pass in custom HTTP headers to be included in requests, and the new `AzureOperationResponse<T>` return type gives you direct access to the `HttpRequestMessage` and `HttpResponseMessage` for the operation.</span><span class="sxs-lookup"><span data-stu-id="7c69d-222">You can now pass in custom HTTP headers to be included in requests, and the new `AzureOperationResponse<T>` return type gives you direct access to the `HttpRequestMessage` and `HttpResponseMessage` for the operation.</span></span> <span data-ttu-id="7c69d-223">`AzureOperationResponse` is defined in the `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-223">`AzureOperationResponse` is defined in the `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="7c69d-224">ScoringParameters changes</span><span class="sxs-lookup"><span data-stu-id="7c69d-224">ScoringParameters changes</span></span>
<span data-ttu-id="7c69d-225">A new class named `ScoringParameter` has been added in the latest SDK to make it easier to provide parameters to scoring profiles in a search query.</span><span class="sxs-lookup"><span data-stu-id="7c69d-225">A new class named `ScoringParameter` has been added in the latest SDK to make it easier to provide parameters to scoring profiles in a search query.</span></span> <span data-ttu-id="7c69d-226">Previously the `ScoringProfiles` property of the `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-226">Previously the `ScoringProfiles` property of the `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="7c69d-227">Example</span><span class="sxs-lookup"><span data-stu-id="7c69d-227">Example</span></span>
<span data-ttu-id="7c69d-228">If your code looks like this:</span><span class="sxs-lookup"><span data-stu-id="7c69d-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="7c69d-229">You can change it to this to fix any build errors:</span><span class="sxs-lookup"><span data-stu-id="7c69d-229">You can change it to this to fix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="7c69d-230">Model class changes</span><span class="sxs-lookup"><span data-stu-id="7c69d-230">Model class changes</span></span>
<span data-ttu-id="7c69d-231">Due to the signature changes described in [Operation method changes](#OperationMethodChanges), many classes in the `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span><span class="sxs-lookup"><span data-stu-id="7c69d-231">Due to the signature changes described in [Operation method changes](#OperationMethodChanges), many classes in the `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="7c69d-232">For example:</span><span class="sxs-lookup"><span data-stu-id="7c69d-232">For example:</span></span>

* <span data-ttu-id="7c69d-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span><span class="sxs-lookup"><span data-stu-id="7c69d-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="7c69d-234">`DocumentSearchResponse` has been renamed to `DocumentSearchResult`</span><span class="sxs-lookup"><span data-stu-id="7c69d-234">`DocumentSearchResponse` has been renamed to `DocumentSearchResult`</span></span>
* <span data-ttu-id="7c69d-235">`IndexResult` has been renamed to `IndexingResult`</span><span class="sxs-lookup"><span data-stu-id="7c69d-235">`IndexResult` has been renamed to `IndexingResult`</span></span>
* <span data-ttu-id="7c69d-236">`Documents.Count()` now returns a `long` with the document count instead of a `DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="7c69d-236">`Documents.Count()` now returns a `long` with the document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="7c69d-237">`IndexGetStatisticsResponse` has been renamed to `IndexGetStatisticsResult`</span><span class="sxs-lookup"><span data-stu-id="7c69d-237">`IndexGetStatisticsResponse` has been renamed to `IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="7c69d-238">`IndexListResponse` has been renamed to `IndexListResult`</span><span class="sxs-lookup"><span data-stu-id="7c69d-238">`IndexListResponse` has been renamed to `IndexListResult`</span></span>

<span data-ttu-id="7c69d-239">To summarize, `OperationResponse`-derived classes that existed only to wrap a model object have been removed.</span><span class="sxs-lookup"><span data-stu-id="7c69d-239">To summarize, `OperationResponse`-derived classes that existed only to wrap a model object have been removed.</span></span> <span data-ttu-id="7c69d-240">The remaining classes have had their suffix changed from `Response` to `Result`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-240">The remaining classes have had their suffix changed from `Response` to `Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="7c69d-241">Example</span><span class="sxs-lookup"><span data-stu-id="7c69d-241">Example</span></span>
<span data-ttu-id="7c69d-242">If your code looks like this:</span><span class="sxs-lookup"><span data-stu-id="7c69d-242">If your code looks like this:</span></span>

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

<span data-ttu-id="7c69d-243">You can change it to this to fix any build errors:</span><span class="sxs-lookup"><span data-stu-id="7c69d-243">You can change it to this to fix any build errors:</span></span>

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="7c69d-244">Response classes and IEnumerable</span><span class="sxs-lookup"><span data-stu-id="7c69d-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="7c69d-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="7c69d-246">Instead, you can access the collection property directly.</span><span class="sxs-lookup"><span data-stu-id="7c69d-246">Instead, you can access the collection property directly.</span></span> <span data-ttu-id="7c69d-247">For example, if your code looks like this:</span><span class="sxs-lookup"><span data-stu-id="7c69d-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="7c69d-248">You can change it to this to fix any build errors:</span><span class="sxs-lookup"><span data-stu-id="7c69d-248">You can change it to this to fix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="7c69d-249">Special case for web applications</span><span class="sxs-lookup"><span data-stu-id="7c69d-249">Special case for web applications</span></span>
<span data-ttu-id="7c69d-250">If you have a web application that serializes `DocumentSearchResponse` directly to send search results to the browser, you will need to change your code or the results will not serialize correctly.</span><span class="sxs-lookup"><span data-stu-id="7c69d-250">If you have a web application that serializes `DocumentSearchResponse` directly to send search results to the browser, you will need to change your code or the results will not serialize correctly.</span></span> <span data-ttu-id="7c69d-251">For example, if your code looks like this:</span><span class="sxs-lookup"><span data-stu-id="7c69d-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="7c69d-252">You can change it by getting the `.Results` property of the search response to fix search result rendering:</span><span class="sxs-lookup"><span data-stu-id="7c69d-252">You can change it by getting the `.Results` property of the search response to fix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="7c69d-253">You will have to look for such cases in your code yourself; **The compiler will not warn you** because `JsonResult.Data` is of type `object`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-253">You will have to look for such cases in your code yourself; **The compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="7c69d-254">CloudException changes</span><span class="sxs-lookup"><span data-stu-id="7c69d-254">CloudException changes</span></span>
<span data-ttu-id="7c69d-255">The `CloudException` class has moved from the `Hyak.Common` namespace to the `Microsoft.Rest.Azure` namespace.</span><span class="sxs-lookup"><span data-stu-id="7c69d-255">The `CloudException` class has moved from the `Hyak.Common` namespace to the `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="7c69d-256">Also, its `Error` property has been renamed to `Body`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-256">Also, its `Error` property has been renamed to `Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="7c69d-257">SearchServiceClient and SearchIndexClient changes</span><span class="sxs-lookup"><span data-stu-id="7c69d-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="7c69d-258">The type of the `Credentials` property has changed from `SearchCredentials` to its base class, `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-258">The type of the `Credentials` property has changed from `SearchCredentials` to its base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="7c69d-259">If you need to access the `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use the new `SearchCredentials` property.</span><span class="sxs-lookup"><span data-stu-id="7c69d-259">If you need to access the `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use the new `SearchCredentials` property.</span></span>

<span data-ttu-id="7c69d-260">In older versions of the SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span><span class="sxs-lookup"><span data-stu-id="7c69d-260">In older versions of the SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="7c69d-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span><span class="sxs-lookup"><span data-stu-id="7c69d-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="7c69d-262">This makes it easier to install custom handlers to pre-process HTTP requests if necessary.</span><span class="sxs-lookup"><span data-stu-id="7c69d-262">This makes it easier to install custom handlers to pre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="7c69d-263">Finally, the constructors that took a `Uri` and `SearchCredentials` have changed.</span><span class="sxs-lookup"><span data-stu-id="7c69d-263">Finally, the constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="7c69d-264">For example, if you have code that looks like this:</span><span class="sxs-lookup"><span data-stu-id="7c69d-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="7c69d-265">You can change it to this to fix any build errors:</span><span class="sxs-lookup"><span data-stu-id="7c69d-265">You can change it to this to fix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="7c69d-266">Also note that the type of the credentials parameter has changed to `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-266">Also note that the type of the credentials parameter has changed to `ServiceClientCredentials`.</span></span> <span data-ttu-id="7c69d-267">This is unlikely to affect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-267">This is unlikely to affect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="7c69d-268">Passing a request ID</span><span class="sxs-lookup"><span data-stu-id="7c69d-268">Passing a request ID</span></span>
<span data-ttu-id="7c69d-269">In older versions of the SDK, you could set a request ID on the `SearchServiceClient` or `SearchIndexClient` and it would be included in every request to the REST API.</span><span class="sxs-lookup"><span data-stu-id="7c69d-269">In older versions of the SDK, you could set a request ID on the `SearchServiceClient` or `SearchIndexClient` and it would be included in every request to the REST API.</span></span> <span data-ttu-id="7c69d-270">This is useful for troubleshooting issues with your search service if you need to contact support.</span><span class="sxs-lookup"><span data-stu-id="7c69d-270">This is useful for troubleshooting issues with your search service if you need to contact support.</span></span> <span data-ttu-id="7c69d-271">However, it is more useful to set a unique request ID for every operation rather than to use the same ID for all operations.</span><span class="sxs-lookup"><span data-stu-id="7c69d-271">However, it is more useful to set a unique request ID for every operation rather than to use the same ID for all operations.</span></span> <span data-ttu-id="7c69d-272">For this reason, the `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span><span class="sxs-lookup"><span data-stu-id="7c69d-272">For this reason, the `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="7c69d-273">Instead, you can pass a request ID to each operation method via the optional `SearchRequestOptions` parameter.</span><span class="sxs-lookup"><span data-stu-id="7c69d-273">Instead, you can pass a request ID to each operation method via the optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="7c69d-274">In a future release of the SDK, we will add a new mechanism for setting a request ID globally on the client objects that is consistent with the approach used by other Azure SDKs.</span><span class="sxs-lookup"><span data-stu-id="7c69d-274">In a future release of the SDK, we will add a new mechanism for setting a request ID globally on the client objects that is consistent with the approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="7c69d-275">Example</span><span class="sxs-lookup"><span data-stu-id="7c69d-275">Example</span></span>
<span data-ttu-id="7c69d-276">If you have code that looks like this:</span><span class="sxs-lookup"><span data-stu-id="7c69d-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="7c69d-277">You can change it to this to fix any build errors:</span><span class="sxs-lookup"><span data-stu-id="7c69d-277">You can change it to this to fix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="7c69d-278">Interface name changes</span><span class="sxs-lookup"><span data-stu-id="7c69d-278">Interface name changes</span></span>
<span data-ttu-id="7c69d-279">The operation group interface names have all changed to be consistent with their corresponding property names:</span><span class="sxs-lookup"><span data-stu-id="7c69d-279">The operation group interface names have all changed to be consistent with their corresponding property names:</span></span>

* <span data-ttu-id="7c69d-280">The type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` to `IIndexesOperations`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-280">The type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` to `IIndexesOperations`.</span></span>
* <span data-ttu-id="7c69d-281">The type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` to `IIndexersOperations`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-281">The type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` to `IIndexersOperations`.</span></span>
* <span data-ttu-id="7c69d-282">The type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` to `IDataSourcesOperations`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-282">The type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` to `IDataSourcesOperations`.</span></span>
* <span data-ttu-id="7c69d-283">The type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` to `IDocumentsOperations`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-283">The type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` to `IDocumentsOperations`.</span></span>

<span data-ttu-id="7c69d-284">This change is unlikely to affect your code unless you created mocks of these interfaces for test purposes.</span><span class="sxs-lookup"><span data-stu-id="7c69d-284">This change is unlikely to affect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="7c69d-285">Bug fixes in version 1.1</span><span class="sxs-lookup"><span data-stu-id="7c69d-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="7c69d-286">There was a bug in older versions of the Azure Search .NET SDK relating to serialization of custom model classes.</span><span class="sxs-lookup"><span data-stu-id="7c69d-286">There was a bug in older versions of the Azure Search .NET SDK relating to serialization of custom model classes.</span></span> <span data-ttu-id="7c69d-287">The bug could occur if you created a custom model class with a property of a non-nullable value type.</span><span class="sxs-lookup"><span data-stu-id="7c69d-287">The bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-to-reproduce"></a><span data-ttu-id="7c69d-288">Steps to reproduce</span><span class="sxs-lookup"><span data-stu-id="7c69d-288">Steps to reproduce</span></span>
<span data-ttu-id="7c69d-289">Create a custom model class with a property of non-nullable value type.</span><span class="sxs-lookup"><span data-stu-id="7c69d-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="7c69d-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="7c69d-291">If you index a document with the default value of that type (for example, 0 for `int`), the field will be null in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="7c69d-291">If you index a document with the default value of that type (for example, 0 for `int`), the field will be null in Azure Search.</span></span> <span data-ttu-id="7c69d-292">If you subsequently search for that document, the `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` to `int`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-292">If you subsequently search for that document, the `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` to `int`.</span></span>

<span data-ttu-id="7c69d-293">Also, filters may not work as expected since null was written to the index instead of the intended value.</span><span class="sxs-lookup"><span data-stu-id="7c69d-293">Also, filters may not work as expected since null was written to the index instead of the intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="7c69d-294">Fix details</span><span class="sxs-lookup"><span data-stu-id="7c69d-294">Fix details</span></span>
<span data-ttu-id="7c69d-295">We have fixed this issue in version 1.1 of the SDK.</span><span class="sxs-lookup"><span data-stu-id="7c69d-295">We have fixed this issue in version 1.1 of the SDK.</span></span> <span data-ttu-id="7c69d-296">Now, if you have a model class like this:</span><span class="sxs-lookup"><span data-stu-id="7c69d-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="7c69d-297">and you set `IntValue` to 0, that value is now correctly serialized as 0 on the wire and stored as 0 in the index.</span><span class="sxs-lookup"><span data-stu-id="7c69d-297">and you set `IntValue` to 0, that value is now correctly serialized as 0 on the wire and stored as 0 in the index.</span></span> <span data-ttu-id="7c69d-298">Round tripping also works as expected.</span><span class="sxs-lookup"><span data-stu-id="7c69d-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="7c69d-299">There is one potential issue to be aware of with this approach: If you use a model type with a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span><span class="sxs-lookup"><span data-stu-id="7c69d-299">There is one potential issue to be aware of with this approach: If you use a model type with a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="7c69d-300">Neither the SDK nor the Azure Search REST API will help you to enforce this.</span><span class="sxs-lookup"><span data-stu-id="7c69d-300">Neither the SDK nor the Azure Search REST API will help you to enforce this.</span></span>

<span data-ttu-id="7c69d-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="7c69d-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="7c69d-302">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span><span class="sxs-lookup"><span data-stu-id="7c69d-302">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="7c69d-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span><span class="sxs-lookup"><span data-stu-id="7c69d-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="7c69d-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span><span class="sxs-lookup"><span data-stu-id="7c69d-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="7c69d-305">For more details on this bug and the fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span><span class="sxs-lookup"><span data-stu-id="7c69d-305">For more details on this bug and the fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

