---
title: Targeting Management Solutions in Azure | Microsoft Docs
description: Targeting management solutions allows you to limit management solutions to a specific set of agents.  This article describes how to create a scope configuration and apply it to a solution.
services: monitoring
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: monitoring
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 65585e6c09def23101d9735c8b9c719d213938ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867475"
---
# <a name="targeting-management-solutions-in-azure-preview"></a><span data-ttu-id="1812b-104">Targeting Management Solutions in Azure (Preview)</span><span class="sxs-lookup"><span data-stu-id="1812b-104">Targeting Management Solutions in Azure (Preview)</span></span>
<span data-ttu-id="1812b-105">When you add a management solution to your subscription, it's automatically deployed by default to all Windows and Linux agents connected to your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="1812b-105">When you add a management solution to your subscription, it's automatically deployed by default to all Windows and Linux agents connected to your Log Analytics workspace.</span></span>  <span data-ttu-id="1812b-106">You may want to manage your costs and limit the amount of data collected for a solution by limiting it to a particular set of agents.</span><span class="sxs-lookup"><span data-stu-id="1812b-106">You may want to manage your costs and limit the amount of data collected for a solution by limiting it to a particular set of agents.</span></span>  <span data-ttu-id="1812b-107">This article describes how to use **Solution Targeting** which is a feature that allows you to apply a scope to your solutions.</span><span class="sxs-lookup"><span data-stu-id="1812b-107">This article describes how to use **Solution Targeting** which is a feature that allows you to apply a scope to your solutions.</span></span>

## <a name="how-to-target-a-solution"></a><span data-ttu-id="1812b-108">How to target a solution</span><span class="sxs-lookup"><span data-stu-id="1812b-108">How to target a solution</span></span>
<span data-ttu-id="1812b-109">There are three steps to targeting a solution as described in the following sections.</span><span class="sxs-lookup"><span data-stu-id="1812b-109">There are three steps to targeting a solution as described in the following sections.</span></span> 


### <a name="1-create-a-computer-group"></a><span data-ttu-id="1812b-110">1. Create a computer group</span><span class="sxs-lookup"><span data-stu-id="1812b-110">1. Create a computer group</span></span>
<span data-ttu-id="1812b-111">You specify the computers that you want to include in a scope by creating a [computer group](../log-analytics/log-analytics-computer-groups.md) in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1812b-111">You specify the computers that you want to include in a scope by creating a [computer group](../log-analytics/log-analytics-computer-groups.md) in Log Analytics.</span></span>  <span data-ttu-id="1812b-112">The computer group can be based on a log search or imported from other sources such as Active Directory or WSUS groups.</span><span class="sxs-lookup"><span data-stu-id="1812b-112">The computer group can be based on a log search or imported from other sources such as Active Directory or WSUS groups.</span></span> <span data-ttu-id="1812b-113">As [described below](#solutions-and-agents-that-cant-be-targeted), only computers that are directly connected to Log Analytics will be included in the scope.</span><span class="sxs-lookup"><span data-stu-id="1812b-113">As [described below](#solutions-and-agents-that-cant-be-targeted), only computers that are directly connected to Log Analytics will be included in the scope.</span></span>

