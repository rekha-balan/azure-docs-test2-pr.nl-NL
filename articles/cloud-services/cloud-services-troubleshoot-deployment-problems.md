---
title: Troubleshoot cloud service deployment problems | Microsoft Docs
description: There are a few common problems you may run into when deploying a cloud service to Azure. This article provides solutions to some of them.
services: cloud-services
documentationcenter: ''
author: simonxjx
manager: felixwu
editor: ''
tags: top-support-issue
ms.assetid: a18ae415-0d1c-4bc4-ab6c-c1ddea02c870
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 4/6/2017
ms.author: v-six
ms.openlocfilehash: 34a7de89ce324bd3c247b681533b6e09e0501cbb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554898"
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a><span data-ttu-id="8a9be-104">Troubleshoot cloud service deployment problems</span><span class="sxs-lookup"><span data-stu-id="8a9be-104">Troubleshoot cloud service deployment problems</span></span>
<span data-ttu-id="8a9be-105">When you deploy a cloud service application package to Azure, you can obtain information about the deployment from the **Properties** pane in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8a9be-105">When you deploy a cloud service application package to Azure, you can obtain information about the deployment from the **Properties** pane in the Azure portal.</span></span> <span data-ttu-id="8a9be-106">You can use the details in this pane to help you troubleshoot problems with the cloud service, and you can provide this information to Azure Support when opening a new support request.</span><span class="sxs-lookup"><span data-stu-id="8a9be-106">You can use the details in this pane to help you troubleshoot problems with the cloud service, and you can provide this information to Azure Support when opening a new support request.</span></span>

<span data-ttu-id="8a9be-107">You can find the **Properties** pane as follows:</span><span class="sxs-lookup"><span data-stu-id="8a9be-107">You can find the **Properties** pane as follows:</span></span>

* <span data-ttu-id="8a9be-108">In the Azure portal, click the deployment of your cloud service, click **All settings**, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="8a9be-108">In the Azure portal, click the deployment of your cloud service, click **All settings**, and then click **Properties**.</span></span>
* <span data-ttu-id="8a9be-109">In the Azure classic portal, click the deployment of your cloud service, click **DASHBOARD**, located at the lower-right corner of the page (under **quick glance**).</span><span class="sxs-lookup"><span data-stu-id="8a9be-109">In the Azure classic portal, click the deployment of your cloud service, click **DASHBOARD**, located at the lower-right corner of the page (under **quick glance**).</span></span> <span data-ttu-id="8a9be-110">Be aware that there's no "Properties" label on this pane.</span><span class="sxs-lookup"><span data-stu-id="8a9be-110">Be aware that there's no "Properties" label on this pane.</span></span>

> [!NOTE]
> <span data-ttu-id="8a9be-111">You can copy the contents of the **Properties** pane to the clipboard by clicking the icon in the upper-right corner of the pane.</span><span class="sxs-lookup"><span data-stu-id="8a9be-111">You can copy the contents of the **Properties** pane to the clipboard by clicking the icon in the upper-right corner of the pane.</span></span>
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a><span data-ttu-id="8a9be-112">Problem: I cannot access my website, but my deployment is started and all role instances are ready</span><span class="sxs-lookup"><span data-stu-id="8a9be-112">Problem: I cannot access my website, but my deployment is started and all role instances are ready</span></span>
<span data-ttu-id="8a9be-113">The website URL link shown in the portal does not include the port.</span><span class="sxs-lookup"><span data-stu-id="8a9be-113">The website URL link shown in the portal does not include the port.</span></span> <span data-ttu-id="8a9be-114">The default port for websites is 80.</span><span class="sxs-lookup"><span data-stu-id="8a9be-114">The default port for websites is 80.</span></span> <span data-ttu-id="8a9be-115">If your application is configured to run in a different port, you must add the correct port number to the URL when accessing the website.</span><span class="sxs-lookup"><span data-stu-id="8a9be-115">If your application is configured to run in a different port, you must add the correct port number to the URL when accessing the website.</span></span>

