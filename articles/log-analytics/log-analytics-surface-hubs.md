---
title: Monitor Surface Hubs with Azure Log Analytics | Microsoft Docs
description: Use the Surface Hub solution to track the health of your Surface Hubs and understand how they are being used.
services: log-analytics
documentationcenter: ''
author: bandersmsft
manager: carmonm
editor: ''
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 66a6cb41f92e7d2d7810dba20b28863bfcb6d1aa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556454"
---
# <a name="monitor-surface-hubs-with-log-analytics-to-track-their-health"></a><span data-ttu-id="ffd57-103">Monitor Surface Hubs with Log Analytics to track their health</span><span class="sxs-lookup"><span data-stu-id="ffd57-103">Monitor Surface Hubs with Log Analytics to track their health</span></span>

<span data-ttu-id="ffd57-104">This article describes how you can use the Surface Hub solution in Log Analytics to monitor Microsoft Surface Hub devices with the Microsoft Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="ffd57-104">This article describes how you can use the Surface Hub solution in Log Analytics to monitor Microsoft Surface Hub devices with the Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="ffd57-105">Log Analytics helps you track the health of your Surface Hubs as well as understand how they are being used.</span><span class="sxs-lookup"><span data-stu-id="ffd57-105">Log Analytics helps you track the health of your Surface Hubs as well as understand how they are being used.</span></span>

<span data-ttu-id="ffd57-106">Each Surface Hub has the Microsoft Monitoring Agent installed.</span><span class="sxs-lookup"><span data-stu-id="ffd57-106">Each Surface Hub has the Microsoft Monitoring Agent installed.</span></span> <span data-ttu-id="ffd57-107">Its through the agent that you can send data from your Surface Hub to OMS.</span><span class="sxs-lookup"><span data-stu-id="ffd57-107">Its through the agent that you can send data from your Surface Hub to OMS.</span></span> <span data-ttu-id="ffd57-108">Log files are read from your Surface Hubs and are then are sent to the OMS service.</span><span class="sxs-lookup"><span data-stu-id="ffd57-108">Log files are read from your Surface Hubs and are then are sent to the OMS service.</span></span> <span data-ttu-id="ffd57-109">Issues like servers being offline, the calendar not syncing, or if the device account is unable to log into Skype are shown in OMS in the Surface Hub dashboard.</span><span class="sxs-lookup"><span data-stu-id="ffd57-109">Issues like servers being offline, the calendar not syncing, or if the device account is unable to log into Skype are shown in OMS in the Surface Hub dashboard.</span></span> <span data-ttu-id="ffd57-110">By using the data in the dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for the detected issues.</span><span class="sxs-lookup"><span data-stu-id="ffd57-110">By using the data in the dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for the detected issues.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="ffd57-111">Installing and configuring the solution</span><span class="sxs-lookup"><span data-stu-id="ffd57-111">Installing and configuring the solution</span></span>
<span data-ttu-id="ffd57-112">Use the following information to install and configure the solution.</span><span class="sxs-lookup"><span data-stu-id="ffd57-112">Use the following information to install and configure the solution.</span></span> <span data-ttu-id="ffd57-113">In order to manage your Surface Hubs from the Microsoft Operations Management Suite (OMS), you'll need the following:</span><span class="sxs-lookup"><span data-stu-id="ffd57-113">In order to manage your Surface Hubs from the Microsoft Operations Management Suite (OMS), you'll need the following:</span></span>

