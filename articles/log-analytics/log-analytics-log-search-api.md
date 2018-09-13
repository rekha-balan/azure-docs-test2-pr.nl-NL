---
title: Log Analytics log search REST API | Microsoft Docs
description: This guide provides a basic tutorial describing how you can use the Log Analytics search REST API in the Operations Management Suite (OMS) and it provides examples that show you how to use the commands.
services: log-analytics
documentationcenter: ''
author: bandersmsft
manager: carmonm
editor: ''
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: b6c96728a23ee66e10e7a4cd76c582ce658ada44
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551337"
---
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="7d314-103">Log Analytics log search REST API</span><span class="sxs-lookup"><span data-stu-id="7d314-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="7d314-104">This guide provides a basic tutorial, including examples, of how you can use the Log Analytics Search REST API.</span><span class="sxs-lookup"><span data-stu-id="7d314-104">This guide provides a basic tutorial, including examples, of how you can use the Log Analytics Search REST API.</span></span> <span data-ttu-id="7d314-105">Log Analytics is part of the Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="7d314-105">Log Analytics is part of the Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="7d314-106">Log Analytics was previously called Operational Insights, which is why it is the name used in the resource provider.</span><span class="sxs-lookup"><span data-stu-id="7d314-106">Log Analytics was previously called Operational Insights, which is why it is the name used in the resource provider.</span></span>
>
>

## <a name="overview-of-the-log-search-rest-api"></a><span data-ttu-id="7d314-107">Overview of the Log Search REST API</span><span class="sxs-lookup"><span data-stu-id="7d314-107">Overview of the Log Search REST API</span></span>
<span data-ttu-id="7d314-108">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager API.</span><span class="sxs-lookup"><span data-stu-id="7d314-108">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager API.</span></span> <span data-ttu-id="7d314-109">This article provides examples of accessing the API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking the Azure Resource Manager API.</span><span class="sxs-lookup"><span data-stu-id="7d314-109">This article provides examples of accessing the API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="7d314-110">The use of ARMClient is one of many options to access the Log Analytics Search API.</span><span class="sxs-lookup"><span data-stu-id="7d314-110">The use of ARMClient is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="7d314-111">Another option is to use the Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span><span class="sxs-lookup"><span data-stu-id="7d314-111">Another option is to use the Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="7d314-112">With these tools, you can utilize the Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span><span class="sxs-lookup"><span data-stu-id="7d314-112">With these tools, you can utilize the Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="7d314-113">The API outputs search results in JSON format, allowing you to use the search results in many different ways programmatically.</span><span class="sxs-lookup"><span data-stu-id="7d314-113">The API outputs search results in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

