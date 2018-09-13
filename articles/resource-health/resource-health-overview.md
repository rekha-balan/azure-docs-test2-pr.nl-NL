---
title: Azure Resource health overview | Microsoft Docs
description: Overview of Azure Resource health
services: Resource health
documentationcenter: ''
author: BernardoAMunoz
manager: ''
editor: ''
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: fb7677ef87a47c36c1277d0351330c066d1b87ac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549610"
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="89030-103">Azure resource health overview</span><span class="sxs-lookup"><span data-stu-id="89030-103">Azure resource health overview</span></span>
 
<span data-ttu-id="89030-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span><span class="sxs-lookup"><span data-stu-id="89030-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="89030-105">It informs you about the current and past health of your resources and helps you mitigate issues.</span><span class="sxs-lookup"><span data-stu-id="89030-105">It informs you about the current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="89030-106">Resource health provides technical support when you need help with Azure service issues.</span><span class="sxs-lookup"><span data-stu-id="89030-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="89030-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of the health of your resources.</span><span class="sxs-lookup"><span data-stu-id="89030-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of the health of your resources.</span></span> <span data-ttu-id="89030-108">Resource health shows you all the times your resources were unavailable in the past due to Azure service issues.</span><span class="sxs-lookup"><span data-stu-id="89030-108">Resource health shows you all the times your resources were unavailable in the past due to Azure service issues.</span></span> <span data-ttu-id="89030-109">This makes it simple for you to understand if an SLA was violated.</span><span class="sxs-lookup"><span data-stu-id="89030-109">This makes it simple for you to understand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="89030-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span><span class="sxs-lookup"><span data-stu-id="89030-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="89030-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span><span class="sxs-lookup"><span data-stu-id="89030-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="89030-112">Resource health relies on signals emitted by the different Azure services to assess if a resource is healthy or not.</span><span class="sxs-lookup"><span data-stu-id="89030-112">Resource health relies on signals emitted by the different Azure services to assess if a resource is healthy or not.</span></span> <span data-ttu-id="89030-113">If a resource is unhealthy, resource health analyzes additional information to determine the source of the problem.</span><span class="sxs-lookup"><span data-stu-id="89030-113">If a resource is unhealthy, resource health analyzes additional information to determine the source of the problem.</span></span> <span data-ttu-id="89030-114">It also identifies actions Microsoft is taking to fix the issue or what actions you can take to address the cause of the problem.</span><span class="sxs-lookup"><span data-stu-id="89030-114">It also identifies actions Microsoft is taking to fix the issue or what actions you can take to address the cause of the problem.</span></span> 

<span data-ttu-id="89030-115">Review the full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span><span class="sxs-lookup"><span data-stu-id="89030-115">Review the full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="89030-116">Health status provided by resource health</span><span class="sxs-lookup"><span data-stu-id="89030-116">Health status provided by resource health</span></span>
<span data-ttu-id="89030-117">The health of a resource is one of the following statuses:</span><span class="sxs-lookup"><span data-stu-id="89030-117">The health of a resource is one of the following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="89030-118">Available</span><span class="sxs-lookup"><span data-stu-id="89030-118">Available</span></span>
<span data-ttu-id="89030-119">The service has not detected any events impacting the health of the resource.</span><span class="sxs-lookup"><span data-stu-id="89030-119">The service has not detected any events impacting the health of the resource.</span></span> <span data-ttu-id="89030-120">In cases where the resource has recovered from unplanned downtime during the last 24 hours you will see the **recently recovered** notification.</span><span class="sxs-lookup"><span data-stu-id="89030-120">In cases where the resource has recovered from unplanned downtime during the last 24 hours you will see the **recently recovered** notification.</span></span>