1. <span data-ttu-id="8a9be-116">In the Azure portal, click the deployment of your cloud service.</span><span class="sxs-lookup"><span data-stu-id="8a9be-116">In the Azure portal, click the deployment of your cloud service.</span></span>
2. <span data-ttu-id="8a9be-117">In the **Properties** pane of the Azure portal, check the ports for the role instances (under **Input Endpoints**).</span><span class="sxs-lookup"><span data-stu-id="8a9be-117">In the **Properties** pane of the Azure portal, check the ports for the role instances (under **Input Endpoints**).</span></span>
3. <span data-ttu-id="8a9be-118">If the port is not 80, add the correct port value to the URL when you access the application.</span><span class="sxs-lookup"><span data-stu-id="8a9be-118">If the port is not 80, add the correct port value to the URL when you access the application.</span></span> <span data-ttu-id="8a9be-119">To specify a non-default port, type the URL, followed by a colon (:), followed by the port number, with no spaces.</span><span class="sxs-lookup"><span data-stu-id="8a9be-119">To specify a non-default port, type the URL, followed by a colon (:), followed by the port number, with no spaces.</span></span>

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a><span data-ttu-id="8a9be-120">Problem: My role instances recycled without me doing anything</span><span class="sxs-lookup"><span data-stu-id="8a9be-120">Problem: My role instances recycled without me doing anything</span></span>
<span data-ttu-id="8a9be-121">Service healing occurs automatically when Azure detects problem nodes and therefore moves role instances to new nodes.</span><span class="sxs-lookup"><span data-stu-id="8a9be-121">Service healing occurs automatically when Azure detects problem nodes and therefore moves role instances to new nodes.</span></span> <span data-ttu-id="8a9be-122">When this occurs, you might see your role instances recycling automatically.</span><span class="sxs-lookup"><span data-stu-id="8a9be-122">When this occurs, you might see your role instances recycling automatically.</span></span> <span data-ttu-id="8a9be-123">To find out if service healing occurred:</span><span class="sxs-lookup"><span data-stu-id="8a9be-123">To find out if service healing occurred:</span></span>

1. <span data-ttu-id="8a9be-124">In the Azure portal, click the deployment of your cloud service.</span><span class="sxs-lookup"><span data-stu-id="8a9be-124">In the Azure portal, click the deployment of your cloud service.</span></span>
2. <span data-ttu-id="8a9be-125">In the **Properties** pane of the Azure portal, review the information and determine whether service healing occurred during the time that you observed the roles recycling.</span><span class="sxs-lookup"><span data-stu-id="8a9be-125">In the **Properties** pane of the Azure portal, review the information and determine whether service healing occurred during the time that you observed the roles recycling.</span></span>

<span data-ttu-id="8a9be-126">Roles will also recycle roughly once per month during host-OS and guest-OS updates.</span><span class="sxs-lookup"><span data-stu-id="8a9be-126">Roles will also recycle roughly once per month during host-OS and guest-OS updates.</span></span>  
<span data-ttu-id="8a9be-127">For more information, see the blog post [Role Instance Restarts Due to OS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)</span><span class="sxs-lookup"><span data-stu-id="8a9be-127">For more information, see the blog post [Role Instance Restarts Due to OS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)</span></span>

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a><span data-ttu-id="8a9be-128">Problem: I cannot do a VIP swap and receive an error</span><span class="sxs-lookup"><span data-stu-id="8a9be-128">Problem: I cannot do a VIP swap and receive an error</span></span>
<span data-ttu-id="8a9be-129">A VIP swap is not allowed if a deployment update is in progress.</span><span class="sxs-lookup"><span data-stu-id="8a9be-129">A VIP swap is not allowed if a deployment update is in progress.</span></span> <span data-ttu-id="8a9be-130">Deployment updates can occur automatically when:</span><span class="sxs-lookup"><span data-stu-id="8a9be-130">Deployment updates can occur automatically when:</span></span>

* <span data-ttu-id="8a9be-131">A new guest operating system is available and you are configured for automatic updates.</span><span class="sxs-lookup"><span data-stu-id="8a9be-131">A new guest operating system is available and you are configured for automatic updates.</span></span>
* <span data-ttu-id="8a9be-132">Service healing occurs.</span><span class="sxs-lookup"><span data-stu-id="8a9be-132">Service healing occurs.</span></span>

<span data-ttu-id="8a9be-133">To find out if an automatic update is preventing you from doing a VIP swap:</span><span class="sxs-lookup"><span data-stu-id="8a9be-133">To find out if an automatic update is preventing you from doing a VIP swap:</span></span>