<span data-ttu-id="7d314-114">The Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and the [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d314-114">The Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and the [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="7d314-115">To learn more, review the linked web pages.</span><span class="sxs-lookup"><span data-stu-id="7d314-115">To learn more, review the linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="7d314-116">If you use an aggregation command such as `|measure count()` or `distinct`, each call to search can return upto 500,000 records.</span><span class="sxs-lookup"><span data-stu-id="7d314-116">If you use an aggregation command such as `|measure count()` or `distinct`, each call to search can return upto 500,000 records.</span></span> <span data-ttu-id="7d314-117">Searches that do not include an aggregation command return upto 5,000 records.</span><span class="sxs-lookup"><span data-stu-id="7d314-117">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="7d314-118">Basic Log Analytics Search REST API tutorial</span><span class="sxs-lookup"><span data-stu-id="7d314-118">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="to-use-armclient"></a><span data-ttu-id="7d314-119">To use ARMClient</span><span class="sxs-lookup"><span data-stu-id="7d314-119">To use ARMClient</span></span>
1. <span data-ttu-id="7d314-120">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span><span class="sxs-lookup"><span data-stu-id="7d314-120">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="7d314-121">Open a command prompt window as administrator and then run the following command:</span><span class="sxs-lookup"><span data-stu-id="7d314-121">Open a command prompt window as administrator and then run the following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="7d314-122">Install ARMClient by running the following command:</span><span class="sxs-lookup"><span data-stu-id="7d314-122">Install ARMClient by running the following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="to-perform-a-search-using-armclient"></a><span data-ttu-id="7d314-123">To perform a search using ARMClient</span><span class="sxs-lookup"><span data-stu-id="7d314-123">To perform a search using ARMClient</span></span>
1. <span data-ttu-id="7d314-124">Log in using your Microsoft account or your work or school account:</span><span class="sxs-lookup"><span data-stu-id="7d314-124">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="7d314-125">A successful login lists all subscriptions tied to the given account:</span><span class="sxs-lookup"><span data-stu-id="7d314-125">A successful login lists all subscriptions tied to the given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="7d314-126">Get the Operations Management Suite workspaces:</span><span class="sxs-lookup"><span data-stu-id="7d314-126">Get the Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="7d314-127">A successful Get call would output all workspaces tied to the subscription:</span><span class="sxs-lookup"><span data-stu-id="7d314-127">A successful Get call would output all workspaces tied to the subscription:</span></span>

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. <span data-ttu-id="7d314-128">Create your search variable:</span><span class="sxs-lookup"><span data-stu-id="7d314-128">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="7d314-129">Search using your new search variable:</span><span class="sxs-lookup"><span data-stu-id="7d314-129">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="7d314-130">Log Analytics Search REST API reference examples</span><span class="sxs-lookup"><span data-stu-id="7d314-130">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="7d314-131">The following examples show you how you can use the Search API.</span><span class="sxs-lookup"><span data-stu-id="7d314-131">The following examples show you how you can use the Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="7d314-132">Search - Action/Read</span><span class="sxs-lookup"><span data-stu-id="7d314-132">Search - Action/Read</span></span>
<span data-ttu-id="7d314-133">**Sample Url:**</span><span class="sxs-lookup"><span data-stu-id="7d314-133">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="7d314-134">**Request:**</span><span class="sxs-lookup"><span data-stu-id="7d314-134">**Request:**</span></span>

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
<span data-ttu-id="7d314-135">The following table describes the properties that are available.</span><span class="sxs-lookup"><span data-stu-id="7d314-135">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="7d314-136">**Property**</span><span class="sxs-lookup"><span data-stu-id="7d314-136">**Property**</span></span> | <span data-ttu-id="7d314-137">**Description**</span><span class="sxs-lookup"><span data-stu-id="7d314-137">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="7d314-138">top</span><span class="sxs-lookup"><span data-stu-id="7d314-138">top</span></span> |<span data-ttu-id="7d314-139">The maximum number of results to return.</span><span class="sxs-lookup"><span data-stu-id="7d314-139">The maximum number of results to return.</span></span> |
| <span data-ttu-id="7d314-140">highlight</span><span class="sxs-lookup"><span data-stu-id="7d314-140">highlight</span></span> |<span data-ttu-id="7d314-141">Contains pre and post parameters, used usually for highlighting matching fields</span><span class="sxs-lookup"><span data-stu-id="7d314-141">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="7d314-142">pre</span><span class="sxs-lookup"><span data-stu-id="7d314-142">pre</span></span> |<span data-ttu-id="7d314-143">Prefixes the given string to your matched fields.</span><span class="sxs-lookup"><span data-stu-id="7d314-143">Prefixes the given string to your matched fields.</span></span> |
| <span data-ttu-id="7d314-144">post</span><span class="sxs-lookup"><span data-stu-id="7d314-144">post</span></span> |<span data-ttu-id="7d314-145">Appends the given string to your matched fields.</span><span class="sxs-lookup"><span data-stu-id="7d314-145">Appends the given string to your matched fields.</span></span> |
| <span data-ttu-id="7d314-146">query</span><span class="sxs-lookup"><span data-stu-id="7d314-146">query</span></span> |<span data-ttu-id="7d314-147">The search query used to collect and return results.</span><span class="sxs-lookup"><span data-stu-id="7d314-147">The search query used to collect and return results.</span></span> |
| <span data-ttu-id="7d314-148">start</span><span class="sxs-lookup"><span data-stu-id="7d314-148">start</span></span> |<span data-ttu-id="7d314-149">The beginning of the time window you want results to be found from.</span><span class="sxs-lookup"><span data-stu-id="7d314-149">The beginning of the time window you want results to be found from.</span></span> |
| <span data-ttu-id="7d314-150">end</span><span class="sxs-lookup"><span data-stu-id="7d314-150">end</span></span> |<span data-ttu-id="7d314-151">The end of the time window you want results to be found from.</span><span class="sxs-lookup"><span data-stu-id="7d314-151">The end of the time window you want results to be found from.</span></span> |

<span data-ttu-id="7d314-152">**Response:**</span><span class="sxs-lookup"><span data-stu-id="7d314-152">**Response:**</span></span>

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a><span data-ttu-id="7d314-153">Search/{ID} - Action/Read</span><span class="sxs-lookup"><span data-stu-id="7d314-153">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="7d314-154">**Request the contents of a Saved Search:**</span><span class="sxs-lookup"><span data-stu-id="7d314-154">**Request the contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="7d314-155">If the search returns with a ‘Pending’ status, then polling the updated results can be done through this API.</span><span class="sxs-lookup"><span data-stu-id="7d314-155">If the search returns with a ‘Pending’ status, then polling the updated results can be done through this API.</span></span> <span data-ttu-id="7d314-156">After 6 min, the result of the search will be dropped from the cache and HTTP Gone will be returned.</span><span class="sxs-lookup"><span data-stu-id="7d314-156">After 6 min, the result of the search will be dropped from the cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="7d314-157">If the initial search request returns a ‘Successful’ status immediately, the results are not added to the cache causing this API to return HTTP Gone if queried.</span><span class="sxs-lookup"><span data-stu-id="7d314-157">If the initial search request returns a ‘Successful’ status immediately, the results are not added to the cache causing this API to return HTTP Gone if queried.</span></span> <span data-ttu-id="7d314-158">The contents of an HTTP 200 result are in the same format as the initial search request just with updated values.</span><span class="sxs-lookup"><span data-stu-id="7d314-158">The contents of an HTTP 200 result are in the same format as the initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="7d314-159">Saved searches</span><span class="sxs-lookup"><span data-stu-id="7d314-159">Saved searches</span></span>
<span data-ttu-id="7d314-160">**Request List of Saved Searches:**</span><span class="sxs-lookup"><span data-stu-id="7d314-160">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="7d314-161">Supported methods: GET PUT DELETE</span><span class="sxs-lookup"><span data-stu-id="7d314-161">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="7d314-162">Supported collection methods: GET</span><span class="sxs-lookup"><span data-stu-id="7d314-162">Supported collection methods: GET</span></span>

<span data-ttu-id="7d314-163">The following table describes the properties that are available.</span><span class="sxs-lookup"><span data-stu-id="7d314-163">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="7d314-164">Property</span><span class="sxs-lookup"><span data-stu-id="7d314-164">Property</span></span> | <span data-ttu-id="7d314-165">Description</span><span class="sxs-lookup"><span data-stu-id="7d314-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7d314-166">Id</span><span class="sxs-lookup"><span data-stu-id="7d314-166">Id</span></span> |<span data-ttu-id="7d314-167">The unique identifier.</span><span class="sxs-lookup"><span data-stu-id="7d314-167">The unique identifier.</span></span> |
| <span data-ttu-id="7d314-168">Etag</span><span class="sxs-lookup"><span data-stu-id="7d314-168">Etag</span></span> |<span data-ttu-id="7d314-169">**Required for Patch**.</span><span class="sxs-lookup"><span data-stu-id="7d314-169">**Required for Patch**.</span></span> <span data-ttu-id="7d314-170">Updated by server on each write.</span><span class="sxs-lookup"><span data-stu-id="7d314-170">Updated by server on each write.</span></span> <span data-ttu-id="7d314-171">Value must be equal to the current stored value or ‘\*’ to update.</span><span class="sxs-lookup"><span data-stu-id="7d314-171">Value must be equal to the current stored value or ‘\*’ to update.</span></span> <span data-ttu-id="7d314-172">409 returned for old/invalid values.</span><span class="sxs-lookup"><span data-stu-id="7d314-172">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="7d314-173">properties.query</span><span class="sxs-lookup"><span data-stu-id="7d314-173">properties.query</span></span> |<span data-ttu-id="7d314-174">**Required**.</span><span class="sxs-lookup"><span data-stu-id="7d314-174">**Required**.</span></span> <span data-ttu-id="7d314-175">The search query.</span><span class="sxs-lookup"><span data-stu-id="7d314-175">The search query.</span></span> |
| <span data-ttu-id="7d314-176">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="7d314-176">properties.displayName</span></span> |<span data-ttu-id="7d314-177">**Required**.</span><span class="sxs-lookup"><span data-stu-id="7d314-177">**Required**.</span></span> <span data-ttu-id="7d314-178">The user-defined display name of the query.</span><span class="sxs-lookup"><span data-stu-id="7d314-178">The user-defined display name of the query.</span></span> |
| <span data-ttu-id="7d314-179">properties.category</span><span class="sxs-lookup"><span data-stu-id="7d314-179">properties.category</span></span> |<span data-ttu-id="7d314-180">**Required**.</span><span class="sxs-lookup"><span data-stu-id="7d314-180">**Required**.</span></span> <span data-ttu-id="7d314-181">The user-defined category of the query.</span><span class="sxs-lookup"><span data-stu-id="7d314-181">The user-defined category of the query.</span></span> |

> [!NOTE]
> <span data-ttu-id="7d314-182">The Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span><span class="sxs-lookup"><span data-stu-id="7d314-182">The Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="7d314-183">The API does not return saved searches provided by solutions.</span><span class="sxs-lookup"><span data-stu-id="7d314-183">The API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="7d314-184">Create saved searches</span><span class="sxs-lookup"><span data-stu-id="7d314-184">Create saved searches</span></span>
<span data-ttu-id="7d314-185">**Request:**</span><span class="sxs-lookup"><span data-stu-id="7d314-185">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="delete-saved-searches"></a><span data-ttu-id="7d314-186">Delete saved searches</span><span class="sxs-lookup"><span data-stu-id="7d314-186">Delete saved searches</span></span>
<span data-ttu-id="7d314-187">**Request:**</span><span class="sxs-lookup"><span data-stu-id="7d314-187">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="7d314-188">Update saved searches</span><span class="sxs-lookup"><span data-stu-id="7d314-188">Update saved searches</span></span>
 <span data-ttu-id="7d314-189">**Request:**</span><span class="sxs-lookup"><span data-stu-id="7d314-189">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="7d314-190">Metadata - JSON only</span><span class="sxs-lookup"><span data-stu-id="7d314-190">Metadata - JSON only</span></span>
<span data-ttu-id="7d314-191">Here’s a way to see the fields for all log types for the data collected in your workspace.</span><span class="sxs-lookup"><span data-stu-id="7d314-191">Here’s a way to see the fields for all log types for the data collected in your workspace.</span></span> <span data-ttu-id="7d314-192">For example, if you want you know if the Event type has a field named Computer, then this query is one way to check.</span><span class="sxs-lookup"><span data-stu-id="7d314-192">For example, if you want you know if the Event type has a field named Computer, then this query is one way to check.</span></span>

<span data-ttu-id="7d314-193">**Request for Fields:**</span><span class="sxs-lookup"><span data-stu-id="7d314-193">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="7d314-194">**Response:**</span><span class="sxs-lookup"><span data-stu-id="7d314-194">**Response:**</span></span>

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

<span data-ttu-id="7d314-195">The following table describes the properties that are available.</span><span class="sxs-lookup"><span data-stu-id="7d314-195">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="7d314-196">**Property**</span><span class="sxs-lookup"><span data-stu-id="7d314-196">**Property**</span></span> | <span data-ttu-id="7d314-197">**Description**</span><span class="sxs-lookup"><span data-stu-id="7d314-197">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="7d314-198">name</span><span class="sxs-lookup"><span data-stu-id="7d314-198">name</span></span> |<span data-ttu-id="7d314-199">Field name.</span><span class="sxs-lookup"><span data-stu-id="7d314-199">Field name.</span></span> |
| <span data-ttu-id="7d314-200">displayName</span><span class="sxs-lookup"><span data-stu-id="7d314-200">displayName</span></span> |<span data-ttu-id="7d314-201">The display name of the field.</span><span class="sxs-lookup"><span data-stu-id="7d314-201">The display name of the field.</span></span> |
| <span data-ttu-id="7d314-202">type</span><span class="sxs-lookup"><span data-stu-id="7d314-202">type</span></span> |<span data-ttu-id="7d314-203">The Type of the field value.</span><span class="sxs-lookup"><span data-stu-id="7d314-203">The Type of the field value.</span></span> |
| <span data-ttu-id="7d314-204">facetable</span><span class="sxs-lookup"><span data-stu-id="7d314-204">facetable</span></span> |<span data-ttu-id="7d314-205">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span><span class="sxs-lookup"><span data-stu-id="7d314-205">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="7d314-206">display</span><span class="sxs-lookup"><span data-stu-id="7d314-206">display</span></span> |<span data-ttu-id="7d314-207">Current ‘display’ property.</span><span class="sxs-lookup"><span data-stu-id="7d314-207">Current ‘display’ property.</span></span> <span data-ttu-id="7d314-208">True if field is visible in search.</span><span class="sxs-lookup"><span data-stu-id="7d314-208">True if field is visible in search.</span></span> |
| <span data-ttu-id="7d314-209">ownerType</span><span class="sxs-lookup"><span data-stu-id="7d314-209">ownerType</span></span> |<span data-ttu-id="7d314-210">Reduced to only Types belonging to onboarded IP’s.</span><span class="sxs-lookup"><span data-stu-id="7d314-210">Reduced to only Types belonging to onboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="7d314-211">Optional parameters</span><span class="sxs-lookup"><span data-stu-id="7d314-211">Optional parameters</span></span>
<span data-ttu-id="7d314-212">The following information describes optional parameters available.</span><span class="sxs-lookup"><span data-stu-id="7d314-212">The following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="7d314-213">Highlighting</span><span class="sxs-lookup"><span data-stu-id="7d314-213">Highlighting</span></span>
<span data-ttu-id="7d314-214">The “Highlight” parameter is an optional parameter you may use to request the search subsystem include a set of markers in its response.</span><span class="sxs-lookup"><span data-stu-id="7d314-214">The “Highlight” parameter is an optional parameter you may use to request the search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="7d314-215">These markers indicate the start and end highlighted text that matches the terms provided in your search query.</span><span class="sxs-lookup"><span data-stu-id="7d314-215">These markers indicate the start and end highlighted text that matches the terms provided in your search query.</span></span>
<span data-ttu-id="7d314-216">You may specify the start and end markers that are used by search to wrap the highlighted term.</span><span class="sxs-lookup"><span data-stu-id="7d314-216">You may specify the start and end markers that are used by search to wrap the highlighted term.</span></span>

<span data-ttu-id="7d314-217">**Example search query**</span><span class="sxs-lookup"><span data-stu-id="7d314-217">**Example search query**</span></span>

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

<span data-ttu-id="7d314-218">**Sample result:**</span><span class="sxs-lookup"><span data-stu-id="7d314-218">**Sample result:**</span></span>

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

<span data-ttu-id="7d314-219">Notice that the preceding result contains an error message that has been prefixed and appended.</span><span class="sxs-lookup"><span data-stu-id="7d314-219">Notice that the preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="7d314-220">Computer groups</span><span class="sxs-lookup"><span data-stu-id="7d314-220">Computer groups</span></span>
<span data-ttu-id="7d314-221">Computer groups are special saved searches that return a set of computers.</span><span class="sxs-lookup"><span data-stu-id="7d314-221">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="7d314-222">You can use a computer group in other queries to limit the results to the computers in the group.</span><span class="sxs-lookup"><span data-stu-id="7d314-222">You can use a computer group in other queries to limit the results to the computers in the group.</span></span>  <span data-ttu-id="7d314-223">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span><span class="sxs-lookup"><span data-stu-id="7d314-223">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="7d314-224">Following is a sample response for a computer group.</span><span class="sxs-lookup"><span data-stu-id="7d314-224">Following is a sample response for a computer group.</span></span>

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a><span data-ttu-id="7d314-225">Retrieving computer groups</span><span class="sxs-lookup"><span data-stu-id="7d314-225">Retrieving computer groups</span></span>
<span data-ttu-id="7d314-226">To retrieve a computer group, use the Get method with the group ID.</span><span class="sxs-lookup"><span data-stu-id="7d314-226">To retrieve a computer group, use the Get method with the group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="7d314-227">Creating or updating a computer group</span><span class="sxs-lookup"><span data-stu-id="7d314-227">Creating or updating a computer group</span></span>
<span data-ttu-id="7d314-228">To create a computer group, use the Put method with a unique saved search ID.</span><span class="sxs-lookup"><span data-stu-id="7d314-228">To create a computer group, use the Put method with a unique saved search ID.</span></span> <span data-ttu-id="7d314-229">If you use an existing computer group ID, then that one is modified.</span><span class="sxs-lookup"><span data-stu-id="7d314-229">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="7d314-230">When you create a computer group in the Log Analytics portal, then the ID is created from the group and name.</span><span class="sxs-lookup"><span data-stu-id="7d314-230">When you create a computer group in the Log Analytics portal, then the ID is created from the group and name.</span></span>

<span data-ttu-id="7d314-231">The query used for the group definition must return a set of computers for the group to function properly.</span><span class="sxs-lookup"><span data-stu-id="7d314-231">The query used for the group definition must return a set of computers for the group to function properly.</span></span>  <span data-ttu-id="7d314-232">It's recommended that you end your query with `| Distinct Computer` to ensure the correct data is returned.</span><span class="sxs-lookup"><span data-stu-id="7d314-232">It's recommended that you end your query with `| Distinct Computer` to ensure the correct data is returned.</span></span>

<span data-ttu-id="7d314-233">The definition of the saved search must include a tag named Group with a value of Computer for the search to be classified as a computer group.</span><span class="sxs-lookup"><span data-stu-id="7d314-233">The definition of the saved search must include a tag named Group with a value of Computer for the search to be classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="7d314-234">Deleting computer groups</span><span class="sxs-lookup"><span data-stu-id="7d314-234">Deleting computer groups</span></span>
<span data-ttu-id="7d314-235">To delete a computer group, use the Delete method with the group ID.</span><span class="sxs-lookup"><span data-stu-id="7d314-235">To delete a computer group, use the Delete method with the group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="7d314-236">Next steps</span><span class="sxs-lookup"><span data-stu-id="7d314-236">Next steps</span></span>
* <span data-ttu-id="7d314-237">Learn about [log searches](log-analytics-log-searches.md) to build queries using custom fields for criteria.</span><span class="sxs-lookup"><span data-stu-id="7d314-237">Learn about [log searches](log-analytics-log-searches.md) to build queries using custom fields for criteria.</span></span>
