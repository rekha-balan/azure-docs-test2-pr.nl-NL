---
title: Customer Billing And Chargeback In Azure Stack | Microsoft Docs
description: Learn how to retrieve resource usage information from Azure Stack.
services: azure-stack
documentationcenter: ''
author: AlfredoPizzirani
manager: byronr
editor: ''
ms.assetid: a9afc7b6-43da-437b-a853-aab73ff14113
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/08/2016
ms.author: alfredop
ms.openlocfilehash: b915985dedb572d595b3fd4a6a273c2f4f458fd6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662402"
---
# <a name="usage-and-billing-in-azure-stack"></a><span data-ttu-id="b514b-103">Usage and billing in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b514b-103">Usage and billing in Azure Stack</span></span>

<span data-ttu-id="b514b-104">Usage represents the quantity of resources consumed by a user.</span><span class="sxs-lookup"><span data-stu-id="b514b-104">Usage represents the quantity of resources consumed by a user.</span></span> <span data-ttu-id="b514b-105">Azure Stack collects usage information for each user and uses it to bill them.</span><span class="sxs-lookup"><span data-stu-id="b514b-105">Azure Stack collects usage information for each user and uses it to bill them.</span></span> <span data-ttu-id="b514b-106">This article describes how Azure Stack users are billed for resource usage, and how the billing information is accessed for analytics, chargeback, etc.</span><span class="sxs-lookup"><span data-stu-id="b514b-106">This article describes how Azure Stack users are billed for resource usage, and how the billing information is accessed for analytics, chargeback, etc.</span></span>

<span data-ttu-id="b514b-107">Azure Stack contains the infrastructure to collect and aggregate usage data for all resources.</span><span class="sxs-lookup"><span data-stu-id="b514b-107">Azure Stack contains the infrastructure to collect and aggregate usage data for all resources.</span></span> <span data-ttu-id="b514b-108">You can access this data and export it to a billing system by using a billing adapter, or export it to a business intelligence tool like Microsoft Power BI.</span><span class="sxs-lookup"><span data-stu-id="b514b-108">You can access this data and export it to a billing system by using a billing adapter, or export it to a business intelligence tool like Microsoft Power BI.</span></span> <span data-ttu-id="b514b-109">After exporting, this billing information is used for analytics or transferred to a chargeback system.</span><span class="sxs-lookup"><span data-stu-id="b514b-109">After exporting, this billing information is used for analytics or transferred to a chargeback system.</span></span>

![Conceptual model of a billing adapter connecting Azure Stack to a Billing application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-billing-and-chargeback/image1.png)

## <a name="what-usage-information-can-i-find-and-how"></a><span data-ttu-id="b514b-111">What usage information can I find, and how?</span><span class="sxs-lookup"><span data-stu-id="b514b-111">What usage information can I find, and how?</span></span>

<span data-ttu-id="b514b-112">Azure Stack Resource providers, such as Compute, Storage, and Network, generate usage data at hourly intervals for each subscription.</span><span class="sxs-lookup"><span data-stu-id="b514b-112">Azure Stack Resource providers, such as Compute, Storage, and Network, generate usage data at hourly intervals for each subscription.</span></span> <span data-ttu-id="b514b-113">The usage data contains information about the resource used such as resource name, meter name, meter ID, quantity used etc. To learn about the meters ID resources, refer to the [usage API FAQ](azure-stack-usage-related-faq.md) article.</span><span class="sxs-lookup"><span data-stu-id="b514b-113">The usage data contains information about the resource used such as resource name, meter name, meter ID, quantity used etc. To learn about the meters ID resources, refer to the [usage API FAQ](azure-stack-usage-related-faq.md) article.</span></span> 

<span data-ttu-id="b514b-114">After the usage data has been collected, it is [reported to Azure](azure-stack-usage-reporting.md) to generate a bill, which can be viewed through the Azure billing portal.</span><span class="sxs-lookup"><span data-stu-id="b514b-114">After the usage data has been collected, it is [reported to Azure](azure-stack-usage-reporting.md) to generate a bill, which can be viewed through the Azure billing portal.</span></span> <span data-ttu-id="b514b-115">The Azure billing portal shows the usage data only for the chargeable resources.</span><span class="sxs-lookup"><span data-stu-id="b514b-115">The Azure billing portal shows the usage data only for the chargeable resources.</span></span> <span data-ttu-id="b514b-116">In addition to the chargeable resources, Azure Stack captures usage data for a broader set of resources, which you can access in your Azure Stack environment through REST APIs or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b514b-116">In addition to the chargeable resources, Azure Stack captures usage data for a broader set of resources, which you can access in your Azure Stack environment through REST APIs or PowerShell.</span></span> <span data-ttu-id="b514b-117">Service administrators can retrieve the usage data for all tenant subscriptions whereas a tenant can get only their usage details.</span><span class="sxs-lookup"><span data-stu-id="b514b-117">Service administrators can retrieve the usage data for all tenant subscriptions whereas a tenant can get only their usage details.</span></span>

