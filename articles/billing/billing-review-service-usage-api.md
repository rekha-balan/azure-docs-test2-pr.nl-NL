---
title: Review Azure service resource usage with REST API | Microsoft Docs
description: Learn how to use Azure REST APIs to review Azure service resource usage.
services: billing
documentationcenter: na
author: lleonard-msft
manager: MBaldwin
editor: ''
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2018
ms.author: alleonar
ms.openlocfilehash: 2af87c87916dd272026a3bd7e1438507c655053b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864630"
---
# <a name="review-azure-resource-usage-using-the-rest-api"></a><span data-ttu-id="5c519-103">Review Azure resource usage using the REST API</span><span class="sxs-lookup"><span data-stu-id="5c519-103">Review Azure resource usage using the REST API</span></span>

<span data-ttu-id="5c519-104">Azure Cost Management APIs help you review and manage consumption of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="5c519-104">Azure Cost Management APIs help you review and manage consumption of your Azure resources.</span></span>

<span data-ttu-id="5c519-105">In this article, you learn how to create a daily report that will generate a comma-separated value document with your hourly usage information, and then how to use filters to customize the report so that you can query the usage of virtual machines, databases, and tagged resources in an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="5c519-105">In this article, you learn how to create a daily report that will generate a comma-separated value document with your hourly usage information, and then how to use filters to customize the report so that you can query the usage of virtual machines, databases, and tagged resources in an Azure resource group.</span></span>

>[!NOTE]
> <span data-ttu-id="5c519-106">The Cost Management API is currently in private preview.</span><span class="sxs-lookup"><span data-stu-id="5c519-106">The Cost Management API is currently in private preview.</span></span>

## <a name="create-a-basic-cost-management-report"></a><span data-ttu-id="5c519-107">Create a basic cost management report</span><span class="sxs-lookup"><span data-stu-id="5c519-107">Create a basic cost management report</span></span>

<span data-ttu-id="5c519-108">Use the `reports` operation in the Cost Management API to define how the cost reporting is generated and where the reports will be published to.</span><span class="sxs-lookup"><span data-stu-id="5c519-108">Use the `reports` operation in the Cost Management API to define how the cost reporting is generated and where the reports will be published to.</span></span>

```http
https://management.azure.com/subscriptions/{subscriptionGuid}/providers/Microsoft.CostManagement/reports/{reportName}?api-version=2018-09-01-preview
Content-Type: application/json   
Authorization: Bearer
```

<span data-ttu-id="5c519-109">The `{subscriptionGuid}` parameter is required and should contain a subscription ID that can be read using the credentials provieed in the API token.</span><span class="sxs-lookup"><span data-stu-id="5c519-109">The `{subscriptionGuid}` parameter is required and should contain a subscription ID that can be read using the credentials provieed in the API token.</span></span> <span data-ttu-id="5c519-110">The `{reportName}`</span><span class="sxs-lookup"><span data-stu-id="5c519-110">The `{reportName}`</span></span>

<span data-ttu-id="5c519-111">The following headers are required:</span><span class="sxs-lookup"><span data-stu-id="5c519-111">The following headers are required:</span></span> 

|<span data-ttu-id="5c519-112">Request header</span><span class="sxs-lookup"><span data-stu-id="5c519-112">Request header</span></span>|<span data-ttu-id="5c519-113">Description</span><span class="sxs-lookup"><span data-stu-id="5c519-113">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="5c519-114">*Content-Type:*</span><span class="sxs-lookup"><span data-stu-id="5c519-114">*Content-Type:*</span></span>| <span data-ttu-id="5c519-115">Required.</span><span class="sxs-lookup"><span data-stu-id="5c519-115">Required.</span></span> <span data-ttu-id="5c519-116">Set to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="5c519-116">Set to `application/json`.</span></span> |  
|<span data-ttu-id="5c519-117">*Authorization:*</span><span class="sxs-lookup"><span data-stu-id="5c519-117">*Authorization:*</span></span>| <span data-ttu-id="5c519-118">Required.</span><span class="sxs-lookup"><span data-stu-id="5c519-118">Required.</span></span> <span data-ttu-id="5c519-119">Set to a valid `Bearer` token.</span><span class="sxs-lookup"><span data-stu-id="5c519-119">Set to a valid `Bearer` token.</span></span> |

<span data-ttu-id="5c519-120">Configure the parameters of the report in the HTTP request body.</span><span class="sxs-lookup"><span data-stu-id="5c519-120">Configure the parameters of the report in the HTTP request body.</span></span> <span data-ttu-id="5c519-121">In the example below, the report is set to generate every day when active, is a CSV file written to an Azure Storage blob container, and contains hourly cost information for all resources in resource group `westus`.</span><span class="sxs-lookup"><span data-stu-id="5c519-121">In the example below, the report is set to generate every day when active, is a CSV file written to an Azure Storage blob container, and contains hourly cost information for all resources in resource group `westus`.</span></span>

