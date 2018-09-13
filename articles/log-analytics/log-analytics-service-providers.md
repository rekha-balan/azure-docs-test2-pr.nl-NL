---
title: Log Analytics Features for Service Providers | Microsoft Docs
description: Log Analytics can help Managed Service Providers (MSPs), Large Enterprises, Independent Sofware Vendors (ISVs) and hosting service providers manage and monitor servers in customer's on-premises or cloud infrastructure.
services: log-analytics
documentationcenter: ''
author: richrundmsft
manager: jochan
editor: ''
ms.assetid: c07f0b9f-ec37-480d-91ec-d9bcf6786464
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: richrund
ms.openlocfilehash: 8a67d9a9d345682e9e6c8f5c7779204a038f5f6a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661679"
---
# <a name="log-analytics-features-for-service-providers"></a><span data-ttu-id="64787-103">Log Analytics features for Service Providers</span><span class="sxs-lookup"><span data-stu-id="64787-103">Log Analytics features for Service Providers</span></span>
<span data-ttu-id="64787-104">Log Analytics can help managed service providers (MSPs), large enterprises, independent software vendors (ISVs), and hosting service providers manage and monitor servers in customer's on-premises or cloud infrastructure.</span><span class="sxs-lookup"><span data-stu-id="64787-104">Log Analytics can help managed service providers (MSPs), large enterprises, independent software vendors (ISVs), and hosting service providers manage and monitor servers in customer's on-premises or cloud infrastructure.</span></span> 

<span data-ttu-id="64787-105">Large enterprises share many similarities with service providers, particularly when there is a centralized IT team that is responsible for managing IT for many different business units.</span><span class="sxs-lookup"><span data-stu-id="64787-105">Large enterprises share many similarities with service providers, particularly when there is a centralized IT team that is responsible for managing IT for many different business units.</span></span> <span data-ttu-id="64787-106">For simplicity, this document uses the term *service provider* but the same functionality is also available for enterprises and other customers.</span><span class="sxs-lookup"><span data-stu-id="64787-106">For simplicity, this document uses the term *service provider* but the same functionality is also available for enterprises and other customers.</span></span>

