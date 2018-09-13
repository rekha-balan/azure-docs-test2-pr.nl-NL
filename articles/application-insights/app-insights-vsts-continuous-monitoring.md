---
title: Continuous Monitoring of your DevOps release pipeline with Azure DevOps and Azure Application Insights  | Microsoft Docs
description: Provides instructions to quickly setup continuous monitoring with Application Insights
services: application-insights
keywords: ''
author: mrbullwinkle
ms.author: mbullwin
ms.date: 11/13/2017
ms.service: application-insights
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: ecda8621640223f1c27f32834f2e4a098da4aba6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857783"
---
# <a name="add-continuous-monitoring-to-your-release-pipeline"></a><span data-ttu-id="7309f-103">Add continuous monitoring to your release pipeline</span><span class="sxs-lookup"><span data-stu-id="7309f-103">Add continuous monitoring to your release pipeline</span></span>

<span data-ttu-id="7309f-104">Azure DevOps Services integrates with Azure Application Insights to allow continuous monitoring of your DevOps release pipeline throughout the software development lifecycle.</span><span class="sxs-lookup"><span data-stu-id="7309f-104">Azure DevOps Services integrates with Azure Application Insights to allow continuous monitoring of your DevOps release pipeline throughout the software development lifecycle.</span></span> 

<span data-ttu-id="7309f-105">Azure DevOps Services now supports continuous monitoring whereby release pipelines can incorporate monitoring data from Application Insights and other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="7309f-105">Azure DevOps Services now supports continuous monitoring whereby release pipelines can incorporate monitoring data from Application Insights and other Azure resources.</span></span> <span data-ttu-id="7309f-106">When an Application Insights alert is detected, the deployment can remain gated or be rolled back until the alert is resolved.</span><span class="sxs-lookup"><span data-stu-id="7309f-106">When an Application Insights alert is detected, the deployment can remain gated or be rolled back until the alert is resolved.</span></span> <span data-ttu-id="7309f-107">If all checks pass, deployments can proceed automatically from test all the way to production without the need for manual intervention.</span><span class="sxs-lookup"><span data-stu-id="7309f-107">If all checks pass, deployments can proceed automatically from test all the way to production without the need for manual intervention.</span></span> 

## <a name="configure-continuous-monitoring"></a><span data-ttu-id="7309f-108">Configure continuous monitoring</span><span class="sxs-lookup"><span data-stu-id="7309f-108">Configure continuous monitoring</span></span>

1. <span data-ttu-id="7309f-109">Select an existing Azure DevOps Services Project.</span><span class="sxs-lookup"><span data-stu-id="7309f-109">Select an existing Azure DevOps Services Project.</span></span>

2. <span data-ttu-id="7309f-110">Hover over **Build and Release** > Select **Releases** > Click the **plus sign** > **Create release definition** > Search for **Monitoring** > **Azure App Service Deployment with Continuous Monitoring.**</span><span class="sxs-lookup"><span data-stu-id="7309f-110">Hover over **Build and Release** > Select **Releases** > Click the **plus sign** > **Create release definition** > Search for **Monitoring** > **Azure App Service Deployment with Continuous Monitoring.**</span></span>

   ![New Azure DevOps Services Release Pipeline](.\media\app-insights-continuous-monitoring\001.png)

3. <span data-ttu-id="7309f-112">Click **Apply.**</span><span class="sxs-lookup"><span data-stu-id="7309f-112">Click **Apply.**</span></span>