1. <span data-ttu-id="8a9be-134">In the Azure portal, click the deployment of your cloud service.</span><span class="sxs-lookup"><span data-stu-id="8a9be-134">In the Azure portal, click the deployment of your cloud service.</span></span>
2. <span data-ttu-id="8a9be-135">In the **Properties** pane of the Azure portal, look at the value of **Status**.</span><span class="sxs-lookup"><span data-stu-id="8a9be-135">In the **Properties** pane of the Azure portal, look at the value of **Status**.</span></span> <span data-ttu-id="8a9be-136">If it is **Ready**, then check **Last operation** to see if one recently happened that might prevent the VIP swap.</span><span class="sxs-lookup"><span data-stu-id="8a9be-136">If it is **Ready**, then check **Last operation** to see if one recently happened that might prevent the VIP swap.</span></span>
3. <span data-ttu-id="8a9be-137">Repeat steps 1 and 2 for the production deployment.</span><span class="sxs-lookup"><span data-stu-id="8a9be-137">Repeat steps 1 and 2 for the production deployment.</span></span>
4. <span data-ttu-id="8a9be-138">If an automatic update is in process, wait for it to finish before trying to do the VIP swap.</span><span class="sxs-lookup"><span data-stu-id="8a9be-138">If an automatic update is in process, wait for it to finish before trying to do the VIP swap.</span></span>

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a><span data-ttu-id="8a9be-139">Problem: A role instance is looping between Started, Initializing, Busy, and Stopped</span><span class="sxs-lookup"><span data-stu-id="8a9be-139">Problem: A role instance is looping between Started, Initializing, Busy, and Stopped</span></span>
<span data-ttu-id="8a9be-140">This condition could indicate a problem with your application code, package, or configuration file.</span><span class="sxs-lookup"><span data-stu-id="8a9be-140">This condition could indicate a problem with your application code, package, or configuration file.</span></span> <span data-ttu-id="8a9be-141">In that case, you should be able to see the status changing every few minutes and the Azure portal may say something like **Recycling**, **Busy**, or **Initializing**.</span><span class="sxs-lookup"><span data-stu-id="8a9be-141">In that case, you should be able to see the status changing every few minutes and the Azure portal may say something like **Recycling**, **Busy**, or **Initializing**.</span></span> <span data-ttu-id="8a9be-142">This indicates that there is something wrong with the application that is keeping the role instance from running.</span><span class="sxs-lookup"><span data-stu-id="8a9be-142">This indicates that there is something wrong with the application that is keeping the role instance from running.</span></span>

<span data-ttu-id="8a9be-143">For more information on how to troubleshoot for this problem, see the blog post [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) and [Common issues that cause roles to recycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).</span><span class="sxs-lookup"><span data-stu-id="8a9be-143">For more information on how to troubleshoot for this problem, see the blog post [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) and [Common issues that cause roles to recycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).</span></span>

## <a name="problem-my-application-stopped-working"></a><span data-ttu-id="8a9be-144">Problem: My application stopped working</span><span class="sxs-lookup"><span data-stu-id="8a9be-144">Problem: My application stopped working</span></span>
1. <span data-ttu-id="8a9be-145">In the Azure portal, click the role instance.</span><span class="sxs-lookup"><span data-stu-id="8a9be-145">In the Azure portal, click the role instance.</span></span>
2. <span data-ttu-id="8a9be-146">In the **Properties** pane of the Azure portal, consider the following conditions to resolve your problem:</span><span class="sxs-lookup"><span data-stu-id="8a9be-146">In the **Properties** pane of the Azure portal, consider the following conditions to resolve your problem:</span></span>
   * <span data-ttu-id="8a9be-147">If the role instance has recently stopped (you can check the value of **Abort count**), the deployment could be updating.</span><span class="sxs-lookup"><span data-stu-id="8a9be-147">If the role instance has recently stopped (you can check the value of **Abort count**), the deployment could be updating.</span></span> <span data-ttu-id="8a9be-148">Wait to see if the role instance resumes functioning on its own.</span><span class="sxs-lookup"><span data-stu-id="8a9be-148">Wait to see if the role instance resumes functioning on its own.</span></span>
   * <span data-ttu-id="8a9be-149">If the role instance is **Busy**, check your application code to see if the [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) event is handled.</span><span class="sxs-lookup"><span data-stu-id="8a9be-149">If the role instance is **Busy**, check your application code to see if the [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) event is handled.</span></span> <span data-ttu-id="8a9be-150">You might need to add or fix some code that handles this event.</span><span class="sxs-lookup"><span data-stu-id="8a9be-150">You might need to add or fix some code that handles this event.</span></span>
   * <span data-ttu-id="8a9be-151">Go through the diagnostic data and troubleshooting scenarios in the blog post [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a9be-151">Go through the diagnostic data and troubleshooting scenarios in the blog post [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="8a9be-152">If you recycle your cloud service, you reset the properties for the deployment, effectively erasing the information for the original problem.</span><span class="sxs-lookup"><span data-stu-id="8a9be-152">If you recycle your cloud service, you reset the properties for the deployment, effectively erasing the information for the original problem.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="8a9be-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="8a9be-153">Next steps</span></span>
<span data-ttu-id="8a9be-154">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span><span class="sxs-lookup"><span data-stu-id="8a9be-154">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="8a9be-155">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a9be-155">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
