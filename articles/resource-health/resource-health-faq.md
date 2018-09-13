---
title: Azure Resource health FAQ | Microsoft Docs
description: Overview of Azure Resource health
services: Resource health
documentationcenter: dev-center-name
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
ms.openlocfilehash: 570688ae363e223d792bec8e6b13d4ec50412130
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563391"
---
# <a name="azure-resource-health-faq"></a><span data-ttu-id="12f23-103">Azure Resource health FAQ</span><span class="sxs-lookup"><span data-stu-id="12f23-103">Azure Resource health FAQ</span></span>
<span data-ttu-id="12f23-104">Learn the answers to common questions about Azure resource health.</span><span class="sxs-lookup"><span data-stu-id="12f23-104">Learn the answers to common questions about Azure resource health.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="12f23-105">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="12f23-105">Frequently asked questions</span></span>
* [<span data-ttu-id="12f23-106">What is Azure resource health?</span><span class="sxs-lookup"><span data-stu-id="12f23-106">What is Azure resource health?</span></span>](#what-is-azure-resource-health)
* [<span data-ttu-id="12f23-107">What is the resource health intended for?</span><span class="sxs-lookup"><span data-stu-id="12f23-107">What is the resource health intended for?</span></span>](#what-is-the-resource-health-intended-for)
* [<span data-ttu-id="12f23-108">What health checks are performed by resource health?</span><span class="sxs-lookup"><span data-stu-id="12f23-108">What health checks are performed by resource health?</span></span>](#what-health-checks-are-performed-by-resource-health)
* [<span data-ttu-id="12f23-109">What does each of the health status mean?</span><span class="sxs-lookup"><span data-stu-id="12f23-109">What does each of the health status mean?</span></span>](#what-does-each-of-the-health-status-mean)
* [<span data-ttu-id="12f23-110">What does the unknown status mean? Is something wrong with my resource?</span><span class="sxs-lookup"><span data-stu-id="12f23-110">What does the unknown status mean? Is something wrong with my resource?</span></span>](#what-does-the-unknown-status-mean-is-something-wrong-with-my-resource)
* [<span data-ttu-id="12f23-111">How can I get help for a resource that is unavailable?</span><span class="sxs-lookup"><span data-stu-id="12f23-111">How can I get help for a resource that is unavailable?</span></span>](#how-can-i-get-help-for-a-resource-that-is-unavailable)
* [<span data-ttu-id="12f23-112">Does resource health differentiate between unavailability cased by platform problems versus something I did?</span><span class="sxs-lookup"><span data-stu-id="12f23-112">Does resource health differentiate between unavailability cased by platform problems versus something I did?</span></span>](#does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did)
* [<span data-ttu-id="12f23-113">Can I integrate resource health with my monitoring tools?</span><span class="sxs-lookup"><span data-stu-id="12f23-113">Can I integrate resource health with my monitoring tools?</span></span>](#can-i-integrate-resource-health-with-my-monitoring-tools)
* [<span data-ttu-id="12f23-114">Where do I find resource health?</span><span class="sxs-lookup"><span data-stu-id="12f23-114">Where do I find resource health?</span></span>](#where-do-i-find-resource-health)
* [<span data-ttu-id="12f23-115">Is resource health available for all resource types?</span><span class="sxs-lookup"><span data-stu-id="12f23-115">Is resource health available for all resource types?</span></span>](#is-resource-health-available-for-all-resource-types)
* [<span data-ttu-id="12f23-116">What should I do if my resource is showing available but I believe it is not?</span><span class="sxs-lookup"><span data-stu-id="12f23-116">What should I do if my resource is showing available but I believe it is not?</span></span>](#what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not)
* [<span data-ttu-id="12f23-117">Is resource health available for all Azure regions?</span><span class="sxs-lookup"><span data-stu-id="12f23-117">Is resource health available for all Azure regions?</span></span>](#is-resource-health-available-for-all-azure-regions)
* [<span data-ttu-id="12f23-118">How is resource health different from the Service Health Dashboard or the Azure portal service notifications?</span><span class="sxs-lookup"><span data-stu-id="12f23-118">How is resource health different from the Service Health Dashboard or the Azure portal service notifications?</span></span>](#how-is-resource-health-different-from-the-service-health-dashboard-or-the-azure-portal-service-notifications)
* [<span data-ttu-id="12f23-119">Do I need to activate resource health for each resource?</span><span class="sxs-lookup"><span data-stu-id="12f23-119">Do I need to activate resource health for each resource?</span></span>](#do-i-need-to-activate-resource-health-for-each-resource)
* [<span data-ttu-id="12f23-120">Do we need to enable resource health for my organization?</span><span class="sxs-lookup"><span data-stu-id="12f23-120">Do we need to enable resource health for my organization?</span></span>](#do-we-need-to-enable-resource-health-for-my-organization)
* [<span data-ttu-id="12f23-121">Is resource health available free of charge?</span><span class="sxs-lookup"><span data-stu-id="12f23-121">Is resource health available free of charge?</span></span>](#is-resource-health-available-free-of-charge)
* [<span data-ttu-id="12f23-122">What are the recommendations that resource health provides?</span><span class="sxs-lookup"><span data-stu-id="12f23-122">What are the recommendations that resource health provides?</span></span>](#what-are-the-recommendations-that-resource-health-provides)


## <a name="what-is-azure-resource-health"></a><span data-ttu-id="12f23-123">What is Azure resource health?</span><span class="sxs-lookup"><span data-stu-id="12f23-123">What is Azure resource health?</span></span>
<span data-ttu-id="12f23-124">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span><span class="sxs-lookup"><span data-stu-id="12f23-124">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="12f23-125">It informs you about the current and past health of your resources and helps you mitigate issues.</span><span class="sxs-lookup"><span data-stu-id="12f23-125">It informs you about the current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="12f23-126">Resource health provides technical support when you need help with Azure service issues.</span><span class="sxs-lookup"><span data-stu-id="12f23-126">Resource health provides technical support when you need help with Azure service issues.</span></span>  

## <a name="what-is-the-resource-health-intended-for"></a><span data-ttu-id="12f23-127">What is the resource health intended for?</span><span class="sxs-lookup"><span data-stu-id="12f23-127">What is the resource health intended for?</span></span>
<span data-ttu-id="12f23-128">Once an issue with a resource has been detected, resource health can help you diagnose the root cause.</span><span class="sxs-lookup"><span data-stu-id="12f23-128">Once an issue with a resource has been detected, resource health can help you diagnose the root cause.</span></span> <span data-ttu-id="12f23-129">It provides help to mitigate the issue and technical support when you need more help with Azure service issues.</span><span class="sxs-lookup"><span data-stu-id="12f23-129">It provides help to mitigate the issue and technical support when you need more help with Azure service issues.</span></span>

## <a name="what-health-checks-are-performed-by-resource-health"></a><span data-ttu-id="12f23-130">What health checks are performed by resource health?</span><span class="sxs-lookup"><span data-stu-id="12f23-130">What health checks are performed by resource health?</span></span>
<span data-ttu-id="12f23-131">Resource health performs various checks based on the [resource type](resource-health-checks-resource-types.md).</span><span class="sxs-lookup"><span data-stu-id="12f23-131">Resource health performs various checks based on the [resource type](resource-health-checks-resource-types.md).</span></span> <span data-ttu-id="12f23-132">These checks are designed to implement three types of issues:</span><span class="sxs-lookup"><span data-stu-id="12f23-132">These checks are designed to implement three types of issues:</span></span> 
1. <span data-ttu-id="12f23-133">Unplanned events, for example an unexpected host reboot</span><span class="sxs-lookup"><span data-stu-id="12f23-133">Unplanned events, for example an unexpected host reboot</span></span>
2. <span data-ttu-id="12f23-134">Planned events, like scheduled host OS updates</span><span class="sxs-lookup"><span data-stu-id="12f23-134">Planned events, like scheduled host OS updates</span></span>
3. <span data-ttu-id="12f23-135">Events triggered by user actions, for example a user rebooting a virtual machine</span><span class="sxs-lookup"><span data-stu-id="12f23-135">Events triggered by user actions, for example a user rebooting a virtual machine</span></span>

## <a name="what-does-each-of-the-health-status-mean"></a><span data-ttu-id="12f23-136">What does each of the health status mean?</span><span class="sxs-lookup"><span data-stu-id="12f23-136">What does each of the health status mean?</span></span>
<span data-ttu-id="12f23-137">There are three different health statuses:</span><span class="sxs-lookup"><span data-stu-id="12f23-137">There are three different health statuses:</span></span>
1. <span data-ttu-id="12f23-138">Available: There aren't any known problems in the Azure platform that could be impacting this resource</span><span class="sxs-lookup"><span data-stu-id="12f23-138">Available: There aren't any known problems in the Azure platform that could be impacting this resource</span></span>
2. <span data-ttu-id="12f23-139">Unavailable: Resource health has detected issues that are impacting the resource</span><span class="sxs-lookup"><span data-stu-id="12f23-139">Unavailable: Resource health has detected issues that are impacting the resource</span></span>
3. <span data-ttu-id="12f23-140">Unknown: Resource health can determine the health of a resource because it has stopped receiving information about it.</span><span class="sxs-lookup"><span data-stu-id="12f23-140">Unknown: Resource health can determine the health of a resource because it has stopped receiving information about it.</span></span> 

## <a name="what-does-the-unknown-status-mean-is-something-wrong-with-my-resource"></a><span data-ttu-id="12f23-141">What does the unknown status mean?</span><span class="sxs-lookup"><span data-stu-id="12f23-141">What does the unknown status mean?</span></span> <span data-ttu-id="12f23-142">Is something wrong with my resource?</span><span class="sxs-lookup"><span data-stu-id="12f23-142">Is something wrong with my resource?</span></span>
<span data-ttu-id="12f23-143">The health status is set to unknown when resource health stops receiving information about a specific resource.</span><span class="sxs-lookup"><span data-stu-id="12f23-143">The health status is set to unknown when resource health stops receiving information about a specific resource.</span></span> <span data-ttu-id="12f23-144">While this status is not a definitive indication of the state of the resource, in cases where you are experiencing problems, it may indicate there is an Azure problem.</span><span class="sxs-lookup"><span data-stu-id="12f23-144">While this status is not a definitive indication of the state of the resource, in cases where you are experiencing problems, it may indicate there is an Azure problem.</span></span>

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a><span data-ttu-id="12f23-145">How can I get help for a resource that is unavailable?</span><span class="sxs-lookup"><span data-stu-id="12f23-145">How can I get help for a resource that is unavailable?</span></span>
<span data-ttu-id="12f23-146">You can submit a support request from the resource health blade.</span><span class="sxs-lookup"><span data-stu-id="12f23-146">You can submit a support request from the resource health blade.</span></span> <span data-ttu-id="12f23-147">You do not need a support agreement with Microsoft to open a request when the resource is unavailable because platform events.</span><span class="sxs-lookup"><span data-stu-id="12f23-147">You do not need a support agreement with Microsoft to open a request when the resource is unavailable because platform events.</span></span>

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a><span data-ttu-id="12f23-148">Does resource health differentiate between unavailability cased by platform problems versus something I did?</span><span class="sxs-lookup"><span data-stu-id="12f23-148">Does resource health differentiate between unavailability cased by platform problems versus something I did?</span></span>
<span data-ttu-id="12f23-149">Yes, when a resource is unavailable, resource health identifies the root cause within one of these categories:</span><span class="sxs-lookup"><span data-stu-id="12f23-149">Yes, when a resource is unavailable, resource health identifies the root cause within one of these categories:</span></span> 
1.  <span data-ttu-id="12f23-150">User initiated action</span><span class="sxs-lookup"><span data-stu-id="12f23-150">User initiated action</span></span>
2.  <span data-ttu-id="12f23-151">Planned event</span><span class="sxs-lookup"><span data-stu-id="12f23-151">Planned event</span></span> 
3.  <span data-ttu-id="12f23-152">Unplanned event</span><span class="sxs-lookup"><span data-stu-id="12f23-152">Unplanned event</span></span>

<span data-ttu-id="12f23-153">In the portal, user initiated actions are shown using a blue notification icon, while planned and unplanned events are shown using a red warning icon.</span><span class="sxs-lookup"><span data-stu-id="12f23-153">In the portal, user initiated actions are shown using a blue notification icon, while planned and unplanned events are shown using a red warning icon.</span></span> <span data-ttu-id="12f23-154">More details are provided in the [resource health overview](Resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="12f23-154">More details are provided in the [resource health overview](Resource-health-overview.md).</span></span>  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a><span data-ttu-id="12f23-155">Can I integrate resource health with my monitoring tools?</span><span class="sxs-lookup"><span data-stu-id="12f23-155">Can I integrate resource health with my monitoring tools?</span></span>
<span data-ttu-id="12f23-156">Resource health is a service designed to help you diagnose and mitigate Azure service issues that impact your resources.</span><span class="sxs-lookup"><span data-stu-id="12f23-156">Resource health is a service designed to help you diagnose and mitigate Azure service issues that impact your resources.</span></span> <span data-ttu-id="12f23-157">While you can use the resource health API to programmatically obtain the health status, we recommend you use metrics to monitor your resources.</span><span class="sxs-lookup"><span data-stu-id="12f23-157">While you can use the resource health API to programmatically obtain the health status, we recommend you use metrics to monitor your resources.</span></span> <span data-ttu-id="12f23-158">Once an issue is detected, resource health helps you determine the root cause and guides you through actions to address them.</span><span class="sxs-lookup"><span data-stu-id="12f23-158">Once an issue is detected, resource health helps you determine the root cause and guides you through actions to address them.</span></span> <span data-ttu-id="12f23-159">Visit [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) to learn more about how you can use metrics to check your resources.</span><span class="sxs-lookup"><span data-stu-id="12f23-159">Visit [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) to learn more about how you can use metrics to check your resources.</span></span>

## <a name="where-do-i-find-resource-health"></a><span data-ttu-id="12f23-160">Where do I find resource health?</span><span class="sxs-lookup"><span data-stu-id="12f23-160">Where do I find resource health?</span></span>
<span data-ttu-id="12f23-161">After you log in to the Azure portal, there are multiple ways you can access resource health:</span><span class="sxs-lookup"><span data-stu-id="12f23-161">After you log in to the Azure portal, there are multiple ways you can access resource health:</span></span>
1. <span data-ttu-id="12f23-162">Navigate to your resource.</span><span class="sxs-lookup"><span data-stu-id="12f23-162">Navigate to your resource.</span></span> <span data-ttu-id="12f23-163">In the left-hand navigation, click **Resource health**.</span><span class="sxs-lookup"><span data-stu-id="12f23-163">In the left-hand navigation, click **Resource health**.</span></span>
2. <span data-ttu-id="12f23-164">Go to the Azure Monitor blade.</span><span class="sxs-lookup"><span data-stu-id="12f23-164">Go to the Azure Monitor blade.</span></span>  <span data-ttu-id="12f23-165">In the left-hand navigation, click **Resource health**.</span><span class="sxs-lookup"><span data-stu-id="12f23-165">In the left-hand navigation, click **Resource health**.</span></span>
3. <span data-ttu-id="12f23-166">Open the **Help + Support** blade by clicking the question mark in the upper right corner of the portal and then selecting **Help + Support**.</span><span class="sxs-lookup"><span data-stu-id="12f23-166">Open the **Help + Support** blade by clicking the question mark in the upper right corner of the portal and then selecting **Help + Support**.</span></span> <span data-ttu-id="12f23-167">Once the blade opens, click **Resource health**</span><span class="sxs-lookup"><span data-stu-id="12f23-167">Once the blade opens, click **Resource health**</span></span>

<span data-ttu-id="12f23-168">You can also use the resource health API to obtain information about the health of your resources.</span><span class="sxs-lookup"><span data-stu-id="12f23-168">You can also use the resource health API to obtain information about the health of your resources.</span></span>

## <a name="is-resource-health-available-for-all-resource-types"></a><span data-ttu-id="12f23-169">Is resource health available for all resource types?</span><span class="sxs-lookup"><span data-stu-id="12f23-169">Is resource health available for all resource types?</span></span>
<span data-ttu-id="12f23-170">The list of health checks and resource types supported through resource health can be found [here](resource-health-checks-resource-types.md)</span><span class="sxs-lookup"><span data-stu-id="12f23-170">The list of health checks and resource types supported through resource health can be found [here](resource-health-checks-resource-types.md)</span></span>

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a><span data-ttu-id="12f23-171">What should I do if my resource is showing available but I believe it is not?”</span><span class="sxs-lookup"><span data-stu-id="12f23-171">What should I do if my resource is showing available but I believe it is not?”</span></span>
<span data-ttu-id="12f23-172">When checking the health of a resource, right under the health status you can click **Report incorrect health status**.</span><span class="sxs-lookup"><span data-stu-id="12f23-172">When checking the health of a resource, right under the health status you can click **Report incorrect health status**.</span></span> <span data-ttu-id="12f23-173">Before submitting the report, you have the option of providing additional details on why you believe the current health status is incorrect.</span><span class="sxs-lookup"><span data-stu-id="12f23-173">Before submitting the report, you have the option of providing additional details on why you believe the current health status is incorrect.</span></span>

## <a name="is-resource-health-available-for-all-azure-regions"></a><span data-ttu-id="12f23-174">Is resource health available for all Azure regions?</span><span class="sxs-lookup"><span data-stu-id="12f23-174">Is resource health available for all Azure regions?</span></span> 
<span data-ttu-id="12f23-175">Resource health is available in across all Azure geos except the following regions:</span><span class="sxs-lookup"><span data-stu-id="12f23-175">Resource health is available in across all Azure geos except the following regions:</span></span>
* <span data-ttu-id="12f23-176">US Gov Virginia</span><span class="sxs-lookup"><span data-stu-id="12f23-176">US Gov Virginia</span></span>
* <span data-ttu-id="12f23-177">US Gov Iowa</span><span class="sxs-lookup"><span data-stu-id="12f23-177">US Gov Iowa</span></span>
* <span data-ttu-id="12f23-178">US DoD East</span><span class="sxs-lookup"><span data-stu-id="12f23-178">US DoD East</span></span>
* <span data-ttu-id="12f23-179">US DoD Central</span><span class="sxs-lookup"><span data-stu-id="12f23-179">US DoD Central</span></span>
* <span data-ttu-id="12f23-180">Germany Central</span><span class="sxs-lookup"><span data-stu-id="12f23-180">Germany Central</span></span>
* <span data-ttu-id="12f23-181">Germany Northeast</span><span class="sxs-lookup"><span data-stu-id="12f23-181">Germany Northeast</span></span>
* <span data-ttu-id="12f23-182">China East</span><span class="sxs-lookup"><span data-stu-id="12f23-182">China East</span></span>
* <span data-ttu-id="12f23-183">China North</span><span class="sxs-lookup"><span data-stu-id="12f23-183">China North</span></span>

## <a name="how-is-resource-health-different-from-the-service-health-dashboard-or-the-azure-portal-service-notifications"></a><span data-ttu-id="12f23-184">How is resource health different from the Service Health Dashboard or the Azure portal service notifications?</span><span class="sxs-lookup"><span data-stu-id="12f23-184">How is resource health different from the Service Health Dashboard or the Azure portal service notifications?</span></span>
<span data-ttu-id="12f23-185">The information provided by resource health is more specific than what is provided by the Azure Service Health Dashboard.</span><span class="sxs-lookup"><span data-stu-id="12f23-185">The information provided by resource health is more specific than what is provided by the Azure Service Health Dashboard.</span></span>

<span data-ttu-id="12f23-186">Whereas [Azure Status](https://status.azure.com) and the portal service notifications inform you about service issues that affect a broad set of customers (for example an Azure region), resource health exposes more granular events that are relevant only to the specific resource.</span><span class="sxs-lookup"><span data-stu-id="12f23-186">Whereas [Azure Status](https://status.azure.com) and the portal service notifications inform you about service issues that affect a broad set of customers (for example an Azure region), resource health exposes more granular events that are relevant only to the specific resource.</span></span> <span data-ttu-id="12f23-187">For example, if a host unexpectedly reboots, resource health alerts only those customers whose virtual machines were running on that host.</span><span class="sxs-lookup"><span data-stu-id="12f23-187">For example, if a host unexpectedly reboots, resource health alerts only those customers whose virtual machines were running on that host.</span></span>

<span data-ttu-id="12f23-188">It is important to notice that to provide you complete visibility of events impacting your resources, resource health also surfaces events published in Service notifications and the Service Health Dashboard.</span><span class="sxs-lookup"><span data-stu-id="12f23-188">It is important to notice that to provide you complete visibility of events impacting your resources, resource health also surfaces events published in Service notifications and the Service Health Dashboard.</span></span>

## <a name="do-i-need-to-activate-resource-health-for-each-resource"></a><span data-ttu-id="12f23-189">Do I need to activate resource health for each resource?</span><span class="sxs-lookup"><span data-stu-id="12f23-189">Do I need to activate resource health for each resource?</span></span>
<span data-ttu-id="12f23-190">No, health information is available for all resource types available through resource health.</span><span class="sxs-lookup"><span data-stu-id="12f23-190">No, health information is available for all resource types available through resource health.</span></span> 

## <a name="do-we-need-to-enable-resource-health-for-my-organization"></a><span data-ttu-id="12f23-191">Do we need to enable resource health for my organization?</span><span class="sxs-lookup"><span data-stu-id="12f23-191">Do we need to enable resource health for my organization?</span></span>
<span data-ttu-id="12f23-192">No.</span><span class="sxs-lookup"><span data-stu-id="12f23-192">No.</span></span>  <span data-ttu-id="12f23-193">Azure resource health is accessible within the Azure portal without any setup requirements.</span><span class="sxs-lookup"><span data-stu-id="12f23-193">Azure resource health is accessible within the Azure portal without any setup requirements.</span></span>

## <a name="is-resource-health-available-free-of-charge"></a><span data-ttu-id="12f23-194">Is resource health available free of charge?</span><span class="sxs-lookup"><span data-stu-id="12f23-194">Is resource health available free of charge?</span></span>
<span data-ttu-id="12f23-195">Yes.</span><span class="sxs-lookup"><span data-stu-id="12f23-195">Yes.</span></span>  <span data-ttu-id="12f23-196">Azure resource health is free of charge.</span><span class="sxs-lookup"><span data-stu-id="12f23-196">Azure resource health is free of charge.</span></span>

## <a name="what-are-the-recommendations-that-resource-health-provides"></a><span data-ttu-id="12f23-197">What are the recommendations that resource health provides?</span><span class="sxs-lookup"><span data-stu-id="12f23-197">What are the recommendations that resource health provides?</span></span>
<span data-ttu-id="12f23-198">Based on the health status, resource health provides you with recommendations with the goal of reducing the time you spent troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="12f23-198">Based on the health status, resource health provides you with recommendations with the goal of reducing the time you spent troubleshooting.</span></span> <span data-ttu-id="12f23-199">For available resources, the recommendations focus on how to solve the most common problems customers encounter.</span><span class="sxs-lookup"><span data-stu-id="12f23-199">For available resources, the recommendations focus on how to solve the most common problems customers encounter.</span></span> <span data-ttu-id="12f23-200">If the resource is unavailable due to an Azure unplanned event, the focus will be on assisting you during and after the recovery process.</span><span class="sxs-lookup"><span data-stu-id="12f23-200">If the resource is unavailable due to an Azure unplanned event, the focus will be on assisting you during and after the recovery process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="12f23-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="12f23-201">Next steps</span></span>

<span data-ttu-id="12f23-202">Check out these resources to learn more about resource health:</span><span class="sxs-lookup"><span data-stu-id="12f23-202">Check out these resources to learn more about resource health:</span></span>
-  [<span data-ttu-id="12f23-203">Azure resource health overview</span><span class="sxs-lookup"><span data-stu-id="12f23-203">Azure resource health overview</span></span>](Resource-health-overview.md)
-  [<span data-ttu-id="12f23-204">Resource types and health checks available through Azure resource health</span><span class="sxs-lookup"><span data-stu-id="12f23-204">Resource types and health checks available through Azure resource health</span></span>](resource-health-checks-resource-types.md)