---
title: Migrate your OMS Update Deployments to Azure
description: This article describes how to migrate your existing OMS Update deployments to Azure
services: automation
ms.service: automation
ms.component: update-management
author: georgewallace
ms.author: gwallace
ms.date: 07/16/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: d0b380aa6046daa235098516a8c93d3ba72533a6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868265"
---
# <a name="migrate-your-oms-update-deployments-to-azure"></a><span data-ttu-id="01a7b-103">Migrate your OMS Update Deployments to Azure</span><span class="sxs-lookup"><span data-stu-id="01a7b-103">Migrate your OMS Update Deployments to Azure</span></span>

<span data-ttu-id="01a7b-104">The Operations Management Suite (OMS) portal is being [deprecated](../log-analytics/log-analytics-oms-portal-transition.md).</span><span class="sxs-lookup"><span data-stu-id="01a7b-104">The Operations Management Suite (OMS) portal is being [deprecated](../log-analytics/log-analytics-oms-portal-transition.md).</span></span> <span data-ttu-id="01a7b-105">All functionality that was available in the OMS portal for Update Management is available in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="01a7b-105">All functionality that was available in the OMS portal for Update Management is available in the Azure portal.</span></span> <span data-ttu-id="01a7b-106">This article provides the information you need in order to migrate to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="01a7b-106">This article provides the information you need in order to migrate to the Azure portal.</span></span>

## <a name="key-information"></a><span data-ttu-id="01a7b-107">Key information</span><span class="sxs-lookup"><span data-stu-id="01a7b-107">Key information</span></span>

* <span data-ttu-id="01a7b-108">Existing deployments will continue to work.</span><span class="sxs-lookup"><span data-stu-id="01a7b-108">Existing deployments will continue to work.</span></span> <span data-ttu-id="01a7b-109">Once you have recreated the deployment in Azure, you can delete your old deployment from OMS.</span><span class="sxs-lookup"><span data-stu-id="01a7b-109">Once you have recreated the deployment in Azure, you can delete your old deployment from OMS.</span></span>
* <span data-ttu-id="01a7b-110">All existing features you had in OMS are available in Azure, to learn more about Update Management, see [Update Management overview](automation-update-management.md).</span><span class="sxs-lookup"><span data-stu-id="01a7b-110">All existing features you had in OMS are available in Azure, to learn more about Update Management, see [Update Management overview](automation-update-management.md).</span></span>

## <a name="access-the-azure-portal"></a><span data-ttu-id="01a7b-111">Access the Azure portal</span><span class="sxs-lookup"><span data-stu-id="01a7b-111">Access the Azure portal</span></span>

<span data-ttu-id="01a7b-112">From your OMS workspace, click **Open in Azure**.</span><span class="sxs-lookup"><span data-stu-id="01a7b-112">From your OMS workspace, click **Open in Azure**.</span></span> <span data-ttu-id="01a7b-113">This navigates to the Log Analytics workspace that OMS used.</span><span class="sxs-lookup"><span data-stu-id="01a7b-113">This navigates to the Log Analytics workspace that OMS used.</span></span>

![Open in Azure - OMS portal](media/migrate-oms-update-deployments/link-to-azure-portal.png)

<span data-ttu-id="01a7b-115">In the Azure portal, click **Automation Account**</span><span class="sxs-lookup"><span data-stu-id="01a7b-115">In the Azure portal, click **Automation Account**</span></span>

![Log Analytics](media/migrate-oms-update-deployments/log-analytics.png)

<span data-ttu-id="01a7b-117">In your Automation Account, click **Update Management** to open up Update Management.</span><span class="sxs-lookup"><span data-stu-id="01a7b-117">In your Automation Account, click **Update Management** to open up Update Management.</span></span>

![Update Management](media/migrate-oms-update-deployments/azure-automation.png)

<span data-ttu-id="01a7b-119">In the future you can go directly to the Azure portal, under **All services**, select **Automation Accounts** under **Management Tools**, select the appropriate Automation Account, and click **Update Management**.</span><span class="sxs-lookup"><span data-stu-id="01a7b-119">In the future you can go directly to the Azure portal, under **All services**, select **Automation Accounts** under **Management Tools**, select the appropriate Automation Account, and click **Update Management**.</span></span>

## <a name="recreate-existing-deployments"></a><span data-ttu-id="01a7b-120">Recreate existing deployments</span><span class="sxs-lookup"><span data-stu-id="01a7b-120">Recreate existing deployments</span></span>