4. <span data-ttu-id="7309f-113">Next to the red exclamation point select the text in blue to **View environment tasks.**</span><span class="sxs-lookup"><span data-stu-id="7309f-113">Next to the red exclamation point select the text in blue to **View environment tasks.**</span></span>

   ![View environment tasks](.\media\app-insights-continuous-monitoring\002.png)

   <span data-ttu-id="7309f-115">A configuration box will appear, use the following table to fill out the input fields.</span><span class="sxs-lookup"><span data-stu-id="7309f-115">A configuration box will appear, use the following table to fill out the input fields.</span></span>

    | <span data-ttu-id="7309f-116">Parameter</span><span class="sxs-lookup"><span data-stu-id="7309f-116">Parameter</span></span>        | <span data-ttu-id="7309f-117">Value</span><span class="sxs-lookup"><span data-stu-id="7309f-117">Value</span></span> |
   | ------------- |:-----|
   | <span data-ttu-id="7309f-118">**Environment name**</span><span class="sxs-lookup"><span data-stu-id="7309f-118">**Environment name**</span></span>      | <span data-ttu-id="7309f-119">Name that describes the release pipeline environment</span><span class="sxs-lookup"><span data-stu-id="7309f-119">Name that describes the release pipeline environment</span></span> |
   | <span data-ttu-id="7309f-120">**Azure subscription**</span><span class="sxs-lookup"><span data-stu-id="7309f-120">**Azure subscription**</span></span> | <span data-ttu-id="7309f-121">Drop-down populates with any Azure subscriptions linked to the Azure DevOps Services organization</span><span class="sxs-lookup"><span data-stu-id="7309f-121">Drop-down populates with any Azure subscriptions linked to the Azure DevOps Services organization</span></span>|
   | <span data-ttu-id="7309f-122">**App Service name**</span><span class="sxs-lookup"><span data-stu-id="7309f-122">**App Service name**</span></span> | <span data-ttu-id="7309f-123">Manual entry of a new value may be required for this field depending on other selections</span><span class="sxs-lookup"><span data-stu-id="7309f-123">Manual entry of a new value may be required for this field depending on other selections</span></span> |
   | <span data-ttu-id="7309f-124">**Resource Group**</span><span class="sxs-lookup"><span data-stu-id="7309f-124">**Resource Group**</span></span>    | <span data-ttu-id="7309f-125">Drop-down populates with available Resource Groups</span><span class="sxs-lookup"><span data-stu-id="7309f-125">Drop-down populates with available Resource Groups</span></span> |
   | <span data-ttu-id="7309f-126">**Application Insights resource name**</span><span class="sxs-lookup"><span data-stu-id="7309f-126">**Application Insights resource name**</span></span> | <span data-ttu-id="7309f-127">Drop-down populates with all Application Insights resources that correspond to the previously selected resource group.</span><span class="sxs-lookup"><span data-stu-id="7309f-127">Drop-down populates with all Application Insights resources that correspond to the previously selected resource group.</span></span>

5. <span data-ttu-id="7309f-128">Select **Configure Application Insights alerts**</span><span class="sxs-lookup"><span data-stu-id="7309f-128">Select **Configure Application Insights alerts**</span></span>

6. <span data-ttu-id="7309f-129">For default alert rules, select **Save** > Enter a descriptive comment > Click **OK**</span><span class="sxs-lookup"><span data-stu-id="7309f-129">For default alert rules, select **Save** > Enter a descriptive comment > Click **OK**</span></span>

## <a name="modify-alert-rules"></a><span data-ttu-id="7309f-130">Modify alert rules</span><span class="sxs-lookup"><span data-stu-id="7309f-130">Modify alert rules</span></span>

1. <span data-ttu-id="7309f-131">To modify the predefined Alert settings, click the box with **ellipses ...** to the right of **Alert rules.**</span><span class="sxs-lookup"><span data-stu-id="7309f-131">To modify the predefined Alert settings, click the box with **ellipses ...** to the right of **Alert rules.**</span></span>

   <span data-ttu-id="7309f-132">(Out-of-box four alert rules are present: Availability, Failed requests, Server response time, Server exceptions.)</span><span class="sxs-lookup"><span data-stu-id="7309f-132">(Out-of-box four alert rules are present: Availability, Failed requests, Server response time, Server exceptions.)</span></span>

2. <span data-ttu-id="7309f-133">Click the drop-down symbol next to **Availability.**</span><span class="sxs-lookup"><span data-stu-id="7309f-133">Click the drop-down symbol next to **Availability.**</span></span>