<span data-ttu-id="1812b-114">Once you have the computer group created in your workspace, then you'll include it in a scope configuration that can be applied to one or more solutions.</span><span class="sxs-lookup"><span data-stu-id="1812b-114">Once you have the computer group created in your workspace, then you'll include it in a scope configuration that can be applied to one or more solutions.</span></span>
 
 
 ### <a name="2-create-a-scope-configuration"></a><span data-ttu-id="1812b-115">2. Create a scope configuration</span><span class="sxs-lookup"><span data-stu-id="1812b-115">2. Create a scope configuration</span></span>
 <span data-ttu-id="1812b-116">A **Scope Configuration** includes one or more computer groups and can be applied to one or more solutions.</span><span class="sxs-lookup"><span data-stu-id="1812b-116">A **Scope Configuration** includes one or more computer groups and can be applied to one or more solutions.</span></span> 
 
 <span data-ttu-id="1812b-117">Create a scope configuration using the following process.</span><span class="sxs-lookup"><span data-stu-id="1812b-117">Create a scope configuration using the following process.</span></span>  

 1. <span data-ttu-id="1812b-118">In the Azure portal, navigate to **Log Analytics** and select your workspace.</span><span class="sxs-lookup"><span data-stu-id="1812b-118">In the Azure portal, navigate to **Log Analytics** and select your workspace.</span></span>
 2. <span data-ttu-id="1812b-119">In the properties for the workspace under **Workspace Data Sources** select **Scope Configurations**.</span><span class="sxs-lookup"><span data-stu-id="1812b-119">In the properties for the workspace under **Workspace Data Sources** select **Scope Configurations**.</span></span>
 3. <span data-ttu-id="1812b-120">Click **Add** to create a new scope configuration.</span><span class="sxs-lookup"><span data-stu-id="1812b-120">Click **Add** to create a new scope configuration.</span></span>
 4. <span data-ttu-id="1812b-121">Type a **Name** for the scope configuration.</span><span class="sxs-lookup"><span data-stu-id="1812b-121">Type a **Name** for the scope configuration.</span></span>
 5. <span data-ttu-id="1812b-122">Click **Select Computer Groups**.</span><span class="sxs-lookup"><span data-stu-id="1812b-122">Click **Select Computer Groups**.</span></span>
 6. <span data-ttu-id="1812b-123">Select the computer group that you created and optionally any other groups to add to the configuration.</span><span class="sxs-lookup"><span data-stu-id="1812b-123">Select the computer group that you created and optionally any other groups to add to the configuration.</span></span>  <span data-ttu-id="1812b-124">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="1812b-124">Click **Select**.</span></span>  
 6. <span data-ttu-id="1812b-125">Click **OK** to create the scope configuration.</span><span class="sxs-lookup"><span data-stu-id="1812b-125">Click **OK** to create the scope configuration.</span></span> 


 ### <a name="3-apply-the-scope-configuration-to-a-solution"></a><span data-ttu-id="1812b-126">3. Apply the scope configuration to a solution.</span><span class="sxs-lookup"><span data-stu-id="1812b-126">3. Apply the scope configuration to a solution.</span></span>
<span data-ttu-id="1812b-127">Once you have a scope configuration, then you can apply it to one or more solutions.</span><span class="sxs-lookup"><span data-stu-id="1812b-127">Once you have a scope configuration, then you can apply it to one or more solutions.</span></span>  <span data-ttu-id="1812b-128">Note that while a single scope configuration can be used with multiple solutions, each solution can only use one scope configuration.</span><span class="sxs-lookup"><span data-stu-id="1812b-128">Note that while a single scope configuration can be used with multiple solutions, each solution can only use one scope configuration.</span></span>

