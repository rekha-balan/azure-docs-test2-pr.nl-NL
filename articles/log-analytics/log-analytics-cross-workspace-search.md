---
title: Search across resources with Azure Log Analytics  | Microsoft Docs
description: This article describes how you can query against resources from multiple workspaces and App Insights app in your subscription.
services: log-analytics
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: magoedte
ms.component: na
ms.openlocfilehash: 75116e0ba50c3f195d528d33822af0c446acd5fe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968571"
---
# <a name="perform-cross-resource-log-searches-in-log-analytics"></a><span data-ttu-id="412ea-103">Perform cross-resource log searches in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="412ea-103">Perform cross-resource log searches in Log Analytics</span></span>  

<span data-ttu-id="412ea-104">Previously with Azure Log Analytics, you could only analyze data from within the current workspace, and it limited your ability to query across multiple workspaces defined in your subscription.</span><span class="sxs-lookup"><span data-stu-id="412ea-104">Previously with Azure Log Analytics, you could only analyze data from within the current workspace, and it limited your ability to query across multiple workspaces defined in your subscription.</span></span>  <span data-ttu-id="412ea-105">Additionally, you could only search telemetry items collected from your web-based application with Application Insights directly in Application Insights or from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="412ea-105">Additionally, you could only search telemetry items collected from your web-based application with Application Insights directly in Application Insights or from Visual Studio.</span></span>  <span data-ttu-id="412ea-106">This also made it a challenge to natively analyze operational and application data together.</span><span class="sxs-lookup"><span data-stu-id="412ea-106">This also made it a challenge to natively analyze operational and application data together.</span></span>   