```json
{
    "properties": {
        "schedule": {
            "status": "Inactive",
            "recurrence": "Daily",
            "recurrencePeriod": {
                "from": "2018-08-21",
                "to": "2019-10-31"
            }
        },
        "deliveryInfo": {
            "destination": {
                "resourceId": "/subscriptions/{subscriptionGuid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}",
                "container": "MyReportContainer",
                "rootFolderPath": "MyScheduleTest"
            }
        },
        "format": "Csv",
        "definition": {
            "type": "Usage",
            "timeframe": "MonthToDate",
            "dataSet": {
                "granularity": "Hourly",
                "filter": {
                    "dimensions": {
                        "name": "ResourceLocation",
                        "operator": "In",
                        "values": [
                            "westus"
                        ]
                    }
                }
            }
        }
    }
}
```

<span data-ttu-id="5c519-122">The</span><span class="sxs-lookup"><span data-stu-id="5c519-122">The</span></span>

## <a name="filtering-reports"></a><span data-ttu-id="5c519-123">Filtering reports</span><span class="sxs-lookup"><span data-stu-id="5c519-123">Filtering reports</span></span>

<span data-ttu-id="5c519-124">The `filter` and `dimensions` section of the request body when creating a report let you focus in on the costs for specific resource types.</span><span class="sxs-lookup"><span data-stu-id="5c519-124">The `filter` and `dimensions` section of the request body when creating a report let you focus in on the costs for specific resource types.</span></span> <span data-ttu-id="5c519-125">The previous request body shows how to filter by all resources in a region.</span><span class="sxs-lookup"><span data-stu-id="5c519-125">The previous request body shows how to filter by all resources in a region.</span></span> 

### <a name="get-all-compute-usage"></a><span data-ttu-id="5c519-126">Get all compute usage</span><span class="sxs-lookup"><span data-stu-id="5c519-126">Get all compute usage</span></span>

<span data-ttu-id="5c519-127">Use the `ResourceType` dimension to report Azure virtual machine costs in your subscription across all regions.</span><span class="sxs-lookup"><span data-stu-id="5c519-127">Use the `ResourceType` dimension to report Azure virtual machine costs in your subscription across all regions.</span></span>

```json
"filter": {
    "dimensions": {
        "name": "ResourceType",
        "operator": "In",
        "values": [
                "Microsoft.ClassicCompute/virtualMachines", 
                "Microsoft.Compute/virtualMachines"
        ] 
    }
}
```

### <a name="get-all-database-usage"></a><span data-ttu-id="5c519-128">Get all database usage</span><span class="sxs-lookup"><span data-stu-id="5c519-128">Get all database usage</span></span>

<span data-ttu-id="5c519-129">Use the `ResourceType` dimension to report Azure SQL Database costs in your subscription across all regions.</span><span class="sxs-lookup"><span data-stu-id="5c519-129">Use the `ResourceType` dimension to report Azure SQL Database costs in your subscription across all regions.</span></span>

```json
"filter": {
    "dimensions": {
        "name": "ResourceType",
        "operator": "In",
        "values": [
                "Microsoft.Sql/servers"
        ] 
    }
}
```

### <a name="report-on-specific-instances"></a><span data-ttu-id="5c519-130">Report on specific instances</span><span class="sxs-lookup"><span data-stu-id="5c519-130">Report on specific instances</span></span>

<span data-ttu-id="5c519-131">The `Resource` dimension lets you report costs for specific resources.</span><span class="sxs-lookup"><span data-stu-id="5c519-131">The `Resource` dimension lets you report costs for specific resources.</span></span>

```json
"filter": {
    "dimensions": {
        "name": "Resource",
        "operator": "In",
        "values": [
            "subscriptions/{subscriptionGuid}/resourceGroups/{resourceGroup}/providers/Microsoft.ClassicCompute/virtualMachines/{ResourceName}"
        ]
    }
}
```

### <a name="changing-timeframes"></a><span data-ttu-id="5c519-132">Changing timeframes</span><span class="sxs-lookup"><span data-stu-id="5c519-132">Changing timeframes</span></span>

<span data-ttu-id="5c519-133">Set the `timeframe` definition to `Custom` to set a timeframe outside of the  week to date and month to date bulit in options.</span><span class="sxs-lookup"><span data-stu-id="5c519-133">Set the `timeframe` definition to `Custom` to set a timeframe outside of the  week to date and month to date bulit in options.</span></span>

```json
"timeframe": "Custom",
"timePeriod": {
    "from": "2017-12-31T00:00:00.000Z",
    "to": "2018-12-30T00:00:00.000Z"
}
```

## <a name="next-steps"></a><span data-ttu-id="5c519-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="5c519-134">Next steps</span></span>
- [<span data-ttu-id="5c519-135">Get started with Azure REST API</span><span class="sxs-lookup"><span data-stu-id="5c519-135">Get started with Azure REST API</span></span>](https://docs.microsoft.com/rest/api/azure/)   