![Resource health Available virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/resource-health/media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="89030-122">Unavailable</span><span class="sxs-lookup"><span data-stu-id="89030-122">Unavailable</span></span>
<span data-ttu-id="89030-123">The service has detected an ongoing platform or non-platform event impacting the health of the resource.</span><span class="sxs-lookup"><span data-stu-id="89030-123">The service has detected an ongoing platform or non-platform event impacting the health of the resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="89030-124">Platform events</span><span class="sxs-lookup"><span data-stu-id="89030-124">Platform events</span></span>
<span data-ttu-id="89030-125">These events are triggered by multiple components of the Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span><span class="sxs-lookup"><span data-stu-id="89030-125">These events are triggered by multiple components of the Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="89030-126">Resource health provides additional details on the event, the recovery process and enables you to contact support even if you don't have an active Microsoft support agreement.</span><span class="sxs-lookup"><span data-stu-id="89030-126">Resource health provides additional details on the event, the recovery process and enables you to contact support even if you don't have an active Microsoft support agreement.</span></span>

![Resource health Unavailable virtual machine due to platform event](https://docstestmedia1.blob.core.windows.net/azure-media/articles/resource-health/media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="89030-128">Non-Platform events</span><span class="sxs-lookup"><span data-stu-id="89030-128">Non-Platform events</span></span>
<span data-ttu-id="89030-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching the maximum number of connections to a Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="89030-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching the maximum number of connections to a Redis Cache.</span></span>

![Resource health Unavailable virtual machine due to non-platform event](https://docstestmedia1.blob.core.windows.net/azure-media/articles/resource-health/media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="89030-131">Unknown</span><span class="sxs-lookup"><span data-stu-id="89030-131">Unknown</span></span>
<span data-ttu-id="89030-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="89030-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="89030-133">While this status is not a definitive indication of the state of the resource, it is an important data point in the troubleshooting process:</span><span class="sxs-lookup"><span data-stu-id="89030-133">While this status is not a definitive indication of the state of the resource, it is an important data point in the troubleshooting process:</span></span>
* <span data-ttu-id="89030-134">If the resource is running as expected the status of the resource will update to Available after a few minutes.</span><span class="sxs-lookup"><span data-stu-id="89030-134">If the resource is running as expected the status of the resource will update to Available after a few minutes.</span></span>
* <span data-ttu-id="89030-135">If you are experiencing problems with the resource, the Unknown health status may suggest the resource is impacted by an event in the platform.</span><span class="sxs-lookup"><span data-stu-id="89030-135">If you are experiencing problems with the resource, the Unknown health status may suggest the resource is impacted by an event in the platform.</span></span>

![Resource health Unknown virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/resource-health/media/resource-health-overview/unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="89030-137">Report an incorrect status</span><span class="sxs-lookup"><span data-stu-id="89030-137">Report an incorrect status</span></span>
<span data-ttu-id="89030-138">If at any point you believe the current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span><span class="sxs-lookup"><span data-stu-id="89030-138">If at any point you believe the current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="89030-139">In cases where you are impacted by an Azure problem, we encourage you to contact support from the resource health blade.</span><span class="sxs-lookup"><span data-stu-id="89030-139">In cases where you are impacted by an Azure problem, we encourage you to contact support from the resource health blade.</span></span> 

![Resource health Report Incorrect Status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/resource-health/media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="89030-141">Historical Information</span><span class="sxs-lookup"><span data-stu-id="89030-141">Historical Information</span></span>
<span data-ttu-id="89030-142">You can access up to 14 days of historical health data by clicking **View History** in the Resource health blade.</span><span class="sxs-lookup"><span data-stu-id="89030-142">You can access up to 14 days of historical health data by clicking **View History** in the Resource health blade.</span></span> 

![Resource health Report History](https://docstestmedia1.blob.core.windows.net/azure-media/articles/resource-health/media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="89030-144">Getting started</span><span class="sxs-lookup"><span data-stu-id="89030-144">Getting started</span></span>
<span data-ttu-id="89030-145">To open Resource health for one resource</span><span class="sxs-lookup"><span data-stu-id="89030-145">To open Resource health for one resource</span></span>
1.  <span data-ttu-id="89030-146">Sign in into the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="89030-146">Sign in into the Azure portal.</span></span>
2.  <span data-ttu-id="89030-147">Navigate to your resource.</span><span class="sxs-lookup"><span data-stu-id="89030-147">Navigate to your resource.</span></span>
3.  <span data-ttu-id="89030-148">In the resource menu located in the left-hand side, click **Resource health**.</span><span class="sxs-lookup"><span data-stu-id="89030-148">In the resource menu located in the left-hand side, click **Resource health**.</span></span>

![Open Resource health from Resource blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/resource-health/media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="89030-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box to open the **Help + Support** blade.</span><span class="sxs-lookup"><span data-stu-id="89030-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box to open the **Help + Support** blade.</span></span> <span data-ttu-id="89030-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="89030-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Open Resource health from More service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/resource-health/media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="89030-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="89030-153">Next steps</span></span>

<span data-ttu-id="89030-154">Check out these resources to learn more about resource health:</span><span class="sxs-lookup"><span data-stu-id="89030-154">Check out these resources to learn more about resource health:</span></span>
-  [<span data-ttu-id="89030-155">Resource types and health checks in Azure resource health</span><span class="sxs-lookup"><span data-stu-id="89030-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="89030-156">Frequently asked questions about Azure resource health</span><span class="sxs-lookup"><span data-stu-id="89030-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)












