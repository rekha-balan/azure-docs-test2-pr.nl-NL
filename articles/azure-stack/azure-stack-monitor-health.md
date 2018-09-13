---
title: Monitor health and alerts in Azure Stack | Microsoft Docs
description: Learn how to monitor health and alerts in Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 9/10/2018
ms.author: mabrigg
ms.openlocfilehash: 69ed08e8f6c820790c432bfa25988e038fd0efbd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44781058"
---
# <a name="monitor-health-and-alerts-in-azure-stack"></a><span data-ttu-id="8e0d8-103">Monitor health and alerts in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8e0d8-103">Monitor health and alerts in Azure Stack</span></span>

<span data-ttu-id="8e0d8-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="8e0d8-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="8e0d8-105">Azure Stack includes infrastructure monitoring capabilities that enable you to view health and alerts for an Azure Stack region.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-105">Azure Stack includes infrastructure monitoring capabilities that enable you to view health and alerts for an Azure Stack region.</span></span> <span data-ttu-id="8e0d8-106">The **Region management** tile, pinned by default in the administrator portal for the Default Provider Subscription, lists all the deployed regions of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-106">The **Region management** tile, pinned by default in the administrator portal for the Default Provider Subscription, lists all the deployed regions of Azure Stack.</span></span> <span data-ttu-id="8e0d8-107">The tile shows the number of active critical and warning alerts for each region, and is your entry point into the health and alert functionality of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-107">The tile shows the number of active critical and warning alerts for each region, and is your entry point into the health and alert functionality of Azure Stack.</span></span>

 ![The Region Management tile](media/azure-stack-monitor-health/image1.png)

 ## <a name="understand-health-in-azure-stack"></a><span data-ttu-id="8e0d8-109">Understand health in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8e0d8-109">Understand health in Azure Stack</span></span>

 <span data-ttu-id="8e0d8-110">Health and alerts are managed by the Health resource provider.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-110">Health and alerts are managed by the Health resource provider.</span></span> <span data-ttu-id="8e0d8-111">Azure Stack infrastructure components register with the Health resource provider during Azure Stack deployment and configuration.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-111">Azure Stack infrastructure components register with the Health resource provider during Azure Stack deployment and configuration.</span></span> <span data-ttu-id="8e0d8-112">This registration enables the display of health and alerts for each component.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-112">This registration enables the display of health and alerts for each component.</span></span> <span data-ttu-id="8e0d8-113">Health in Azure Stack is a simple concept.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-113">Health in Azure Stack is a simple concept.</span></span> <span data-ttu-id="8e0d8-114">If alerts for a registered instance of a component exist, the health state of that component reflects the worst active alert severity; warning, or critical.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-114">If alerts for a registered instance of a component exist, the health state of that component reflects the worst active alert severity; warning, or critical.</span></span>

## <a name="alert-severity-definition"></a><span data-ttu-id="8e0d8-115">Alert severity definition</span><span class="sxs-lookup"><span data-stu-id="8e0d8-115">Alert severity definition</span></span>

<span data-ttu-id="8e0d8-116">In Azure Stack alerts are raised with only two severities: **warning** and **critical**.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-116">In Azure Stack alerts are raised with only two severities: **warning** and **critical**.</span></span>

- <span data-ttu-id="8e0d8-117">**Warning**</span><span class="sxs-lookup"><span data-stu-id="8e0d8-117">**Warning**</span></span>  
  <span data-ttu-id="8e0d8-118">An operator can address the warning alert in a scheduled manner.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-118">An operator can address the warning alert in a scheduled manner.</span></span> <span data-ttu-id="8e0d8-119">The alert typically does not impact user workloads.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-119">The alert typically does not impact user workloads.</span></span>