<span data-ttu-id="1812b-129">Apply a scope configuration using the following process.</span><span class="sxs-lookup"><span data-stu-id="1812b-129">Apply a scope configuration using the following process.</span></span>  

 1. <span data-ttu-id="1812b-130">In the Azure portal, navigate to **Log Analytics** and select your workspace.</span><span class="sxs-lookup"><span data-stu-id="1812b-130">In the Azure portal, navigate to **Log Analytics** and select your workspace.</span></span>
 2. <span data-ttu-id="1812b-131">In the properties for the workspace select **Solutions**.</span><span class="sxs-lookup"><span data-stu-id="1812b-131">In the properties for the workspace select **Solutions**.</span></span>
 3. <span data-ttu-id="1812b-132">Click on the solution you want to scope.</span><span class="sxs-lookup"><span data-stu-id="1812b-132">Click on the solution you want to scope.</span></span>
 4. <span data-ttu-id="1812b-133">In the properties for the solution under **Workspace Data Sources** select **Solution Targeting**.</span><span class="sxs-lookup"><span data-stu-id="1812b-133">In the properties for the solution under **Workspace Data Sources** select **Solution Targeting**.</span></span>  <span data-ttu-id="1812b-134">If the option is not available then [this solution cannot be targeted](#solutions-and-agents-that-cant-be-targeted).</span><span class="sxs-lookup"><span data-stu-id="1812b-134">If the option is not available then [this solution cannot be targeted](#solutions-and-agents-that-cant-be-targeted).</span></span>
 5. <span data-ttu-id="1812b-135">Click **Add scope configuration**.</span><span class="sxs-lookup"><span data-stu-id="1812b-135">Click **Add scope configuration**.</span></span>  <span data-ttu-id="1812b-136">If you already have a configuration applied to this solution then this option will be unavailable.</span><span class="sxs-lookup"><span data-stu-id="1812b-136">If you already have a configuration applied to this solution then this option will be unavailable.</span></span>  <span data-ttu-id="1812b-137">You must remove the existing configuration before adding another one.</span><span class="sxs-lookup"><span data-stu-id="1812b-137">You must remove the existing configuration before adding another one.</span></span>
 6. <span data-ttu-id="1812b-138">Click on the scope configuration that you created.</span><span class="sxs-lookup"><span data-stu-id="1812b-138">Click on the scope configuration that you created.</span></span>
 7. <span data-ttu-id="1812b-139">Watch the **Status** of the configuration to ensure that it shows **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="1812b-139">Watch the **Status** of the configuration to ensure that it shows **Succeeded**.</span></span>  <span data-ttu-id="1812b-140">If the status indicates an error, then click the ellipse to the right of the configuration and select **Edit scope configuration** to make changes.</span><span class="sxs-lookup"><span data-stu-id="1812b-140">If the status indicates an error, then click the ellipse to the right of the configuration and select **Edit scope configuration** to make changes.</span></span>

## <a name="solutions-and-agents-that-cant-be-targeted"></a><span data-ttu-id="1812b-141">Solutions and agents that can't be targeted</span><span class="sxs-lookup"><span data-stu-id="1812b-141">Solutions and agents that can't be targeted</span></span>
<span data-ttu-id="1812b-142">Following are the criteria for agents and solutions that can't be used with solution targeting.</span><span class="sxs-lookup"><span data-stu-id="1812b-142">Following are the criteria for agents and solutions that can't be used with solution targeting.</span></span>

- <span data-ttu-id="1812b-143">Solution targeting only applies to solutions that deploy to agents.</span><span class="sxs-lookup"><span data-stu-id="1812b-143">Solution targeting only applies to solutions that deploy to agents.</span></span>
- <span data-ttu-id="1812b-144">Solution targeting only applies to solutions provided by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1812b-144">Solution targeting only applies to solutions provided by Microsoft.</span></span>  <span data-ttu-id="1812b-145">It does not apply to solutions [created by yourself or partners](monitoring-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="1812b-145">It does not apply to solutions [created by yourself or partners](monitoring-solutions-creating.md).</span></span>
- <span data-ttu-id="1812b-146">You can only filter out agents that connect directly to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1812b-146">You can only filter out agents that connect directly to Log Analytics.</span></span>  <span data-ttu-id="1812b-147">Solutions will automatically deploy to any agents that are part of a connected Operations Manager management group whether or not they're included in a scope configuration.</span><span class="sxs-lookup"><span data-stu-id="1812b-147">Solutions will automatically deploy to any agents that are part of a connected Operations Manager management group whether or not they're included in a scope configuration.</span></span>

### <a name="exceptions"></a><span data-ttu-id="1812b-148">Exceptions</span><span class="sxs-lookup"><span data-stu-id="1812b-148">Exceptions</span></span>
<span data-ttu-id="1812b-149">Solution targeting cannot be used with the following solutions even though they fit the stated criteria.</span><span class="sxs-lookup"><span data-stu-id="1812b-149">Solution targeting cannot be used with the following solutions even though they fit the stated criteria.</span></span>

- <span data-ttu-id="1812b-150">Agent Health Assessment</span><span class="sxs-lookup"><span data-stu-id="1812b-150">Agent Health Assessment</span></span>

## <a name="next-steps"></a><span data-ttu-id="1812b-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="1812b-151">Next steps</span></span>
- <span data-ttu-id="1812b-152">Learn more about management solutions including the solutions that are available to install in your environment at [Add Azure Log Analytics management solutions to your workspace](../log-analytics/log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="1812b-152">Learn more about management solutions including the solutions that are available to install in your environment at [Add Azure Log Analytics management solutions to your workspace](../log-analytics/log-analytics-add-solutions.md).</span></span>
- <span data-ttu-id="1812b-153">Learn more about creating computer groups at [Computer groups in Log Analytics log searches](../log-analytics/log-analytics-computer-groups.md).</span><span class="sxs-lookup"><span data-stu-id="1812b-153">Learn more about creating computer groups at [Computer groups in Log Analytics log searches](../log-analytics/log-analytics-computer-groups.md).</span></span>