* <span data-ttu-id="ffd57-114">A valid subscription to [OMS](http://www.microsoft.com/oms).</span><span class="sxs-lookup"><span data-stu-id="ffd57-114">A valid subscription to [OMS](http://www.microsoft.com/oms).</span></span>
* <span data-ttu-id="ffd57-115">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support the number of devices you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="ffd57-115">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support the number of devices you want to monitor.</span></span> <span data-ttu-id="ffd57-116">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span><span class="sxs-lookup"><span data-stu-id="ffd57-116">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span></span> <span data-ttu-id="ffd57-117">You'll want to take this into consideration when planning your Surface Hub rollout.</span><span class="sxs-lookup"><span data-stu-id="ffd57-117">You'll want to take this into consideration when planning your Surface Hub rollout.</span></span>

<span data-ttu-id="ffd57-118">Next, you will either add an OMS subscription to your existing Microsoft Azure subscription or create a new workspace directly through the OMS portal.</span><span class="sxs-lookup"><span data-stu-id="ffd57-118">Next, you will either add an OMS subscription to your existing Microsoft Azure subscription or create a new workspace directly through the OMS portal.</span></span> <span data-ttu-id="ffd57-119">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ffd57-119">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span></span> <span data-ttu-id="ffd57-120">Once the OMS subscription is set up, there are two ways to enroll your Surface Hub devices:</span><span class="sxs-lookup"><span data-stu-id="ffd57-120">Once the OMS subscription is set up, there are two ways to enroll your Surface Hub devices:</span></span>

* <span data-ttu-id="ffd57-121">Automatically through InTune</span><span class="sxs-lookup"><span data-stu-id="ffd57-121">Automatically through InTune</span></span>
* <span data-ttu-id="ffd57-122">Manually through **Settings** on your Surface Hub device.</span><span class="sxs-lookup"><span data-stu-id="ffd57-122">Manually through **Settings** on your Surface Hub device.</span></span>

## <a name="set-up-monitoring"></a><span data-ttu-id="ffd57-123">Set up monitoring</span><span class="sxs-lookup"><span data-stu-id="ffd57-123">Set up monitoring</span></span>
<span data-ttu-id="ffd57-124">You can monitor the health and activity of your Surface Hub using Log Analytics in OMS.</span><span class="sxs-lookup"><span data-stu-id="ffd57-124">You can monitor the health and activity of your Surface Hub using Log Analytics in OMS.</span></span> <span data-ttu-id="ffd57-125">You can enroll the Surface Hub in OMS by using InTune, or locally by using **Settings** on the Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="ffd57-125">You can enroll the Surface Hub in OMS by using InTune, or locally by using **Settings** on the Surface Hub.</span></span>

## <a name="connect-surface-hubs-to-oms-through-intune"></a><span data-ttu-id="ffd57-126">Connect Surface Hubs to OMS through InTune</span><span class="sxs-lookup"><span data-stu-id="ffd57-126">Connect Surface Hubs to OMS through InTune</span></span>
<span data-ttu-id="ffd57-127">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span><span class="sxs-lookup"><span data-stu-id="ffd57-127">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="ffd57-128">You can get those from the OMS portal.</span><span class="sxs-lookup"><span data-stu-id="ffd57-128">You can get those from the OMS portal.</span></span>

<span data-ttu-id="ffd57-129">InTune is a Microsoft product that allows you to centrally manage the OMS configuration settings that are applied to one or more of your devices.</span><span class="sxs-lookup"><span data-stu-id="ffd57-129">InTune is a Microsoft product that allows you to centrally manage the OMS configuration settings that are applied to one or more of your devices.</span></span> <span data-ttu-id="ffd57-130">Follow these steps to configure your devices through InTune:</span><span class="sxs-lookup"><span data-stu-id="ffd57-130">Follow these steps to configure your devices through InTune:</span></span>

1. <span data-ttu-id="ffd57-131">Sign in to InTune.</span><span class="sxs-lookup"><span data-stu-id="ffd57-131">Sign in to InTune.</span></span>
2. <span data-ttu-id="ffd57-132">Navigate to **Settings** > **Connected Sources**.</span><span class="sxs-lookup"><span data-stu-id="ffd57-132">Navigate to **Settings** > **Connected Sources**.</span></span>
3. <span data-ttu-id="ffd57-133">Create or edit a policy based on the Surface Hub template.</span><span class="sxs-lookup"><span data-stu-id="ffd57-133">Create or edit a policy based on the Surface Hub template.</span></span>
4. <span data-ttu-id="ffd57-134">Navigate to the OMS (Azure Operational Insights) section of the policy, and add the *Workspace ID* and *Workspace Key* to the policy.</span><span class="sxs-lookup"><span data-stu-id="ffd57-134">Navigate to the OMS (Azure Operational Insights) section of the policy, and add the *Workspace ID* and *Workspace Key* to the policy.</span></span>
5. <span data-ttu-id="ffd57-135">Save the policy.</span><span class="sxs-lookup"><span data-stu-id="ffd57-135">Save the policy.</span></span>
6. <span data-ttu-id="ffd57-136">Associate the policy with the appropriate group of devices.</span><span class="sxs-lookup"><span data-stu-id="ffd57-136">Associate the policy with the appropriate group of devices.</span></span>

   ![InTune policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-surface-hubs/intune.png)

<span data-ttu-id="ffd57-138">InTune then syncs the OMS settings with the devices in the target group, enrolling them in your OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="ffd57-138">InTune then syncs the OMS settings with the devices in the target group, enrolling them in your OMS workspace.</span></span>

## <a name="connect-surface-hubs-to-oms-using-the-settings-app"></a><span data-ttu-id="ffd57-139">Connect Surface Hubs to OMS using the Settings app</span><span class="sxs-lookup"><span data-stu-id="ffd57-139">Connect Surface Hubs to OMS using the Settings app</span></span>
<span data-ttu-id="ffd57-140">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span><span class="sxs-lookup"><span data-stu-id="ffd57-140">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="ffd57-141">You can get those from the OMS portal.</span><span class="sxs-lookup"><span data-stu-id="ffd57-141">You can get those from the OMS portal.</span></span>

<span data-ttu-id="ffd57-142">If you don't use InTune to manage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span><span class="sxs-lookup"><span data-stu-id="ffd57-142">If you don't use InTune to manage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span></span>

1. <span data-ttu-id="ffd57-143">From your Surface Hub, open **Settings**.</span><span class="sxs-lookup"><span data-stu-id="ffd57-143">From your Surface Hub, open **Settings**.</span></span>
2. <span data-ttu-id="ffd57-144">Enter the device admin credentials when prompted.</span><span class="sxs-lookup"><span data-stu-id="ffd57-144">Enter the device admin credentials when prompted.</span></span>
3. <span data-ttu-id="ffd57-145">Click **This device**, and the under **Monitoring**, click **Configure OMS Settings**.</span><span class="sxs-lookup"><span data-stu-id="ffd57-145">Click **This device**, and the under **Monitoring**, click **Configure OMS Settings**.</span></span>
4. <span data-ttu-id="ffd57-146">Select **Enable monitoring**.</span><span class="sxs-lookup"><span data-stu-id="ffd57-146">Select **Enable monitoring**.</span></span>
5. <span data-ttu-id="ffd57-147">In the OMS settings dialog, type the **Workspace ID** and type the **Workspace Key**.</span><span class="sxs-lookup"><span data-stu-id="ffd57-147">In the OMS settings dialog, type the **Workspace ID** and type the **Workspace Key**.</span></span>  
   <span data-ttu-id="ffd57-148">![settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-surface-hubs/settings.png)</span><span class="sxs-lookup"><span data-stu-id="ffd57-148">![settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-surface-hubs/settings.png)</span></span>
6. <span data-ttu-id="ffd57-149">Click **OK** to complete the configuration.</span><span class="sxs-lookup"><span data-stu-id="ffd57-149">Click **OK** to complete the configuration.</span></span>

<span data-ttu-id="ffd57-150">A confirmation appears telling you whether or not the OMS configuration was successfully applied to the device.</span><span class="sxs-lookup"><span data-stu-id="ffd57-150">A confirmation appears telling you whether or not the OMS configuration was successfully applied to the device.</span></span> <span data-ttu-id="ffd57-151">If it was, a message appears stating that the agent successfully connected to the OMS service.</span><span class="sxs-lookup"><span data-stu-id="ffd57-151">If it was, a message appears stating that the agent successfully connected to the OMS service.</span></span> <span data-ttu-id="ffd57-152">The device then starts sending data to OMS where you can view and act on it.</span><span class="sxs-lookup"><span data-stu-id="ffd57-152">The device then starts sending data to OMS where you can view and act on it.</span></span>

## <a name="monitor-surface-hubs"></a><span data-ttu-id="ffd57-153">Monitor Surface Hubs</span><span class="sxs-lookup"><span data-stu-id="ffd57-153">Monitor Surface Hubs</span></span>
<span data-ttu-id="ffd57-154">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span><span class="sxs-lookup"><span data-stu-id="ffd57-154">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span></span>

1. <span data-ttu-id="ffd57-155">Sign in to the OMS portal.</span><span class="sxs-lookup"><span data-stu-id="ffd57-155">Sign in to the OMS portal.</span></span>
2. <span data-ttu-id="ffd57-156">Navigate to the Surface Hub solution pack dashboard.</span><span class="sxs-lookup"><span data-stu-id="ffd57-156">Navigate to the Surface Hub solution pack dashboard.</span></span>
3. <span data-ttu-id="ffd57-157">Your device's health is displayed.</span><span class="sxs-lookup"><span data-stu-id="ffd57-157">Your device's health is displayed.</span></span>

   ![Surface Hub dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-surface-hubs/surface-hub-dashboard.png)

<span data-ttu-id="ffd57-159">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span><span class="sxs-lookup"><span data-stu-id="ffd57-159">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span></span> <span data-ttu-id="ffd57-160">Using the data the OMS collects from your Surface Hubs, you can search for issues and alert on the conditions that you define for your devices.</span><span class="sxs-lookup"><span data-stu-id="ffd57-160">Using the data the OMS collects from your Surface Hubs, you can search for issues and alert on the conditions that you define for your devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffd57-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="ffd57-161">Next steps</span></span>
* <span data-ttu-id="ffd57-162">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Surface Hub data.</span><span class="sxs-lookup"><span data-stu-id="ffd57-162">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Surface Hub data.</span></span>
* <span data-ttu-id="ffd57-163">Create [alerts](log-analytics-alerts.md) to notify you when issues occur with your Surface Hubs.</span><span class="sxs-lookup"><span data-stu-id="ffd57-163">Create [alerts](log-analytics-alerts.md) to notify you when issues occur with your Surface Hubs.</span></span>



