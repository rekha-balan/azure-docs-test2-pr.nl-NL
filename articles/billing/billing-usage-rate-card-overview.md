---
title: Azure Billing APIs | Microsoft Docs
description: Learn about Azure Billing Usage and RateCard APIs, which are used to provide insights into Azure resource consumption and trends.
services: ''
documentationcenter: ''
author: BryanLa
manager: ruchic
editor: ''
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 03/25/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: 869734ad4eb2d7a408cc0d33d1492b50b1b8dc0f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554035"
---
# <a name="use-azure-billing-apis-to-programmatically-get-insight-into-your-azure-usage"></a><span data-ttu-id="c02c9-103">Use Azure Billing APIs to programmatically get insight into your Azure usage</span><span class="sxs-lookup"><span data-stu-id="c02c9-103">Use Azure Billing APIs to programmatically get insight into your Azure usage</span></span>
<span data-ttu-id="c02c9-104">Use Azure Billing APIs to pull usage and resource data into your preferred data analysis tools.</span><span class="sxs-lookup"><span data-stu-id="c02c9-104">Use Azure Billing APIs to pull usage and resource data into your preferred data analysis tools.</span></span> <span data-ttu-id="c02c9-105">The Azure Resource Usage and RateCard APIs can help you accurately predict and manage your costs.</span><span class="sxs-lookup"><span data-stu-id="c02c9-105">The Azure Resource Usage and RateCard APIs can help you accurately predict and manage your costs.</span></span> <span data-ttu-id="c02c9-106">The APIs are implemented as a Resource Provider and part of the family of APIs exposed by the Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c02c9-106">The APIs are implemented as a Resource Provider and part of the family of APIs exposed by the Azure Resource Manager.</span></span>  

## <a name="azure-resource-usage-api-preview"></a><span data-ttu-id="c02c9-107">Azure Resource Usage API (Preview)</span><span class="sxs-lookup"><span data-stu-id="c02c9-107">Azure Resource Usage API (Preview)</span></span>
<span data-ttu-id="c02c9-108">Use the Azure Resource Usage API to get your estimated Azure consumption data.</span><span class="sxs-lookup"><span data-stu-id="c02c9-108">Use the Azure Resource Usage API to get your estimated Azure consumption data.</span></span> <span data-ttu-id="c02c9-109">The API includes:</span><span class="sxs-lookup"><span data-stu-id="c02c9-109">The API includes:</span></span>