<span data-ttu-id="01a7b-121">All update deployments created in the OMS portal have a [saved search](../log-analytics/log-analytics-computer-groups.md) also known as a computer group, with the same name as the update deployment that exists.</span><span class="sxs-lookup"><span data-stu-id="01a7b-121">All update deployments created in the OMS portal have a [saved search](../log-analytics/log-analytics-computer-groups.md) also known as a computer group, with the same name as the update deployment that exists.</span></span> <span data-ttu-id="01a7b-122">The saved search contains the list of machines that were scheduled in the update deployment.</span><span class="sxs-lookup"><span data-stu-id="01a7b-122">The saved search contains the list of machines that were scheduled in the update deployment.</span></span>

![Update Management](media/migrate-oms-update-deployments/oms-deployment.png)

<span data-ttu-id="01a7b-124">To use this existing saved search, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="01a7b-124">To use this existing saved search, follow these steps:</span></span>

<span data-ttu-id="01a7b-125">To create a new update deployment, go to the Azure portal, select the Automation Account that is used, and click **Update Management**.</span><span class="sxs-lookup"><span data-stu-id="01a7b-125">To create a new update deployment, go to the Azure portal, select the Automation Account that is used, and click **Update Management**.</span></span> <span data-ttu-id="01a7b-126">Click **Schedule update deployment**.</span><span class="sxs-lookup"><span data-stu-id="01a7b-126">Click **Schedule update deployment**.</span></span>

![Schedule update deployment](media/migrate-oms-update-deployments/schedule-update-deployment.png)

<span data-ttu-id="01a7b-128">The **New Update Deployment** pane opens.</span><span class="sxs-lookup"><span data-stu-id="01a7b-128">The **New Update Deployment** pane opens.</span></span> <span data-ttu-id="01a7b-129">Enter values for the properties described in the following table and then click **Create**:</span><span class="sxs-lookup"><span data-stu-id="01a7b-129">Enter values for the properties described in the following table and then click **Create**:</span></span>

<span data-ttu-id="01a7b-130">For Machines to update, select the saved search used by the existing OMS deployment.</span><span class="sxs-lookup"><span data-stu-id="01a7b-130">For Machines to update, select the saved search used by the existing OMS deployment.</span></span>

