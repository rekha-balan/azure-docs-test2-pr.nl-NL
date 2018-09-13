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
# <a name="upgrading-to-the-azure-search-net-sdk-version-3"></a>Upgrading to the Azure Search .NET SDK version 3
If you're using version 2.0-preview or older of the [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application to use version 3.

For a more general walkthrough of the SDK including examples, see [How to use Azure Search from a .NET Application](search-howto-dotnet-sdk.md).

Version 3 of the Azure Search .NET SDK contains some changes from earlier versions. These are mostly minor, so changing your code should require only minimal effort. See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new SDK version.

> [!NOTE]
> If you're using version 1.0.2-preview or older, you should upgrade to version 1.1 first, and then upgrade to version 3. See [Appendix: Steps to upgrade to version 1.1](#UpgradeStepsV1) for instructions.
>
> Your Azure Search service instance supports several REST API versions, including the latest one. You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version. When using the REST API, you must specify the API version in every request via the api-version parameter. When using the .NET SDK, the version of the SDK you’re using determines the corresponding version of the REST API. If you are using an older SDK, you can continue to run that code with no changes even if the service is upgraded to support a newer API version.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a>What's new in version 3
Version 3 of the Azure Search .NET SDK targets the latest generally available version of the Azure Search REST API, specifically 2016-09-01. This makes it possible to use many new features of Azure Search from a .NET application, including the following:

