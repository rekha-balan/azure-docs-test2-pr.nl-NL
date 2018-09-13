---
title: Autoscale in Azure using a custom metric
description: Learn how to scale your resource by custom metric in Azure.
author: anirudhcavale
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 05/07/2017
ms.author: ancav
ms.component: autoscale
ms.openlocfilehash: 97836c4160349b8095ba2095176783ae17b46e82
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866117"
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="d99e3-103">Get started with auto scale by custom metric in Azure</span><span class="sxs-lookup"><span data-stu-id="d99e3-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="d99e3-104">This article describes how to scale your resource by a custom metric in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d99e3-104">This article describes how to scale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="d99e3-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span><span class="sxs-lookup"><span data-stu-id="d99e3-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="d99e3-106">Lets get started</span><span class="sxs-lookup"><span data-stu-id="d99e3-106">Lets get started</span></span>
<span data-ttu-id="d99e3-107">This article assumes that you have a web app with application insights configured.</span><span class="sxs-lookup"><span data-stu-id="d99e3-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="d99e3-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span><span class="sxs-lookup"><span data-stu-id="d99e3-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="d99e3-109">Open [Azure portal][2]</span><span class="sxs-lookup"><span data-stu-id="d99e3-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="d99e3-110">Click on Azure Monitor icon in the left navigation pane.</span><span class="sxs-lookup"><span data-stu-id="d99e3-110">Click on Azure Monitor icon in the left navigation pane.</span></span>
  <span data-ttu-id="d99e3-111">![Launch Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="d99e3-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="d99e3-112">Click on Autoscale setting to view all the resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span><span class="sxs-lookup"><span data-stu-id="d99e3-112">Click on Autoscale setting to view all the resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="d99e3-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want to scale</span><span class="sxs-lookup"><span data-stu-id="d99e3-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want to scale</span></span>
> <span data-ttu-id="d99e3-114">Note: The steps below use an app service plan associated with a web app that has app insights configured.</span><span class="sxs-lookup"><span data-stu-id="d99e3-114">Note: The steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="d99e3-115">In the scale setting blade for the resource, notice that the current instance count is 1.</span><span class="sxs-lookup"><span data-stu-id="d99e3-115">In the scale setting blade for the resource, notice that the current instance count is 1.</span></span> <span data-ttu-id="d99e3-116">Click on 'Enable autoscale'.</span><span class="sxs-lookup"><span data-stu-id="d99e3-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="d99e3-117">![Scale setting for new web app][5]</span><span class="sxs-lookup"><span data-stu-id="d99e3-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="d99e3-118">Provide a name for the scale setting, and the click on "Add a rule".</span><span class="sxs-lookup"><span data-stu-id="d99e3-118">Provide a name for the scale setting, and the click on "Add a rule".</span></span> <span data-ttu-id="d99e3-119">Notice the scale rule options that opens as a context pane in the right hand side.</span><span class="sxs-lookup"><span data-stu-id="d99e3-119">Notice the scale rule options that opens as a context pane in the right hand side.</span></span> <span data-ttu-id="d99e3-120">By default, it sets the option to scale your instance count by 1 if the CPU percetage of the resource exceeds 70%.</span><span class="sxs-lookup"><span data-stu-id="d99e3-120">By default, it sets the option to scale your instance count by 1 if the CPU percetage of the resource exceeds 70%.</span></span> <span data-ttu-id="d99e3-121">Change the metric source at the top to "Application Insights", select the app insights resource in the 'Resource' dropdown and then select the custom metric based on which you want to scale.</span><span class="sxs-lookup"><span data-stu-id="d99e3-121">Change the metric source at the top to "Application Insights", select the app insights resource in the 'Resource' dropdown and then select the custom metric based on which you want to scale.</span></span>
  <span data-ttu-id="d99e3-122">![Scale by custom metric][6]</span><span class="sxs-lookup"><span data-stu-id="d99e3-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="d99e3-123">Similar to the step above, add a scale rule that will scale in and decrease the scale count by 1 if the custom metric is below a threshold.</span><span class="sxs-lookup"><span data-stu-id="d99e3-123">Similar to the step above, add a scale rule that will scale in and decrease the scale count by 1 if the custom metric is below a threshold.</span></span>
  <span data-ttu-id="d99e3-124">![Scale based on cpu][7]</span><span class="sxs-lookup"><span data-stu-id="d99e3-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="d99e3-125">Set the you instance limits.</span><span class="sxs-lookup"><span data-stu-id="d99e3-125">Set the you instance limits.</span></span> <span data-ttu-id="d99e3-126">For example, if you want to scale between 2-5 instances depending on the custom metric fluctuations, set 'minimum' to '2', 'maximum' to '5' and 'default' to '2'</span><span class="sxs-lookup"><span data-stu-id="d99e3-126">For example, if you want to scale between 2-5 instances depending on the custom metric fluctuations, set 'minimum' to '2', 'maximum' to '5' and 'default' to '2'</span></span>
> <span data-ttu-id="d99e3-127">Note: In case there is a problem reading the resource metrics and the current capacity is below the default capacity, then to ensure the availability of the resource, Autoscale will scale out to the default value.</span><span class="sxs-lookup"><span data-stu-id="d99e3-127">Note: In case there is a problem reading the resource metrics and the current capacity is below the default capacity, then to ensure the availability of the resource, Autoscale will scale out to the default value.</span></span> <span data-ttu-id="d99e3-128">If the current capacity is already higher than default capacity, Autoscale will not scale in.</span><span class="sxs-lookup"><span data-stu-id="d99e3-128">If the current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="d99e3-129">Click on 'Save'</span><span class="sxs-lookup"><span data-stu-id="d99e3-129">Click on 'Save'</span></span>

<span data-ttu-id="d99e3-130">Congratulations.</span><span class="sxs-lookup"><span data-stu-id="d99e3-130">Congratulations.</span></span> <span data-ttu-id="d99e3-131">You now succesfully created your scale setting to auto scale your web app based on a custom metric.</span><span class="sxs-lookup"><span data-stu-id="d99e3-131">You now succesfully created your scale setting to auto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="d99e3-132">Note: The same steps are applicable to get started with a VMSS or cloud service role.</span><span class="sxs-lookup"><span data-stu-id="d99e3-132">Note: The same steps are applicable to get started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
