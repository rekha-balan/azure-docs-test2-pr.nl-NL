---
title: Entity search API C# quickstart | Microsoft Docs
description: Setup for Entity search SDK console application.
titleSuffix: Azure cognitive services entity search API C# quickstart
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-entity-search
ms.topic: article
ms.date: 01/30/2018
ms.author: v-gedod
ms.openlocfilehash: 185e1b4fc1b7ef2aa5964e2e95314727f8e1b0a5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857053"
---
# <a name="entity-search-sdk-c-quickstart"></a><span data-ttu-id="6d1b9-103">Entity Search SDK C# quickstart</span><span class="sxs-lookup"><span data-stu-id="6d1b9-103">Entity Search SDK C# quickstart</span></span>

<span data-ttu-id="6d1b9-104">The Bing Entity Search API contains the functionality of the REST API for entity search and parsing the results.</span><span class="sxs-lookup"><span data-stu-id="6d1b9-104">The Bing Entity Search API contains the functionality of the REST API for entity search and parsing the results.</span></span>

<span data-ttu-id="6d1b9-105">The [source code for C# Bing Entity Search SDK samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7/BingEntitySearch) is available on Git Hub.</span><span class="sxs-lookup"><span data-stu-id="6d1b9-105">The [source code for C# Bing Entity Search SDK samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7/BingEntitySearch) is available on Git Hub.</span></span>

## <a name="application-dependencies"></a><span data-ttu-id="6d1b9-106">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="6d1b9-106">Application dependencies</span></span>

<span data-ttu-id="6d1b9-107">To set up a console application using the Bing Entity Search SDK, browse to the `Manage NuGet Packages` option from the Solution Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6d1b9-107">To set up a console application using the Bing Entity Search SDK, browse to the `Manage NuGet Packages` option from the Solution Explorer in Visual Studio.</span></span>  <span data-ttu-id="6d1b9-108">Add the `Microsoft.Azure.CognitiveServices.Search.EntitySearch` package.</span><span class="sxs-lookup"><span data-stu-id="6d1b9-108">Add the `Microsoft.Azure.CognitiveServices.Search.EntitySearch` package.</span></span>

<span data-ttu-id="6d1b9-109">Installing the [NuGet Entity Search package](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.EntitySearch/1.2.0) will also install dependencies, including the following assemblies:</span><span class="sxs-lookup"><span data-stu-id="6d1b9-109">Installing the [NuGet Entity Search package](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.EntitySearch/1.2.0) will also install dependencies, including the following assemblies:</span></span>
* <span data-ttu-id="6d1b9-110">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="6d1b9-110">Microsoft.Rest.ClientRuntime</span></span>
* <span data-ttu-id="6d1b9-111">Microsoft.Rest.ClientRuntime.Azure</span><span class="sxs-lookup"><span data-stu-id="6d1b9-111">Microsoft.Rest.ClientRuntime.Azure</span></span>
* <span data-ttu-id="6d1b9-112">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="6d1b9-112">Newtonsoft.Json</span></span>

## <a name="entity-search-client"></a><span data-ttu-id="6d1b9-113">Entity Search client</span><span class="sxs-lookup"><span data-stu-id="6d1b9-113">Entity Search client</span></span>
<span data-ttu-id="6d1b9-114">To create an instance of the `EntitySearchAPI` client, add using directives:</span><span class="sxs-lookup"><span data-stu-id="6d1b9-114">To create an instance of the `EntitySearchAPI` client, add using directives:</span></span>
```
using Microsoft.Azure.CognitiveServices.Search.EntitySearch;
using Microsoft.Azure.CognitiveServices.Search.EntitySearch.Models;

```
<span data-ttu-id="6d1b9-115">Then, instantiate the client:</span><span class="sxs-lookup"><span data-stu-id="6d1b9-115">Then, instantiate the client:</span></span>
```
var client = new EntitySearchAPI(new ApiKeyServiceClientCredentials("YOUR-ACCESS-KEY"));


```
<span data-ttu-id="6d1b9-116">Use the client to search with a query text:</span><span class="sxs-lookup"><span data-stu-id="6d1b9-116">Use the client to search with a query text:</span></span>
```
var entityData = client.Entities.Search(query: "Satya Nadella");

```
<span data-ttu-id="6d1b9-117">Parse the results of previous query:</span><span class="sxs-lookup"><span data-stu-id="6d1b9-117">Parse the results of previous query:</span></span>
```
if (entityData?.Entities?.Value?.Count > 0)
{
    // find the entity that represents the dominant one
    var mainEntity = entityData.Entities.Value.Where(thing => thing.EntityPresentationInfo.EntityScenario == EntityScenario.DominantEntity).FirstOrDefault();

    if (mainEntity != null)
    {
        Console.WriteLine("Searched for \"Satya Nadella\" and found a dominant entity with this description:");
        Console.WriteLine(mainEntity.Description);
    }
    else
    {
        Console.WriteLine("Couldn't find main entity Satya Nadella!");
    }
}
else
{
    Console.WriteLine("Didn't see any data..");
}

```

## <a name="complete-console-application"></a><span data-ttu-id="6d1b9-118">Complete console application</span><span class="sxs-lookup"><span data-stu-id="6d1b9-118">Complete console application</span></span>
<span data-ttu-id="6d1b9-119">The following console application looks up a single entity on query "Satya Nadella" and prints out a short description.</span><span class="sxs-lookup"><span data-stu-id="6d1b9-119">The following console application looks up a single entity on query "Satya Nadella" and prints out a short description.</span></span>
```
using System;
using System.Linq;
using System.Text;
using Microsoft.Azure.CognitiveServices.Search.EntitySearch;
using Microsoft.Azure.CognitiveServices.Search.EntitySearch.Models;
using Newtonsoft.Json;

namespace EntitySrchSDK
{
    class Program
    {
        static void Main(string[] args)
        {
            var client = new EntitySearchAPI(new ApiKeyServiceClientCredentials("19aa718a79d6444daaa415981d9f54ad"));

            DominantEntityLookup(client);
            
            // Include the following methods to use queries defined under the headings following this example.
            //HandlingDisambiguation(client);
            //RestaurantLookup(client);
            //MultipleRestaurantLookup(client);
            //Error(client);

            Console.WriteLine("Any key to exit...");
            Console.ReadKey();
        }

        public static void DominantEntityLookup(EntitySearchAPI client)
        {
            try
            {
                var entityData = client.Entities.Search(query: "Satya Nadella");

                if (entityData?.Entities?.Value?.Count > 0)
                {
                    // find the entity that represents the dominant one
                    var mainEntity = entityData.Entities.Value.Where(thing => thing.EntityPresentationInfo.EntityScenario == EntityScenario.DominantEntity).FirstOrDefault();

                    if (mainEntity != null)
                    {
                        Console.WriteLine("Searched for \"Satya Nadella\" and found a dominant entity with this description:");
                        Console.WriteLine(mainEntity.Description);
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find main entity Satya Nadella!");
                    }
                }
                else
                {
                    Console.WriteLine("Didn't see any data..");
                }
            }
            catch (ErrorResponseException ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }
        }
    }
}

```

## <a name="ambiguous-results"></a><span data-ttu-id="6d1b9-120">Ambiguous results</span><span class="sxs-lookup"><span data-stu-id="6d1b9-120">Ambiguous results</span></span>
<span data-ttu-id="6d1b9-121">The following code handles disambiguation of results for an ambiguous query "William Gates".</span><span class="sxs-lookup"><span data-stu-id="6d1b9-121">The following code handles disambiguation of results for an ambiguous query "William Gates".</span></span>
```
       public static void HandlingDisambiguation(EntitySearchAPI client)
        {
            try
            {
                var entityData = client.Entities.Search(query: "william gates");

                if (entityData?.Entities?.Value?.Count > 0)
                {
                    // find the entity that represents the dominant one
                    var mainEntity = entityData.Entities.Value.Where(thing => thing.EntityPresentationInfo.EntityScenario == EntityScenario.DominantEntity).FirstOrDefault();
                    var disambigEntities = entityData.Entities.Value.Where(thing => thing.EntityPresentationInfo.EntityScenario == EntityScenario.DisambiguationItem).ToList();

                    if (mainEntity != null)
                    {
                        Console.WriteLine("Searched for \"William Gates\" and found a dominant entity with type hint \"{0}\" with this description:", mainEntity.EntityPresentationInfo.EntityTypeDisplayHint);
                        Console.WriteLine(mainEntity.Description);
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find a reliable dominant entity for William Gates!");
                    }

                    if (disambigEntities?.Count > 0)
                    {
                        Console.WriteLine();
                        Console.WriteLine("This query is pretty ambiguous and can be referring to multiple things. Did you mean one of these: ");

                        var sb = new StringBuilder();

                        foreach (var disambig in disambigEntities)
                        {
                            sb.AppendFormat(", or {0} the {1}", disambig.Name, disambig.EntityPresentationInfo.EntityTypeDisplayHint);
                        }

                        Console.WriteLine(sb.ToString().Substring(5) + "?");
                    }
                    else
                    {
                        Console.WriteLine("We didn't find any disambiguation items for William Gates, so we must be certain what you're talking about!");
                    }
                }
                else
                {
                    Console.WriteLine("Didn't see any data..");
                }
            }
            catch (ErrorResponseException ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }
        }

```

## <a name="entitydata-places"></a><span data-ttu-id="6d1b9-122">EntityData places</span><span class="sxs-lookup"><span data-stu-id="6d1b9-122">EntityData places</span></span>
<span data-ttu-id="6d1b9-123">The following code looks up a single store "Microsoft Store" and prints out its phone number.</span><span class="sxs-lookup"><span data-stu-id="6d1b9-123">The following code looks up a single store "Microsoft Store" and prints out its phone number.</span></span>
```
        public static void StoreLookup(EntitySearchAPI client)
        {
            try
            {
                var entityData = client.Entities.Search(query: "microsoft store");

                if (entityData?.Places?.Value?.Count > 0)
                {
                    // Some local entities will be places, others won't be. Depending on the data you want, try to cast to the appropriate schema.
                    // In this case, the item being returned is technically a store, but the Place schema has the data we want (telephone)
                    var store = entityData.Places.Value.FirstOrDefault() as Place;

                    if (store != null)
                    {
                        Console.WriteLine("Searched for \"Microsoft Store\" and found a store with this phone number:");
                        Console.WriteLine(store.Telephone);
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find a place!");
                    }
                }
                else
                {
                    Console.WriteLine("Didn't see any data..");
                }
            }
            catch (ErrorResponseException ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }
        }

```
## <a name="entityscenario-list"></a><span data-ttu-id="6d1b9-124">EntityScenario list</span><span class="sxs-lookup"><span data-stu-id="6d1b9-124">EntityScenario list</span></span>
<span data-ttu-id="6d1b9-125">The following code looks up a list of "Seattle restaurants" and prints their names and phone numbers.</span><span class="sxs-lookup"><span data-stu-id="6d1b9-125">The following code looks up a list of "Seattle restaurants" and prints their names and phone numbers.</span></span>
```
       public static void MultipleRestaurantLookup(EntitySearchAPI client)
        {
            try
            {
                var restaurants = client.Entities.Search(query: "seattle restaurants");

                if (restaurants?.Places?.Value?.Count > 0)
                {
                    // get all the list items that relate to this query
                    var listItems = restaurants.Places.Value.Where(thing => thing.EntityPresentationInfo.EntityScenario == EntityScenario.ListItem).ToList();

                    if (listItems?.Count > 0)
                    {
                        var sb = new StringBuilder();

                        foreach (var item in listItems)
                        {
                            var place = item as Place;

                            if (place == null)
                            {
                                Console.WriteLine("Unexpectedly found something that isn't a place named \"{0}\"", item.Name);
                                continue;
                            }

                            sb.AppendFormat(",{0} ({1}) ", place.Name, place.Telephone);
                        }

                        Console.WriteLine("Ok, we found these places: ");
                        Console.WriteLine(sb.ToString().Substring(1));
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find any relevant results for \"seattle restaurants\"");
                    }
                }
                else
                {
                    Console.WriteLine("Didn't see any data..");
                }
            }
            catch (ErrorResponseException ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }
        }

```
## <a name="error-results"></a><span data-ttu-id="6d1b9-126">Error results</span><span class="sxs-lookup"><span data-stu-id="6d1b9-126">Error results</span></span>
<span data-ttu-id="6d1b9-127">The following code triggers a bad request and shows how to read the error response.</span><span class="sxs-lookup"><span data-stu-id="6d1b9-127">The following code triggers a bad request and shows how to read the error response.</span></span>
```
        public static void Error(EntitySearchAPI client)
        {
            try
            {
                var entityData = client.Entities.Search(query: "satya nadella", market: "no-ty");
            }
            catch (ErrorResponseException ex)
            {
                // The status code of the error should be a good indication of what occurred. However, if you'd like more details, you can dig into the response.
                // Please note that depending on the type of error, the response schema might be different, so you aren't guaranteed a specific error response schema.
                Console.WriteLine("Exception occurred, status code {0} with reason {1}.", ex.Response.StatusCode, ex.Response.ReasonPhrase);

                // if you'd like more descriptive information (if available), attempt to parse the content as an ErrorResponse
                var issue = JsonConvert.DeserializeObject<ErrorResponse>(ex.Response.Content);

                if (issue != null && issue.Errors?.Count > 0)
                {
                    if (issue.Errors[0].SubCode == ErrorSubCode.ParameterInvalidValue)
                    {
                        Console.WriteLine("Turns out the issue is parameter \"{0}\" has an invalid value \"{1}\". Detailed message is \"{2}\"", issue.Errors[0].Parameter, issue.Errors[0].Value, issue.Errors[0].Message);
                    }
                }
            }
        }

```
## <a name="next-steps"></a><span data-ttu-id="6d1b9-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="6d1b9-128">Next steps</span></span>

[<span data-ttu-id="6d1b9-129">Cognitive services .NET SDK samples</span><span class="sxs-lookup"><span data-stu-id="6d1b9-129">Cognitive services .NET SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7)