* [Custom analyzers](https://aka.ms/customanalyzers)
* [Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support
* Indexer customization via [field mappings](search-indexer-field-mappings.md)
* ETags support to enable safe concurrent updating of index definitions, indexers, and data sources
* Support for building index field definitions declaratively by decorating your model class and using the new `FieldBuilder` class.
* Support for .NET Core and .NET Portable Profile 111

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a>Steps to upgrade
First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.

Once NuGet has downloaded the new packages and their dependencies, rebuild your project. Depending on how your code is structured, it may rebuild successfully. If so, you're ready to go!

If your build fails, you should see a build error like the following:

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' to 'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

The next step is to fix this build error. See [Breaking changes in version 3](#ListOfChanges) for details on what causes the error and how to fix it.

You may see additional build warnings related to obsolete methods or properties. The warnings will include instructions on what to use instead of the deprecated feature. For example, if your application uses the `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`

Once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish. New features in the SDK are detailed in [What's new in version 3](#WhatsNew).

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a>Breaking changes in version 3
There a small number of breaking changes in version 3 that may require code changes in addition to rebuilding your application.

### <a name="indexesgetclient-return-type"></a>Indexes.GetClient return type
The `Indexes.GetClient` method has a new return type. Previously, it returned `SearchIndexClient`, but this was changed to `ISearchIndexClient` in version 2.0-preview, and that change carries over to version 3. This is to support customers that wish to mock the `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.

#### <a name="example"></a>Example
If your code looks like this:

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

You can change it to this to fix any build errors:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-to-strings"></a>AnalyzerName, DataType, and others are no longer implicitly convertible to strings
There are many types in the Azure Search .NET SDK that derive from `ExtensibleEnum`. Previously these types were all implicitly convertible to type `string`. However, a bug was discovered in the `Object.Equals` implementation for these classes, and fixing the bug required disabling this implicit conversion. Explicit conversion to `string` is still allowed.

#### <a name="example"></a>Example
If your code looks like this:

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

You can change it to this to fix any build errors:

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

### <a name="removed-obsolete-members"></a>Removed obsolete members

You may see build errors related to methods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3. If you encounter such errors, here is how to resolve them:

- If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`
- If you were using the `ScoringParameter.Value` property, use the `ScoringParameter.Values` property or the `ToString` method instead.
- If you were using the `SearchRequestOptions.RequestId` property, use the `ClientRequestId` property instead.

### <a name="removed-preview-features"></a>Removed preview features

If you are upgrading from version 2.0-preview to version 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview. Specifically, the following methods of the `IndexingParametersExtensions` class have been removed:

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

If your application has a hard dependency on these features, you will not be able to upgrade to version 3 of the Azure Search .NET SDK. You can continue to use version 2.0-preview. However, please keep in mind that **we do not recommend using preview SDKs in production applications**. Preview features are for evaluation only and may change.

## <a name="conclusion"></a>Conclusion
If you need more details on using the Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).

We welcome your feedback on the SDK. If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch). If you find a bug, you can file an issue in the [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues). Make sure to prefix your issue title with "Search SDK: ".

Thank you for using Azure Search!

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-to-upgrade-to-version-11"></a>Appendix: Steps to upgrade to version 1.1
> [!NOTE]
> This section applies only to users of the Azure Search .NET SDK version 1.0.2-preview and older.
> 
> 

First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.

Once NuGet has downloaded the new packages and their dependencies, rebuild your project.

If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, the build should succeed and you're ready to go!

If you were previously using version 0.13.0-preview or older, you should see build errors like the following:

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: The type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

The next step is to fix the build errors one by one. Most will require changing some class and method names that have been renamed in the SDK. [List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.

If you're using custom classes to model your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in the 1.1 version of the SDK of which you should be aware. See [Bug fixes in version 1.1](#BugFixesV1) for more details.

Finally, once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a>List of breaking changes in version 1.1
The following list is ordered by the likelihood that the change will affect your application code.

#### <a name="indexbatch-and-indexaction-changes"></a>IndexBatch and IndexAction changes
`IndexBatch.Create` has been renamed to `IndexBatch.New` and no longer has a `params` argument. You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.). In addition, there are new static methods for creating batches where all the actions are the same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.

`IndexAction` no longer has public constructors and its properties are now immutable. You should use the new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`. `IndexAction.Create` has been removed. If you used the overload that takes only a document, make sure to use `Upload` instead.

##### <a name="example"></a>Example
If your code looks like this:

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

You can change it to this to fix any build errors:

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

If you want, you can further simplify it to this:

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a>IndexBatchException changes
The `IndexBatchException.IndexResponse` property has been renamed to `IndexingResults`, and its type is now `IList<IndexingResult>`.

##### <a name="example"></a>Example
If your code looks like this:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

You can change it to this to fix any build errors:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a>Operation method changes
Each operation in the Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers. The signatures and factoring of these method overloads has changed in version 1.1.

For example, the "Get Index Statistics" operation in older versions of the SDK exposed these signatures:

In `IIndexOperations`:

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

In `IndexOperationsExtensions`:

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

The method signatures for the same operation in version 1.1 look like this:

In `IIndexesOperations`:

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

In `IndexesOperationsExtensions`:

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

Starting with version 1.1, the Azure Search .NET SDK organizes operation methods differently:

* Optional parameters are now modeled as default parameters rather than additional method overloads. This reduces the number of method overloads, sometimes dramatically.
* The extension methods now hide a lot of the extraneous details of HTTP from the caller. For example, older versions of the SDK returned a response object with an HTTP status code, which you often didn't need to check because operation methods throw `CloudException` for any status code that indicates an error. The new extension methods just return model objects, saving you the trouble of having to unwrap them in your code.
* Conversely, the core interfaces now expose methods that give you more control at the HTTP level if you need it. You can now pass in custom HTTP headers to be included in requests, and the new `AzureOperationResponse<T>` return type gives you direct access to the `HttpRequestMessage` and `HttpResponseMessage` for the operation. `AzureOperationResponse` is defined in the `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.

#### <a name="scoringparameters-changes"></a>ScoringParameters changes
A new class named `ScoringParameter` has been added in the latest SDK to make it easier to provide parameters to scoring profiles in a search query. Previously the `ScoringProfiles` property of the `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.

##### <a name="example"></a>Example
If your code looks like this:

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

You can change it to this to fix any build errors: 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a>Model class changes
Due to the signature changes described in [Operation method changes](#OperationMethodChanges), many classes in the `Microsoft.Azure.Search.Models` namespace have been renamed or removed. For example:

* `IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`
* `DocumentSearchResponse` has been renamed to `DocumentSearchResult`
* `IndexResult` has been renamed to `IndexingResult`
* `Documents.Count()` now returns a `long` with the document count instead of a `DocumentCountResponse`
* `IndexGetStatisticsResponse` has been renamed to `IndexGetStatisticsResult`
* `IndexListResponse` has been renamed to `IndexListResult`

To summarize, `OperationResponse`-derived classes that existed only to wrap a model object have been removed. The remaining classes have had their suffix changed from `Response` to `Result`.

##### <a name="example"></a>Example
If your code looks like this:

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

You can change it to this to fix any build errors:

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

##### <a name="response-classes-and-ienumerable"></a>Response classes and IEnumerable
An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`. Instead, you can access the collection property directly. For example, if your code looks like this:

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

You can change it to this to fix any build errors:

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a>Special case for web applications
If you have a web application that serializes `DocumentSearchResponse` directly to send search results to the browser, you will need to change your code or the results will not serialize correctly. For example, if your code looks like this:

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

You can change it by getting the `.Results` property of the search response to fix search result rendering:

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

You will have to look for such cases in your code yourself; **The compiler will not warn you** because `JsonResult.Data` is of type `object`.

#### <a name="cloudexception-changes"></a>CloudException changes
The `CloudException` class has moved from the `Hyak.Common` namespace to the `Microsoft.Rest.Azure` namespace. Also, its `Error` property has been renamed to `Body`.

#### <a name="searchserviceclient-and-searchindexclient-changes"></a>SearchServiceClient and SearchIndexClient changes
The type of the `Credentials` property has changed from `SearchCredentials` to its base class, `ServiceClientCredentials`. If you need to access the `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use the new `SearchCredentials` property.

In older versions of the SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter. These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects. This makes it easier to install custom handlers to pre-process HTTP requests if necessary.

Finally, the constructors that took a `Uri` and `SearchCredentials` have changed. For example, if you have code that looks like this:

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

You can change it to this to fix any build errors:

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

Also note that the type of the credentials parameter has changed to `ServiceClientCredentials`. This is unlikely to affect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.

#### <a name="passing-a-request-id"></a>Passing a request ID
In older versions of the SDK, you could set a request ID on the `SearchServiceClient` or `SearchIndexClient` and it would be included in every request to the REST API. This is useful for troubleshooting issues with your search service if you need to contact support. However, it is more useful to set a unique request ID for every operation rather than to use the same ID for all operations. For this reason, the `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed. Instead, you can pass a request ID to each operation method via the optional `SearchRequestOptions` parameter.

> [!NOTE]
> In a future release of the SDK, we will add a new mechanism for setting a request ID globally on the client objects that is consistent with the approach used by other Azure SDKs.
> 
> 

#### <a name="example"></a>Example
If you have code that looks like this:

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

You can change it to this to fix any build errors:

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a>Interface name changes
The operation group interface names have all changed to be consistent with their corresponding property names:

* The type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` to `IIndexesOperations`.
* The type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` to `IIndexersOperations`.
* The type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` to `IDataSourcesOperations`.
* The type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` to `IDocumentsOperations`.

This change is unlikely to affect your code unless you created mocks of these interfaces for test purposes.

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a>Bug fixes in version 1.1
There was a bug in older versions of the Azure Search .NET SDK relating to serialization of custom model classes. The bug could occur if you created a custom model class with a property of a non-nullable value type.

#### <a name="steps-to-reproduce"></a>Steps to reproduce
Create a custom model class with a property of non-nullable value type. For example, add a public `UnitCount` property of type `int` instead of `int?`.

If you index a document with the default value of that type (for example, 0 for `int`), the field will be null in Azure Search. If you subsequently search for that document, the `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` to `int`.

Also, filters may not work as expected since null was written to the index instead of the intended value.

#### <a name="fix-details"></a>Fix details
We have fixed this issue in version 1.1 of the SDK. Now, if you have a model class like this:

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

and you set `IntValue` to 0, that value is now correctly serialized as 0 on the wire and stored as 0 in the index. Round tripping also works as expected.

There is one potential issue to be aware of with this approach: If you use a model type with a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field. Neither the SDK nor the Azure Search REST API will help you to enforce this.

This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`. After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search). If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

For this reason, we still recommend that you use nullable types in your model classes as a best practice.

For more details on this bug and the fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).

