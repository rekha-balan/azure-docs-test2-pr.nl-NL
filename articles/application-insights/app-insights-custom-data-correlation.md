---
title: Azure Application Insights | Microsoft Docs
description: ''
services: application-insights
documentationcenter: ''
author: eternovsky
manager: carmonm
ms.assetid: ea2a28ed-4cd9-4006-bd5a-d4c76f4ec20b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 08/08/2018
ms.reviewer: mbullwin
ms.author: Evgeny.Ternovsky
ms.openlocfilehash: 31e37efc1aad3d355bdd8391535f317ec137f5d7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966787"
---
# <a name="correlating-application-insights-data-with-custom-data-sources"></a><span data-ttu-id="6dcf9-102">Correlating Application Insights data with custom data sources</span><span class="sxs-lookup"><span data-stu-id="6dcf9-102">Correlating Application Insights data with custom data sources</span></span>

<span data-ttu-id="6dcf9-103">Application Insights collects several different data types: exceptions, traces, page views, and others.</span><span class="sxs-lookup"><span data-stu-id="6dcf9-103">Application Insights collects several different data types: exceptions, traces, page views, and others.</span></span> <span data-ttu-id="6dcf9-104">While this is often sufficient to investigate your application’s performance, reliability, and usage, there are cases when it is useful to correlate the data stored in Application Insights to other completely custom datasets.</span><span class="sxs-lookup"><span data-stu-id="6dcf9-104">While this is often sufficient to investigate your application’s performance, reliability, and usage, there are cases when it is useful to correlate the data stored in Application Insights to other completely custom datasets.</span></span>

<span data-ttu-id="6dcf9-105">Some situations where you might want custom data include:</span><span class="sxs-lookup"><span data-stu-id="6dcf9-105">Some situations where you might want custom data include:</span></span>

- <span data-ttu-id="6dcf9-106">Data enrichment or lookup tables: for example, supplement a server name with the owner of the server and the lab location in which it can be found</span><span class="sxs-lookup"><span data-stu-id="6dcf9-106">Data enrichment or lookup tables: for example, supplement a server name with the owner of the server and the lab location in which it can be found</span></span> 
- <span data-ttu-id="6dcf9-107">Correlation with non-Application Insights data sources: for example, correlate data about a purchase on a web-store with information from your purchase-fulfillment service to determine how accurate your shipping time estimates were</span><span class="sxs-lookup"><span data-stu-id="6dcf9-107">Correlation with non-Application Insights data sources: for example, correlate data about a purchase on a web-store with information from your purchase-fulfillment service to determine how accurate your shipping time estimates were</span></span> 
- <span data-ttu-id="6dcf9-108">Completely custom data: many of our customers love the query language and performance of the Log Analytics data platform that backs Application Insights, and want to use it to query data that is not at all related to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6dcf9-108">Completely custom data: many of our customers love the query language and performance of the Log Analytics data platform that backs Application Insights, and want to use it to query data that is not at all related to Application Insights.</span></span> <span data-ttu-id="6dcf9-109">For example, to track the solar panel performance as part of a smart home installation as outlined [here]( http://blogs.catapultsystems.com/cfuller/archive/2017/10/04/using-log-analytics-and-a-special-guest-to-forecast-electricity-generation/).</span><span class="sxs-lookup"><span data-stu-id="6dcf9-109">For example, to track the solar panel performance as part of a smart home installation as outlined [here]( http://blogs.catapultsystems.com/cfuller/archive/2017/10/04/using-log-analytics-and-a-special-guest-to-forecast-electricity-generation/).</span></span>

## <a name="how-to-correlate-custom-data-with-application-insights-data"></a><span data-ttu-id="6dcf9-110">How to correlate custom data with Application Insights data</span><span class="sxs-lookup"><span data-stu-id="6dcf9-110">How to correlate custom data with Application Insights data</span></span> 

<span data-ttu-id="6dcf9-111">Since Application Insights is backed by the powerful Log Analytics data platform, we are able to use the full power of Log Analytics to ingest the data.</span><span class="sxs-lookup"><span data-stu-id="6dcf9-111">Since Application Insights is backed by the powerful Log Analytics data platform, we are able to use the full power of Log Analytics to ingest the data.</span></span> <span data-ttu-id="6dcf9-112">Then, we will write queries using the “join” operator that will correlate this custom data with the data available to us in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6dcf9-112">Then, we will write queries using the “join” operator that will correlate this custom data with the data available to us in Log Analytics.</span></span> 

## <a name="ingesting-data"></a><span data-ttu-id="6dcf9-113">Ingesting data</span><span class="sxs-lookup"><span data-stu-id="6dcf9-113">Ingesting data</span></span>