* <span data-ttu-id="c02c9-110">**Azure Role-based Access Control** - Configure access policies on the [Azure portal](https://portal.azure.com) or through [Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs) to specify which users or applications can get access to the subscription’s usage data.</span><span class="sxs-lookup"><span data-stu-id="c02c9-110">**Azure Role-based Access Control** - Configure access policies on the [Azure portal](https://portal.azure.com) or through [Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs) to specify which users or applications can get access to the subscription’s usage data.</span></span> <span data-ttu-id="c02c9-111">Callers must use standard Azure Active Directory tokens for authentication.</span><span class="sxs-lookup"><span data-stu-id="c02c9-111">Callers must use standard Azure Active Directory tokens for authentication.</span></span> <span data-ttu-id="c02c9-112">Add the caller to either the Reader, Owner, or Contributor role to get access to the usage data for a specific Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c02c9-112">Add the caller to either the Reader, Owner, or Contributor role to get access to the usage data for a specific Azure subscription.</span></span>
* <span data-ttu-id="c02c9-113">**Hourly or Daily Aggregations** - Callers can specify whether they want their Azure usage data in hourly buckets or daily buckets.</span><span class="sxs-lookup"><span data-stu-id="c02c9-113">**Hourly or Daily Aggregations** - Callers can specify whether they want their Azure usage data in hourly buckets or daily buckets.</span></span> <span data-ttu-id="c02c9-114">The default is daily.</span><span class="sxs-lookup"><span data-stu-id="c02c9-114">The default is daily.</span></span>
* <span data-ttu-id="c02c9-115">**Instance metadata (includes resource tags)** – Get instance-level detail like the fully qualified resource uri (/subscriptions/{subscription-id}/..), the resource group information, and resource tags.</span><span class="sxs-lookup"><span data-stu-id="c02c9-115">**Instance metadata (includes resource tags)** – Get instance-level detail like the fully qualified resource uri (/subscriptions/{subscription-id}/..), the resource group information, and resource tags.</span></span> <span data-ttu-id="c02c9-116">This metadata helps you deterministically and programmatically allocate usage by the tags, for use-cases like cross-charging.</span><span class="sxs-lookup"><span data-stu-id="c02c9-116">This metadata helps you deterministically and programmatically allocate usage by the tags, for use-cases like cross-charging.</span></span>
* <span data-ttu-id="c02c9-117">**Resource metadata** - Resource details such as the meter name, meter category, meter sub category, unit, and region give the caller a better understanding of what was consumed.</span><span class="sxs-lookup"><span data-stu-id="c02c9-117">**Resource metadata** - Resource details such as the meter name, meter category, meter sub category, unit, and region give the caller a better understanding of what was consumed.</span></span> <span data-ttu-id="c02c9-118">We're also working to align resource metadata terminology across the Azure portal, Azure usage CSV, EA billing CSV, and other public-facing experiences, to let you correlate data across experiences.</span><span class="sxs-lookup"><span data-stu-id="c02c9-118">We're also working to align resource metadata terminology across the Azure portal, Azure usage CSV, EA billing CSV, and other public-facing experiences, to let you correlate data across experiences.</span></span>
* <span data-ttu-id="c02c9-119">**Usage for all offer types** – Usage data is available for all offer types like Pay-as-you-go, MSDN, Monetary commitment, Monetary credit, and EA.</span><span class="sxs-lookup"><span data-stu-id="c02c9-119">**Usage for all offer types** – Usage data is available for all offer types like Pay-as-you-go, MSDN, Monetary commitment, Monetary credit, and EA.</span></span>

## <a name="azure-resource-ratecard-api-preview"></a><span data-ttu-id="c02c9-120">Azure Resource RateCard API (Preview)</span><span class="sxs-lookup"><span data-stu-id="c02c9-120">Azure Resource RateCard API (Preview)</span></span>
<span data-ttu-id="c02c9-121">Use the Azure Resource RateCard API to get the list of available Azure resources and estimated pricing information for each.</span><span class="sxs-lookup"><span data-stu-id="c02c9-121">Use the Azure Resource RateCard API to get the list of available Azure resources and estimated pricing information for each.</span></span> <span data-ttu-id="c02c9-122">The API includes:</span><span class="sxs-lookup"><span data-stu-id="c02c9-122">The API includes:</span></span>

* <span data-ttu-id="c02c9-123">**Azure Role-based Access Control** - Configure your access policies on the [Azure portal](https://portal.azure.com) or through [Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs) to specify which users or applications can get access to the RateCard data.</span><span class="sxs-lookup"><span data-stu-id="c02c9-123">**Azure Role-based Access Control** - Configure your access policies on the [Azure portal](https://portal.azure.com) or through [Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs) to specify which users or applications can get access to the RateCard data.</span></span> <span data-ttu-id="c02c9-124">Callers must use standard Azure Active Directory tokens for authentication.</span><span class="sxs-lookup"><span data-stu-id="c02c9-124">Callers must use standard Azure Active Directory tokens for authentication.</span></span> <span data-ttu-id="c02c9-125">Add the caller to either the Reader, Owner, or Contributor role to get access to the usage data for a particular Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c02c9-125">Add the caller to either the Reader, Owner, or Contributor role to get access to the usage data for a particular Azure subscription.</span></span>
* <span data-ttu-id="c02c9-126">**Support for Pay-as-you-go, MSDN, Monetary commitment, and Monetary credit offers (EA not supported)** - This API provides Azure offer-level rate information.</span><span class="sxs-lookup"><span data-stu-id="c02c9-126">**Support for Pay-as-you-go, MSDN, Monetary commitment, and Monetary credit offers (EA not supported)** - This API provides Azure offer-level rate information.</span></span>  <span data-ttu-id="c02c9-127">The caller of this API must pass in the offer information to get resource details and rates.</span><span class="sxs-lookup"><span data-stu-id="c02c9-127">The caller of this API must pass in the offer information to get resource details and rates.</span></span> <span data-ttu-id="c02c9-128">We're currently unable to provide EA rates because EA offers have customized rates per enrollment.</span><span class="sxs-lookup"><span data-stu-id="c02c9-128">We're currently unable to provide EA rates because EA offers have customized rates per enrollment.</span></span> 

## <a name="scenarios"></a><span data-ttu-id="c02c9-129">Scenarios</span><span class="sxs-lookup"><span data-stu-id="c02c9-129">Scenarios</span></span>
<span data-ttu-id="c02c9-130">Here are some of the scenarios that are made possible with the combination of the Usage and the RateCard APIs:</span><span class="sxs-lookup"><span data-stu-id="c02c9-130">Here are some of the scenarios that are made possible with the combination of the Usage and the RateCard APIs:</span></span>

* <span data-ttu-id="c02c9-131">**Azure spend during the month** - Use the combination of the Usage and RateCard APIs to get better insights into your cloud spend during the month.</span><span class="sxs-lookup"><span data-stu-id="c02c9-131">**Azure spend during the month** - Use the combination of the Usage and RateCard APIs to get better insights into your cloud spend during the month.</span></span> <span data-ttu-id="c02c9-132">You can analyze the hourly and daily buckets of usage and charge estimates.</span><span class="sxs-lookup"><span data-stu-id="c02c9-132">You can analyze the hourly and daily buckets of usage and charge estimates.</span></span>
* <span data-ttu-id="c02c9-133">**Set up alerts** – Use the Usage and the RateCard APIs to get estimated cloud consumption and charges, and set up resource-based or monetary-based alerts.</span><span class="sxs-lookup"><span data-stu-id="c02c9-133">**Set up alerts** – Use the Usage and the RateCard APIs to get estimated cloud consumption and charges, and set up resource-based or monetary-based alerts.</span></span>
* <span data-ttu-id="c02c9-134">**Predict bill** – Get your estimated consumption and cloud spend, and apply machine learning algorithms to predict what the bill would be at the end of the billing cycle.</span><span class="sxs-lookup"><span data-stu-id="c02c9-134">**Predict bill** – Get your estimated consumption and cloud spend, and apply machine learning algorithms to predict what the bill would be at the end of the billing cycle.</span></span>
* <span data-ttu-id="c02c9-135">**Pre-consumption cost analysis** – Use the RateCard API to predict how much your bill would be for your expected usage when you move your workloads to Azure.</span><span class="sxs-lookup"><span data-stu-id="c02c9-135">**Pre-consumption cost analysis** – Use the RateCard API to predict how much your bill would be for your expected usage when you move your workloads to Azure.</span></span> <span data-ttu-id="c02c9-136">If you have existing workloads in other clouds or private clouds, you can also map your usage with the Azure rates to get a better estimate of Azure spend.</span><span class="sxs-lookup"><span data-stu-id="c02c9-136">If you have existing workloads in other clouds or private clouds, you can also map your usage with the Azure rates to get a better estimate of Azure spend.</span></span> <span data-ttu-id="c02c9-137">This estimate gives you the ability to pivot on offer, and compare and contrast between the different offer types beyond Pay-As-You-Go, like Monetary commitment and Monetary credit.</span><span class="sxs-lookup"><span data-stu-id="c02c9-137">This estimate gives you the ability to pivot on offer, and compare and contrast between the different offer types beyond Pay-As-You-Go, like Monetary commitment and Monetary credit.</span></span> <span data-ttu-id="c02c9-138">The API also gives you the ability to see cost differences by region and allows you to do a what-if cost analysis to help you make deployment decisions.</span><span class="sxs-lookup"><span data-stu-id="c02c9-138">The API also gives you the ability to see cost differences by region and allows you to do a what-if cost analysis to help you make deployment decisions.</span></span>
* <span data-ttu-id="c02c9-139">**What-if analysis** -</span><span class="sxs-lookup"><span data-stu-id="c02c9-139">**What-if analysis** -</span></span>
  
  * <span data-ttu-id="c02c9-140">You can determine whether it is more cost-effective to run workloads in another region, or on another configuration of the Azure resource.</span><span class="sxs-lookup"><span data-stu-id="c02c9-140">You can determine whether it is more cost-effective to run workloads in another region, or on another configuration of the Azure resource.</span></span> <span data-ttu-id="c02c9-141">Azure resource costs may differ based on the Azure region you're using.</span><span class="sxs-lookup"><span data-stu-id="c02c9-141">Azure resource costs may differ based on the Azure region you're using.</span></span>
  * <span data-ttu-id="c02c9-142">You can also determine if another Azure offer type gives a better rate on an Azure resource.</span><span class="sxs-lookup"><span data-stu-id="c02c9-142">You can also determine if another Azure offer type gives a better rate on an Azure resource.</span></span>

## <a name="partner-solutions"></a><span data-ttu-id="c02c9-143">Partner solutions</span><span class="sxs-lookup"><span data-stu-id="c02c9-143">Partner solutions</span></span>
<span data-ttu-id="c02c9-144">[Microsoft Azure Usage and RateCard APIs Enable Cloudyn to Provide ITFM for Customers](billing-usage-rate-card-partner-solution-cloudyn.md) describes the integration experience offered by Azure Billing API partner [Cloudyn](https://www.cloudyn.com/microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="c02c9-144">[Microsoft Azure Usage and RateCard APIs Enable Cloudyn to Provide ITFM for Customers](billing-usage-rate-card-partner-solution-cloudyn.md) describes the integration experience offered by Azure Billing API partner [Cloudyn](https://www.cloudyn.com/microsoft-azure/).</span></span> <span data-ttu-id="c02c9-145">This article talks about their experiences and includes a video that shows how you can use Cloudyn and the Azure Billing APIs to get insights from Azure consumption data.</span><span class="sxs-lookup"><span data-stu-id="c02c9-145">This article talks about their experiences and includes a video that shows how you can use Cloudyn and the Azure Billing APIs to get insights from Azure consumption data.</span></span>

<span data-ttu-id="c02c9-146">[Cloud Cruiser and Microsoft Azure Billing API Integration](billing-usage-rate-card-partner-solution-cloudcruiser.md) describes how [Cloud Cruiser's Express for Azure Pack](http://www.cloudcruiser.com/partners/microsoft/) works directly from the Windows Azure Pack (WAP) portal.</span><span class="sxs-lookup"><span data-stu-id="c02c9-146">[Cloud Cruiser and Microsoft Azure Billing API Integration](billing-usage-rate-card-partner-solution-cloudcruiser.md) describes how [Cloud Cruiser's Express for Azure Pack](http://www.cloudcruiser.com/partners/microsoft/) works directly from the Windows Azure Pack (WAP) portal.</span></span> <span data-ttu-id="c02c9-147">You can seamlessly manage both the operational and financial aspects of the Microsoft Azure private or hosted public cloud from a single user interface.</span><span class="sxs-lookup"><span data-stu-id="c02c9-147">You can seamlessly manage both the operational and financial aspects of the Microsoft Azure private or hosted public cloud from a single user interface.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="c02c9-148">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c02c9-148">Next Steps</span></span>
* <span data-ttu-id="c02c9-149">Check out the [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) for more details on both APIs.</span><span class="sxs-lookup"><span data-stu-id="c02c9-149">Check out the [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) for more details on both APIs.</span></span>
* <span data-ttu-id="c02c9-150">If you would like to dive right into the sample code, check out our Microsoft Azure Billing API Code Samples on [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?term=billing).</span><span class="sxs-lookup"><span data-stu-id="c02c9-150">If you would like to dive right into the sample code, check out our Microsoft Azure Billing API Code Samples on [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?term=billing).</span></span>

## <a name="learn-more"></a><span data-ttu-id="c02c9-151">Learn more</span><span class="sxs-lookup"><span data-stu-id="c02c9-151">Learn more</span></span>
* <span data-ttu-id="c02c9-152">See the [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c02c9-152">See the [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="c02c9-153">For more information on the suite of tools necessary to help you get an understanding of cloud spend, see the Gartner article [Market Guide for IT Financial Management (ITFM) Tools](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).</span><span class="sxs-lookup"><span data-stu-id="c02c9-153">For more information on the suite of tools necessary to help you get an understanding of cloud spend, see the Gartner article [Market Guide for IT Financial Management (ITFM) Tools](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).</span></span>
