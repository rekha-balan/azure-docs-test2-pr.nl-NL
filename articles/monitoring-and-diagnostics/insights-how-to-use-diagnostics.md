---
title: Enable monitoring and diagnostics in Microsoft Azure | Microsoft Docs
description: Learn how to set up diagnostics for your resources in Azure.
author: rboucher
manager: carolz
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: af1947a9-c211-4aa1-8924-880a86240be4
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2015
ms.author: robb
ms.openlocfilehash: ab4d6b3517192cfe3df85b2a45eb417a3fd6f519
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660566"
---
# <a name="enable-monitoring-and-diagnostics"></a><span data-ttu-id="e7b0b-103">Enable monitoring and diagnostics</span><span class="sxs-lookup"><span data-stu-id="e7b0b-103">Enable monitoring and diagnostics</span></span>
<span data-ttu-id="e7b0b-104">In the [Azure Portal](https://portal.azure.com), you can configure rich, frequent, monitoring and diagnostics data about your resources.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-104">In the [Azure Portal](https://portal.azure.com), you can configure rich, frequent, monitoring and diagnostics data about your resources.</span></span> <span data-ttu-id="e7b0b-105">You can also use the [REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx) or [.NET SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights/) to configure diagnostics programmatically.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-105">You can also use the [REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx) or [.NET SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights/) to configure diagnostics programmatically.</span></span>

<span data-ttu-id="e7b0b-106">Diagnostics, monitoring and metric data in Azure is saved into a Storage account of your choice.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-106">Diagnostics, monitoring and metric data in Azure is saved into a Storage account of your choice.</span></span> <span data-ttu-id="e7b0b-107">This allows you to use whatever tooling you want to read the data, from a storage explorer, to Power BI to third-party tooling.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-107">This allows you to use whatever tooling you want to read the data, from a storage explorer, to Power BI to third-party tooling.</span></span>

## <a name="when-you-create-a-resource"></a><span data-ttu-id="e7b0b-108">When you create a resource</span><span class="sxs-lookup"><span data-stu-id="e7b0b-108">When you create a resource</span></span>
<span data-ttu-id="e7b0b-109">Most services allow you to enable diagnostics when you first create them in the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e7b0b-109">Most services allow you to enable diagnostics when you first create them in the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="e7b0b-110">Go to **New** and choose the resource you are interested in.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-110">Go to **New** and choose the resource you are interested in.</span></span>
2. <span data-ttu-id="e7b0b-111">Select **Optional configuration**.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-111">Select **Optional configuration**.</span></span>
    <span data-ttu-id="e7b0b-112">![Diagnostics blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-how-to-use-diagnostics/Insights_CreateTime.png)</span><span class="sxs-lookup"><span data-stu-id="e7b0b-112">![Diagnostics blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-how-to-use-diagnostics/Insights_CreateTime.png)</span></span>
3. <span data-ttu-id="e7b0b-113">Select **Diagnostics**, and click **On**.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-113">Select **Diagnostics**, and click **On**.</span></span> <span data-ttu-id="e7b0b-114">You will need to choose the Storage account that you want diagnostics to be saved to.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-114">You will need to choose the Storage account that you want diagnostics to be saved to.</span></span> <span data-ttu-id="e7b0b-115">You’ll be charged normal data rates for storage and transactions when you send diagnostics to a storage account.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-115">You’ll be charged normal data rates for storage and transactions when you send diagnostics to a storage account.</span></span>
4. <span data-ttu-id="e7b0b-116">Click **OK** and create the resource.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-116">Click **OK** and create the resource.</span></span>

## <a name="change-settings-for-an-existing-resource"></a><span data-ttu-id="e7b0b-117">Change settings for an existing resource</span><span class="sxs-lookup"><span data-stu-id="e7b0b-117">Change settings for an existing resource</span></span>
<span data-ttu-id="e7b0b-118">If you have already created a resource and you want to change the diagnostics settings (to change the level of data collection, for example), you can do that right in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-118">If you have already created a resource and you want to change the diagnostics settings (to change the level of data collection, for example), you can do that right in the Azure Portal.</span></span>

1. <span data-ttu-id="e7b0b-119">Go to the resource and click the **Settings** command.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-119">Go to the resource and click the **Settings** command.</span></span>
2. <span data-ttu-id="e7b0b-120">Select **Diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-120">Select **Diagnostics**.</span></span>
3. <span data-ttu-id="e7b0b-121">The **Diagnostics** blade has all of the possible diagnostics and monitoring collection data for that resource.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-121">The **Diagnostics** blade has all of the possible diagnostics and monitoring collection data for that resource.</span></span> <span data-ttu-id="e7b0b-122">For some resources you can also choose a **Retention** policy for the data, to clean it up from your storage account.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-122">For some resources you can also choose a **Retention** policy for the data, to clean it up from your storage account.</span></span>
    <span data-ttu-id="e7b0b-123">![Storage diagnostics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)</span><span class="sxs-lookup"><span data-stu-id="e7b0b-123">![Storage diagnostics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)</span></span>
4. <span data-ttu-id="e7b0b-124">Once you've chosen your settings, click the **Save** command.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-124">Once you've chosen your settings, click the **Save** command.</span></span> <span data-ttu-id="e7b0b-125">It may take a little while for monitoring data to show up if you are enabling it for the first time.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-125">It may take a little while for monitoring data to show up if you are enabling it for the first time.</span></span>

### <a name="categories-of-data-collection-for-virtual-machines"></a><span data-ttu-id="e7b0b-126">Categories of data collection for virtual machines</span><span class="sxs-lookup"><span data-stu-id="e7b0b-126">Categories of data collection for virtual machines</span></span>
<span data-ttu-id="e7b0b-127">For virtual machines all metrics and logs will be recorded at one-minute intervals, so you can always have the most up-to-date information about your machine.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-127">For virtual machines all metrics and logs will be recorded at one-minute intervals, so you can always have the most up-to-date information about your machine.</span></span>

* <span data-ttu-id="e7b0b-128">**Basic metrics** : Health metrics about your virtual machine such as processor and memory</span><span class="sxs-lookup"><span data-stu-id="e7b0b-128">**Basic metrics** : Health metrics about your virtual machine such as processor and memory</span></span>
* <span data-ttu-id="e7b0b-129">**Network and web metrics** : Metrics about your network connections and web services</span><span class="sxs-lookup"><span data-stu-id="e7b0b-129">**Network and web metrics** : Metrics about your network connections and web services</span></span>
* <span data-ttu-id="e7b0b-130">**.NET metrics** : Metrics about the .NET and ASP.NET applications running on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="e7b0b-130">**.NET metrics** : Metrics about the .NET and ASP.NET applications running on your virtual machine</span></span>
* <span data-ttu-id="e7b0b-131">**SQL metrics** : If you are running Microsoft SQL Service, its performance metrics</span><span class="sxs-lookup"><span data-stu-id="e7b0b-131">**SQL metrics** : If you are running Microsoft SQL Service, its performance metrics</span></span>
* <span data-ttu-id="e7b0b-132">**Windows event application logs** : Windows events that are sent to the application channel</span><span class="sxs-lookup"><span data-stu-id="e7b0b-132">**Windows event application logs** : Windows events that are sent to the application channel</span></span>
* <span data-ttu-id="e7b0b-133">**Windows event system logs** : Windows events that are sent to the system channel.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-133">**Windows event system logs** : Windows events that are sent to the system channel.</span></span> <span data-ttu-id="e7b0b-134">This also includes all events from [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="e7b0b-134">This also includes all events from [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).</span></span>
* <span data-ttu-id="e7b0b-135">**Windows event security logs** : Windows events that are sent to the security channel</span><span class="sxs-lookup"><span data-stu-id="e7b0b-135">**Windows event security logs** : Windows events that are sent to the security channel</span></span>
* <span data-ttu-id="e7b0b-136">**Diagnostics infrastructure logs** : Logging about the diagnostics collection infrastructure</span><span class="sxs-lookup"><span data-stu-id="e7b0b-136">**Diagnostics infrastructure logs** : Logging about the diagnostics collection infrastructure</span></span>
* <span data-ttu-id="e7b0b-137">**IIS logs** : Logs about your IIS server</span><span class="sxs-lookup"><span data-stu-id="e7b0b-137">**IIS logs** : Logs about your IIS server</span></span>

<span data-ttu-id="e7b0b-138">Note that at this time certain distributions of Linux are not supported, and, the Guest Agent must be installed on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-138">Note that at this time certain distributions of Linux are not supported, and, the Guest Agent must be installed on the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7b0b-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="e7b0b-139">Next steps</span></span>
* <span data-ttu-id="e7b0b-140">[Receive alert notifications](insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-140">[Receive alert notifications](insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="e7b0b-141">[Monitor service metrics](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-141">[Monitor service metrics](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="e7b0b-142">[Scale instance count automatically](insights-how-to-scale.md) to make sure your service scale based on demand.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-142">[Scale instance count automatically](insights-how-to-scale.md) to make sure your service scale based on demand.</span></span>
* <span data-ttu-id="e7b0b-143">[Monitor application performance](../application-insights/app-insights-azure-web-apps.md) if you want to understand exactly how your code is performing in the cloud.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-143">[Monitor application performance](../application-insights/app-insights-azure-web-apps.md) if you want to understand exactly how your code is performing in the cloud.</span></span>
* <span data-ttu-id="e7b0b-144">[View events and activity log](insights-debugging-with-events.md) to learn everything that has happened in your service.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-144">[View events and activity log](insights-debugging-with-events.md) to learn everything that has happened in your service.</span></span>
* <span data-ttu-id="e7b0b-145">[Track service health](insights-service-health.md) to find out when Azure has experienced performance degradation or service interruptions.</span><span class="sxs-lookup"><span data-stu-id="e7b0b-145">[Track service health](insights-service-health.md) to find out when Azure has experienced performance degradation or service interruptions.</span></span>