## <a name="cloud-solution-provider"></a><span data-ttu-id="64787-107">Cloud Solution Provider</span><span class="sxs-lookup"><span data-stu-id="64787-107">Cloud Solution Provider</span></span>
<span data-ttu-id="64787-108">For partners and service providers who are part of the [Cloud Solution Provider (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) program, Log Analytics is one of the Azure services available on a CSP subscription.</span><span class="sxs-lookup"><span data-stu-id="64787-108">For partners and service providers who are part of the [Cloud Solution Provider (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) program, Log Analytics is one of the Azure services available on a CSP subscription.</span></span> 

<span data-ttu-id="64787-109">For Log Analytics, the following capabilities are enabled in *Cloud Solution Provider* subscriptions.</span><span class="sxs-lookup"><span data-stu-id="64787-109">For Log Analytics, the following capabilities are enabled in *Cloud Solution Provider* subscriptions.</span></span>

<span data-ttu-id="64787-110">As a *Cloud Solution Provider* you can:</span><span class="sxs-lookup"><span data-stu-id="64787-110">As a *Cloud Solution Provider* you can:</span></span>

* <span data-ttu-id="64787-111">Create Log Analytics workspaces in a tenant (customer's) subscription.</span><span class="sxs-lookup"><span data-stu-id="64787-111">Create Log Analytics workspaces in a tenant (customer's) subscription.</span></span>
* <span data-ttu-id="64787-112">Access workspaces created by tenants.</span><span class="sxs-lookup"><span data-stu-id="64787-112">Access workspaces created by tenants.</span></span> 
* <span data-ttu-id="64787-113">Add and remove user access to the workspace using Azure user management.</span><span class="sxs-lookup"><span data-stu-id="64787-113">Add and remove user access to the workspace using Azure user management.</span></span> <span data-ttu-id="64787-114">When in a tenant’s workspace in the OMS portal the user management page under Settings is not available</span><span class="sxs-lookup"><span data-stu-id="64787-114">When in a tenant’s workspace in the OMS portal the user management page under Settings is not available</span></span>
  * <span data-ttu-id="64787-115">Log Analytics does not support role-based access yet - giving a user `reader` permission in the Azure portal allows them to make configuration changes in the OMS portal</span><span class="sxs-lookup"><span data-stu-id="64787-115">Log Analytics does not support role-based access yet - giving a user `reader` permission in the Azure portal allows them to make configuration changes in the OMS portal</span></span>

<span data-ttu-id="64787-116">To log in to a tenant’s subscription, you need to specify the tenant identifier.</span><span class="sxs-lookup"><span data-stu-id="64787-116">To log in to a tenant’s subscription, you need to specify the tenant identifier.</span></span> <span data-ttu-id="64787-117">The tenant identifier is often that last part of the e-mail address used to sign in.</span><span class="sxs-lookup"><span data-stu-id="64787-117">The tenant identifier is often that last part of the e-mail address used to sign in.</span></span>

* <span data-ttu-id="64787-118">In the OMS portal, add `?tenant=contoso.com` in the URL for the portal.</span><span class="sxs-lookup"><span data-stu-id="64787-118">In the OMS portal, add `?tenant=contoso.com` in the URL for the portal.</span></span> <span data-ttu-id="64787-119">For example, `mms.microsoft.com/?tenant=contoso.com`</span><span class="sxs-lookup"><span data-stu-id="64787-119">For example, `mms.microsoft.com/?tenant=contoso.com`</span></span>
* <span data-ttu-id="64787-120">In PowerShell, use the `-Tenant contoso.com` parameter when using `Add-AzureRmAccount` cmdlet</span><span class="sxs-lookup"><span data-stu-id="64787-120">In PowerShell, use the `-Tenant contoso.com` parameter when using `Add-AzureRmAccount` cmdlet</span></span>
* <span data-ttu-id="64787-121">The tenant identifier is automatically added when you use the `OMS portal` link from the Azure portal to open and log in to the OMS portal for the selected workspace</span><span class="sxs-lookup"><span data-stu-id="64787-121">The tenant identifier is automatically added when you use the `OMS portal` link from the Azure portal to open and log in to the OMS portal for the selected workspace</span></span>

<span data-ttu-id="64787-122">As a *customer* of a Cloud Solution Provider you can:</span><span class="sxs-lookup"><span data-stu-id="64787-122">As a *customer* of a Cloud Solution Provider you can:</span></span>

* <span data-ttu-id="64787-123">Create log analytics workspaces in a CSP subscription</span><span class="sxs-lookup"><span data-stu-id="64787-123">Create log analytics workspaces in a CSP subscription</span></span>
* <span data-ttu-id="64787-124">Access workspaces created by the CSP</span><span class="sxs-lookup"><span data-stu-id="64787-124">Access workspaces created by the CSP</span></span>
  * <span data-ttu-id="64787-125">Use the `OMS portal` link from the Azure portal to open and log in to the OMS portal for the selected workspace</span><span class="sxs-lookup"><span data-stu-id="64787-125">Use the `OMS portal` link from the Azure portal to open and log in to the OMS portal for the selected workspace</span></span>
* <span data-ttu-id="64787-126">View and use the user management page under Settings in the OMS portal</span><span class="sxs-lookup"><span data-stu-id="64787-126">View and use the user management page under Settings in the OMS portal</span></span>

> [!NOTE]
> <span data-ttu-id="64787-127">The included Backup and Site Recovery solutions for Log Analytics are not able to connect to a Recovery Services vault and cannot be configured in a CSP subscription.</span><span class="sxs-lookup"><span data-stu-id="64787-127">The included Backup and Site Recovery solutions for Log Analytics are not able to connect to a Recovery Services vault and cannot be configured in a CSP subscription.</span></span> 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a><span data-ttu-id="64787-128">Managing multiple customers using Log Analytics</span><span class="sxs-lookup"><span data-stu-id="64787-128">Managing multiple customers using Log Analytics</span></span>
<span data-ttu-id="64787-129">It is recommended that you create a Log Analytics workspace for each customer you manage.</span><span class="sxs-lookup"><span data-stu-id="64787-129">It is recommended that you create a Log Analytics workspace for each customer you manage.</span></span> <span data-ttu-id="64787-130">A Log Analytics workspace provides:</span><span class="sxs-lookup"><span data-stu-id="64787-130">A Log Analytics workspace provides:</span></span>

* <span data-ttu-id="64787-131">A geographic location for data to be stored.</span><span class="sxs-lookup"><span data-stu-id="64787-131">A geographic location for data to be stored.</span></span> 
* <span data-ttu-id="64787-132">Granularity for billing</span><span class="sxs-lookup"><span data-stu-id="64787-132">Granularity for billing</span></span> 
* <span data-ttu-id="64787-133">Data isolation</span><span class="sxs-lookup"><span data-stu-id="64787-133">Data isolation</span></span> 
* <span data-ttu-id="64787-134">Unique configuration</span><span class="sxs-lookup"><span data-stu-id="64787-134">Unique configuration</span></span>

<span data-ttu-id="64787-135">By creating a workspace per customer, you are able to keep each customer’s data separate and also track the usage of each customer.</span><span class="sxs-lookup"><span data-stu-id="64787-135">By creating a workspace per customer, you are able to keep each customer’s data separate and also track the usage of each customer.</span></span>

<span data-ttu-id="64787-136">More details on when and why to create multiple workspaces is described in [manage access to log analytics](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need).</span><span class="sxs-lookup"><span data-stu-id="64787-136">More details on when and why to create multiple workspaces is described in [manage access to log analytics](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need).</span></span>

<span data-ttu-id="64787-137">Creation and configuration of customer workspaces can be automated using [PowerShell](log-analytics-powershell-workspace-configuration.md), [Resource Manager templates](log-analytics-template-workspace-configuration.md), or using the [REST API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/).</span><span class="sxs-lookup"><span data-stu-id="64787-137">Creation and configuration of customer workspaces can be automated using [PowerShell](log-analytics-powershell-workspace-configuration.md), [Resource Manager templates](log-analytics-template-workspace-configuration.md), or using the [REST API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/).</span></span>

<span data-ttu-id="64787-138">The use of Resource Manager templates for workspace configuration allows you to have a master configuration that can be used to create and configure workspaces.</span><span class="sxs-lookup"><span data-stu-id="64787-138">The use of Resource Manager templates for workspace configuration allows you to have a master configuration that can be used to create and configure workspaces.</span></span> <span data-ttu-id="64787-139">You can be confident that as workspaces are created for customers they are automatically configured to your requirements.</span><span class="sxs-lookup"><span data-stu-id="64787-139">You can be confident that as workspaces are created for customers they are automatically configured to your requirements.</span></span> <span data-ttu-id="64787-140">When you update your requirements, the template is updated and then reapplied the existing workspaces.</span><span class="sxs-lookup"><span data-stu-id="64787-140">When you update your requirements, the template is updated and then reapplied the existing workspaces.</span></span> <span data-ttu-id="64787-141">This process ensures that even existing workspaces meet your new standards.</span><span class="sxs-lookup"><span data-stu-id="64787-141">This process ensures that even existing workspaces meet your new standards.</span></span>    

<span data-ttu-id="64787-142">When managing multiple Log Analytics workspaces, we recommend integrating each workspace with your existing ticketing system / operations console using the [Alerts](log-analytics-alerts.md) functionality.</span><span class="sxs-lookup"><span data-stu-id="64787-142">When managing multiple Log Analytics workspaces, we recommend integrating each workspace with your existing ticketing system / operations console using the [Alerts](log-analytics-alerts.md) functionality.</span></span> <span data-ttu-id="64787-143">By integrating with your existing systems, support staff can continue to follow their familiar processes.</span><span class="sxs-lookup"><span data-stu-id="64787-143">By integrating with your existing systems, support staff can continue to follow their familiar processes.</span></span> <span data-ttu-id="64787-144">Log Analytics regularly checks each workspace against the alert criteria you specify and generates an alert when action is needed.</span><span class="sxs-lookup"><span data-stu-id="64787-144">Log Analytics regularly checks each workspace against the alert criteria you specify and generates an alert when action is needed.</span></span>

<span data-ttu-id="64787-145">For personalized views of data, use the [dashboard](../azure-portal/azure-portal-dashboards.md) capability in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="64787-145">For personalized views of data, use the [dashboard](../azure-portal/azure-portal-dashboards.md) capability in the Azure portal.</span></span>  

<span data-ttu-id="64787-146">For executive level reports that summarize data across workspaces you can use the integration between Log Analytics and [PowerBI](log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="64787-146">For executive level reports that summarize data across workspaces you can use the integration between Log Analytics and [PowerBI](log-analytics-powerbi.md).</span></span> <span data-ttu-id="64787-147">If you need to integrate with another reporting system, you can use the Search API (via PowerShell or [REST](log-analytics-log-search-api.md)) to run queries and export search results.</span><span class="sxs-lookup"><span data-stu-id="64787-147">If you need to integrate with another reporting system, you can use the Search API (via PowerShell or [REST](log-analytics-log-search-api.md)) to run queries and export search results.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64787-148">Next Steps</span><span class="sxs-lookup"><span data-stu-id="64787-148">Next Steps</span></span>
* <span data-ttu-id="64787-149">Automate creation and configuration of workspaces using [Resource Manager templates](log-analytics-template-workspace-configuration.md)</span><span class="sxs-lookup"><span data-stu-id="64787-149">Automate creation and configuration of workspaces using [Resource Manager templates](log-analytics-template-workspace-configuration.md)</span></span>
* <span data-ttu-id="64787-150">Automate creation of workspaces using [PowerShell](log-analytics-powershell-workspace-configuration.md)</span><span class="sxs-lookup"><span data-stu-id="64787-150">Automate creation of workspaces using [PowerShell](log-analytics-powershell-workspace-configuration.md)</span></span> 
* <span data-ttu-id="64787-151">Use [Alerts](log-analytics-alerts.md) to integrate with existing systems</span><span class="sxs-lookup"><span data-stu-id="64787-151">Use [Alerts](log-analytics-alerts.md) to integrate with existing systems</span></span>
* <span data-ttu-id="64787-152">Generate summary reports using [PowerBI](log-analytics-powerbi.md)</span><span class="sxs-lookup"><span data-stu-id="64787-152">Generate summary reports using [PowerBI](log-analytics-powerbi.md)</span></span>