3. <span data-ttu-id="7309f-134">Modify the availability **Threshold** to meet your service level requirements.</span><span class="sxs-lookup"><span data-stu-id="7309f-134">Modify the availability **Threshold** to meet your service level requirements.</span></span>

   ![Modify Alert](.\media\app-insights-continuous-monitoring\003.png)

4. <span data-ttu-id="7309f-136">Select **OK** > **Save** > Enter a descriptive comment > Click **OK.**</span><span class="sxs-lookup"><span data-stu-id="7309f-136">Select **OK** > **Save** > Enter a descriptive comment > Click **OK.**</span></span>

## <a name="add-deployment-conditions"></a><span data-ttu-id="7309f-137">Add deployment conditions</span><span class="sxs-lookup"><span data-stu-id="7309f-137">Add deployment conditions</span></span>

1. <span data-ttu-id="7309f-138">Click **Pipeline** > Select the **Pre** or **Post-deployment conditions** symbol depending on the stage that requires a continuous monitoring gate.</span><span class="sxs-lookup"><span data-stu-id="7309f-138">Click **Pipeline** > Select the **Pre** or **Post-deployment conditions** symbol depending on the stage that requires a continuous monitoring gate.</span></span>

   ![Pre-Deployment Conditions](.\media\app-insights-continuous-monitoring\004.png)

2. <span data-ttu-id="7309f-140">Set **Gates** to  **Enabled** > **Approval gates**>  Click **Add.**</span><span class="sxs-lookup"><span data-stu-id="7309f-140">Set **Gates** to  **Enabled** > **Approval gates**>  Click **Add.**</span></span>

3. <span data-ttu-id="7309f-141">Select **Azure Monitor** (This option gives you the ability to access alerts both from Azure Monitor and Application Insights)</span><span class="sxs-lookup"><span data-stu-id="7309f-141">Select **Azure Monitor** (This option gives you the ability to access alerts both from Azure Monitor and Application Insights)</span></span>

    ![Azure Monitor](.\media\app-insights-continuous-monitoring\005.png)

4. <span data-ttu-id="7309f-143">Enter a **Gates timeout** value.</span><span class="sxs-lookup"><span data-stu-id="7309f-143">Enter a **Gates timeout** value.</span></span>

5. <span data-ttu-id="7309f-144">Enter a **Sampling Interval.**</span><span class="sxs-lookup"><span data-stu-id="7309f-144">Enter a **Sampling Interval.**</span></span>

## <a name="deployment-gate-status-logs"></a><span data-ttu-id="7309f-145">Deployment gate status logs</span><span class="sxs-lookup"><span data-stu-id="7309f-145">Deployment gate status logs</span></span>

<span data-ttu-id="7309f-146">Once you add deployment gates, an alert in Application Insights which exceeds your previously defined threshold, guards your deployment from unwanted release promotion.</span><span class="sxs-lookup"><span data-stu-id="7309f-146">Once you add deployment gates, an alert in Application Insights which exceeds your previously defined threshold, guards your deployment from unwanted release promotion.</span></span> <span data-ttu-id="7309f-147">Once the alert is resolved, the deployment can proceed automatically.</span><span class="sxs-lookup"><span data-stu-id="7309f-147">Once the alert is resolved, the deployment can proceed automatically.</span></span>

<span data-ttu-id="7309f-148">To observe this behavior, Select **Releases** > Right-click Release name **open** > **Logs.**</span><span class="sxs-lookup"><span data-stu-id="7309f-148">To observe this behavior, Select **Releases** > Right-click Release name **open** > **Logs.**</span></span>

![Logs](.\media\app-insights-continuous-monitoring\006.png)

## <a name="next-steps"></a><span data-ttu-id="7309f-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="7309f-150">Next steps</span></span>

<span data-ttu-id="7309f-151">To learn more about Azure Pipelines try these [quickstarts.](https://docs.microsoft.com/azure/devops/pipelines)</span><span class="sxs-lookup"><span data-stu-id="7309f-151">To learn more about Azure Pipelines try these [quickstarts.](https://docs.microsoft.com/azure/devops/pipelines)</span></span>
