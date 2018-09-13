---
title: Azure Monitoring REST API Walkthrough | Microsoft Docs
description: How to authenticate requests to and use the Azure Monitoring REST API.
author: mcollier
manager: carolz
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 565e6a88-3131-4a48-8b82-3effc9a3d5c6
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: mcollier
ms.openlocfilehash: ed290673121122ee44ac2e764206bc6acda4d48e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552751"
---
# <a name="azure-monitoring-rest-api-walkthrough"></a><span data-ttu-id="0cc4b-103">Azure Monitoring REST API Walkthrough</span><span class="sxs-lookup"><span data-stu-id="0cc4b-103">Azure Monitoring REST API Walkthrough</span></span>
<span data-ttu-id="0cc4b-104">This article shows you how to perform authentication so your code can use the [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cc4b-104">This article shows you how to perform authentication so your code can use the [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>         

<span data-ttu-id="0cc4b-105">The Azure Monitor API makes it possible to programmatically retrieve the available default metric definitions (the type of metric such as CPU Time, Requests, etc.), granularity, and metric values.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-105">The Azure Monitor API makes it possible to programmatically retrieve the available default metric definitions (the type of metric such as CPU Time, Requests, etc.), granularity, and metric values.</span></span> <span data-ttu-id="0cc4b-106">Once retrieved, the data can be saved in a separate data store such as Azure SQL Database, DocumentDB, or Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-106">Once retrieved, the data can be saved in a separate data store such as Azure SQL Database, DocumentDB, or Azure Data Lake.</span></span> <span data-ttu-id="0cc4b-107">From there additional analysis can be performed as needed.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-107">From there additional analysis can be performed as needed.</span></span>

<span data-ttu-id="0cc4b-108">Besides working with various metric data points, as this article demonstrates, the Monitor API makes it possible to list alert rules, view activity logs, and much more.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-108">Besides working with various metric data points, as this article demonstrates, the Monitor API makes it possible to list alert rules, view activity logs, and much more.</span></span> <span data-ttu-id="0cc4b-109">For a full list of available operations, see the [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cc4b-109">For a full list of available operations, see the [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

## <a name="authenticating-azure-monitor-requests"></a><span data-ttu-id="0cc4b-110">Authenticating Azure Monitor Requests</span><span class="sxs-lookup"><span data-stu-id="0cc4b-110">Authenticating Azure Monitor Requests</span></span>
<span data-ttu-id="0cc4b-111">The first step is to authenticate the request.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-111">The first step is to authenticate the request.</span></span>

<span data-ttu-id="0cc4b-112">All the tasks executed against the Azure Monitor API use the Azure Resource Manager authentication model.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-112">All the tasks executed against the Azure Monitor API use the Azure Resource Manager authentication model.</span></span> <span data-ttu-id="0cc4b-113">Therefore, all requests must be authenticated with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0cc4b-113">Therefore, all requests must be authenticated with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="0cc4b-114">One approach to authenticate the client application is to create an Azure AD service principal and retrieve the authentication (JWT) token.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-114">One approach to authenticate the client application is to create an Azure AD service principal and retrieve the authentication (JWT) token.</span></span> <span data-ttu-id="0cc4b-115">The following sample script demonstrates creating an Azure AD service principal via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-115">The following sample script demonstrates creating an Azure AD service principal via PowerShell.</span></span> <span data-ttu-id="0cc4b-116">For a more detailed walk-through, refer to the documentation on [using Azure PowerShell to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span><span class="sxs-lookup"><span data-stu-id="0cc4b-116">For a more detailed walk-through, refer to the documentation on [using Azure PowerShell to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span></span> <span data-ttu-id="0cc4b-117">It is also possible to [create a service principle via the Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0cc4b-117">It is also possible to [create a service principle via the Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"
$location = "centralus"

# Authenticate to a specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for the service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with the designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role to the newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

<span data-ttu-id="0cc4b-118">To query the Azure Monitor API, the client application should use the previously created service principal to authenticate.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-118">To query the Azure Monitor API, the client application should use the previously created service principal to authenticate.</span></span> <span data-ttu-id="0cc4b-119">The following example PowerShell script shows one approach, using the [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) to help get the JWT authentication token.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-119">The following example PowerShell script shows one approach, using the [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) to help get the JWT authentication token.</span></span> <span data-ttu-id="0cc4b-120">The JWT token is passed as part of an HTTP Authorization parameter in requests to the Azure Monitor REST API.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-120">The JWT token is passed as part of an HTTP Authorization parameter in requests to the Azure Monitor REST API.</span></span>

```PowerShell
$azureAdApplication = Get-AzureRmADApplication -IdentifierUri "https://localhost/azure-monitor"

$subscription = Get-AzureRmSubscription -SubscriptionId $subscriptionId

$clientId = $azureAdApplication.ApplicationId.Guid
$tenantId = $subscription.TenantId
$authUrl = "https://login.windows.net/${tenantId}"

$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl
$cred = New-Object -TypeName Microsoft.IdentityModel.Clients.ActiveDirectory.ClientCredential -ArgumentList ($clientId, $pwd)

$result = $AuthContext.AcquireToken("https://management.core.windows.net/", $cred)

# Build an array of HTTP header values
$authHeader = @{
'Content-Type'='application/json'
'Accept'='application/json'
'Authorization'=$result.CreateAuthorizationHeader()
}
```

<span data-ttu-id="0cc4b-121">Once the authentication setup step is complete, queries can then be executed against the Azure Monitor REST API.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-121">Once the authentication setup step is complete, queries can then be executed against the Azure Monitor REST API.</span></span> <span data-ttu-id="0cc4b-122">There are two helpful queries:</span><span class="sxs-lookup"><span data-stu-id="0cc4b-122">There are two helpful queries:</span></span>

1. <span data-ttu-id="0cc4b-123">List the metric definitions for a resource</span><span class="sxs-lookup"><span data-stu-id="0cc4b-123">List the metric definitions for a resource</span></span>
2. <span data-ttu-id="0cc4b-124">Retrieve the metric values</span><span class="sxs-lookup"><span data-stu-id="0cc4b-124">Retrieve the metric values</span></span>

## <a name="retrieve-metric-definitions"></a><span data-ttu-id="0cc4b-125">Retrieve Metric Definitions</span><span class="sxs-lookup"><span data-stu-id="0cc4b-125">Retrieve Metric Definitions</span></span>
> [!NOTE]
> <span data-ttu-id="0cc4b-126">To retrieve metric definitions using the Azure Monitor REST API, use "2016-03-01" as the API version.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-126">To retrieve metric definitions using the Azure Monitor REST API, use "2016-03-01" as the API version.</span></span>
>
>

```PowerShell
$apiVersion = "2016-03-01"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metricDefinitions?api-version=${apiVersion}"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -Verbose
```
<span data-ttu-id="0cc4b-127">For an Azure Logic App, the metric definitions would appear similar to the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="0cc4b-127">For an Azure Logic App, the metric definitions would appear similar to the following screenshot:</span></span>

![Alt "JSON view of metric definition response."](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

<span data-ttu-id="0cc4b-129">For more information, see the [List the metric definitions for a resource in Azure Monitor REST API](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentation.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-129">For more information, see the [List the metric definitions for a resource in Azure Monitor REST API](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentation.</span></span>

## <a name="retrieve-metric-values"></a><span data-ttu-id="0cc4b-130">Retrieve Metric Values</span><span class="sxs-lookup"><span data-stu-id="0cc4b-130">Retrieve Metric Values</span></span>
<span data-ttu-id="0cc4b-131">Once the available metric definitions are known, it is then possible to retrieve the related metric values.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-131">Once the available metric definitions are known, it is then possible to retrieve the related metric values.</span></span> <span data-ttu-id="0cc4b-132">Use the metric’s name ‘value’ (not the ‘localizedValue’) for any filtering requests (for example, retrieve the ‘CpuTime’ and ‘Requests’ metric data points).</span><span class="sxs-lookup"><span data-stu-id="0cc4b-132">Use the metric’s name ‘value’ (not the ‘localizedValue’) for any filtering requests (for example, retrieve the ‘CpuTime’ and ‘Requests’ metric data points).</span></span> <span data-ttu-id="0cc4b-133">If no filters are specified, the default metric is returned.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-133">If no filters are specified, the default metric is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="0cc4b-134">To retrieve metric values using the Azure Monitor REST API, use "2016-06-01" as the API version.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-134">To retrieve metric values using the Azure Monitor REST API, use "2016-06-01" as the API version.</span></span>
>
>

<span data-ttu-id="0cc4b-135">**Method**: GET</span><span class="sxs-lookup"><span data-stu-id="0cc4b-135">**Method**: GET</span></span>

<span data-ttu-id="0cc4b-136">**Request URI**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span><span class="sxs-lookup"><span data-stu-id="0cc4b-136">**Request URI**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span></span>

<span data-ttu-id="0cc4b-137">For example, to retrieve the RunsSucceeded metric data points for the given time range and for a time grain of 1 hour, the request would be as follows:</span><span class="sxs-lookup"><span data-stu-id="0cc4b-137">For example, to retrieve the RunsSucceeded metric data points for the given time range and for a time grain of 1 hour, the request would be as follows:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

<span data-ttu-id="0cc4b-138">The result would appear similar to the example following screenshot:</span><span class="sxs-lookup"><span data-stu-id="0cc4b-138">The result would appear similar to the example following screenshot:</span></span>

![Alt "JSON response showing Average Response Time metric value"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

<span data-ttu-id="0cc4b-140">To retrieve multiple data or aggregation points, add the metric definition names and aggregation types to the filter, as seen in the following example:</span><span class="sxs-lookup"><span data-stu-id="0cc4b-140">To retrieve multiple data or aggregation points, add the metric definition names and aggregation types to the filter, as seen in the following example:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a><span data-ttu-id="0cc4b-141">Use ARMClient</span><span class="sxs-lookup"><span data-stu-id="0cc4b-141">Use ARMClient</span></span>
<span data-ttu-id="0cc4b-142">An alternative to using PowerShell (as shown above), is to use [ARMClient](https://github.com/projectkudu/ARMClient) on your Windows machine.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-142">An alternative to using PowerShell (as shown above), is to use [ARMClient](https://github.com/projectkudu/ARMClient) on your Windows machine.</span></span> <span data-ttu-id="0cc4b-143">ARMClient handles the Azure AD authentication (and resulting JWT token) automatically.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-143">ARMClient handles the Azure AD authentication (and resulting JWT token) automatically.</span></span> <span data-ttu-id="0cc4b-144">The following steps outline use of ARMClient for retrieving metric data:</span><span class="sxs-lookup"><span data-stu-id="0cc4b-144">The following steps outline use of ARMClient for retrieving metric data:</span></span>

1. <span data-ttu-id="0cc4b-145">Install [Chocolatey](https://chocolatey.org/) and [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="0cc4b-145">Install [Chocolatey](https://chocolatey.org/) and [ARMClient](https://github.com/projectkudu/ARMClient).</span></span>
2. <span data-ttu-id="0cc4b-146">In a terminal window, type *armclient.exe login*.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-146">In a terminal window, type *armclient.exe login*.</span></span> <span data-ttu-id="0cc4b-147">This prompts you to log in to Azure.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-147">This prompts you to log in to Azure.</span></span>
3. <span data-ttu-id="0cc4b-148">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span><span class="sxs-lookup"><span data-stu-id="0cc4b-148">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span></span>
4. <span data-ttu-id="0cc4b-149">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span><span class="sxs-lookup"><span data-stu-id="0cc4b-149">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span></span>

![Alt "Using ARMClient to work with the Azure Monitoring REST API"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-the-resource-id"></a><span data-ttu-id="0cc4b-151">Retrieve the Resource ID</span><span class="sxs-lookup"><span data-stu-id="0cc4b-151">Retrieve the Resource ID</span></span>
<span data-ttu-id="0cc4b-152">Using the REST API can really help to understand the available metric definitions, granularity, and related values.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-152">Using the REST API can really help to understand the available metric definitions, granularity, and related values.</span></span> <span data-ttu-id="0cc4b-153">That information is helpful when using the [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cc4b-153">That information is helpful when using the [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>

<span data-ttu-id="0cc4b-154">For the preceding code, the resource ID to use is the full path to the desired Azure resource.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-154">For the preceding code, the resource ID to use is the full path to the desired Azure resource.</span></span> <span data-ttu-id="0cc4b-155">For example, to query against an Azure Web App, the resource ID would be:</span><span class="sxs-lookup"><span data-stu-id="0cc4b-155">For example, to query against an Azure Web App, the resource ID would be:</span></span>

<span data-ttu-id="0cc4b-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span><span class="sxs-lookup"><span data-stu-id="0cc4b-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span></span>

<span data-ttu-id="0cc4b-157">The following list contains a few examples of resource ID formats for various Azure resources:</span><span class="sxs-lookup"><span data-stu-id="0cc4b-157">The following list contains a few examples of resource ID formats for various Azure resources:</span></span>

* <span data-ttu-id="0cc4b-158">**IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span><span class="sxs-lookup"><span data-stu-id="0cc4b-158">**IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span></span>
* <span data-ttu-id="0cc4b-159">**Elastic SQL Pool** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span><span class="sxs-lookup"><span data-stu-id="0cc4b-159">**Elastic SQL Pool** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span></span>
* <span data-ttu-id="0cc4b-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span><span class="sxs-lookup"><span data-stu-id="0cc4b-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span></span>
* <span data-ttu-id="0cc4b-161">**Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span><span class="sxs-lookup"><span data-stu-id="0cc4b-161">**Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span></span>
* <span data-ttu-id="0cc4b-162">**VM Scale Sets** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span><span class="sxs-lookup"><span data-stu-id="0cc4b-162">**VM Scale Sets** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span></span>
* <span data-ttu-id="0cc4b-163">**VMs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span><span class="sxs-lookup"><span data-stu-id="0cc4b-163">**VMs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span></span>
* <span data-ttu-id="0cc4b-164">**Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span><span class="sxs-lookup"><span data-stu-id="0cc4b-164">**Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span></span>

<span data-ttu-id="0cc4b-165">There are alternative approaches to retrieving the resource ID, including using Azure Resource Explorer, viewing the desired resource in the Azure portal, and via PowerShell or the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-165">There are alternative approaches to retrieving the resource ID, including using Azure Resource Explorer, viewing the desired resource in the Azure portal, and via PowerShell or the Azure CLI.</span></span>

### <a name="azure-resource-explorer"></a><span data-ttu-id="0cc4b-166">Azure Resource Explorer</span><span class="sxs-lookup"><span data-stu-id="0cc4b-166">Azure Resource Explorer</span></span>
<span data-ttu-id="0cc4b-167">To find the resource ID for a desired resource, one helpful approach is to use the [Azure Resource Explorer](https://resources.azure.com) tool.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-167">To find the resource ID for a desired resource, one helpful approach is to use the [Azure Resource Explorer](https://resources.azure.com) tool.</span></span> <span data-ttu-id="0cc4b-168">Navigate to the desired resource and then look at the ID shown, as in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="0cc4b-168">Navigate to the desired resource and then look at the ID shown, as in the following screenshot:</span></span>

![Alt "Azure Resource Explorer"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a><span data-ttu-id="0cc4b-170">Azure portal</span><span class="sxs-lookup"><span data-stu-id="0cc4b-170">Azure portal</span></span>
<span data-ttu-id="0cc4b-171">The resource ID can also be obtained from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-171">The resource ID can also be obtained from the Azure portal.</span></span> <span data-ttu-id="0cc4b-172">To do so, navigate to the desired resource and then select Properties.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-172">To do so, navigate to the desired resource and then select Properties.</span></span> <span data-ttu-id="0cc4b-173">The Resource ID is displayed in the Properties blade, as seen in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="0cc4b-173">The Resource ID is displayed in the Properties blade, as seen in the following screenshot:</span></span>

![Alt "Resource ID displayed in the Properties blade in the Azure portal"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a><span data-ttu-id="0cc4b-175">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0cc4b-175">Azure PowerShell</span></span>
<span data-ttu-id="0cc4b-176">The resource ID can be retrieved using Azure PowerShell cmdlets as well.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-176">The resource ID can be retrieved using Azure PowerShell cmdlets as well.</span></span> <span data-ttu-id="0cc4b-177">For example, to obtain the resource ID for an Azure Web App, execute the Get-AzureRmWebApp cmdlet, as in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="0cc4b-177">For example, to obtain the resource ID for an Azure Web App, execute the Get-AzureRmWebApp cmdlet, as in the following screenshot:</span></span>

![Alt "Resource ID obtained via PowerShell"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a><span data-ttu-id="0cc4b-179">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0cc4b-179">Azure CLI</span></span>
<span data-ttu-id="0cc4b-180">To retrieve the resource ID using the Azure CLI, execute the 'azure webapp show' command, specifying the '--json' option, as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="0cc4b-180">To retrieve the resource ID using the Azure CLI, execute the 'azure webapp show' command, specifying the '--json' option, as shown in the following screenshot:</span></span>

![Alt "Resource ID obtained via PowerShell"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a><span data-ttu-id="0cc4b-182">Retrieve Activity Log Data</span><span class="sxs-lookup"><span data-stu-id="0cc4b-182">Retrieve Activity Log Data</span></span>
<span data-ttu-id="0cc4b-183">In addition to working with metric definitions and related values, it is also possible to retrieve additional interesting insights related to Azure resources.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-183">In addition to working with metric definitions and related values, it is also possible to retrieve additional interesting insights related to Azure resources.</span></span> <span data-ttu-id="0cc4b-184">As an example, it is possible to query [activity log](https://msdn.microsoft.com/library/azure/dn931934.aspx) data.</span><span class="sxs-lookup"><span data-stu-id="0cc4b-184">As an example, it is possible to query [activity log](https://msdn.microsoft.com/library/azure/dn931934.aspx) data.</span></span> <span data-ttu-id="0cc4b-185">The following sample demonstrates using the Azure Monitor REST API to query activity log data within a specific date range for an Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="0cc4b-185">The following sample demonstrates using the Azure Monitor REST API to query activity log data within a specific date range for an Azure subscription:</span></span>

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a><span data-ttu-id="0cc4b-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="0cc4b-186">Next steps</span></span>
* <span data-ttu-id="0cc4b-187">Review the [Overview of Monitoring](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0cc4b-187">Review the [Overview of Monitoring](monitoring-overview.md).</span></span>
* <span data-ttu-id="0cc4b-188">View the [Supported metrics with Azure Monitor](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0cc4b-188">View the [Supported metrics with Azure Monitor](monitoring-supported-metrics.md).</span></span>
* <span data-ttu-id="0cc4b-189">Review the [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cc4b-189">Review the [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>
* <span data-ttu-id="0cc4b-190">Review the [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cc4b-190">Review the [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>