<span data-ttu-id="412ea-107">Now you can query not only across multiple Log Analytics workspaces, but also data from a specific Application Insights app in the same resource group, another resource group, or another subscription.</span><span class="sxs-lookup"><span data-stu-id="412ea-107">Now you can query not only across multiple Log Analytics workspaces, but also data from a specific Application Insights app in the same resource group, another resource group, or another subscription.</span></span> <span data-ttu-id="412ea-108">This provides you with a system-wide view of your data.</span><span class="sxs-lookup"><span data-stu-id="412ea-108">This provides you with a system-wide view of your data.</span></span>  <span data-ttu-id="412ea-109">You can only perform these types of queries in the [Log Analytics page (preview)](log-analytics-log-search-portals.md#log-analytics-page-preview), not in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="412ea-109">You can only perform these types of queries in the [Log Analytics page (preview)](log-analytics-log-search-portals.md#log-analytics-page-preview), not in the Azure portal.</span></span> <span data-ttu-id="412ea-110">The number of resources (Log Analytics workspaces and Application Insights app) that you can include in a single query is limited to 100.</span><span class="sxs-lookup"><span data-stu-id="412ea-110">The number of resources (Log Analytics workspaces and Application Insights app) that you can include in a single query is limited to 100.</span></span> 

## <a name="querying-across-log-analytics-workspaces-and-from-application-insights"></a><span data-ttu-id="412ea-111">Querying across Log Analytics workspaces and from Application Insights</span><span class="sxs-lookup"><span data-stu-id="412ea-111">Querying across Log Analytics workspaces and from Application Insights</span></span>
<span data-ttu-id="412ea-112">To reference another workspace in your query, use the [*workspace*](https://docs.loganalytics.io/docs/Language-Reference/Scope-functions/workspace()) identifier, and for an app from Application Insights, use the [*app*](https://docs.loganalytics.io/docs/Language-Reference/Scope-functions/app()) identifier.</span><span class="sxs-lookup"><span data-stu-id="412ea-112">To reference another workspace in your query, use the [*workspace*](https://docs.loganalytics.io/docs/Language-Reference/Scope-functions/workspace()) identifier, and for an app from Application Insights, use the [*app*](https://docs.loganalytics.io/docs/Language-Reference/Scope-functions/app()) identifier.</span></span>  

### <a name="identifying-workspace-resources"></a><span data-ttu-id="412ea-113">Identifying workspace resources</span><span class="sxs-lookup"><span data-stu-id="412ea-113">Identifying workspace resources</span></span>
<span data-ttu-id="412ea-114">The following examples demonstrate queries across Log Analytics workspaces to return summarized counts of logs from the Update table on a workspace named *contosoretail-it*.</span><span class="sxs-lookup"><span data-stu-id="412ea-114">The following examples demonstrate queries across Log Analytics workspaces to return summarized counts of logs from the Update table on a workspace named *contosoretail-it*.</span></span> 

<span data-ttu-id="412ea-115">Identifying a workspace can be accomplished one of several ways:</span><span class="sxs-lookup"><span data-stu-id="412ea-115">Identifying a workspace can be accomplished one of several ways:</span></span>

* <span data-ttu-id="412ea-116">Resource name - is a human-readable name of the workspace, sometimes referred to as *component name*.</span><span class="sxs-lookup"><span data-stu-id="412ea-116">Resource name - is a human-readable name of the workspace, sometimes referred to as *component name*.</span></span> 

    `workspace("contosoretail").Update | count`
 
    >[!NOTE]
    ><span data-ttu-id="412ea-117">Identifying a workspace by name assumes uniqueness across all accessible subscriptions.</span><span class="sxs-lookup"><span data-stu-id="412ea-117">Identifying a workspace by name assumes uniqueness across all accessible subscriptions.</span></span> <span data-ttu-id="412ea-118">If you have multiple applications with the specified name, the query fails because of the ambiguity.</span><span class="sxs-lookup"><span data-stu-id="412ea-118">If you have multiple applications with the specified name, the query fails because of the ambiguity.</span></span> <span data-ttu-id="412ea-119">In this case, you must use one of the other identifiers.</span><span class="sxs-lookup"><span data-stu-id="412ea-119">In this case, you must use one of the other identifiers.</span></span>

* <span data-ttu-id="412ea-120">Qualified name - is the “full name” of the workspace, composed of the subscription name, resource group, and component name in this format: *subscriptionName/resourceGroup/componentName*.</span><span class="sxs-lookup"><span data-stu-id="412ea-120">Qualified name - is the “full name” of the workspace, composed of the subscription name, resource group, and component name in this format: *subscriptionName/resourceGroup/componentName*.</span></span> 

    `workspace('contoso/contosoretail/contosoretail-it').Update | count `

    >[!NOTE]
    ><span data-ttu-id="412ea-121">Because Azure subscription names are not unique, this identifier might be ambiguous.</span><span class="sxs-lookup"><span data-stu-id="412ea-121">Because Azure subscription names are not unique, this identifier might be ambiguous.</span></span> 
    >

* <span data-ttu-id="412ea-122">Workspace ID - A workspace ID is the unique, immutable, identifier assigned to each workspace represented as a globally unique identifier (GUID).</span><span class="sxs-lookup"><span data-stu-id="412ea-122">Workspace ID - A workspace ID is the unique, immutable, identifier assigned to each workspace represented as a globally unique identifier (GUID).</span></span>

    `workspace("b459b4u5-912x-46d5-9cb1-p43069212nb4").Update | count`

* <span data-ttu-id="412ea-123">Azure Resource ID – the Azure-defined unique identity of the workspace.</span><span class="sxs-lookup"><span data-stu-id="412ea-123">Azure Resource ID – the Azure-defined unique identity of the workspace.</span></span> <span data-ttu-id="412ea-124">You use the Resource ID when the resource name is ambiguous.</span><span class="sxs-lookup"><span data-stu-id="412ea-124">You use the Resource ID when the resource name is ambiguous.</span></span>  <span data-ttu-id="412ea-125">For workspaces, the format is: */subscriptions/subscriptionId/resourcegroups/resourceGroup/providers/microsoft.OperationalInsights/workspaces/componentName*.</span><span class="sxs-lookup"><span data-stu-id="412ea-125">For workspaces, the format is: */subscriptions/subscriptionId/resourcegroups/resourceGroup/providers/microsoft.OperationalInsights/workspaces/componentName*.</span></span>  

    <span data-ttu-id="412ea-126">For example:</span><span class="sxs-lookup"><span data-stu-id="412ea-126">For example:</span></span>
    ``` 
    workspace("/subscriptions/e427519-5645-8x4e-1v67-3b84b59a1985/resourcegroups/ContosoAzureHQ/providers/Microsoft.OperationalInsights/workspaces/contosoretail").Update | count
    ```

### <a name="identifying-an-application"></a><span data-ttu-id="412ea-127">Identifying an application</span><span class="sxs-lookup"><span data-stu-id="412ea-127">Identifying an application</span></span>
<span data-ttu-id="412ea-128">The following examples return a summarized count of requests made against an app named *fabrikamapp* in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="412ea-128">The following examples return a summarized count of requests made against an app named *fabrikamapp* in Application Insights.</span></span> 

<span data-ttu-id="412ea-129">Identifying an application in Application Insights can be accomplished with the *app(Identifier)* expression.</span><span class="sxs-lookup"><span data-stu-id="412ea-129">Identifying an application in Application Insights can be accomplished with the *app(Identifier)* expression.</span></span>  <span data-ttu-id="412ea-130">The *Identifier* argument specifies the app using one of the following:</span><span class="sxs-lookup"><span data-stu-id="412ea-130">The *Identifier* argument specifies the app using one of the following:</span></span>

* <span data-ttu-id="412ea-131">Resource name - is a human readable name of the app, sometimes referred to as the *component name*.</span><span class="sxs-lookup"><span data-stu-id="412ea-131">Resource name - is a human readable name of the app, sometimes referred to as the *component name*.</span></span>  

    `app("fabrikamapp")`

* <span data-ttu-id="412ea-132">Qualified name - is the “full name” of the app, composed of the subscription name, resource group, and component name in this format: *subscriptionName/resourceGroup/componentName*.</span><span class="sxs-lookup"><span data-stu-id="412ea-132">Qualified name - is the “full name” of the app, composed of the subscription name, resource group, and component name in this format: *subscriptionName/resourceGroup/componentName*.</span></span> 

    `app("AI-Prototype/Fabrikam/fabrikamapp").requests | count`

     >[!NOTE]
    ><span data-ttu-id="412ea-133">Because Azure subscription names are not unique, this identifier might be ambiguous.</span><span class="sxs-lookup"><span data-stu-id="412ea-133">Because Azure subscription names are not unique, this identifier might be ambiguous.</span></span> 
    >

* <span data-ttu-id="412ea-134">ID - the app GUID of the application.</span><span class="sxs-lookup"><span data-stu-id="412ea-134">ID - the app GUID of the application.</span></span>

    `app("b459b4f6-912x-46d5-9cb1-b43069212ab4").requests | count`

* <span data-ttu-id="412ea-135">Azure Resource ID - the Azure-defined unique identity of the app.</span><span class="sxs-lookup"><span data-stu-id="412ea-135">Azure Resource ID - the Azure-defined unique identity of the app.</span></span> <span data-ttu-id="412ea-136">You use the Resource ID when the resource name is ambiguous.</span><span class="sxs-lookup"><span data-stu-id="412ea-136">You use the Resource ID when the resource name is ambiguous.</span></span> <span data-ttu-id="412ea-137">The format is: */subscriptions/subscriptionId/resourcegroups/resourceGroup/providers/microsoft.OperationalInsights/components/componentName*.</span><span class="sxs-lookup"><span data-stu-id="412ea-137">The format is: */subscriptions/subscriptionId/resourcegroups/resourceGroup/providers/microsoft.OperationalInsights/components/componentName*.</span></span>  

    <span data-ttu-id="412ea-138">For example:</span><span class="sxs-lookup"><span data-stu-id="412ea-138">For example:</span></span>
    ```
    app("/subscriptions/b459b4f6-912x-46d5-9cb1-b43069212ab4/resourcegroups/Fabrikam/providers/microsoft.insights/components/fabrikamapp").requests | count
    ```

### <a name="performing-a-query-across-multiple-resources"></a><span data-ttu-id="412ea-139">Performing a query across multiple resources</span><span class="sxs-lookup"><span data-stu-id="412ea-139">Performing a query across multiple resources</span></span>
<span data-ttu-id="412ea-140">You can query multiple resorces from any of your resource instances, these can be workspaces and apps combined.</span><span class="sxs-lookup"><span data-stu-id="412ea-140">You can query multiple resorces from any of your resource instances, these can be workspaces and apps combined.</span></span>
    
<span data-ttu-id="412ea-141">Example for query across two workspaces:</span><span class="sxs-lookup"><span data-stu-id="412ea-141">Example for query across two workspaces:</span></span>    
    ```
    union Update, workspace("contosoretail-it").Update, workspace("b459b4u5-912x-46d5-9cb1-p43069212nb4").Update
    | where TimeGenerated >= ago(1h)
    | where UpdateState == "Needed"
    | summarize dcount(Computer) by Classification
    ```

## <a name="next-steps"></a><span data-ttu-id="412ea-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="412ea-142">Next steps</span></span>

<span data-ttu-id="412ea-143">Review the [Log Analytics log search reference](https://docs.loganalytics.io/docs/Language-Reference) to view all of the query syntax options available in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="412ea-143">Review the [Log Analytics log search reference](https://docs.loganalytics.io/docs/Language-Reference) to view all of the query syntax options available in Log Analytics.</span></span>    