| <span data-ttu-id="01a7b-131">Property</span><span class="sxs-lookup"><span data-stu-id="01a7b-131">Property</span></span> | <span data-ttu-id="01a7b-132">Description</span><span class="sxs-lookup"><span data-stu-id="01a7b-132">Description</span></span> |
| --- | --- |
|<span data-ttu-id="01a7b-133">Name</span><span class="sxs-lookup"><span data-stu-id="01a7b-133">Name</span></span> |<span data-ttu-id="01a7b-134">Unique name to identify the update deployment.</span><span class="sxs-lookup"><span data-stu-id="01a7b-134">Unique name to identify the update deployment.</span></span> |
|<span data-ttu-id="01a7b-135">Operating System</span><span class="sxs-lookup"><span data-stu-id="01a7b-135">Operating System</span></span>| <span data-ttu-id="01a7b-136">Select **Linux** or **Windows**.</span><span class="sxs-lookup"><span data-stu-id="01a7b-136">Select **Linux** or **Windows**.</span></span>|
|<span data-ttu-id="01a7b-137">Machines to update</span><span class="sxs-lookup"><span data-stu-id="01a7b-137">Machines to update</span></span> |<span data-ttu-id="01a7b-138">Select a Saved search, Imported group, or pick Machine from the drop-down and select individual machines.</span><span class="sxs-lookup"><span data-stu-id="01a7b-138">Select a Saved search, Imported group, or pick Machine from the drop-down and select individual machines.</span></span> <span data-ttu-id="01a7b-139">If you choose **Machines**, the readiness of the machine is shown in the **UPDATE AGENT READINESS** column.</span><span class="sxs-lookup"><span data-stu-id="01a7b-139">If you choose **Machines**, the readiness of the machine is shown in the **UPDATE AGENT READINESS** column.</span></span></br> <span data-ttu-id="01a7b-140">To learn about the different methods of creating computer groups in Log Analytics, see [Computer groups in Log Analytics](../log-analytics/log-analytics-computer-groups.md)</span><span class="sxs-lookup"><span data-stu-id="01a7b-140">To learn about the different methods of creating computer groups in Log Analytics, see [Computer groups in Log Analytics](../log-analytics/log-analytics-computer-groups.md)</span></span> |
|<span data-ttu-id="01a7b-141">Update classifications</span><span class="sxs-lookup"><span data-stu-id="01a7b-141">Update classifications</span></span>|<span data-ttu-id="01a7b-142">Select all the update classifications that you need.</span><span class="sxs-lookup"><span data-stu-id="01a7b-142">Select all the update classifications that you need.</span></span> <span data-ttu-id="01a7b-143">CentOS does not support this out of the box.</span><span class="sxs-lookup"><span data-stu-id="01a7b-143">CentOS does not support this out of the box.</span></span>|
|<span data-ttu-id="01a7b-144">Updates to exclude</span><span class="sxs-lookup"><span data-stu-id="01a7b-144">Updates to exclude</span></span>|<span data-ttu-id="01a7b-145">Enter the updates to exclude.</span><span class="sxs-lookup"><span data-stu-id="01a7b-145">Enter the updates to exclude.</span></span> <span data-ttu-id="01a7b-146">For Windows, enter the KB article without the **KB** prefix.</span><span class="sxs-lookup"><span data-stu-id="01a7b-146">For Windows, enter the KB article without the **KB** prefix.</span></span> <span data-ttu-id="01a7b-147">For Linux, enter the package name or use a wildcard character.</span><span class="sxs-lookup"><span data-stu-id="01a7b-147">For Linux, enter the package name or use a wildcard character.</span></span>  |
|<span data-ttu-id="01a7b-148">Schedule settings</span><span class="sxs-lookup"><span data-stu-id="01a7b-148">Schedule settings</span></span>|<span data-ttu-id="01a7b-149">Select the time to start, and then select either **Once** or **Recurring** for the recurrence.</span><span class="sxs-lookup"><span data-stu-id="01a7b-149">Select the time to start, and then select either **Once** or **Recurring** for the recurrence.</span></span>|| <span data-ttu-id="01a7b-150">Maintenance window</span><span class="sxs-lookup"><span data-stu-id="01a7b-150">Maintenance window</span></span> |<span data-ttu-id="01a7b-151">Number of minutes set for updates.</span><span class="sxs-lookup"><span data-stu-id="01a7b-151">Number of minutes set for updates.</span></span> <span data-ttu-id="01a7b-152">The value can't be less than 30 minutes or more than 6 hours.</span><span class="sxs-lookup"><span data-stu-id="01a7b-152">The value can't be less than 30 minutes or more than 6 hours.</span></span> |
| <span data-ttu-id="01a7b-153">Maintenance window</span><span class="sxs-lookup"><span data-stu-id="01a7b-153">Maintenance window</span></span> |<span data-ttu-id="01a7b-154">Number of minutes set for updates.</span><span class="sxs-lookup"><span data-stu-id="01a7b-154">Number of minutes set for updates.</span></span> <span data-ttu-id="01a7b-155">The value can be not be less than 30 minutes and no more than 6 hours</span><span class="sxs-lookup"><span data-stu-id="01a7b-155">The value can be not be less than 30 minutes and no more than 6 hours</span></span> |
| <span data-ttu-id="01a7b-156">Reboot control</span><span class="sxs-lookup"><span data-stu-id="01a7b-156">Reboot control</span></span>| <span data-ttu-id="01a7b-157">Detemines how reboots should be handled.</span><span class="sxs-lookup"><span data-stu-id="01a7b-157">Detemines how reboots should be handled.</span></span></br><span data-ttu-id="01a7b-158">Available options are:</span><span class="sxs-lookup"><span data-stu-id="01a7b-158">Available options are:</span></span></br><span data-ttu-id="01a7b-159">Reboot if required (Default)</span><span class="sxs-lookup"><span data-stu-id="01a7b-159">Reboot if required (Default)</span></span></br><span data-ttu-id="01a7b-160">Always reboot</span><span class="sxs-lookup"><span data-stu-id="01a7b-160">Always reboot</span></span></br><span data-ttu-id="01a7b-161">Never reboot</span><span class="sxs-lookup"><span data-stu-id="01a7b-161">Never reboot</span></span></br><span data-ttu-id="01a7b-162">Only reboot - will not install updates</span><span class="sxs-lookup"><span data-stu-id="01a7b-162">Only reboot - will not install updates</span></span>|

<span data-ttu-id="01a7b-163">Click **Scheduled update deployments** to view the status of the newly created update deployment.</span><span class="sxs-lookup"><span data-stu-id="01a7b-163">Click **Scheduled update deployments** to view the status of the newly created update deployment.</span></span>

![new update deployment](media/migrate-oms-update-deployments/new-update-deployment.png)

<span data-ttu-id="01a7b-165">As mentioned previously, once your new deployments are configured through the Azure portal, the existing deployments can be removed from the OMS portal.</span><span class="sxs-lookup"><span data-stu-id="01a7b-165">As mentioned previously, once your new deployments are configured through the Azure portal, the existing deployments can be removed from the OMS portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01a7b-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="01a7b-166">Next steps</span></span>

<span data-ttu-id="01a7b-167">To learn more about Update Management in Azure, see [Update Management](automation-update-management.md)</span><span class="sxs-lookup"><span data-stu-id="01a7b-167">To learn more about Update Management in Azure, see [Update Management](automation-update-management.md)</span></span>