## <a name="retrieve-usage-information"></a><span data-ttu-id="b514b-118">Retrieve usage information</span><span class="sxs-lookup"><span data-stu-id="b514b-118">Retrieve usage information</span></span>

<span data-ttu-id="b514b-119">To generate the usage data, you should have resources that are running and actively using the system.</span><span class="sxs-lookup"><span data-stu-id="b514b-119">To generate the usage data, you should have resources that are running and actively using the system.</span></span> <span data-ttu-id="b514b-120">If you’re not sure whether you have any resources running in Azure Stack Marketplace, deploy a virtual machine (VM), and verify the VM monitoring blade to make sure it’s running.</span><span class="sxs-lookup"><span data-stu-id="b514b-120">If you’re not sure whether you have any resources running in Azure Stack Marketplace, deploy a virtual machine (VM), and verify the VM monitoring blade to make sure it’s running.</span></span> <span data-ttu-id="b514b-121">Use the following PowerShell cmdlets to view the usage data:</span><span class="sxs-lookup"><span data-stu-id="b514b-121">Use the following PowerShell cmdlets to view the usage data:</span></span>

1. [<span data-ttu-id="b514b-122">Install PowerShell for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b514b-122">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)
2. [<span data-ttu-id="b514b-123">Configure PowerShell and sign in to your Azure Stack administrator or user subscription.</span><span class="sxs-lookup"><span data-stu-id="b514b-123">Configure PowerShell and sign in to your Azure Stack administrator or user subscription.</span></span>](azure-stack-powershell-configure.md)
3. <span data-ttu-id="b514b-124">To retrieve the usage data, use the [Get-UsageAggregates](https://docs.microsoft.com/powershell/module/azurerm.usageaggregates/get-usageaggregates?view=azurermps-3.7.0) PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b514b-124">To retrieve the usage data, use the [Get-UsageAggregates](https://docs.microsoft.com/powershell/module/azurerm.usageaggregates/get-usageaggregates?view=azurermps-3.7.0) PowerShell cmdlet:</span></span>
   ```PowerShell
   Get-UsageAggregates -ReportedStartTime "<Start time for usage reporting>" -ReportedEndTime "<end time for usage reporting>" -AggregationGranularity <Hourly or Daily>
   ```

   <span data-ttu-id="b514b-125">If usage data is available, it’s returned in as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="b514b-125">If usage data is available, it’s returned in as shown in the following screenshot:</span></span> 
   
   ![Usage aggregates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-billing-and-chargeback/image2.png)
   
   <span data-ttu-id="b514b-127">PowerShell returns 1,000 lines of usage per call.</span><span class="sxs-lookup"><span data-stu-id="b514b-127">PowerShell returns 1,000 lines of usage per call.</span></span> <span data-ttu-id="b514b-128">You can use the continuation parameter to retrieve more than 1,000 lines</span><span class="sxs-lookup"><span data-stu-id="b514b-128">You can use the continuation parameter to retrieve more than 1,000 lines</span></span>

## <a name="next-steps"></a><span data-ttu-id="b514b-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="b514b-129">Next steps</span></span>

[<span data-ttu-id="b514b-130">Report Azure Stack usage data to Azure</span><span class="sxs-lookup"><span data-stu-id="b514b-130">Report Azure Stack usage data to Azure</span></span>](azure-stack-usage-reporting.md)

[<span data-ttu-id="b514b-131">Provider Resource Usage API</span><span class="sxs-lookup"><span data-stu-id="b514b-131">Provider Resource Usage API</span></span>](azure-stack-provider-resource-api.md)

[<span data-ttu-id="b514b-132">Tenant Resource Usage API</span><span class="sxs-lookup"><span data-stu-id="b514b-132">Tenant Resource Usage API</span></span>](azure-stack-tenant-resource-usage-api.md)

[<span data-ttu-id="b514b-133">Usage-related FAQ</span><span class="sxs-lookup"><span data-stu-id="b514b-133">Usage-related FAQ</span></span>](azure-stack-usage-related-faq.md)