- <span data-ttu-id="8e0d8-120">**Critical**</span><span class="sxs-lookup"><span data-stu-id="8e0d8-120">**Critical**</span></span>  
  <span data-ttu-id="8e0d8-121">An operator should address the critical alert with urgency.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-121">An operator should address the critical alert with urgency.</span></span> <span data-ttu-id="8e0d8-122">These are issues that currently impact or will soon impact Azure Stack users.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-122">These are issues that currently impact or will soon impact Azure Stack users.</span></span> 

 
 ## <a name="view-and-manage-component-health-state"></a><span data-ttu-id="8e0d8-123">View and manage component health state</span><span class="sxs-lookup"><span data-stu-id="8e0d8-123">View and manage component health state</span></span>
 
 <span data-ttu-id="8e0d8-124">As an Azure Stack operator, you can view the health state of components in the administrator portal and through REST API and PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-124">As an Azure Stack operator, you can view the health state of components in the administrator portal and through REST API and PowerShell.</span></span>
 
<span data-ttu-id="8e0d8-125">To view the health state in the portal, click the region that you want to view in the **Region management** tile.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-125">To view the health state in the portal, click the region that you want to view in the **Region management** tile.</span></span> <span data-ttu-id="8e0d8-126">You can view the health state of infrastructure roles and of resource providers.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-126">You can view the health state of infrastructure roles and of resource providers.</span></span>

![List of infrastructure roles](media/azure-stack-monitor-health/image2.png)

<span data-ttu-id="8e0d8-128">You can click a resource provider or infrastructure role to view more detailed information.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-128">You can click a resource provider or infrastructure role to view more detailed information.</span></span>

> [!WARNING]  
> <span data-ttu-id="8e0d8-129">If you click an infrastructure role, and then click the role instance, there are options to Start, Restart, or Shutdown.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-129">If you click an infrastructure role, and then click the role instance, there are options to Start, Restart, or Shutdown.</span></span> <span data-ttu-id="8e0d8-130">Do not use these actions when you apply updates to an integrated system.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-130">Do not use these actions when you apply updates to an integrated system.</span></span> <span data-ttu-id="8e0d8-131">Also, do **not** use these options in an Azure Stack Development Kit environment.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-131">Also, do **not** use these options in an Azure Stack Development Kit environment.</span></span> <span data-ttu-id="8e0d8-132">These options are designed only for an integrated systems environment, where there is more than one role instance per infrastructure role.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-132">These options are designed only for an integrated systems environment, where there is more than one role instance per infrastructure role.</span></span> <span data-ttu-id="8e0d8-133">Restarting a role instance (especially AzS-Xrp01) in the development kit causes system instability.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-133">Restarting a role instance (especially AzS-Xrp01) in the development kit causes system instability.</span></span> <span data-ttu-id="8e0d8-134">For troubleshooting assistance, post your issue to the [Azure Stack forum](https://aka.ms/azurestackforum).</span><span class="sxs-lookup"><span data-stu-id="8e0d8-134">For troubleshooting assistance, post your issue to the [Azure Stack forum](https://aka.ms/azurestackforum).</span></span>
>
 
## <a name="view-alerts"></a><span data-ttu-id="8e0d8-135">View alerts</span><span class="sxs-lookup"><span data-stu-id="8e0d8-135">View alerts</span></span>

<span data-ttu-id="8e0d8-136">The list of active alerts for each Azure Stack region is available directly from the **Region management** blade.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-136">The list of active alerts for each Azure Stack region is available directly from the **Region management** blade.</span></span> <span data-ttu-id="8e0d8-137">The first tile in the default configuration is the **Alerts** tile, which displays a summary of the critical and warning alerts for the region.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-137">The first tile in the default configuration is the **Alerts** tile, which displays a summary of the critical and warning alerts for the region.</span></span> <span data-ttu-id="8e0d8-138">You can pin the Alerts tile, like any other tile on this blade, to the dashboard for quick access.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-138">You can pin the Alerts tile, like any other tile on this blade, to the dashboard for quick access.</span></span>   

![Alerts tile that shows a warning](media/azure-stack-monitor-health/image3.png)