<span data-ttu-id="6dcf9-114">In this section, we will review how to get your data into Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6dcf9-114">In this section, we will review how to get your data into Log Analytics.</span></span>

<span data-ttu-id="6dcf9-115">If you don’t already have one, provision a new Log Analytics workspace by following [these instructions]( https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-collect-azurevm) through and including the “create a workspace” step.</span><span class="sxs-lookup"><span data-stu-id="6dcf9-115">If you don’t already have one, provision a new Log Analytics workspace by following [these instructions]( https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-collect-azurevm) through and including the “create a workspace” step.</span></span>

<span data-ttu-id="6dcf9-116">To start sending data into Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6dcf9-116">To start sending data into Log Analytics.</span></span> <span data-ttu-id="6dcf9-117">Several options exist:</span><span class="sxs-lookup"><span data-stu-id="6dcf9-117">Several options exist:</span></span>

- <span data-ttu-id="6dcf9-118">For a synchronous mechanism, you can either directly call the [data collector API](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-collector-api) or use our Logic App connector – simply look for “Azure Log Analytics” and pick the “Send Data” option:</span><span class="sxs-lookup"><span data-stu-id="6dcf9-118">For a synchronous mechanism, you can either directly call the [data collector API](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-collector-api) or use our Logic App connector – simply look for “Azure Log Analytics” and pick the “Send Data” option:</span></span>

 ![Screenshot choose and action](./media/app-insights-custom-data-correlation/01-logic-app-connector.png)  

- <span data-ttu-id="6dcf9-120">For an asynchronous option, use the Data Collector API to build a processing pipeline.</span><span class="sxs-lookup"><span data-stu-id="6dcf9-120">For an asynchronous option, use the Data Collector API to build a processing pipeline.</span></span> <span data-ttu-id="6dcf9-121">See [this article](https://docs.microsoft.com/azure/log-analytics/log-analytics-create-pipeline-datacollector-api) for details.</span><span class="sxs-lookup"><span data-stu-id="6dcf9-121">See [this article](https://docs.microsoft.com/azure/log-analytics/log-analytics-create-pipeline-datacollector-api) for details.</span></span>

## <a name="correlating-data"></a><span data-ttu-id="6dcf9-122">Correlating data</span><span class="sxs-lookup"><span data-stu-id="6dcf9-122">Correlating data</span></span>

<span data-ttu-id="6dcf9-123">Application Insights is based on the Log Analytics data platform.</span><span class="sxs-lookup"><span data-stu-id="6dcf9-123">Application Insights is based on the Log Analytics data platform.</span></span> <span data-ttu-id="6dcf9-124">We can therefore use [cross-resource joins](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-cross-workspace-search) to correlate any data we ingested into Log Analytics with our Application Insights data.</span><span class="sxs-lookup"><span data-stu-id="6dcf9-124">We can therefore use [cross-resource joins](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-cross-workspace-search) to correlate any data we ingested into Log Analytics with our Application Insights data.</span></span>

<span data-ttu-id="6dcf9-125">For example, we can ingest our lab inventory and locations into a table called “LabLocations_CL” in a Log Analytics workspace called “myLA”.</span><span class="sxs-lookup"><span data-stu-id="6dcf9-125">For example, we can ingest our lab inventory and locations into a table called “LabLocations_CL” in a Log Analytics workspace called “myLA”.</span></span> <span data-ttu-id="6dcf9-126">If we then wanted to review our requests tracked in Application Insights app called “myAI” and correlate the machine names that served the requests to the locations of these machines stored in the previously mentioned custom table, we can run the following query from either the Application Insights or Log Analytics context:</span><span class="sxs-lookup"><span data-stu-id="6dcf9-126">If we then wanted to review our requests tracked in Application Insights app called “myAI” and correlate the machine names that served the requests to the locations of these machines stored in the previously mentioned custom table, we can run the following query from either the Application Insights or Log Analytics context:</span></span>

```
app('myAI').requests
| join kind= leftouter (
    workspace('myLA').LabLocations_CL
    | project Computer_S, Owner_S, Lab_S
) on $left.cloud_RoleInstance == $right.Computer
```

## <a name="next-steps"></a><span data-ttu-id="6dcf9-127">Next Steps</span><span class="sxs-lookup"><span data-stu-id="6dcf9-127">Next Steps</span></span>

- <span data-ttu-id="6dcf9-128">Check out the [Data Collector API](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-collector-api) reference.</span><span class="sxs-lookup"><span data-stu-id="6dcf9-128">Check out the [Data Collector API](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-collector-api) reference.</span></span>
- <span data-ttu-id="6dcf9-129">For more information on [cross-resource joins](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-cross-workspace-search).</span><span class="sxs-lookup"><span data-stu-id="6dcf9-129">For more information on [cross-resource joins](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-cross-workspace-search).</span></span>
