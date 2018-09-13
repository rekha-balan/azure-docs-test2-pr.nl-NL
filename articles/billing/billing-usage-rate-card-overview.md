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
# <a name="use-azure-billing-apis-to-programmatically-get-insight-into-your-azure-usage"></a>Use Azure Billing APIs to programmatically get insight into your Azure usage
Use Azure Billing APIs to pull usage and resource data into your preferred data analysis tools. The Azure Resource Usage and RateCard APIs can help you accurately predict and manage your costs. The APIs are implemented as a Resource Provider and part of the family of APIs exposed by the Azure Resource Manager.  

## <a name="azure-resource-usage-api-preview"></a>Azure Resource Usage API (Preview)
Use the Azure Resource Usage API to get your estimated Azure consumption data. The API includes:

* **Azure Role-based Access Control** - Configure access policies on the [Azure portal](https://portal.azure.com) or through [Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs) to specify which users or applications can get access to the subscription’s usage data. Callers must use standard Azure Active Directory tokens for authentication. Add the caller to either the Reader, Owner, or Contributor role to get access to the usage data for a specific Azure subscription.
* **Hourly or Daily Aggregations** - Callers can specify whether they want their Azure usage data in hourly buckets or daily buckets. The default is daily.
* **Instance metadata (includes resource tags)** – Get instance-level detail like the fully qualified resource uri (/subscriptions/{subscription-id}/..), the resource group information, and resource tags. This metadata helps you deterministically and programmatically allocate usage by the tags, for use-cases like cross-charging.
* **Resource metadata** - Resource details such as the meter name, meter category, meter sub category, unit, and region give the caller a better understanding of what was consumed. We're also working to align resource metadata terminology across the Azure portal, Azure usage CSV, EA billing CSV, and other public-facing experiences, to let you correlate data across experiences.
* **Usage for all offer types** – Usage data is available for all offer types like Pay-as-you-go, MSDN, Monetary commitment, Monetary credit, and EA.

## <a name="azure-resource-ratecard-api-preview"></a>Azure Resource RateCard API (Preview)
Use the Azure Resource RateCard API to get the list of available Azure resources and estimated pricing information for each. The API includes:

* **Azure Role-based Access Control** - Configure your access policies on the [Azure portal](https://portal.azure.com) or through [Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs) to specify which users or applications can get access to the RateCard data. Callers must use standard Azure Active Directory tokens for authentication. Add the caller to either the Reader, Owner, or Contributor role to get access to the usage data for a particular Azure subscription.
* **Support for Pay-as-you-go, MSDN, Monetary commitment, and Monetary credit offers (EA not supported)** - This API provides Azure offer-level rate information.  The caller of this API must pass in the offer information to get resource details and rates. We're currently unable to provide EA rates because EA offers have customized rates per enrollment. 

## <a name="scenarios"></a>Scenarios
Here are some of the scenarios that are made possible with the combination of the Usage and the RateCard APIs:

* **Azure spend during the month** - Use the combination of the Usage and RateCard APIs to get better insights into your cloud spend during the month. You can analyze the hourly and daily buckets of usage and charge estimates.
* **Set up alerts** – Use the Usage and the RateCard APIs to get estimated cloud consumption and charges, and set up resource-based or monetary-based alerts.
* **Predict bill** – Get your estimated consumption and cloud spend, and apply machine learning algorithms to predict what the bill would be at the end of the billing cycle.
* **Pre-consumption cost analysis** – Use the RateCard API to predict how much your bill would be for your expected usage when you move your workloads to Azure. If you have existing workloads in other clouds or private clouds, you can also map your usage with the Azure rates to get a better estimate of Azure spend. This estimate gives you the ability to pivot on offer, and compare and contrast between the different offer types beyond Pay-As-You-Go, like Monetary commitment and Monetary credit. The API also gives you the ability to see cost differences by region and allows you to do a what-if cost analysis to help you make deployment decisions.
* **What-if analysis** -
  
  * You can determine whether it is more cost-effective to run workloads in another region, or on another configuration of the Azure resource. Azure resource costs may differ based on the Azure region you're using.
  * You can also determine if another Azure offer type gives a better rate on an Azure resource.

## <a name="partner-solutions"></a>Partner solutions
[Microsoft Azure Usage and RateCard APIs Enable Cloudyn to Provide ITFM for Customers](billing-usage-rate-card-partner-solution-cloudyn.md) describes the integration experience offered by Azure Billing API partner [Cloudyn](https://www.cloudyn.com/microsoft-azure/). This article talks about their experiences and includes a video that shows how you can use Cloudyn and the Azure Billing APIs to get insights from Azure consumption data.

[Cloud Cruiser and Microsoft Azure Billing API Integration](billing-usage-rate-card-partner-solution-cloudcruiser.md) describes how [Cloud Cruiser's Express for Azure Pack](http://www.cloudcruiser.com/partners/microsoft/) works directly from the Windows Azure Pack (WAP) portal. You can seamlessly manage both the operational and financial aspects of the Microsoft Azure private or hosted public cloud from a single user interface.   

## <a name="next-steps"></a>Next Steps
* Check out the [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) for more details on both APIs.
* If you would like to dive right into the sample code, check out our Microsoft Azure Billing API Code Samples on [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?term=billing).

## <a name="learn-more"></a>Learn more
* See the [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).
* For more information on the suite of tools necessary to help you get an understanding of cloud spend, see the Gartner article [Market Guide for IT Financial Management (ITFM) Tools](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