<span data-ttu-id="8e0d8-140">By selecting the top part of the **Alerts** tile, you navigate to the list of all active alerts for the region.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-140">By selecting the top part of the **Alerts** tile, you navigate to the list of all active alerts for the region.</span></span> <span data-ttu-id="8e0d8-141">If you select either the **Critical** or **Warning** line item within the tile, you navigate to a filtered list of alerts (Critical or Warning).</span><span class="sxs-lookup"><span data-stu-id="8e0d8-141">If you select either the **Critical** or **Warning** line item within the tile, you navigate to a filtered list of alerts (Critical or Warning).</span></span> 

![Filtered warning alerts](media/azure-stack-monitor-health/image4.png)
  
<span data-ttu-id="8e0d8-143">The **Alerts** blade supports the ability to filter both on status (Active or Closed) and severity (Critical or Warning).</span><span class="sxs-lookup"><span data-stu-id="8e0d8-143">The **Alerts** blade supports the ability to filter both on status (Active or Closed) and severity (Critical or Warning).</span></span> <span data-ttu-id="8e0d8-144">The default view displays all active alerts.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-144">The default view displays all active alerts.</span></span> <span data-ttu-id="8e0d8-145">All closed alerts are removed from the system after seven days.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-145">All closed alerts are removed from the system after seven days.</span></span>

![Filter pane to filter by critical or warning status](media/azure-stack-monitor-health/image5.png)

<span data-ttu-id="8e0d8-147">The **View API** action displays the REST API that was used to generate the list view.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-147">The **View API** action displays the REST API that was used to generate the list view.</span></span> <span data-ttu-id="8e0d8-148">This action provides a quick way to become familiar with the REST API syntax that you can use to query alerts.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-148">This action provides a quick way to become familiar with the REST API syntax that you can use to query alerts.</span></span> <span data-ttu-id="8e0d8-149">You can use this API in automation or for integration with your existing datacenter monitoring, reporting, and ticketing solutions.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-149">You can use this API in automation or for integration with your existing datacenter monitoring, reporting, and ticketing solutions.</span></span> 

![The View API option that shows the REST API](media/azure-stack-monitor-health/image6.png)

<span data-ttu-id="8e0d8-151">You can click a specific alert to view the alert details.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-151">You can click a specific alert to view the alert details.</span></span> <span data-ttu-id="8e0d8-152">The alert details show all fields that are associated with the alert, and enable quick navigation to the affected component and source of the alert.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-152">The alert details show all fields that are associated with the alert, and enable quick navigation to the affected component and source of the alert.</span></span> <span data-ttu-id="8e0d8-153">For example, the following alert occurs if one of the infrastructure role instances goes offline or is not accessible.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-153">For example, the following alert occurs if one of the infrastructure role instances goes offline or is not accessible.</span></span>  

![The Alert details blade](media/azure-stack-monitor-health/image7.png)

<span data-ttu-id="8e0d8-155">After the infrastructure role instance is back online, this alert automatically closes.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-155">After the infrastructure role instance is back online, this alert automatically closes.</span></span> <span data-ttu-id="8e0d8-156">Many, but not every alert automatically closes when the underlying issue is resolved.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-156">Many, but not every alert automatically closes when the underlying issue is resolved.</span></span> <span data-ttu-id="8e0d8-157">We recommend that you select **Close Alert** after you perform remediation steps.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-157">We recommend that you select **Close Alert** after you perform remediation steps.</span></span> <span data-ttu-id="8e0d8-158">If the issue persists, Azure Stack generates a new alert.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-158">If the issue persists, Azure Stack generates a new alert.</span></span> <span data-ttu-id="8e0d8-159">If you resolve the issue, the alert remains closed and requires no additional action.</span><span class="sxs-lookup"><span data-stu-id="8e0d8-159">If you resolve the issue, the alert remains closed and requires no additional action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e0d8-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="8e0d8-160">Next steps</span></span>

[<span data-ttu-id="8e0d8-161">Manage updates in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8e0d8-161">Manage updates in Azure Stack</span></span>](azure-stack-updates.md)

[<span data-ttu-id="8e0d8-162">Region management in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8e0d8-162">Region management in Azure Stack</span></span>](azure-stack-region-management.md)
